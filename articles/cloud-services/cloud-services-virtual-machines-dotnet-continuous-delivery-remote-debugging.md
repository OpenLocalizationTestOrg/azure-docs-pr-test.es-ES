---
title: "depuración remota con la entrega continua aaaEnable | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooenable depuración remota al utilizar la entrega continua toodeploy tooAzure"
services: cloud-services
documentationcenter: .net
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d423639-3b2f-4ca5-ac5a-9ac19a217c29
ms.service: cloud-services
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: d9d9d1cfe5304c9526586a9164f172746a448e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a><span data-ttu-id="db328-103">Habilitar la depuración remota al utilizar la entrega continua toopublish tooAzure</span><span class="sxs-lookup"><span data-stu-id="db328-103">Enable remote debugging when using continuous delivery toopublish tooAzure</span></span>
<span data-ttu-id="db328-104">Puede habilitar la depuración remota en Azure, para los servicios en la nube o máquinas virtuales, cuando se usa [la entrega continua](cloud-services-dotnet-continuous-delivery.md) toopublish tooAzure siguiendo estos pasos.</span><span class="sxs-lookup"><span data-stu-id="db328-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) toopublish tooAzure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="db328-105">Habilitación de la depuración remota para los servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="db328-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="db328-106">En el agente de compilación de hello, configurar Hola inicial entorno de Azure como se describe en [de línea de comandos de compilación para Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span><span class="sxs-lookup"><span data-stu-id="db328-106">On hello build agent, set up hello initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="db328-107">Porque se requiere para el paquete de Hola Hola tiempo de ejecución de depuración remota (msvsmon.exe), instale hello **herramientas remotas para Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="db328-107">Because hello remote debug runtime (msvsmon.exe) is required for hello package, install hello **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="db328-108">Herramientas remotas para Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="db328-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="db328-109">Herramientas remotas para Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="db328-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="db328-110">Herramientas remotas para Visual Studio 2013 Update 5</span><span class="sxs-lookup"><span data-stu-id="db328-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="db328-111">Como alternativa, puede copiar los archivos binarios de depuración remota de Hola desde un sistema que tiene instalado Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db328-111">As an alternative, you can copy hello remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="db328-112">Cree un certificado como se describe en [Información general de los certificados para los servicios en la nube de Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="db328-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="db328-113">Mantener .pfx hello y huella digital del certificado RDP y cargar el servicio de nube de destino de hello certificado toohello.</span><span class="sxs-lookup"><span data-stu-id="db328-113">Keep hello .pfx and RDP certificate thumbprint and upload hello certificate toohello target cloud service.</span></span>
4. <span data-ttu-id="db328-114">Usar hello siguientes opciones en toobuild de línea de comandos de MSBuild Hola y el paquete con la depuración remota habilitada.</span><span class="sxs-lookup"><span data-stu-id="db328-114">Use hello following options in hello MSBuild command line toobuild and package with remote debug enabled.</span></span> <span data-ttu-id="db328-115">(Sustituya los archivos de proyecto y del sistema de tooyour en las rutas de acceso real para los elementos entre corchetes angulares de hello).</span><span class="sxs-lookup"><span data-stu-id="db328-115">(Substitute actual paths tooyour system and project files for hello angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    <span data-ttu-id="db328-116">`VSX64RemoteDebuggerPath`es toohello carpetas de hello ruta de acceso que contiene msvsmon.exe en Hola de herramientas remotas para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db328-116">`VSX64RemoteDebuggerPath` is hello path toohello folder containing msvsmon.exe in hello Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="db328-117">`RemoteDebuggerConnectorVersion`es la versión de SDK de Azure de hello en el servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="db328-117">`RemoteDebuggerConnectorVersion` is hello Azure SDK version in your cloud service.</span></span> <span data-ttu-id="db328-118">También debe coincidir con versión de Hola que se instala con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db328-118">It should also match hello version installed with Visual Studio.</span></span>
5. <span data-ttu-id="db328-119">Publicar toohello servicio de nube de destino mediante el archivo de paquete y .cscfg de hello generado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="db328-119">Publish toohello target cloud service by using hello package and .cscfg file generated in hello previous step.</span></span>
6. <span data-ttu-id="db328-120">Importar máquina Hola de toohello del certificado (archivo .pfx) que tiene Visual Studio con Azure SDK para .NET instalado.</span><span class="sxs-lookup"><span data-stu-id="db328-120">Import hello certificate (.pfx file) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="db328-121">Asegúrese de que toohello tooimport `CurrentUser\My` almacén de certificados, en caso contrario, adjuntar depurador toohello en Visual Studio se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="db328-121">Make sure tooimport toohello `CurrentUser\My` certificate store, otherwise attaching toohello debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="db328-122">Habilitación de la depuración remota para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="db328-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="db328-123">Cree una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="db328-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="db328-124">Consulte [Creación de una máquina virtual que ejecuta Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [Creación y administración de máquinas virtuales de Azure en Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="db328-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="db328-125">En hello [página del portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=269851), ver panel toosee Hola máquinas virtuales del Hola máquinas virtuales **huella digital del certificado de RDP**.</span><span class="sxs-lookup"><span data-stu-id="db328-125">On hello [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view hello virtual machine's dashboard toosee hello virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="db328-126">Este valor se utiliza para hello `ServerThumbprint` valor de configuración de la extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="db328-126">This value is used for hello `ServerThumbprint` value in hello extension configuration.</span></span>
3. <span data-ttu-id="db328-127">Crear un certificado de cliente, tal como se describe en [Introducción a los certificados para servicios en la nube](cloud-services-certs-create.md) (mantenga Hola .pfx y la huella digital de certificado RDP).</span><span class="sxs-lookup"><span data-stu-id="db328-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep hello .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="db328-128">Instalar Azure Powershell (versión 0.7.4 o posterior) como se describe en [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="db328-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="db328-129">Ejecute hello después de la extensión de script tooenable hello RemoteDebug.</span><span class="sxs-lookup"><span data-stu-id="db328-129">Run hello following script tooenable hello RemoteDebug extension.</span></span> <span data-ttu-id="db328-130">Reemplace las rutas de acceso de Hola y sus datos personales con su cuenta, como el nombre de suscripción, el nombre del servicio y la huella digital.</span><span class="sxs-lookup"><span data-stu-id="db328-130">Replace hello paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="db328-131">Este script está configurado para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="db328-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="db328-132">Si usa Visual Studio 2013 o Visual Studio de 2017, modificar hello `$referenceName` y `$extensionName` asignaciones siguiente demasiado`RemoteDebugVS2013` o `RemoteDebugVS2017`.</span><span class="sxs-lookup"><span data-stu-id="db328-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify hello `$referenceName` and `$extensionName` assignments below too`RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

    ```powershell   
    Add-AzureAccount

    Select-AzureSubscription "My Microsoft Subscription"

    $vm = Get-AzureVM -ServiceName "mytestvm1" -Name "mytestvm1"

    $endpoints = @(
                    ,@{Name="RDConnVS2013"; PublicPort=30400; PrivatePort=30398}
                    ,@{Name="RDFwdrVS2013"; PublicPort=31400; PrivatePort=31398}
                )

    foreach($endpoint in $endpoints)
    {
        Add-AzureEndpoint -VM $vm -Name $endpoint.Name -Protocol tcp -PublicPort $endpoint.PublicPort -LocalPort $endpoint.PrivatePort
    }

    $referenceName = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug.RemoteDebugVS2015"
    $publisher = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug"
    $extensionName = "RemoteDebugVS2015"
    $version = "1.*"
    $publicConfiguration = "<PublicConfig><Connector.Enabled>true</Connector.Enabled><ClientThumbprint>56D7D1B25B472268E332F7FC0C87286458BFB6B2</ClientThumbprint><ServerThumbprint>E7DCB00CB916C468CC3228261D6E4EE45C8ED3C6</ServerThumbprint><ConnectorPort>30398</ConnectorPort><ForwarderPort>31398</ForwarderPort></PublicConfig>"

    $vm | Set-AzureVMExtension -ReferenceName $referenceName -Publisher $publisher -ExtensionName $extensionName -Version $version -PublicConfiguration $publicConfiguration

    foreach($extension in $vm.VM.ResourceExtensionReferences)
    {
        if(($extension.ReferenceName -eq $referenceName) `
        -and ($extension.Publisher -eq $publisher) `
        -and ($extension.Name -eq $extensionName) `
        -and ($extension.Version -eq $version))
        {
            $extension.ResourceExtensionParameterValues[0].Key = 'config.txt'
            break
        }
    }

    $vm | Update-AzureVM
    ```

6. <span data-ttu-id="db328-133">Importar máquina Hola de toohello del certificado (.pfx) que tiene Visual Studio con Azure SDK para .NET instalado.</span><span class="sxs-lookup"><span data-stu-id="db328-133">Import hello certificate (.pfx) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span>


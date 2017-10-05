---
title: "Habilitación de la depuración remota con entrega continua | Microsoft Docs"
description: "Sepa cómo habilitar la depuración remota cuando se usa entrega continua para implementar en Azure."
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
ms.openlocfilehash: 7a8a853a93e3e9915f687a20c871444e6a0de50d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-to-publish-to-azure"></a><span data-ttu-id="fe283-103">Habilitación de la depuración remota al usar la entrega continua para publicar en Azure</span><span class="sxs-lookup"><span data-stu-id="fe283-103">Enable remote debugging when using continuous delivery to publish to Azure</span></span>
<span data-ttu-id="fe283-104">Puede habilitar la depuración remota en Azure, para servicios en la nube o máquinas virtuales, cuando use la [entrega continua](cloud-services-dotnet-continuous-delivery.md) para publicar en Azure; para ello, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="fe283-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) to publish to Azure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="fe283-105">Habilitación de la depuración remota para los servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="fe283-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="fe283-106">En el agente de compilación, configure el entorno inicial para Azure como se describe en [Compilación de línea de comandos para Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe283-106">On the build agent, set up the initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="fe283-107">Como se requiere el tiempo de ejecución de depuración remota (msvsmon.exe) para el paquete, instale las **Herramientas remotas para Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="fe283-107">Because the remote debug runtime (msvsmon.exe) is required for the package, install the **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="fe283-108">Herramientas remotas para Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="fe283-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="fe283-109">Herramientas remotas para Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="fe283-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="fe283-110">Herramientas remotas para Visual Studio 2013 Update 5</span><span class="sxs-lookup"><span data-stu-id="fe283-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="fe283-111">También puede copiar los binarios de depuración remota desde un sistema que tenga instalado Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe283-111">As an alternative, you can copy the remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="fe283-112">Cree un certificado como se describe en [Información general de los certificados para los servicios en la nube de Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="fe283-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="fe283-113">Mantenga la huella digital del certificado de .pfx y RDP y cargue el certificado en el servicio en la nube de destino.</span><span class="sxs-lookup"><span data-stu-id="fe283-113">Keep the .pfx and RDP certificate thumbprint and upload the certificate to the target cloud service.</span></span>
4. <span data-ttu-id="fe283-114">Use las siguientes opciones de la línea de comandos MSBuild para compilarlo y empaquetarlo con la depuración remota habilitada.</span><span class="sxs-lookup"><span data-stu-id="fe283-114">Use the following options in the MSBuild command line to build and package with remote debug enabled.</span></span> <span data-ttu-id="fe283-115">(Actualice las rutas de acceso de sus archivos de sistema y de proyecto.)</span><span class="sxs-lookup"><span data-stu-id="fe283-115">(Substitute actual paths to your system and project files for the angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of the certificate added to the cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path to your VS solution file>"
   
    <span data-ttu-id="fe283-116">`VSX64RemoteDebuggerPath` es la ruta de acceso a la carpeta que contiene msvsmon.exe en las Herramientas para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe283-116">`VSX64RemoteDebuggerPath` is the path to the folder containing msvsmon.exe in the Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="fe283-117">`RemoteDebuggerConnectorVersion` es la versión de Azure SDK del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="fe283-117">`RemoteDebuggerConnectorVersion` is the Azure SDK version in your cloud service.</span></span> <span data-ttu-id="fe283-118">También debe coincidir con la versión instalada con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe283-118">It should also match the version installed with Visual Studio.</span></span>
5. <span data-ttu-id="fe283-119">Publíquelo en el servicio en la nube de destino mediante el paquete y el archivo .cscfg generado en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="fe283-119">Publish to the target cloud service by using the package and .cscfg file generated in the previous step.</span></span>
6. <span data-ttu-id="fe283-120">Importe el certificado (archivo .pfx) en la máquina que tiene instalado Visual Studio con el SDK de Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="fe283-120">Import the certificate (.pfx file) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="fe283-121">No se olvide de importar el almacén de certificados `CurrentUser\My` ; de lo contrario, no se podrá asociar al depurador de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe283-121">Make sure to import to the `CurrentUser\My` certificate store, otherwise attaching to the debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="fe283-122">Habilitación de la depuración remota para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="fe283-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="fe283-123">Cree una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe283-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="fe283-124">Consulte [Creación de una máquina virtual que ejecuta Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [Creación y administración de máquinas virtuales de Azure en Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe283-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="fe283-125">En la [página del Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=269851), examine el panel de máquinas virtuales para ver la **HUELLA DIGITAL DEL CERTIFICADO RDP**de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe283-125">On the [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view the virtual machine's dashboard to see the virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="fe283-126">Este valor se usa para el valor de `ServerThumbprint` en la configuración de la extensión.</span><span class="sxs-lookup"><span data-stu-id="fe283-126">This value is used for the `ServerThumbprint` value in the extension configuration.</span></span>
3. <span data-ttu-id="fe283-127">Cree un certificado de cliente como se describe en [Información general sobre certificados para los servicios en la nube de Azure](cloud-services-certs-create.md) (mantenga la huella digital del certificado de .pfx y RDP).</span><span class="sxs-lookup"><span data-stu-id="fe283-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep the .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="fe283-128">Instale Azure Powershell (versión 0.7.4 o posterior) como se describe en [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fe283-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="fe283-129">Ejecute el siguiente script para habilitar la extensión RemoteDebug.</span><span class="sxs-lookup"><span data-stu-id="fe283-129">Run the following script to enable the RemoteDebug extension.</span></span> <span data-ttu-id="fe283-130">Sustituya las rutas de acceso y los datos personales por los suyos propios, como el nombre de la suscripción, el nombre de servicio y la huella digital.</span><span class="sxs-lookup"><span data-stu-id="fe283-130">Replace the paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fe283-131">Este script está configurado para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="fe283-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="fe283-132">Si usa Visual Studio 2013 o Visual Studio 2017, cambie las asignaciones `$referenceName` y `$extensionName` siguientes por `RemoteDebugVS2013` o `RemoteDebugVS2017`.</span><span class="sxs-lookup"><span data-stu-id="fe283-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify the `$referenceName` and `$extensionName` assignments below to `RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

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

6. <span data-ttu-id="fe283-133">Importe el certificado (.pfx) en la máquina que tiene instalado Visual Studio con el SDK de Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="fe283-133">Import the certificate (.pfx) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span>


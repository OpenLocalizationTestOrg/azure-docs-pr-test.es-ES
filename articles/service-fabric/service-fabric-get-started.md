---
title: "Configuración de un entorno de desarrollo para microservicios de Azure | Microsoft Docs"
description: "Instale las herramientas, el SDK y el motor en tiempo de ejecución y cree un clúster de desarrollo local. Después de completar esta instalación, estará listo para crear aplicaciones."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: f0c6957217c21bdfd76498944e248fc808f2d271
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="298fd-104">Preparación del entorno de desarrollo</span><span class="sxs-lookup"><span data-stu-id="298fd-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="298fd-105">Windows</span><span class="sxs-lookup"><span data-stu-id="298fd-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="298fd-106">Linux</span><span class="sxs-lookup"><span data-stu-id="298fd-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="298fd-107">OSX</span><span class="sxs-lookup"><span data-stu-id="298fd-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="298fd-108">Para compilar y ejecutar [aplicaciones de Azure Service Fabric][1] en la máquina de desarrollo, debe instalar el motor en tiempo de ejecución, el SDK y las herramientas.</span><span class="sxs-lookup"><span data-stu-id="298fd-108">To build and run [Azure Service Fabric applications][1] on your development machine, install the runtime, SDK, and tools.</span></span> <span data-ttu-id="298fd-109">También es preciso que habilite la ejecución de los scripts de Windows PowerShell que se incluyen en el SDK.</span><span class="sxs-lookup"><span data-stu-id="298fd-109">You also need to enable execution of the Windows PowerShell scripts included in the SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="298fd-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="298fd-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="298fd-111">Versiones de sistemas operativos compatibles</span><span class="sxs-lookup"><span data-stu-id="298fd-111">Supported operating system versions</span></span>
<span data-ttu-id="298fd-112">Se admiten las siguientes versiones de sistemas operativos para desarrollo:</span><span class="sxs-lookup"><span data-stu-id="298fd-112">The following operating system versions are supported for development:</span></span>

* <span data-ttu-id="298fd-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="298fd-113">Windows 7</span></span>
* <span data-ttu-id="298fd-114">Windows 8/Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="298fd-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="298fd-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="298fd-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="298fd-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="298fd-116">Windows Server 2016</span></span>
* <span data-ttu-id="298fd-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="298fd-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="298fd-118">Windows 7 solo incluye de forma predeterminada Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="298fd-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="298fd-119">Los cmdlets de PowerShell de Service Fabric requieren PowerShell 3.0 o superior.</span><span class="sxs-lookup"><span data-stu-id="298fd-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="298fd-120">Puede [descargar Windows PowerShell 5.0][powershell5-download] desde el Centro de descarga de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="298fd-120">You can [download Windows PowerShell 5.0][powershell5-download] from the Microsoft Download Center.</span></span>
> 
> 

## <a name="install-the-sdk-and-tools"></a><span data-ttu-id="298fd-121">Instalación de SDK y herramientas</span><span class="sxs-lookup"><span data-stu-id="298fd-121">Install the SDK and tools</span></span>
### <a name="to-use-visual-studio-2017"></a><span data-ttu-id="298fd-122">Cómo usar Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="298fd-122">To use Visual Studio 2017</span></span>
<span data-ttu-id="298fd-123">Las herramientas de Service Fabric forman parte de la carga de trabajo de Azure Development and Management de Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="298fd-123">Service Fabric Tools are part of the Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="298fd-124">Habilite esta carga de trabajo durante la instalación de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="298fd-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="298fd-125">Además, debe instalar el SDK de Microsoft Azure Service Fabric mediante el Instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="298fd-125">In addition, you need to install the Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="298fd-126">[Instalación del SDK de Microsoft Azure Service Fabric][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="298fd-126">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="to-use-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="298fd-127">Para utilizar Visual Studio 2015 (es necesario usar Visual Studio 2015 Update 2 o versiones posteriores)</span><span class="sxs-lookup"><span data-stu-id="298fd-127">To use Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="298fd-128">En Visual Studio 2015, las herramientas de Service Fabric se instalan con el SDK mediante el Instalador de plataforma web:</span><span class="sxs-lookup"><span data-stu-id="298fd-128">For Visual Studio 2015, Service Fabric tools are installed together with the SDK, using the Web Platform Installer:</span></span>

* <span data-ttu-id="298fd-129">[Instalación del SDK y las herramientas de Microsoft Azure Service Fabric][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="298fd-129">[Install the Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="298fd-130">Para instalar solamente el SDK</span><span class="sxs-lookup"><span data-stu-id="298fd-130">SDK installation only</span></span>
<span data-ttu-id="298fd-131">Si únicamente necesita el SDK, puede instalar este paquete:</span><span class="sxs-lookup"><span data-stu-id="298fd-131">If you only need the SDK, you can install this package:</span></span>
* <span data-ttu-id="298fd-132">[Instalación del SDK de Microsoft Azure Service Fabric][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="298fd-132">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="298fd-133">Las versiones actuales son:</span><span class="sxs-lookup"><span data-stu-id="298fd-133">The current versions are:</span></span>
* <span data-ttu-id="298fd-134">SDK de Service Fabric 2.7.198</span><span class="sxs-lookup"><span data-stu-id="298fd-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="298fd-135">Runtime de Service Fabric 5.7.198</span><span class="sxs-lookup"><span data-stu-id="298fd-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="298fd-136">Herramientas de Service Fabric para Visual Studio 2015 1.7.50721</span><span class="sxs-lookup"><span data-stu-id="298fd-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="298fd-137">Visual Studio 2017 Update 2 incluye Herramientas de Service Fabric para Visual Studio 1.6.20170504</span><span class="sxs-lookup"><span data-stu-id="298fd-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="298fd-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) incluye Herramientas de Service Fabric para Visual Studio 1.7.20170721</span><span class="sxs-lookup"><span data-stu-id="298fd-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="298fd-139">Para obtener una lista de las versiones admitidas, consulte [Compatibilidad con Service Fabric](service-fabric-support.md).</span><span class="sxs-lookup"><span data-stu-id="298fd-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="298fd-140">Habilitar la ejecución del script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="298fd-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="298fd-141">Service Fabric usa scripts de Windows PowerShell para crear un clúster de desarrollo local e implementar aplicaciones desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="298fd-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="298fd-142">De forma predeterminada, Windows bloquea la ejecución de estos scripts.</span><span class="sxs-lookup"><span data-stu-id="298fd-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="298fd-143">Para habilitarlos, debe modificar la directiva de ejecución de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="298fd-143">To enable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="298fd-144">Abra PowerShell como administrador y escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="298fd-144">Open PowerShell as an administrator and enter the following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="298fd-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="298fd-145">Next steps</span></span>
<span data-ttu-id="298fd-146">Ahora que ha terminado la configuración del entorno de desarrollo, puede empezar a compilar y ejecutar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="298fd-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="298fd-147">Creación de la primera aplicación de Service Fabric en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="298fd-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="298fd-148">Introducción a la implementación y actualización de aplicaciones en un clúster local</span><span class="sxs-lookup"><span data-stu-id="298fd-148">Learn how to deploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="298fd-149">Más información sobre los modelos de programación: Reliable Services y Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="298fd-149">Learn about the programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="298fd-150">Consulta de los ejemplos de código de Service Fabric en GitHub</span><span class="sxs-lookup"><span data-stu-id="298fd-150">Check out the Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="298fd-151">Visualización del clúster mediante el Explorador de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="298fd-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="298fd-152">Siga la ruta de aprendizaje de Service Fabric para obtener una amplia introducción a la plataforma</span><span class="sxs-lookup"><span data-stu-id="298fd-152">Follow the Service Fabric learning path to get a broad introduction to the platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="298fd-153">Más información sobre las [opciones de soporte técnico de Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="298fd-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

<span data-ttu-id="298fd-154">[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Página de campaña de Service Fabric"</span><span class="sxs-lookup"><span data-stu-id="298fd-154">[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric campaign page"</span></span>
<span data-ttu-id="298fd-155">[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"</span><span class="sxs-lookup"><span data-stu-id="298fd-155">[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"</span></span>
<span data-ttu-id="298fd-156">[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "Vínculo de WebPI de VS 2015"</span><span class="sxs-lookup"><span data-stu-id="298fd-156">[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI link"</span></span>
<span data-ttu-id="298fd-157">[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Vínculo de WebPI de Dev15"</span><span class="sxs-lookup"><span data-stu-id="298fd-157">[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI link"</span></span>
<span data-ttu-id="298fd-158">[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Vínculo de WebPI de SDK de núcleo"</span><span class="sxs-lookup"><span data-stu-id="298fd-158">[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI link"</span></span>
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395

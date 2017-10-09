---
title: aaaSet un entorno de desarrollo para Azure microservicios | Documentos de Microsoft
description: "Instalar en tiempo de ejecución de hello, SDK y herramientas y crear un clúster de desarrollo local. Después de completar la instalación, estará listo toobuild aplicaciones."
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
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="6988f-104">Preparación del entorno de desarrollo</span><span class="sxs-lookup"><span data-stu-id="6988f-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6988f-105">Windows</span><span class="sxs-lookup"><span data-stu-id="6988f-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="6988f-106">Linux</span><span class="sxs-lookup"><span data-stu-id="6988f-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="6988f-107">OSX</span><span class="sxs-lookup"><span data-stu-id="6988f-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="6988f-108">toobuild y ejecute [aplicaciones de Azure Service Fabric] [ 1] en el equipo de desarrollo, instale en tiempo de ejecución de hello, SDK y herramientas.</span><span class="sxs-lookup"><span data-stu-id="6988f-108">toobuild and run [Azure Service Fabric applications][1] on your development machine, install hello runtime, SDK, and tools.</span></span> <span data-ttu-id="6988f-109">También debe tooenable ejecución de scripts de Windows PowerShell de hello incluidos en hello SDK.</span><span class="sxs-lookup"><span data-stu-id="6988f-109">You also need tooenable execution of hello Windows PowerShell scripts included in hello SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6988f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6988f-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="6988f-111">Versiones de sistemas operativos compatibles</span><span class="sxs-lookup"><span data-stu-id="6988f-111">Supported operating system versions</span></span>
<span data-ttu-id="6988f-112">Hola siguientes versiones de sistema operativo es compatibles para el desarrollo:</span><span class="sxs-lookup"><span data-stu-id="6988f-112">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="6988f-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="6988f-113">Windows 7</span></span>
* <span data-ttu-id="6988f-114">Windows 8/Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="6988f-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="6988f-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="6988f-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="6988f-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="6988f-116">Windows Server 2016</span></span>
* <span data-ttu-id="6988f-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="6988f-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="6988f-118">Windows 7 solo incluye de forma predeterminada Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="6988f-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="6988f-119">Los cmdlets de PowerShell de Service Fabric requieren PowerShell 3.0 o superior.</span><span class="sxs-lookup"><span data-stu-id="6988f-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="6988f-120">También puede [descargar Windows PowerShell 5.0] [ powershell5-download] de hello Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="6988f-120">You can [download Windows PowerShell 5.0][powershell5-download] from hello Microsoft Download Center.</span></span>
> 
> 

## <a name="install-hello-sdk-and-tools"></a><span data-ttu-id="6988f-121">Instalar Hola SDK y herramientas</span><span class="sxs-lookup"><span data-stu-id="6988f-121">Install hello SDK and tools</span></span>
### <a name="toouse-visual-studio-2017"></a><span data-ttu-id="6988f-122">toouse 2017 de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6988f-122">toouse Visual Studio 2017</span></span>
<span data-ttu-id="6988f-123">Herramientas del servicio de Fabric forman parte de la carga de trabajo de hello administración y desarrollo de Azure en Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="6988f-123">Service Fabric Tools are part of hello Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="6988f-124">Habilite esta carga de trabajo durante la instalación de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6988f-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="6988f-125">Además, necesitará tooinstall Hola Microsoft Azure Service Fabric SDK, mediante el instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="6988f-125">In addition, you need tooinstall hello Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="6988f-126">[Instalar SDK del servicio de Microsoft Azure Fabric Hola][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="6988f-126">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="6988f-127">toouse Visual Studio 2015 (requiere Visual Studio 2015 Update 2 o posterior)</span><span class="sxs-lookup"><span data-stu-id="6988f-127">toouse Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="6988f-128">Para Visual Studio 2015, herramientas de Service Fabric se instalan junto con el SDK, con el instalador de plataforma Web de Hola Hola:</span><span class="sxs-lookup"><span data-stu-id="6988f-128">For Visual Studio 2015, Service Fabric tools are installed together with hello SDK, using hello Web Platform Installer:</span></span>

* <span data-ttu-id="6988f-129">[Instalar SDK del servicio de Microsoft Azure Fabric hello y herramientas][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="6988f-129">[Install hello Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="6988f-130">Para instalar solamente el SDK</span><span class="sxs-lookup"><span data-stu-id="6988f-130">SDK installation only</span></span>
<span data-ttu-id="6988f-131">Si solo necesita Hola SDK, puede instalar este paquete:</span><span class="sxs-lookup"><span data-stu-id="6988f-131">If you only need hello SDK, you can install this package:</span></span>
* <span data-ttu-id="6988f-132">[Instalar SDK del servicio de Microsoft Azure Fabric Hola][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="6988f-132">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="6988f-133">las versiones actuales de Hello son:</span><span class="sxs-lookup"><span data-stu-id="6988f-133">hello current versions are:</span></span>
* <span data-ttu-id="6988f-134">SDK de Service Fabric 2.7.198</span><span class="sxs-lookup"><span data-stu-id="6988f-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="6988f-135">Runtime de Service Fabric 5.7.198</span><span class="sxs-lookup"><span data-stu-id="6988f-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="6988f-136">Herramientas de Service Fabric para Visual Studio 2015 1.7.50721</span><span class="sxs-lookup"><span data-stu-id="6988f-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="6988f-137">Visual Studio 2017 Update 2 incluye Herramientas de Service Fabric para Visual Studio 1.6.20170504</span><span class="sxs-lookup"><span data-stu-id="6988f-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="6988f-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) incluye Herramientas de Service Fabric para Visual Studio 1.7.20170721</span><span class="sxs-lookup"><span data-stu-id="6988f-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="6988f-139">Para obtener una lista de las versiones admitidas, consulte [Compatibilidad con Service Fabric](service-fabric-support.md).</span><span class="sxs-lookup"><span data-stu-id="6988f-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="6988f-140">Habilitar la ejecución del script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="6988f-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="6988f-141">Service Fabric usa scripts de Windows PowerShell para crear un clúster de desarrollo local e implementar aplicaciones desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6988f-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="6988f-142">De forma predeterminada, Windows bloquea la ejecución de estos scripts.</span><span class="sxs-lookup"><span data-stu-id="6988f-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="6988f-143">tooenable usarlas, debe modificar la directiva de ejecución de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6988f-143">tooenable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="6988f-144">Abra PowerShell como administrador y escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6988f-144">Open PowerShell as an administrator and enter hello following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="6988f-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6988f-145">Next steps</span></span>
<span data-ttu-id="6988f-146">Ahora que ha terminado la configuración del entorno de desarrollo, puede empezar a compilar y ejecutar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6988f-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="6988f-147">Creación de la primera aplicación de Service Fabric en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6988f-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="6988f-148">Obtenga información acerca de cómo toodeploy y administrar aplicaciones en el clúster local</span><span class="sxs-lookup"><span data-stu-id="6988f-148">Learn how toodeploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="6988f-149">Obtener información sobre los modelos de programación de hello: servicios de confianza y actores confiable</span><span class="sxs-lookup"><span data-stu-id="6988f-149">Learn about hello programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="6988f-150">Extraer del repositorio Hola Service Fabric ejemplos de código en GitHub</span><span class="sxs-lookup"><span data-stu-id="6988f-150">Check out hello Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="6988f-151">Visualización del clúster mediante el Explorador de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6988f-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="6988f-152">Siga hello tooget de ruta de acceso de aprendizaje de una plataforma de toohello introducción amplia de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6988f-152">Follow hello Service Fabric learning path tooget a broad introduction toohello platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="6988f-153">Más información sobre las [opciones de soporte técnico de Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="6988f-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Página de campaña de Service Fabric"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "Vínculo de WebPI de VS 2015"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Vínculo de WebPI de Dev15"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Vínculo de WebPI de SDK de núcleo"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395

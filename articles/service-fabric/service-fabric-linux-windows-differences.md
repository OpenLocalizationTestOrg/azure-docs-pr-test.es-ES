---
title: Diferencias entre Azure Service Fabric en Windows y en Linux | Documentos de Microsoft
description: "Diferencias entre Azure Service Fabric, versión preliminar, en Linux y Azure Service Fabric en Windows."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 7b80bb7d4a4e6a1b4cf47ce87200f47339785c53
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a><span data-ttu-id="50e7f-103">Diferencias entre Service Fabric en Linux (versión preliminar) y Windows (disponible con carácter general)</span><span class="sxs-lookup"><span data-stu-id="50e7f-103">Differences between Service Fabric on Linux (preview) and Windows (generally available)</span></span>

<span data-ttu-id="50e7f-104">Dado que Service Fabric en Linux está en versión preliminar, hay varias características que se admiten en Windows, pero aún no en Linux.</span><span class="sxs-lookup"><span data-stu-id="50e7f-104">Since Service Fabric on Linux is a preview, there are some features that are supported on Windows, but not yet on Linux.</span></span> <span data-ttu-id="50e7f-105">Por último, los conjuntos de características estarán a la par cuando Service Fabric en Linux esté disponible con carácter general.</span><span class="sxs-lookup"><span data-stu-id="50e7f-105">Eventually, the feature sets will be at parity when Service Fabric on Linux becomes generally available.</span></span> <span data-ttu-id="50e7f-106">En las próximas versiones, esta distancia se reducirá.</span><span class="sxs-lookup"><span data-stu-id="50e7f-106">With upcoming releases, this feature gap will shrink.</span></span> <span data-ttu-id="50e7f-107">Existen las siguientes diferencias entre las últimas versiones disponibles (es decir, entre la versión 5.6 en Windows y la versión 5.5 en Linux):</span><span class="sxs-lookup"><span data-stu-id="50e7f-107">The following differences exist between the latest available releases (that is, between version 5.6 on Windows and version 5.5 on Linux):</span></span> 

* <span data-ttu-id="50e7f-108">Colecciones confiables (y servicios con estado confiables)</span><span class="sxs-lookup"><span data-stu-id="50e7f-108">Reliable Collections (and Reliable Stateful Services)</span></span> 
* <span data-ttu-id="50e7f-109">ReverseProxy</span><span class="sxs-lookup"><span data-stu-id="50e7f-109">ReverseProxy</span></span> 
* <span data-ttu-id="50e7f-110">Instalador independiente</span><span class="sxs-lookup"><span data-stu-id="50e7f-110">Standalone installer</span></span> 
* <span data-ttu-id="50e7f-111">Validación del esquema XML para archivos de manifiesto</span><span class="sxs-lookup"><span data-stu-id="50e7f-111">XML schema validation for manifest files</span></span> 
* <span data-ttu-id="50e7f-112">Redireccionamiento de la consola</span><span class="sxs-lookup"><span data-stu-id="50e7f-112">Console redirection</span></span> 
* <span data-ttu-id="50e7f-113">El servicio de análisis de errores (FAS)</span><span class="sxs-lookup"><span data-stu-id="50e7f-113">The Fault Analysis Service (FAS)</span></span>
* <span data-ttu-id="50e7f-114">Docker Compose y controladores de volúmenes y de registro para contenedores</span><span class="sxs-lookup"><span data-stu-id="50e7f-114">Docker compose and volume and logging drivers for containers</span></span> 
* <span data-ttu-id="50e7f-115">Regulación de recursos para contenedores y servicios</span><span class="sxs-lookup"><span data-stu-id="50e7f-115">Resource governance for containers and services</span></span> 
* <span data-ttu-id="50e7f-116">Servicio DNS</span><span class="sxs-lookup"><span data-stu-id="50e7f-116">DNS service</span></span>
* <span data-ttu-id="50e7f-117">Compatibilidad con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50e7f-117">Azure Active Directory support</span></span>
* <span data-ttu-id="50e7f-118">Comandos de la CLI equivalentes a ciertos comandos de Powershell</span><span class="sxs-lookup"><span data-stu-id="50e7f-118">CLI command equivalents of certain Powershell commands</span></span> 
* <span data-ttu-id="50e7f-119">Solo se puede ejecutar un subconjunto de comandos de Powershell en un clúster de Linux (tal como se explica detalladamente en la sección siguiente).</span><span class="sxs-lookup"><span data-stu-id="50e7f-119">Only a subset of Powershell commands can be run against a Linux cluster (as expanded in the next section).</span></span>

>[!NOTE]
><span data-ttu-id="50e7f-120">El redireccionamiento de la consola no se admite en los clústeres de producción, ni siquiera en Windows.</span><span class="sxs-lookup"><span data-stu-id="50e7f-120">Console redirection is not supported in production clusters, even on Windows.</span></span>

<span data-ttu-id="50e7f-121">Las herramientas de desarrollo también son diferentes en Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="50e7f-121">Development tooling is also different between Windows and Linux.</span></span> <span data-ttu-id="50e7f-122">VisualStudio, Powershell, VSTS, and ETW se usan en Windows, mientras que Yeoman, Eclipse, Jenkins, y LTTng se usan en Linux.</span><span class="sxs-lookup"><span data-stu-id="50e7f-122">VisualStudio, Powershell, VSTS, and ETW are used on Windows while Yeoman, Eclipse, Jenkins, and LTTng are used on Linux.</span></span>

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a><span data-ttu-id="50e7f-123">Cmdlets de PowerShell que no funcionan en un clúster de Service Fabric para Linux</span><span class="sxs-lookup"><span data-stu-id="50e7f-123">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span></span>

* <span data-ttu-id="50e7f-124">Invoke-ServiceFabricChaosTestScenario</span><span class="sxs-lookup"><span data-stu-id="50e7f-124">Invoke-ServiceFabricChaosTestScenario</span></span>
* <span data-ttu-id="50e7f-125">Invoke-ServiceFabricFailoverTestScenario</span><span class="sxs-lookup"><span data-stu-id="50e7f-125">Invoke-ServiceFabricFailoverTestScenario</span></span>
* <span data-ttu-id="50e7f-126">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="50e7f-126">Invoke-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="50e7f-127">Invoke-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="50e7f-127">Invoke-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="50e7f-128">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="50e7f-128">Restart-ServiceFabricPartition</span></span>
* <span data-ttu-id="50e7f-129">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="50e7f-129">Start-ServiceFabricNode</span></span>
* <span data-ttu-id="50e7f-130">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="50e7f-130">Stop-ServiceFabricNode</span></span>
* <span data-ttu-id="50e7f-131">Get-ServiceFabricImageStoreContent</span><span class="sxs-lookup"><span data-stu-id="50e7f-131">Get-ServiceFabricImageStoreContent</span></span>
* <span data-ttu-id="50e7f-132">Get-ServiceFabricChaosReport</span><span class="sxs-lookup"><span data-stu-id="50e7f-132">Get-ServiceFabricChaosReport</span></span>
* <span data-ttu-id="50e7f-133">Get-ServiceFabricNodeTransitionProgress</span><span class="sxs-lookup"><span data-stu-id="50e7f-133">Get-ServiceFabricNodeTransitionProgress</span></span>
* <span data-ttu-id="50e7f-134">Get-ServiceFabricPartitionDataLossProgress</span><span class="sxs-lookup"><span data-stu-id="50e7f-134">Get-ServiceFabricPartitionDataLossProgress</span></span>
* <span data-ttu-id="50e7f-135">Get-ServiceFabricPartitionQuorumLossProgress</span><span class="sxs-lookup"><span data-stu-id="50e7f-135">Get-ServiceFabricPartitionQuorumLossProgress</span></span>
* <span data-ttu-id="50e7f-136">Get-ServiceFabricPartitionRestartProgress</span><span class="sxs-lookup"><span data-stu-id="50e7f-136">Get-ServiceFabricPartitionRestartProgress</span></span>
* <span data-ttu-id="50e7f-137">Get-ServiceFabricTestCommandStatusList</span><span class="sxs-lookup"><span data-stu-id="50e7f-137">Get-ServiceFabricTestCommandStatusList</span></span>
* <span data-ttu-id="50e7f-138">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="50e7f-138">Remove-ServiceFabricTestState</span></span>
* <span data-ttu-id="50e7f-139">Start-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="50e7f-139">Start-ServiceFabricChaos</span></span>
* <span data-ttu-id="50e7f-140">Start-ServiceFabricNodeTransition</span><span class="sxs-lookup"><span data-stu-id="50e7f-140">Start-ServiceFabricNodeTransition</span></span>
* <span data-ttu-id="50e7f-141">Start-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="50e7f-141">Start-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="50e7f-142">Start-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="50e7f-142">Start-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="50e7f-143">Start-ServiceFabricPartitionRestart</span><span class="sxs-lookup"><span data-stu-id="50e7f-143">Start-ServiceFabricPartitionRestart</span></span>
* <span data-ttu-id="50e7f-144">Stop-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="50e7f-144">Stop-ServiceFabricChaos</span></span>
* <span data-ttu-id="50e7f-145">Stop-ServiceFabricTestCommand</span><span class="sxs-lookup"><span data-stu-id="50e7f-145">Stop-ServiceFabricTestCommand</span></span>
* <span data-ttu-id="50e7f-146">Cmd</span><span class="sxs-lookup"><span data-stu-id="50e7f-146">Cmd</span></span>
* <span data-ttu-id="50e7f-147">Get-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="50e7f-147">Get-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="50e7f-148">Get-ServiceFabricClusterConfiguration</span><span class="sxs-lookup"><span data-stu-id="50e7f-148">Get-ServiceFabricClusterConfiguration</span></span>
* <span data-ttu-id="50e7f-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span><span class="sxs-lookup"><span data-stu-id="50e7f-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span></span>
* <span data-ttu-id="50e7f-150">Get-ServiceFabricPackageDebugParameters</span><span class="sxs-lookup"><span data-stu-id="50e7f-150">Get-ServiceFabricPackageDebugParameters</span></span>
* <span data-ttu-id="50e7f-151">New-ServiceFabricPackageDebugParameter</span><span class="sxs-lookup"><span data-stu-id="50e7f-151">New-ServiceFabricPackageDebugParameter</span></span>
* <span data-ttu-id="50e7f-152">New-ServiceFabricPackageSharingPolicy</span><span class="sxs-lookup"><span data-stu-id="50e7f-152">New-ServiceFabricPackageSharingPolicy</span></span>
* <span data-ttu-id="50e7f-153">Add-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="50e7f-153">Add-ServiceFabricNode</span></span>
* <span data-ttu-id="50e7f-154">Copy-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="50e7f-154">Copy-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="50e7f-155">Get-ServiceFabricRuntimeSupportedVersion</span><span class="sxs-lookup"><span data-stu-id="50e7f-155">Get-ServiceFabricRuntimeSupportedVersion</span></span>
* <span data-ttu-id="50e7f-156">Get-ServiceFabricRuntimeUpgradeVersion</span><span class="sxs-lookup"><span data-stu-id="50e7f-156">Get-ServiceFabricRuntimeUpgradeVersion</span></span>
* <span data-ttu-id="50e7f-157">New-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="50e7f-157">New-ServiceFabricCluster</span></span>
* <span data-ttu-id="50e7f-158">New-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="50e7f-158">New-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="50e7f-159">Remove-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="50e7f-159">Remove-ServiceFabricCluster</span></span>
* <span data-ttu-id="50e7f-160">Remove-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="50e7f-160">Remove-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="50e7f-161">Remove-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="50e7f-161">Remove-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="50e7f-162">Test-ServiceFabricClusterManifest</span><span class="sxs-lookup"><span data-stu-id="50e7f-162">Test-ServiceFabricClusterManifest</span></span>
* <span data-ttu-id="50e7f-163">Test-ServiceFabricConfiguration</span><span class="sxs-lookup"><span data-stu-id="50e7f-163">Test-ServiceFabricConfiguration</span></span>
* <span data-ttu-id="50e7f-164">Update-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="50e7f-164">Update-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="50e7f-165">Approve-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="50e7f-165">Approve-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="50e7f-166">Complete-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="50e7f-166">Complete-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="50e7f-167">Get-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="50e7f-167">Get-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="50e7f-168">Invoke-ServiceFabricDecryptText</span><span class="sxs-lookup"><span data-stu-id="50e7f-168">Invoke-ServiceFabricDecryptText</span></span>
* <span data-ttu-id="50e7f-169">Invoke-ServiceFabricEncryptSecret</span><span class="sxs-lookup"><span data-stu-id="50e7f-169">Invoke-ServiceFabricEncryptSecret</span></span>
* <span data-ttu-id="50e7f-170">Invoke-ServiceFabricEncryptText</span><span class="sxs-lookup"><span data-stu-id="50e7f-170">Invoke-ServiceFabricEncryptText</span></span>
* <span data-ttu-id="50e7f-171">Invoke-ServiceFabricInfrastructureCommand</span><span class="sxs-lookup"><span data-stu-id="50e7f-171">Invoke-ServiceFabricInfrastructureCommand</span></span>
* <span data-ttu-id="50e7f-172">Invoke-ServiceFabricInfrastructureQuery</span><span class="sxs-lookup"><span data-stu-id="50e7f-172">Invoke-ServiceFabricInfrastructureQuery</span></span>
* <span data-ttu-id="50e7f-173">Remove-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="50e7f-173">Remove-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="50e7f-174">Start-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="50e7f-174">Start-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="50e7f-175">Stop-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="50e7f-175">Stop-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="50e7f-176">Update-ServiceFabricRepairTaskHealthPolicy</span><span class="sxs-lookup"><span data-stu-id="50e7f-176">Update-ServiceFabricRepairTaskHealthPolicy</span></span>



## <a name="next-steps"></a><span data-ttu-id="50e7f-177">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="50e7f-177">Next steps</span></span>
* [<span data-ttu-id="50e7f-178">Prepare your development environment on Linux</span><span class="sxs-lookup"><span data-stu-id="50e7f-178">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="50e7f-179">Prepare your development environment on OSX</span><span class="sxs-lookup"><span data-stu-id="50e7f-179">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="50e7f-180">Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con Yeoman</span><span class="sxs-lookup"><span data-stu-id="50e7f-180">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="50e7f-181">Creación e implementación de la primera aplicación de Java para Service Fabric con el complemento de Eclipse para Service Fabric</span><span class="sxs-lookup"><span data-stu-id="50e7f-181">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="50e7f-182">Creación de su primera aplicación de CSharp en Linux</span><span class="sxs-lookup"><span data-stu-id="50e7f-182">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="50e7f-183">Uso de la CLI de Service Fabric para administrar las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="50e7f-183">Use the Service Fabric CLI to manage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)

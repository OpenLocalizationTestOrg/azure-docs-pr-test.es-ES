---
title: Paquete de Service Fabric independientes para Windows Server aaaAzure | Documentos de Microsoft
description: "Descripción y el contenido del paquete de hello Azure Service Fabric independientes para Windows Server."
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik
ms.openlocfilehash: e4c6cb9128d659144e559fcad06bb78c9969dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="contents-of-service-fabric-standalone-package-for-windows-server"></a><span data-ttu-id="e769e-103">Contenido del paquete independiente de Service Fabric para Windows Server</span><span class="sxs-lookup"><span data-stu-id="e769e-103">Contents of Service Fabric Standalone package for Windows Server</span></span>
<span data-ttu-id="e769e-104">Hola [descargado](http://go.microsoft.com/fwlink/?LinkId=730690) paquete independiente de tejido de servicio, encontrará Hola siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="e769e-104">In hello [downloaded](http://go.microsoft.com/fwlink/?LinkId=730690) Service Fabric Standalone package, you will find hello following files:</span></span>

| <span data-ttu-id="e769e-105">**Nombre de archivo**</span><span class="sxs-lookup"><span data-stu-id="e769e-105">**File name**</span></span> | <span data-ttu-id="e769e-106">**Descripción breve**</span><span class="sxs-lookup"><span data-stu-id="e769e-106">**Short description**</span></span> |
| --- | --- |
| <span data-ttu-id="e769e-107">CreateServiceFabricCluster.ps1</span><span class="sxs-lookup"><span data-stu-id="e769e-107">CreateServiceFabricCluster.ps1</span></span> |<span data-ttu-id="e769e-108">Un script de PowerShell que crea el clúster de hello mediante configuración de hello en ClusterConfig.json.</span><span class="sxs-lookup"><span data-stu-id="e769e-108">A PowerShell script that creates hello cluster using hello settings in ClusterConfig.json.</span></span> |
| <span data-ttu-id="e769e-109">RemoveServiceFabricCluster.ps1</span><span class="sxs-lookup"><span data-stu-id="e769e-109">RemoveServiceFabricCluster.ps1</span></span> |<span data-ttu-id="e769e-110">Un script de PowerShell que quita un clúster con configuración de hello en ClusterConfig.json.</span><span class="sxs-lookup"><span data-stu-id="e769e-110">A PowerShell script that removes a cluster using hello settings in ClusterConfig.json.</span></span> |
| <span data-ttu-id="e769e-111">AddNode.ps1</span><span class="sxs-lookup"><span data-stu-id="e769e-111">AddNode.ps1</span></span> |<span data-ttu-id="e769e-112">Un script de PowerShell para agregar un nodo existente de tooan implementa clústeres de máquina actual Hola.</span><span class="sxs-lookup"><span data-stu-id="e769e-112">A PowerShell script for adding a node tooan existing deployed cluster on hello current machine.</span></span> |
| <span data-ttu-id="e769e-113">RemoveNode.ps1</span><span class="sxs-lookup"><span data-stu-id="e769e-113">RemoveNode.ps1</span></span> |<span data-ttu-id="e769e-114">Un script de PowerShell para quitar un nodo de una existente implementa clústeres de máquina actual Hola.</span><span class="sxs-lookup"><span data-stu-id="e769e-114">A PowerShell script for removing a node from an existing deployed cluster from hello current machine.</span></span> |
| <span data-ttu-id="e769e-115">CleanFabric.ps1</span><span class="sxs-lookup"><span data-stu-id="e769e-115">CleanFabric.ps1</span></span> |<span data-ttu-id="e769e-116">Un script de PowerShell para la limpieza de una instalación de Service Fabric máquina actual Hola independiente.</span><span class="sxs-lookup"><span data-stu-id="e769e-116">A PowerShell script for cleaning a standalone Service Fabric installation off hello current machine.</span></span> <span data-ttu-id="e769e-117">Las instalaciones anteriores de MSI se deben quitar mediante sus propios desinstaladores asociados.</span><span class="sxs-lookup"><span data-stu-id="e769e-117">Previous MSI installations should be removed using their own associated uninstallers.</span></span> |
| <span data-ttu-id="e769e-118">TestConfiguration.ps1</span><span class="sxs-lookup"><span data-stu-id="e769e-118">TestConfiguration.ps1</span></span> |<span data-ttu-id="e769e-119">Un script de PowerShell para analizar la infraestructura de hello como se especifica en hello Cluster.json.</span><span class="sxs-lookup"><span data-stu-id="e769e-119">A PowerShell script for analyzing hello infrastructure as specified in hello Cluster.json.</span></span> |
| <span data-ttu-id="e769e-120">DownloadServiceFabricRuntimePackage.ps1</span><span class="sxs-lookup"><span data-stu-id="e769e-120">DownloadServiceFabricRuntimePackage.ps1</span></span> |<span data-ttu-id="e769e-121">Un script de PowerShell que se usa para descargar el paquete en tiempo de ejecución más reciente de hello fuera de banda, para escenarios donde hello implementar máquina no está conectado toohello internet.</span><span class="sxs-lookup"><span data-stu-id="e769e-121">A PowerShell script used for downloading hello latest runtime package out of band, for scenarios where hello deploying machine is not connected toohello internet.</span></span> |
| <span data-ttu-id="e769e-122">DeploymentComponentsAutoextractor.exe</span><span class="sxs-lookup"><span data-stu-id="e769e-122">DeploymentComponentsAutoextractor.exe</span></span> |<span data-ttu-id="e769e-123">Archivo que contiene los componentes de implementación autoextraíble utiliza Hola scripts de paquete independiente.</span><span class="sxs-lookup"><span data-stu-id="e769e-123">Self-extracting archive containing Deployment Components used by hello Standalone package scripts.</span></span> |
| <span data-ttu-id="e769e-124">EULA_ENU.txt</span><span class="sxs-lookup"><span data-stu-id="e769e-124">EULA_ENU.txt</span></span> |<span data-ttu-id="e769e-125">términos de licencia de Hola para hello el uso de paquete de Windows Server de Microsoft Azure Service Fabric independiente.</span><span class="sxs-lookup"><span data-stu-id="e769e-125">hello license terms for hello use of Microsoft Azure Service Fabric standalone Windows Server package.</span></span> <span data-ttu-id="e769e-126">También puede [descargar una copia del CLUF de hello](http://go.microsoft.com/fwlink/?LinkID=733084) ahora.</span><span class="sxs-lookup"><span data-stu-id="e769e-126">You can [download a copy of hello EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span> |
| <span data-ttu-id="e769e-127">Readme.txt</span><span class="sxs-lookup"><span data-stu-id="e769e-127">Readme.txt</span></span> |<span data-ttu-id="e769e-128">Un vínculo toohello versión notas e instrucciones básicas para la instalación.</span><span class="sxs-lookup"><span data-stu-id="e769e-128">A link toohello release notes and basic installation instructions.</span></span> <span data-ttu-id="e769e-129">Es un subconjunto de instrucciones de hello en este documento.</span><span class="sxs-lookup"><span data-stu-id="e769e-129">It is a subset of hello instructions in this document.</span></span> |
| <span data-ttu-id="e769e-130">ThirdPartyNotice.rtf</span><span class="sxs-lookup"><span data-stu-id="e769e-130">ThirdPartyNotice.rtf</span></span> |<span data-ttu-id="e769e-131">Aviso de software de terceros que se encuentra en el paquete de saludo.</span><span class="sxs-lookup"><span data-stu-id="e769e-131">Notice of third-party software that is in hello package.</span></span> |
| <span data-ttu-id="e769e-132">Tools\Microsoft.Azure.ServiceFabric.WindowsServer.SupportPackage.zip</span><span class="sxs-lookup"><span data-stu-id="e769e-132">Tools\Microsoft.Azure.ServiceFabric.WindowsServer.SupportPackage.zip</span></span> |<span data-ttu-id="e769e-133">StandaloneLogCollector.exe que se ejecuta en petición toocollect y carga el seguimiento de los registros de tooMicrosoft con el fin de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="e769e-133">StandaloneLogCollector.exe which is run on demand toocollect and upload trace logs tooMicrosoft for support purpose.</span></span> |
| <span data-ttu-id="e769e-134">Tools\ServiceFabricUpdateService.zip</span><span class="sxs-lookup"><span data-stu-id="e769e-134">Tools\ServiceFabricUpdateService.zip</span></span> |<span data-ttu-id="e769e-135">Utiliza una herramienta tooenable la actualización automática de código para los clústeres que no tienen acceso a internet.</span><span class="sxs-lookup"><span data-stu-id="e769e-135">A tool used tooenable auto code upgrade for clusters which don't have internet access.</span></span> <span data-ttu-id="e769e-136">[aquí](service-fabric-cluster-upgrade-windows-server.md)</span><span class="sxs-lookup"><span data-stu-id="e769e-136">More details can be found [here](service-fabric-cluster-upgrade-windows-server.md)</span></span>|

<span data-ttu-id="e769e-137">**Plantillas**</span><span class="sxs-lookup"><span data-stu-id="e769e-137">**Templates**</span></span> 
| <span data-ttu-id="e769e-138">**Nombre de archivo**</span><span class="sxs-lookup"><span data-stu-id="e769e-138">**File name**</span></span> | <span data-ttu-id="e769e-139">**Descripción breve**</span><span class="sxs-lookup"><span data-stu-id="e769e-139">**Short description**</span></span> |
| --- | --- |
| <span data-ttu-id="e769e-140">ClusterConfig.Unsecure.DevCluster.json</span><span class="sxs-lookup"><span data-stu-id="e769e-140">ClusterConfig.Unsecure.DevCluster.json</span></span> |<span data-ttu-id="e769e-141">Un archivo de ejemplo de configuración de clúster que contiene la configuración de Hola para una no seguro, tres nodos, solo el equipo (o máquina virtual) clúster de desarrollo, incluida la información de Hola para cada nodo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e769e-141">A cluster configuration sample file that contains hello settings for an unsecured, three-node, single-machine (or virtual machine) development cluster, including hello information for each node in hello cluster.</span></span> |
| <span data-ttu-id="e769e-142">ClusterConfig.Unsecure.MultiMachine.json</span><span class="sxs-lookup"><span data-stu-id="e769e-142">ClusterConfig.Unsecure.MultiMachine.json</span></span> |<span data-ttu-id="e769e-143">Un archivo de ejemplo de configuración de clúster que contiene la configuración de Hola para un clúster no seguro, varios equipos (o máquina virtual), incluida la información de Hola para cada máquina en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e769e-143">A cluster configuration sample file that contains hello settings for an unsecured, multi-machine (or virtual machine) cluster, including hello information for each machine in hello cluster.</span></span> |
| <span data-ttu-id="e769e-144">ClusterConfig.Windows.DevCluster.json</span><span class="sxs-lookup"><span data-stu-id="e769e-144">ClusterConfig.Windows.DevCluster.json</span></span> |<span data-ttu-id="e769e-145">Un archivo de ejemplo de configuración de clúster que contiene todos los clúster de desarrollo de configuración para un único equipo seguro y tres nodos, (o la máquina virtual) de hello, incluida la información de Hola para cada nodo que está en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e769e-145">A cluster configuration sample file that contains all hello settings for a secure, three-node, single-machine (or virtual machine) development cluster, including hello information for each node that is in hello cluster.</span></span> <span data-ttu-id="e769e-146">clúster de Hello está protegido mediante [identidades de Windows](https://msdn.microsoft.com/library/ff649396.aspx).</span><span class="sxs-lookup"><span data-stu-id="e769e-146">hello cluster is secured by using [Windows identities](https://msdn.microsoft.com/library/ff649396.aspx).</span></span> |
| <span data-ttu-id="e769e-147">ClusterConfig.Windows.MultiMachine.json</span><span class="sxs-lookup"><span data-stu-id="e769e-147">ClusterConfig.Windows.MultiMachine.json</span></span> |<span data-ttu-id="e769e-148">Un archivo de ejemplo de configuración de clúster que contiene toda la configuración para un clúster de varios equipos (o máquinas virtuales) seguro, utilizando la seguridad de Windows, incluida la información de Hola para cada máquina que se encuentra en clúster segura Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="e769e-148">A cluster configuration sample file that contains all hello settings for a secure, multi-machine (or virtual machine) cluster using Windows security, including hello information for each machine that is in hello secure cluster.</span></span> <span data-ttu-id="e769e-149">clúster de Hello está protegido mediante [identidades de Windows](https://msdn.microsoft.com/library/ff649396.aspx).</span><span class="sxs-lookup"><span data-stu-id="e769e-149">hello cluster is secured by using [Windows identities](https://msdn.microsoft.com/library/ff649396.aspx).</span></span> |
| <span data-ttu-id="e769e-150">ClusterConfig.x509.DevCluster.json</span><span class="sxs-lookup"><span data-stu-id="e769e-150">ClusterConfig.x509.DevCluster.json</span></span> |<span data-ttu-id="e769e-151">Un archivo de ejemplo de configuración de clúster que contiene todos los valores de hello para un seguro, tres nodos, solo el equipo (o máquina virtual) clúster de desarrollo, incluida la información de Hola para cada nodo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e769e-151">A cluster configuration sample file that contains all hello settings for a secure, three-node, single-machine (or virtual machine) development cluster, including hello information for each node in hello cluster.</span></span> <span data-ttu-id="e769e-152">Hello clúster se protege utilizando x509 certificados.</span><span class="sxs-lookup"><span data-stu-id="e769e-152">hello cluster is secured using x509 certificates.</span></span> |
| <span data-ttu-id="e769e-153">ClusterConfig.x509.MultiMachine.json</span><span class="sxs-lookup"><span data-stu-id="e769e-153">ClusterConfig.x509.MultiMachine.json</span></span> |<span data-ttu-id="e769e-154">Un archivo de ejemplo de configuración de clúster que contiene todos los valores de hello para hello seguros, clúster de varios equipos (o máquinas virtuales), incluida la información de Hola para cada nodo de clúster segura Hola.</span><span class="sxs-lookup"><span data-stu-id="e769e-154">A cluster configuration sample file that contains all hello settings for hello secure, multi-machine (or virtual machine) cluster, including hello information for each node in hello secure cluster.</span></span> <span data-ttu-id="e769e-155">Hello clúster se protege utilizando x509 certificados.</span><span class="sxs-lookup"><span data-stu-id="e769e-155">hello cluster is secured using x509 certificates.</span></span> |
| <span data-ttu-id="e769e-156">ClusterConfig.gMSA.Windows.MultiMachine.json</span><span class="sxs-lookup"><span data-stu-id="e769e-156">ClusterConfig.gMSA.Windows.MultiMachine.json</span></span> |<span data-ttu-id="e769e-157">Un archivo de ejemplo de configuración de clúster que contiene todos los valores de hello para hello seguros, clúster de varios equipos (o máquinas virtuales), incluida la información de Hola para cada nodo de clúster segura Hola.</span><span class="sxs-lookup"><span data-stu-id="e769e-157">A cluster configuration sample file that contains all hello settings for hello secure, multi-machine (or virtual machine) cluster, including hello information for each node in hello secure cluster.</span></span> <span data-ttu-id="e769e-158">Hello clúster se protege utilizando [cuentas de servicio administradas de grupo](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="e769e-158">hello cluster is secured using [Group Managed Service Accounts](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11).aspx).</span></span> |

## <a name="cluster-configuration-samples"></a><span data-ttu-id="e769e-159">Ejemplos de configuración del clúster</span><span class="sxs-lookup"><span data-stu-id="e769e-159">Cluster Configuration Samples</span></span>
<span data-ttu-id="e769e-160">Las versiones más recientes de plantillas de configuración de clúster pueden encontrarse en la página de GitHub de hello: [ejemplos de configuración de clúster independiente](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="e769e-160">Latest versions of cluster configuration templates can be found at hello GitHub page: [Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

## <a name="independent-runtime-package"></a><span data-ttu-id="e769e-161">Paquete del entorno en tiempo de ejecución independiente</span><span class="sxs-lookup"><span data-stu-id="e769e-161">Independent Runtime Package</span></span>
<span data-ttu-id="e769e-162">paquete en tiempo de ejecución más reciente de Hola se descarga automáticamente durante la implementación de clúster de [vínculo Download - servicio de Fabric en tiempo de ejecución - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span><span class="sxs-lookup"><span data-stu-id="e769e-162">hello latest runtime package is downloaded automatically during cluster deployment from [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span>

## <a name="related"></a><span data-ttu-id="e769e-163">Temas relacionados</span><span class="sxs-lookup"><span data-stu-id="e769e-163">Related</span></span>
* [<span data-ttu-id="e769e-164">Creación de un clúster de Azure Service Fabric independiente</span><span class="sxs-lookup"><span data-stu-id="e769e-164">Create a standalone Azure Service Fabric cluster</span></span>](service-fabric-cluster-creation-for-windows-server.md)
* [<span data-ttu-id="e769e-165">Escenarios de seguridad de los clústeres de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e769e-165">Service Fabric cluster security scenarios</span></span>](service-fabric-windows-cluster-windows-security.md)
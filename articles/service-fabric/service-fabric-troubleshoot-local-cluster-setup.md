---
title: "Solucionar problemas de instalación del clúster local de Service Fabric | Microsoft Docs"
description: "En este artículo se trata de un conjunto de sugerencias para solucionar problemas de su clúster de desarrollo local"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: aa393f884b564cee81fcf75cc2eff895efea9471
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="46548-103">Solución de problemas de instalación del clúster de desarrollo local</span><span class="sxs-lookup"><span data-stu-id="46548-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="46548-104">Si surge un problema al interactuar con el clúster de desarrollo local de Azure Service Fabric, revise las siguientes sugerencias para obtener posibles soluciones.</span><span class="sxs-lookup"><span data-stu-id="46548-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review the following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="46548-105">Errores de instalación de clúster</span><span class="sxs-lookup"><span data-stu-id="46548-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="46548-106">No se pueden limpiar los registros de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="46548-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="46548-107">Problema</span><span class="sxs-lookup"><span data-stu-id="46548-107">Problem</span></span>
<span data-ttu-id="46548-108">Mientras se ejecuta el script DevClusterSetup, verá un error similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="46548-108">While running the DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held to items in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="46548-109">Solución</span><span class="sxs-lookup"><span data-stu-id="46548-109">Solution</span></span>
<span data-ttu-id="46548-110">Cierre la ventana de PowerShell actual y abra una nueva ventana de PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="46548-110">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="46548-111">Ahora podrá ejecutar correctamente el script.</span><span class="sxs-lookup"><span data-stu-id="46548-111">You should now be able to successfully run the script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="46548-112">Errores de conexión del clúster</span><span class="sxs-lookup"><span data-stu-id="46548-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="46548-113">Los cmdlets de PowerShell de Service Fabric no se reconocen en Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="46548-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="46548-114">Problema</span><span class="sxs-lookup"><span data-stu-id="46548-114">Problem</span></span>
<span data-ttu-id="46548-115">Si intenta ejecutar cualquiera de los cmdlets de PowerShell de Service Fabric, como por ejemplo `Connect-ServiceFabricCluster` en una ventana de Azure PowerShell, se produce un error que indica que no se reconoce el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="46548-115">If you try to run any of the Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that the cmdlet is not recognized.</span></span> <span data-ttu-id="46548-116">Esto se debe a que Azure PowerShell usa la versión de 32 bits de Windows PowerShell (incluso en las versiones de 64 bits del sistema operativo), mientras que los cmdlets de Service Fabric solo funcionan en entornos de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="46548-116">The reason for this is that Azure PowerShell uses the 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas the Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="46548-117">Solución</span><span class="sxs-lookup"><span data-stu-id="46548-117">Solution</span></span>
<span data-ttu-id="46548-118">Ejecute siempre los cmdlets de Service Fabric directamente desde Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46548-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="46548-119">La versión más reciente de Azure PowerShell no crea un acceso directo especial, por lo que esto ya no debería ocurrir.</span><span class="sxs-lookup"><span data-stu-id="46548-119">The latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="46548-120">Excepción de inicialización de tipo</span><span class="sxs-lookup"><span data-stu-id="46548-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="46548-121">Problema</span><span class="sxs-lookup"><span data-stu-id="46548-121">Problem</span></span>
<span data-ttu-id="46548-122">Cuando se conecta al clúster en PowerShell, aparece el error TypeInitializationException para System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="46548-122">When you are connecting to the cluster in PowerShell, you see the error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="46548-123">Solución</span><span class="sxs-lookup"><span data-stu-id="46548-123">Solution</span></span>
<span data-ttu-id="46548-124">La variable de ruta de acceso no se estableció correctamente durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="46548-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="46548-125">Cierre la sesión de Windows y vuelva a iniciarla.</span><span class="sxs-lookup"><span data-stu-id="46548-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="46548-126">Esto actualiza la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="46548-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="46548-127">Se produce un error de conexión del clúster con el mensaje "El objeto está cerrado"</span><span class="sxs-lookup"><span data-stu-id="46548-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="46548-128">Problema</span><span class="sxs-lookup"><span data-stu-id="46548-128">Problem</span></span>
<span data-ttu-id="46548-129">Se produce un error en una llamada a Connect-ServiceFabricCluster con un error similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="46548-129">A call to Connect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : The object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="46548-130">Solución</span><span class="sxs-lookup"><span data-stu-id="46548-130">Solution</span></span>
<span data-ttu-id="46548-131">Cierre la ventana de PowerShell actual y abra una nueva ventana de PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="46548-131">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="46548-132">Ahora podrá conectarse correctamente.</span><span class="sxs-lookup"><span data-stu-id="46548-132">You should now be able to successfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="46548-133">Excepción de conexión de tejido denegada</span><span class="sxs-lookup"><span data-stu-id="46548-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="46548-134">Problema</span><span class="sxs-lookup"><span data-stu-id="46548-134">Problem</span></span>
<span data-ttu-id="46548-135">Cuando se depura desde Visual Studio, se obtiene un error FabricConnectionDeniedException.</span><span class="sxs-lookup"><span data-stu-id="46548-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="46548-136">Solución</span><span class="sxs-lookup"><span data-stu-id="46548-136">Solution</span></span>
<span data-ttu-id="46548-137">Este error suele producirse cuando se intenta iniciar manualmente un proceso de host de servicio en lugar de permitir que el tiempo de ejecución de Service Fabric lo inicie automáticamente.</span><span class="sxs-lookup"><span data-stu-id="46548-137">This error usually occurs when you try to start a service host process manually, rather than allowing the Service Fabric runtime to start it for you.</span></span>

<span data-ttu-id="46548-138">Asegúrese de que no tenga ningún proyecto de servicio establecido como proyecto de inicio de la solución.</span><span class="sxs-lookup"><span data-stu-id="46548-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="46548-139">Solo los proyectos de aplicación de Service Fabric deben establecerse como proyectos de inicio.</span><span class="sxs-lookup"><span data-stu-id="46548-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="46548-140">Si, después de la configuración, el clúster local comienza a comportarse de forma anormal, puede restablecerse con la aplicación de la bandeja del sistema de administrador de clústeres locales.</span><span class="sxs-lookup"><span data-stu-id="46548-140">If, following setup, your local cluster begins to behave abnormally, you can reset it using the local cluster manager system tray application.</span></span> <span data-ttu-id="46548-141">De este modo se quita el clúster existente y se configura uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="46548-141">This removes the existing cluster and set up a new one.</span></span> <span data-ttu-id="46548-142">Tenga en cuenta que todas las aplicaciones implementadas y los datos asociados también se quitan.</span><span class="sxs-lookup"><span data-stu-id="46548-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="46548-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46548-143">Next steps</span></span>
* [<span data-ttu-id="46548-144">Comprensión y solución de problemas de clústeres con informes de mantenimiento del sistema</span><span class="sxs-lookup"><span data-stu-id="46548-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="46548-145">Visualización del clúster mediante el Explorador de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="46548-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)


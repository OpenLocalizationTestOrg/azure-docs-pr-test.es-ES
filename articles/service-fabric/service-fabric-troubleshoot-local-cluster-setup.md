---
title: "aaaTroubleshoot el programa de instalación de clúster de Service Fabric local | Documentos de Microsoft"
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
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="d02d7-103">Solución de problemas de instalación del clúster de desarrollo local</span><span class="sxs-lookup"><span data-stu-id="d02d7-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="d02d7-104">Si experimenta un problema al interactuar con el clúster de desarrollo local de Azure Service Fabric, revise Hola siguiendo las sugerencias sobre posibles soluciones.</span><span class="sxs-lookup"><span data-stu-id="d02d7-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review hello following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="d02d7-105">Errores de instalación de clúster</span><span class="sxs-lookup"><span data-stu-id="d02d7-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="d02d7-106">No se pueden limpiar los registros de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d02d7-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="d02d7-107">Problema</span><span class="sxs-lookup"><span data-stu-id="d02d7-107">Problem</span></span>
<span data-ttu-id="d02d7-108">Mientras se ejecuta la secuencia de comandos de hello DevClusterSetup, verá un error similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="d02d7-108">While running hello DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="d02d7-109">Solución</span><span class="sxs-lookup"><span data-stu-id="d02d7-109">Solution</span></span>
<span data-ttu-id="d02d7-110">Cerrar ventana actual de PowerShell de Hola y abrir una nueva ventana de PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="d02d7-110">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="d02d7-111">Ahora debe ser capaz de toosuccessfully ejecutar script de Hola.</span><span class="sxs-lookup"><span data-stu-id="d02d7-111">You should now be able toosuccessfully run hello script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="d02d7-112">Errores de conexión del clúster</span><span class="sxs-lookup"><span data-stu-id="d02d7-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="d02d7-113">Los cmdlets de PowerShell de Service Fabric no se reconocen en Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d02d7-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="d02d7-114">Problema</span><span class="sxs-lookup"><span data-stu-id="d02d7-114">Problem</span></span>
<span data-ttu-id="d02d7-115">Si intentas toorun cualquiera de hello cmdlets de PowerShell de tejido de servicio, como `Connect-ServiceFabricCluster` en una ventana de PowerShell de Azure, se produce un error, que indica que no se reconoce el cmdlet Hola.</span><span class="sxs-lookup"><span data-stu-id="d02d7-115">If you try toorun any of hello Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that hello cmdlet is not recognized.</span></span> <span data-ttu-id="d02d7-116">motivo Hello es que Azure PowerShell utiliza la versión de 32 bits de Hola de Windows PowerShell (incluso en versiones de sistema operativo de 64 bits), mientras que Hola cmdlets de Service Fabric solo funcionan en entornos de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="d02d7-116">hello reason for this is that Azure PowerShell uses hello 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas hello Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="d02d7-117">Solución</span><span class="sxs-lookup"><span data-stu-id="d02d7-117">Solution</span></span>
<span data-ttu-id="d02d7-118">Ejecute siempre los cmdlets de Service Fabric directamente desde Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d02d7-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="d02d7-119">versión más reciente de Hola de PowerShell de Azure no crea un acceso directo especial, por lo que ya no debería ocurrir.</span><span class="sxs-lookup"><span data-stu-id="d02d7-119">hello latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="d02d7-120">Excepción de inicialización de tipo</span><span class="sxs-lookup"><span data-stu-id="d02d7-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="d02d7-121">Problema</span><span class="sxs-lookup"><span data-stu-id="d02d7-121">Problem</span></span>
<span data-ttu-id="d02d7-122">Cuando se conecta el clúster de toohello en PowerShell, consulte error Hola TypeInitializationException para System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="d02d7-122">When you are connecting toohello cluster in PowerShell, you see hello error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="d02d7-123">Solución</span><span class="sxs-lookup"><span data-stu-id="d02d7-123">Solution</span></span>
<span data-ttu-id="d02d7-124">La variable de ruta de acceso no se estableció correctamente durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="d02d7-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="d02d7-125">Cierre la sesión de Windows y vuelva a iniciarla.</span><span class="sxs-lookup"><span data-stu-id="d02d7-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="d02d7-126">Esto actualiza la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="d02d7-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="d02d7-127">Se produce un error de conexión del clúster con el mensaje "El objeto está cerrado"</span><span class="sxs-lookup"><span data-stu-id="d02d7-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="d02d7-128">Problema</span><span class="sxs-lookup"><span data-stu-id="d02d7-128">Problem</span></span>
<span data-ttu-id="d02d7-129">Se produce un error en una llamada tooConnect-ServiceFabricCluster con un error similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="d02d7-129">A call tooConnect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="d02d7-130">Solución</span><span class="sxs-lookup"><span data-stu-id="d02d7-130">Solution</span></span>
<span data-ttu-id="d02d7-131">Cerrar ventana actual de PowerShell de Hola y abrir una nueva ventana de PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="d02d7-131">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="d02d7-132">Ahora debe poder conectarse toosuccessfully.</span><span class="sxs-lookup"><span data-stu-id="d02d7-132">You should now be able toosuccessfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="d02d7-133">Excepción de conexión de tejido denegada</span><span class="sxs-lookup"><span data-stu-id="d02d7-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="d02d7-134">Problema</span><span class="sxs-lookup"><span data-stu-id="d02d7-134">Problem</span></span>
<span data-ttu-id="d02d7-135">Cuando se depura desde Visual Studio, se obtiene un error FabricConnectionDeniedException.</span><span class="sxs-lookup"><span data-stu-id="d02d7-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="d02d7-136">Solución</span><span class="sxs-lookup"><span data-stu-id="d02d7-136">Solution</span></span>
<span data-ttu-id="d02d7-137">Este error suele producirse cuando intenta toostart un proceso de host de servicio manualmente, en lugar de permitir Hola Service Fabric en tiempo de ejecución toostart lo automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d02d7-137">This error usually occurs when you try toostart a service host process manually, rather than allowing hello Service Fabric runtime toostart it for you.</span></span>

<span data-ttu-id="d02d7-138">Asegúrese de que no tenga ningún proyecto de servicio establecido como proyecto de inicio de la solución.</span><span class="sxs-lookup"><span data-stu-id="d02d7-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="d02d7-139">Solo los proyectos de aplicación de Service Fabric deben establecerse como proyectos de inicio.</span><span class="sxs-lookup"><span data-stu-id="d02d7-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="d02d7-140">Si, después de la instalación, el clúster local empieza toobehave anormalmente, pueden restablecer mediante la aplicación de bandeja del sistema de hello clúster local Administrador.</span><span class="sxs-lookup"><span data-stu-id="d02d7-140">If, following setup, your local cluster begins toobehave abnormally, you can reset it using hello local cluster manager system tray application.</span></span> <span data-ttu-id="d02d7-141">Esta forma se elimina Hola clúster existente y configurar uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="d02d7-141">This removes hello existing cluster and set up a new one.</span></span> <span data-ttu-id="d02d7-142">Tenga en cuenta que todas las aplicaciones implementadas y los datos asociados también se quitan.</span><span class="sxs-lookup"><span data-stu-id="d02d7-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d02d7-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d02d7-143">Next steps</span></span>
* [<span data-ttu-id="d02d7-144">Comprensión y solución de problemas de clústeres con informes de mantenimiento del sistema</span><span class="sxs-lookup"><span data-stu-id="d02d7-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="d02d7-145">Visualización del clúster mediante el Explorador de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d02d7-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)


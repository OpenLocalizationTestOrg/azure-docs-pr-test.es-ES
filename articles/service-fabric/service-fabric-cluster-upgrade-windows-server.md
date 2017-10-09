---
title: "aaaUpgrade una independiente Azure Service Fabric de clúster en Windows Server | Documentos de Microsoft"
description: "Actualizar código de hello Azure Service Fabric o configuración que se ejecuta un clúster de Service Fabric independientes, incluida la configuración de modo de actualización de clúster de Hola."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a><span data-ttu-id="66c1b-103">Actualización del clúster de Azure Service Fabric independiente en Windows Server</span><span class="sxs-lookup"><span data-stu-id="66c1b-103">Upgrade your standalone Azure Service Fabric on Windows Server cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="66c1b-104">Clúster de Azure</span><span class="sxs-lookup"><span data-stu-id="66c1b-104">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="66c1b-105">Clúster independiente</span><span class="sxs-lookup"><span data-stu-id="66c1b-105">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="66c1b-106">Para cualquier sistema moderna, Hola capacidad tooupgrade es un éxito a largo plazo toohello clave del producto.</span><span class="sxs-lookup"><span data-stu-id="66c1b-106">For any modern system, hello ability tooupgrade is a key toohello long-term success of your product.</span></span> <span data-ttu-id="66c1b-107">Un clúster de Azure Service Fabric es un recurso que usted posee.</span><span class="sxs-lookup"><span data-stu-id="66c1b-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="66c1b-108">Este artículo describe cómo puede asegurarse de que ese clúster Hola siempre ejecuta en las versiones compatibles de código de Fabric de servicio y las configuraciones.</span><span class="sxs-lookup"><span data-stu-id="66c1b-108">This article describes how you can make sure that hello cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="66c1b-109">Versión de Service Fabric Hola de control que se ejecuta en el clúster</span><span class="sxs-lookup"><span data-stu-id="66c1b-109">Control hello Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="66c1b-110">tooset actualiza su toodownload de clúster de Service Fabric cuando Microsoft publica una nueva versión, conjunto hello **fabricClusterAutoupgradeEnabled** tootrue de configuración de clúster.</span><span class="sxs-lookup"><span data-stu-id="66c1b-110">tooset your cluster toodownload updates of Service Fabric when Microsoft releases a new version, set hello **fabricClusterAutoupgradeEnabled** cluster configuration tootrue.</span></span> <span data-ttu-id="66c1b-111">una versión compatible de Service Fabric que desea que su toobe de clúster en conjunto hello tooselect **fabricClusterAutoupgradeEnabled** toofalse de configuración de clúster.</span><span class="sxs-lookup"><span data-stu-id="66c1b-111">tooselect a supported version of Service Fabric that you want your cluster toobe on, set hello **fabricClusterAutoupgradeEnabled** cluster configuration toofalse.</span></span>

> [!NOTE]
> <span data-ttu-id="66c1b-112">Asegúrese de que el clúster siempre ejecuta una versión compatible de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="66c1b-112">Make sure that your cluster always runs a supported Service Fabric version.</span></span> <span data-ttu-id="66c1b-113">Cuando Microsoft anuncia el lanzamiento de Hola de una nueva versión de Service Fabric, versión anterior de hello está marcado para la finalización del soporte después de un mínimo de 60 días desde la fecha de Hola de anuncio Hola.</span><span class="sxs-lookup"><span data-stu-id="66c1b-113">When Microsoft announces hello release of a new version of Service Fabric, hello previous version is marked for end of support after a minimum of 60 days from hello date of hello announcement.</span></span> <span data-ttu-id="66c1b-114">Nuevas versiones se anuncian [en el blog del equipo de Service Fabric hello](https://blogs.msdn.microsoft.com/azureservicefabric/).</span><span class="sxs-lookup"><span data-stu-id="66c1b-114">New releases are announced [on hello Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="66c1b-115">nueva versión de Hello es toochoose disponible en ese momento.</span><span class="sxs-lookup"><span data-stu-id="66c1b-115">hello new release is available toochoose at that point.</span></span>
>
>

<span data-ttu-id="66c1b-116">Puede actualizar la nueva versión del clúster toohello solo si está usando una configuración de nodo de estilo de producción, donde cada nodo de Service Fabric está asignada a una máquina virtual o física independiente.</span><span class="sxs-lookup"><span data-stu-id="66c1b-116">You can upgrade your cluster toohello new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="66c1b-117">Si tiene un clúster de desarrollo, donde más de un nodo de Service Fabric está en una única máquina física o virtual, deberá crear de nuevo clúster Hola con la nueva versión de hello.</span><span class="sxs-lookup"><span data-stu-id="66c1b-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create hello cluster with hello new version.</span></span>

<span data-ttu-id="66c1b-118">Dos flujos de trabajo distintos pueden actualizar la versión más reciente de toohello de clúster o una versión compatible de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="66c1b-118">Two distinct workflows can upgrade your cluster toohello latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="66c1b-119">Un flujo de trabajo es para los clústeres que tienen la versión más reciente de conectividad toodownload Hola automáticamente.</span><span class="sxs-lookup"><span data-stu-id="66c1b-119">One workflow is for clusters that have connectivity toodownload hello latest version automatically.</span></span> <span data-ttu-id="66c1b-120">Hola otro flujo de trabajo es para los clústeres que no tiene la versión más reciente de Service Fabric de conectividad toodownload Hola.</span><span class="sxs-lookup"><span data-stu-id="66c1b-120">hello other workflow is for clusters that do not have connectivity toodownload hello latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="66c1b-121">Actualizar clústeres que tienen la configuración y el código más reciente de conectividad toodownload Hola</span><span class="sxs-lookup"><span data-stu-id="66c1b-121">Upgrade clusters that have connectivity toodownload hello latest code and configuration</span></span>
<span data-ttu-id="66c1b-122">Use estos pasos tooupgrade su tooa admitida la versión de clúster si los nodos del clúster tienen conectividad a Internet demasiado[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="66c1b-122">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

<span data-ttu-id="66c1b-123">Para los clústeres que tienen conectividad también[http://download.microsoft.com](http://download.microsoft.com), Microsoft comprueba periódicamente la disponibilidad de Hola de nuevas versiones de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="66c1b-123">For clusters that have connectivity too[http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for hello availability of new Service Fabric versions.</span></span>

<span data-ttu-id="66c1b-124">Cuando hay disponible una nueva versión de Service Fabric, paquetes de saludo se descargan localmente toohello clúster y aprovisionado para la actualización.</span><span class="sxs-lookup"><span data-stu-id="66c1b-124">When a new Service Fabric version is available, hello package is downloaded locally toohello cluster and provisioned for upgrade.</span></span> <span data-ttu-id="66c1b-125">Además, cliente de hello tooinform de esta nueva versión, sistema de hello muestra una advertencia de estado de clúster explícito que sea similar toohello después de:</span><span class="sxs-lookup"><span data-stu-id="66c1b-125">Additionally, tooinform hello customer of this new version, hello system shows an explicit cluster health warning that's similar toohello following:</span></span>

<span data-ttu-id="66c1b-126">"Hola actual clúster versión # compatibilidad con la versión finaliza [Date]."</span><span class="sxs-lookup"><span data-stu-id="66c1b-126">“hello current cluster version [version#] support ends [Date]."</span></span>

<span data-ttu-id="66c1b-127">Después de clúster de Hola se ejecuta la versión más reciente de hello, advertencia Hola desaparece.</span><span class="sxs-lookup"><span data-stu-id="66c1b-127">After hello cluster is running hello latest version, hello warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="66c1b-128">Flujo de trabajo de actualización de clúster</span><span class="sxs-lookup"><span data-stu-id="66c1b-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="66c1b-129">Una vez que aparezca la advertencia de estado del clúster de hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="66c1b-129">After you see hello cluster health warning, do hello following:</span></span>

1. <span data-ttu-id="66c1b-130">Conectar toohello clúster desde cualquier equipo que tenga equipos Hola de tooall de acceso de administrador que se muestran como nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="66c1b-130">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="66c1b-131">máquina de Hola que este script se ejecuta en no tiene toobe parte del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="66c1b-131">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. <span data-ttu-id="66c1b-132">Obtener lista de Hola de versiones Service Fabric que puede actualizar a.</span><span class="sxs-lookup"><span data-stu-id="66c1b-132">Get hello list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="66c1b-133">Debería obtener un toothis similar de salida:</span><span class="sxs-lookup"><span data-stu-id="66c1b-133">You should get an output similar toothis:</span></span>

    ![obtener versiones de tejido][getfabversions]
3. <span data-ttu-id="66c1b-135">Iniciar una versión disponible del tooan de actualización de clúster mediante el [ServiceFabricClusterUpgrade inicio](https://msdn.microsoft.com/library/mt125872.aspx) cmd de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66c1b-135">Start a cluster upgrade tooan available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="66c1b-136">progreso de hello toomonitor de actualización de hello, puede utilizar Service Fabric Explorer o ejecución hello siguiente comando de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66c1b-136">toomonitor hello progress of hello upgrade, you can use Service Fabric Explorer or run hello following Windows PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="66c1b-137">Si no se cumplen las directivas de mantenimiento de clúster de hello, Hola actualización se ha revertido.</span><span class="sxs-lookup"><span data-stu-id="66c1b-137">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="66c1b-138">las directivas de mantenimiento personalizado de toospecify para hello **inicio ServiceFabricClusterUpgrade** command, consulte la documentación de [ServiceFabricClusterUpgrade inicio](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="66c1b-138">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="66c1b-139">Después de corregir los problemas de Hola que dan como resultado de reversión de hello, Iniciar actualización de hello nuevo por siguiente Hola mismos pasos como se describen anteriormente.</span><span class="sxs-lookup"><span data-stu-id="66c1b-139">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="66c1b-140">Actualizar clústeres que tienen <U>sin conectividad</u> código más reciente de toodownload hello y configuración</span><span class="sxs-lookup"><span data-stu-id="66c1b-140">Upgrade clusters that have <U>no connectivity</u> toodownload hello latest code and configuration</span></span>
<span data-ttu-id="66c1b-141">Use estos pasos tooupgrade su tooa admitida la versión de clúster si los nodos del clúster no tiene conectividad a Internet demasiado[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="66c1b-141">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes do not have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="66c1b-142">Si está ejecutando un clúster que no esté conectado toohello Internet, tendrá toolearn toomonitor Hola Service Fabric team blog sobre una nueva versión.</span><span class="sxs-lookup"><span data-stu-id="66c1b-142">If you are running a cluster that is not connected toohello Internet, you will have toomonitor hello Service Fabric team blog toolearn about a new release.</span></span> <span data-ttu-id="66c1b-143">Hola sistema sin mostrar un tooalert de advertencia de estado de clúster de una nueva versión.</span><span class="sxs-lookup"><span data-stu-id="66c1b-143">hello system does not show a cluster health warning tooalert you of a new release.</span></span>  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="66c1b-144">Aprovisionamiento automático frente a aprovisionamiento manual</span><span class="sxs-lookup"><span data-stu-id="66c1b-144">Auto Provisioning vs Manual Provisioning</span></span>
<span data-ttu-id="66c1b-145">tooenable la descarga automática y el registro de versión de código más reciente de hello, configure el servicio de actualización de servicio de Fabric.</span><span class="sxs-lookup"><span data-stu-id="66c1b-145">tooenable automatic downloading and registration for hello latest code version, set up Service Fabric Update Service.</span></span> <span data-ttu-id="66c1b-146">Consulte toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt dentro de hello [paquete independiente](service-fabric-cluster-standalone-package-contents.md) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="66c1b-146">Refer toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside hello [Standalone Package](service-fabric-cluster-standalone-package-contents.md) for instructions.</span></span>
<span data-ttu-id="66c1b-147">Para un proceso manual, siga estas instrucciones Hola.</span><span class="sxs-lookup"><span data-stu-id="66c1b-147">For manual process, follow hello instructions below.</span></span>

<span data-ttu-id="66c1b-148">Modifique su Hola de tooset de configuración de clúster después de propiedad toofalse antes de iniciar una actualización de la configuración.</span><span class="sxs-lookup"><span data-stu-id="66c1b-148">Modify your cluster configuration tooset hello following property toofalse before you start a configuration upgrade.</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="66c1b-149">Consulte demasiado[ServiceFabricClusterConfigurationUpgrade inicio PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) para obtener detalles de uso.</span><span class="sxs-lookup"><span data-stu-id="66c1b-149">Refer too[Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details.</span></span> <span data-ttu-id="66c1b-150">Asegúrese de tooupdate seguro 'clusterConfigurationVersion' en su JSON antes de empezar la actualización de la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="66c1b-150">Make sure tooupdate 'clusterConfigurationVersion' in your JSON before you start hello configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="66c1b-151">Flujo de trabajo de actualización de clúster</span><span class="sxs-lookup"><span data-stu-id="66c1b-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="66c1b-152">Ejecute Get-ServiceFabricClusterUpgrade desde uno de los nodos de hello en clúster de hello y observe hello TargetCodeVersion.</span><span class="sxs-lookup"><span data-stu-id="66c1b-152">Run Get-ServiceFabricClusterUpgrade from one of hello nodes in hello cluster and note hello TargetCodeVersion.</span></span>
2. <span data-ttu-id="66c1b-153">Siguiente ejecución Hola desde un toolist de equipo conectado internet todos actualiza las versiones compatibles con la versión actual de Hola y descarga Hola correspondiente paquete de hello asociados vínculos de descarga.</span><span class="sxs-lookup"><span data-stu-id="66c1b-153">Run hello following from an internet connected machine toolist all upgrade compatible versions with hello current version and download hello corresponding package from hello associated download links.</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="66c1b-154">Conectar toohello clúster desde cualquier equipo que tenga equipos Hola de tooall de acceso de administrador que se muestran como nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="66c1b-154">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="66c1b-155">máquina de Hola que este script se ejecuta en no tiene toobe parte del clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="66c1b-155">hello machine that this script is run on does not have toobe part of hello cluster</span></span>

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="66c1b-156">Copie el paquete de hello descargado en almacén de imágenes de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="66c1b-156">Copy hello downloaded package into hello cluster image store.</span></span>

5. <span data-ttu-id="66c1b-157">Registrar el paquete de hello copiado.</span><span class="sxs-lookup"><span data-stu-id="66c1b-157">Register hello copied package.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="66c1b-158">Iniciar una versión disponible del tooan de actualización de clúster.</span><span class="sxs-lookup"><span data-stu-id="66c1b-158">Start a cluster upgrade tooan available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="66c1b-159">Puede supervisar el progreso de Hola de actualización de hello en el Explorador de Service Fabric o puede ejecutar el siguiente comando de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="66c1b-159">You can monitor hello progress of hello upgrade on Service Fabric Explorer, or you can run hello following PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="66c1b-160">Si no se cumplen las directivas de mantenimiento de clúster de hello, Hola actualización se ha revertido.</span><span class="sxs-lookup"><span data-stu-id="66c1b-160">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="66c1b-161">las directivas de mantenimiento personalizado de toospecify para hello **inicio ServiceFabricClusterUpgrade** command, consulte la documentación de Hola para [ServiceFabricClusterUpgrade inicio](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="66c1b-161">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see hello documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="66c1b-162">Después de corregir los problemas de Hola que dan como resultado de reversión de hello, Iniciar actualización de hello nuevo por siguiente Hola mismos pasos como se describen anteriormente.</span><span class="sxs-lookup"><span data-stu-id="66c1b-162">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>


## <a name="upgrade-hello-cluster-configuration"></a><span data-ttu-id="66c1b-163">Actualice la configuración de clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="66c1b-163">Upgrade hello cluster configuration</span></span>
<span data-ttu-id="66c1b-164">Antes de iniciar la actualización de la configuración de hello, puede probar el nuevo json de configuración de clúster mediante la ejecución de script de powershell de hello en el paquete independiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="66c1b-164">Before you initiate hello configuration upgrade, you can test your new cluster configuration json by running hello powershell script in hello standalone package.</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
<span data-ttu-id="66c1b-165">o</span><span class="sxs-lookup"><span data-stu-id="66c1b-165">or</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

<span data-ttu-id="66c1b-166">Algunas configuraciones no se pueden actualizar, como los puntos de conexión, el nombre del clúster, la dirección IP del nodo, etc. Esto probará Hola nuevo clúster configuración json contra Hola antiguo y producir errores en la ventana de Powershell de hello si hay algún problema.</span><span class="sxs-lookup"><span data-stu-id="66c1b-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. This will test hello new cluster configuration json against hello old one and throw errors in hello Powershell window if there is any issue.</span></span>

<span data-ttu-id="66c1b-167">actualización de la configuración de clúster de tooupgrade hello, ejecute **ServiceFabricClusterConfigurationUpgrade inicio**.</span><span class="sxs-lookup"><span data-stu-id="66c1b-167">tooupgrade hello cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**.</span></span> <span data-ttu-id="66c1b-168">actualización de la configuración de Hello es dominio de actualización procesado por dominio de actualización.</span><span class="sxs-lookup"><span data-stu-id="66c1b-168">hello configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="66c1b-169">Actualización de la configuración de un certificado de clúster</span><span class="sxs-lookup"><span data-stu-id="66c1b-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="66c1b-170">Certificado de clúster se utiliza para la autenticación entre los nodos de clúster, por lo que la sustitución del certificado de hello debe realizarse con precaución adicional porque logra, se bloqueará la comunicación Hola entre los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="66c1b-170">Cluster certificate is used for authentication between cluster nodes, so hello certificate roll over should be performed with extra caution because failure will block hello communication among cluster nodes.</span></span>  
<span data-ttu-id="66c1b-171">Desde el punto de vista técnico, se admiten tres opciones:</span><span class="sxs-lookup"><span data-stu-id="66c1b-171">Technically, three options are supported:</span></span>  

1. <span data-ttu-id="66c1b-172">Actualización de los certificados única: ruta de actualización de hello es ' certificado (principal) -> (principal) del certificado B -> C de certificado (principal) ->...'.</span><span class="sxs-lookup"><span data-stu-id="66c1b-172">Single certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.</span></span>   
2. <span data-ttu-id="66c1b-173">Actualización de certificados de Double: ruta de actualización de hello es ' certificado -> (principal) de certificados (principal) y B (secundario) -> B de certificado (principal) -> B de certificado (principal) y C (secundario) -> C de certificado (principal) ->...'.</span><span class="sxs-lookup"><span data-stu-id="66c1b-173">Double certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.</span></span>
3. <span data-ttu-id="66c1b-174">Actualización del tipo de certificado: configuración de certificado basada en huella digital <-> Configuración de certificado basada en CommonName.</span><span class="sxs-lookup"><span data-stu-id="66c1b-174">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="66c1b-175">Por ejemplo, Huella digital del certificado A (principal) y Huella digital B (secundaria) -> Certificado CommonName C.</span><span class="sxs-lookup"><span data-stu-id="66c1b-175">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>


## <a name="next-steps"></a><span data-ttu-id="66c1b-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="66c1b-176">Next steps</span></span>
* <span data-ttu-id="66c1b-177">Obtenga información acerca de cómo toocustomize algunos [configuración de clúster de Service Fabric](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="66c1b-177">Learn how toocustomize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="66c1b-178">Obtenga información acerca de cómo demasiado[escalar el clúster de entrada y salida](service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="66c1b-178">Learn how too[scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="66c1b-179">Obtenga información sobre [actualizaciones de aplicaciones](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="66c1b-179">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG

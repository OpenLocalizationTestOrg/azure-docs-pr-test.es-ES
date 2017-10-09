---
title: "un clúster de Azure Service Fabric independientes aaaCreate | Documentos de Microsoft"
description: "Cree un clúster de Azure Service Fabric en cualquier máquina (física o virtual) que ejecute Windows Server, ya sea local o en una nube."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="eb607-103">Creación de un clúster independiente con Windows Server</span><span class="sxs-lookup"><span data-stu-id="eb607-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="eb607-104">Puede usar Azure Service Fabric toocreate Service Fabric clústeres en las máquinas virtuales o equipos que ejecutan Windows Server.</span><span class="sxs-lookup"><span data-stu-id="eb607-104">You can use Azure Service Fabric toocreate Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="eb607-105">Es decir, podrá implementar y ejecutar aplicaciones de Service Fabric en cualquier entorno donde haya un conjunto de equipos con Windows Server que estén conectados entre sí, ya sea de manera local o con algún proveedor de servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="eb607-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="eb607-106">Service Fabric proporciona un toocreate de paquete de instalación de clústeres de Service Fabric denominada paquete de Windows Server de hello independiente.</span><span class="sxs-lookup"><span data-stu-id="eb607-106">Service Fabric provides a setup package toocreate Service Fabric clusters called hello standalone Windows Server package.</span></span>

<span data-ttu-id="eb607-107">En este artículo le guiará por los pasos de Hola para crear un clúster de Service Fabric independientes.</span><span class="sxs-lookup"><span data-stu-id="eb607-107">This article walks you through hello steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="eb607-108">Este paquete de Windows Server independiente está disponible en el mercado y puede usarse para las implementaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="eb607-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="eb607-109">Además, puede contener nuevas características de Service Fabric que están en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="eb607-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="eb607-110">Desplácese hacia abajo demasiado"[incluidos en este paquete de características de vista previa](#previewfeatures_anchor)."</span><span class="sxs-lookup"><span data-stu-id="eb607-110">Scroll down too"[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="eb607-111">sección de la lista de Hola de características de vista previa de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb607-111">section for hello list of hello preview features.</span></span> <span data-ttu-id="eb607-112">También puede [descargar una copia del CLUF de hello](http://go.microsoft.com/fwlink/?LinkID=733084) ahora.</span><span class="sxs-lookup"><span data-stu-id="eb607-112">You can [download a copy of hello EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="eb607-113">Obtener soporte técnico para el paquete de hello Service Fabric para Windows Server</span><span class="sxs-lookup"><span data-stu-id="eb607-113">Get support for hello Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="eb607-114">Preguntarme Comunidad Hola paquete independiente de Service Fabric de Hola para Windows Server en hello [foro de Azure Service Fabric](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span><span class="sxs-lookup"><span data-stu-id="eb607-114">Ask hello community about hello Service Fabric standalone package for Windows Server in hello [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="eb607-115">Abra una incidencia para obtener [soporte técnico profesional para Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span><span class="sxs-lookup"><span data-stu-id="eb607-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="eb607-116">Más información sobre el soporte técnico profesional de Microsoft[aquí](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="eb607-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="eb607-117">También puede obtener soporte técnico para este paquete como parte del [soporte técnico Premier de Microsoft](https://support.microsoft.com/en-us/premier).</span><span class="sxs-lookup"><span data-stu-id="eb607-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="eb607-118">Para más información, consulte [Opciones de soporte técnico de Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span><span class="sxs-lookup"><span data-stu-id="eb607-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="eb607-119">registros de toocollect por motivos de compatibilidad, ejecute hello [compilador de registros de Service Fabric independientes](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="eb607-119">toocollect logs for support purposes, run hello [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="eb607-120">Descargar paquete de hello Service Fabric para Windows Server</span><span class="sxs-lookup"><span data-stu-id="eb607-120">Download hello Service Fabric for Windows Server package</span></span>
<span data-ttu-id="eb607-121">clúster de hello toocreate, use el paquete de hello Service Fabric para Windows Server (Windows Server 2012 R2 y versiones más recientes) encontrar aquí:</span><span class="sxs-lookup"><span data-stu-id="eb607-121">toocreate hello cluster, use hello Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="eb607-122">
[Vínculo de descarga del paquete independiente de Service Fabric de Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="eb607-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="eb607-123">Buscar detalles sobre el contenido del paquete de hello [aquí](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="eb607-123">Find details on contents of hello package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="eb607-124">paquete de Hello Service Fabric en tiempo de ejecución se descarga automáticamente en tiempo de creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="eb607-124">hello Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="eb607-125">Si la implementación desde un equipo no conectado toohello internet, descargue paquete en tiempo de ejecución de hello fuera de banda desde aquí:</span><span class="sxs-lookup"><span data-stu-id="eb607-125">If deploying from a machine not connected toohello internet, please download hello runtime package out of band from here:</span></span> <br><span data-ttu-id="eb607-126">
[Vínculo de descarga del entorno de tiempo de ejecución de Service Fabric para Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="eb607-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="eb607-127">Puede encontrar ejemplos de configuración de clúster independiente en:</span><span class="sxs-lookup"><span data-stu-id="eb607-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="eb607-128">
[Ejemplos de configuración de clúster independiente](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="eb607-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a><span data-ttu-id="eb607-129">Crear clúster Hola</span><span class="sxs-lookup"><span data-stu-id="eb607-129">Create hello cluster</span></span>
<span data-ttu-id="eb607-130">Service Fabric puede ser clúster de desarrollo de una máquina de tooa implementado mediante el uso de hello *ClusterConfig.Unsecure.DevCluster.json* los archivos incluidos en [ejemplos](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="eb607-130">Service Fabric can be deployed tooa one-machine development cluster by using hello *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="eb607-131">Desempaquetar máquina de hello independiente paquete tooyour, equipo local del toohello de archivo de copia Hola ejemplo configuración y luego Hola ejecución *CreateServiceFabricCluster.ps1* secuencia de comandos a través de una sesión de PowerShell de administrador de hello independiente carpeta de paquete:</span><span class="sxs-lookup"><span data-stu-id="eb607-131">Unpack hello standalone package tooyour machine, copy hello sample config file toohello local machine, then run hello *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from hello standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="eb607-132">Paso 1A: Creación de un clúster de desarrollo local poco seguro</span><span class="sxs-lookup"><span data-stu-id="eb607-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="eb607-133">Vea Hola sección de configuración del entorno en [planear y preparar la implementación de clúster](service-fabric-cluster-standalone-deployment-preparation.md) para obtener más información de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="eb607-133">See hello Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="eb607-134">Si ya ha terminado de ejecutar escenarios de desarrollo, puede quitar clúster de Service Fabric Hola de máquina de hello consultando toosteps en la sección "[quitar un clúster](#removecluster_anchor)".</span><span class="sxs-lookup"><span data-stu-id="eb607-134">If you're finished running development scenarios, you can remove hello Service Fabric cluster from hello machine by referring toosteps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="eb607-135">Paso 1B: Creación de un clúster de varias máquinas</span><span class="sxs-lookup"><span data-stu-id="eb607-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="eb607-136">Después de haber pasado a través de planeación de Hola y detallan de los pasos de preparación en hello siguiente vínculo, está listo toocreate su clúster de producción mediante el archivo de configuración de clúster.</span><span class="sxs-lookup"><span data-stu-id="eb607-136">After you have gone through hello planning and preparation steps detailed at hello below link, you are ready toocreate your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="eb607-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) (Planeamiento y preparación del desarrollo del clúster)</span><span class="sxs-lookup"><span data-stu-id="eb607-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="eb607-138">Validar archivo de configuración de Hola que haya escrito mediante la ejecución de hello *TestConfiguration.ps1* secuencia de comandos de la carpeta de paquete de hello independiente:</span><span class="sxs-lookup"><span data-stu-id="eb607-138">Validate hello configuration file you have written by running hello *TestConfiguration.ps1* script from hello standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="eb607-139">El resultado debería ser parecido al que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="eb607-139">You should see output like below.</span></span> <span data-ttu-id="eb607-140">Si el campo de hello inferior "Correcto" aparece como "True", han pasado las comprobaciones de integridad y clúster Hola busca toobe pueden implementar en función de la configuración de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb607-140">If hello bottom field "Passed" is returned as "True", sanity checks have passed and hello cluster looks toobe deployable based on hello input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. <span data-ttu-id="eb607-141">Crear clúster hello: ejecute hello *CreateServiceFabricCluster.ps1* clúster de secuencia de comandos toodeploy Hola Service Fabric a través de cada máquina en la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb607-141">Create hello cluster:  Run hello *CreateServiceFabricCluster.ps1* script toodeploy hello Service Fabric cluster across each machine in hello configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="eb607-142">Los seguimientos de implementación se escriben toohello VM/máquina en la que se ejecutó el script de PowerShell de CreateServiceFabricCluster.ps1 de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb607-142">Deployment traces are written toohello VM/machine on which you ran hello CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="eb607-143">Estos pueden encontrarse en la subcarpeta de hello DeploymentTraces, basada en directorio Hola desde qué Hola se ejecutó la secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="eb607-143">These can be found in hello subfolder DeploymentTraces, based in hello directory from which hello script was run.</span></span> <span data-ttu-id="eb607-144">toosee si Service Fabric se ha había implementado correctamente tooa máquina, buscar archivos de hello instalado en directorio de FabricDataRoot hello, como se detalla en el archivo de configuración del clúster de hello FabricSettings sección (de c:\ProgramData\SF de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="eb607-144">toosee if Service Fabric was deployed correctly tooa machine, find hello installed files in hello FabricDataRoot directory, as detailed in hello cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="eb607-145">También, los procesos FabricHost.exe y Fabric.exe se pueden ver ejecutando el Administrador de tareas.</span><span class="sxs-lookup"><span data-stu-id="eb607-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="eb607-146">Paso 1C: Creación de un clúster sin conexión (desconectado de internet)</span><span class="sxs-lookup"><span data-stu-id="eb607-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="eb607-147">paquete de Hello Service Fabric en tiempo de ejecución se descarga automáticamente durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="eb607-147">hello Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="eb607-148">Al implementar un clúster toomachines no conectado toohello internet, deberá hello toodownload Service Fabric en tiempo de ejecución del paquete por separado y proporcionar hello tooit de ruta de acceso en la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="eb607-148">When deploying a cluster toomachines not connected toohello internet, you will need toodownload hello Service Fabric runtime package separately, and provide hello path tooit at cluster creation.</span></span>
<span data-ttu-id="eb607-149">se puede descargar por separado Hello paquete en tiempo de ejecución, desde otro equipo conectado toohello internet, en [vínculo Download - servicio de Fabric en tiempo de ejecución - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span><span class="sxs-lookup"><span data-stu-id="eb607-149">hello runtime package can be downloaded separately, from another machine connected toohello internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="eb607-150">Copiar hello toowhere de paquete en tiempo de ejecución va a implementar el clúster sin conexión de Hola de y crea clúster hello mediante la ejecución de `CreateServiceFabricCluster.ps1` con hello `-FabricRuntimePackagePath` parámetro incluido, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="eb607-150">Copy hello runtime package toowhere you are deploying hello offline cluster from, and create hello cluster by running `CreateServiceFabricCluster.ps1` with hello `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="eb607-151">donde `.\ClusterConfig.json` y `.\MicrosoftAzureServiceFabric.cab` son configuración de clúster toohello de hello las rutas de acceso y el archivo .cab de hello en tiempo de ejecución, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="eb607-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are hello paths toohello cluster configuration and hello runtime .cab file respectively.</span></span>


### <a name="step-2-connect-toohello-cluster"></a><span data-ttu-id="eb607-152">Paso 2: Conectar toohello clúster</span><span class="sxs-lookup"><span data-stu-id="eb607-152">Step 2: Connect toohello cluster</span></span>
<span data-ttu-id="eb607-153">clúster de tooconnect tooa segura, consulte [Service fabric conectarse clúster toosecure](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="eb607-153">tooconnect tooa secure cluster, see [Service fabric connect toosecure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="eb607-154">tooconnect tooan clúster, ejecute el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="eb607-154">tooconnect tooan unsecure cluster, run hello following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="eb607-155">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="eb607-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="eb607-156">Paso 3: Incorporación de Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="eb607-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="eb607-157">Ahora puede conectarse toohello clúster con Service Fabric Explorer ya sea directamente a uno de los equipos de hello con http://localhost:19080/Explorer/index.html o de forma remota con http://<*IPAddressofaMachine*>: 19080 / Explorer/index.HTML.</span><span class="sxs-lookup"><span data-stu-id="eb607-157">Now you can connect toohello cluster with Service Fabric Explorer either directly from one of hello machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="eb607-158">Agregar y quitar nodos</span><span class="sxs-lookup"><span data-stu-id="eb607-158">Add and remove nodes</span></span>
<span data-ttu-id="eb607-159">Puede agregar o quitar clúster de Service Fabric de nodos tooyour independiente, ya que cambien las necesidades empresariales.</span><span class="sxs-lookup"><span data-stu-id="eb607-159">You can add or remove nodes tooyour standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="eb607-160">Vea [agregar o quitar nodos tooa Service Fabric independientes clúster](service-fabric-cluster-windows-server-add-remove-nodes.md) para obtener pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="eb607-160">See [Add or Remove nodes tooa Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="eb607-161">Eliminación de un clúster</span><span class="sxs-lookup"><span data-stu-id="eb607-161">Remove a cluster</span></span>
<span data-ttu-id="eb607-162">tooremove un clúster, ejecute hello *RemoveServiceFabricCluster.ps1* script de PowerShell desde la carpeta del paquete hello y pase el archivo de configuración de hello ruta de acceso toohello JSON.</span><span class="sxs-lookup"><span data-stu-id="eb607-162">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="eb607-163">También puede especificar una ubicación para el registro de hello de eliminación de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb607-163">You can optionally specify a location for hello log of hello deletion.</span></span>

<span data-ttu-id="eb607-164">Este script se puede ejecutar en cualquier equipo que tenga equipos Hola de tooall de acceso de administrador que se muestran como nodos en el archivo de configuración del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb607-164">This script can be run on any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster configuration file.</span></span> <span data-ttu-id="eb607-165">máquina de Hola que este script se ejecuta en no tiene toobe parte del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb607-165">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a><span data-ttu-id="eb607-166">Datos de telemetría recopilados y cómo tooopt fuera de ella</span><span class="sxs-lookup"><span data-stu-id="eb607-166">Telemetry data collected and how tooopt out of it</span></span>
<span data-ttu-id="eb607-167">De forma predeterminada, el producto de Hola recopila telemetría en hello Service Fabric uso tooimprove Hola del producto.</span><span class="sxs-lookup"><span data-stu-id="eb607-167">As a default, hello product collects telemetry on hello Service Fabric usage tooimprove hello product.</span></span> <span data-ttu-id="eb607-168">Hola analizador de procedimientos recomendados que se ejecuta como parte del programa de instalación de hello comprueba si hay conectividad demasiado[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span><span class="sxs-lookup"><span data-stu-id="eb607-168">hello Best Practice Analyzer that runs as a part of hello setup checks for connectivity too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="eb607-169">Si no está accesible, se produce un error en el programa de instalación de Hola a menos que rechazar telemetría.</span><span class="sxs-lookup"><span data-stu-id="eb607-169">If it is not reachable, hello setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="eb607-170">canalización de telemetría Hello intenta hello tooupload después de datos demasiado[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) una vez al día.</span><span class="sxs-lookup"><span data-stu-id="eb607-170">hello telemetry pipeline tries tooupload hello following data too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="eb607-171">Es una carga de mejor esfuerzo y no tiene ningún efecto en la funcionalidad de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb607-171">It is a best-effort upload and has no impact on hello cluster functionality.</span></span> <span data-ttu-id="eb607-172">telemetría Hola solo se envía desde el nodo de Hola que se ejecuta Hola principal del Administrador de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="eb607-172">hello telemetry is only sent from hello node that runs hello failover manager primary.</span></span> <span data-ttu-id="eb607-173">Ningún otro nodo envía telemetría.</span><span class="sxs-lookup"><span data-stu-id="eb607-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="eb607-174">telemetría Hola consta de siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="eb607-174">hello telemetry consists of hello following:</span></span>

* <span data-ttu-id="eb607-175">Número de servicios</span><span class="sxs-lookup"><span data-stu-id="eb607-175">Number of services</span></span>
* <span data-ttu-id="eb607-176">Número de ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="eb607-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="eb607-177">Número de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="eb607-177">Number of Applications</span></span>
* <span data-ttu-id="eb607-178">Número de ApplicationUpgrades</span><span class="sxs-lookup"><span data-stu-id="eb607-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="eb607-179">Número de FailoverUnits</span><span class="sxs-lookup"><span data-stu-id="eb607-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="eb607-180">Número de InBuildFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="eb607-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="eb607-181">Número de UnhealthyFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="eb607-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="eb607-182">Número de réplicas</span><span class="sxs-lookup"><span data-stu-id="eb607-182">Number of Replicas</span></span>
* <span data-ttu-id="eb607-183">Número de InBuildReplicas</span><span class="sxs-lookup"><span data-stu-id="eb607-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="eb607-184">Número de StandByReplicas</span><span class="sxs-lookup"><span data-stu-id="eb607-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="eb607-185">Número de OfflineReplicas</span><span class="sxs-lookup"><span data-stu-id="eb607-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="eb607-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="eb607-186">CommonQueueLength</span></span>
* <span data-ttu-id="eb607-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="eb607-187">QueryQueueLength</span></span>
* <span data-ttu-id="eb607-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="eb607-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="eb607-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="eb607-189">CommitQueueLength</span></span>
* <span data-ttu-id="eb607-190">Número de nodos</span><span class="sxs-lookup"><span data-stu-id="eb607-190">Number of Nodes</span></span>
* <span data-ttu-id="eb607-191">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="eb607-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="eb607-192">ClusterId: se trata de un GUID generado aleatoriamente para cada clúster</span><span class="sxs-lookup"><span data-stu-id="eb607-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="eb607-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="eb607-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="eb607-194">Dirección IP de máquina virtual de Hola o una máquina de qué Hola se carga la telemetría</span><span class="sxs-lookup"><span data-stu-id="eb607-194">IP address of hello virtual machine or machine from which hello telemetry is uploaded</span></span>

<span data-ttu-id="eb607-195">telemetría toodisable, agregue la Hola siguiente demasiado*propiedades* en la configuración del clúster: *enableTelemetry: false*.</span><span class="sxs-lookup"><span data-stu-id="eb607-195">toodisable telemetry, add hello following too*properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="eb607-196">Características de versión preliminar incluidas en este paquete</span><span class="sxs-lookup"><span data-stu-id="eb607-196">Preview features included in this package</span></span>
<span data-ttu-id="eb607-197">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="eb607-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="eb607-198">A partir de hello nueva [versión de GA de clúster de hello independiente para Windows Server (versión 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), puede actualizar las versiones de toofuture de clúster, manual o automáticamente.</span><span class="sxs-lookup"><span data-stu-id="eb607-198">Starting with hello new [GA version of hello standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster toofuture releases, manually or automatically.</span></span> <span data-ttu-id="eb607-199">Consulte demasiado[actualizar una versión independiente del clúster de Service Fabric](service-fabric-cluster-upgrade-windows-server.md) documento para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="eb607-199">Refer too[Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="eb607-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eb607-200">Next steps</span></span>
* [<span data-ttu-id="eb607-201">Implementación y eliminación de aplicaciones con PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb607-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="eb607-202">Opciones de configuración de clústeres de Windows independientes</span><span class="sxs-lookup"><span data-stu-id="eb607-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="eb607-203">Agregar o quitar el clúster de Service Fabric de nodos tooa independiente</span><span class="sxs-lookup"><span data-stu-id="eb607-203">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="eb607-204">Actualización de nodos de un clúster de Service Fabric independiente</span><span class="sxs-lookup"><span data-stu-id="eb607-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="eb607-205">Creación de un clúster de Service Fabric independiente con máquinas virtuales de Azure con Windows</span><span class="sxs-lookup"><span data-stu-id="eb607-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="eb607-206">Proteger un clúster independiente en Windows mediante la seguridad de Windows</span><span class="sxs-lookup"><span data-stu-id="eb607-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="eb607-207">Protección de un clúster de Windows independiente mediante certificados</span><span class="sxs-lookup"><span data-stu-id="eb607-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png

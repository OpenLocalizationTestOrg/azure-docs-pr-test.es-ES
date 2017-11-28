---
title: "Creación de un clúster de Azure Service Fabric independiente | Microsoft Docs"
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
ms.openlocfilehash: 6aa2905a97ec6b8c125f2ab9572a8e40bf525b27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="fe8af-103">Creación de un clúster independiente con Windows Server</span><span class="sxs-lookup"><span data-stu-id="fe8af-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="fe8af-104">Puede usar Azure Service Fabric para crear clústeres de Service Fabric en las máquinas virtuales o los equipos que ejecutan Windows Server.</span><span class="sxs-lookup"><span data-stu-id="fe8af-104">You can use Azure Service Fabric to create Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="fe8af-105">Es decir, podrá implementar y ejecutar aplicaciones de Service Fabric en cualquier entorno donde haya un conjunto de equipos con Windows Server que estén conectados entre sí, ya sea de manera local o con algún proveedor de servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="fe8af-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="fe8af-106">Service Fabric proporciona un paquete de instalación para crear clústeres de Service Fabric, llamado paquete independiente de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="fe8af-106">Service Fabric provides a setup package to create Service Fabric clusters called the standalone Windows Server package.</span></span>

<span data-ttu-id="fe8af-107">Este artículo le guía por los pasos para crear un clúster independiente de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fe8af-107">This article walks you through the steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="fe8af-108">Este paquete de Windows Server independiente está disponible en el mercado y puede usarse para las implementaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="fe8af-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="fe8af-109">Además, puede contener nuevas características de Service Fabric que están en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="fe8af-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="fe8af-110">Desplácese hacia abajo hasta "[Características de versión preliminar incluidas en este paquete](#previewfeatures_anchor)".</span><span class="sxs-lookup"><span data-stu-id="fe8af-110">Scroll down to "[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="fe8af-111">Sección de la lista de las características de versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="fe8af-111">section for the list of the preview features.</span></span> <span data-ttu-id="fe8af-112">Puede [descargar una copia de los términos de licencia](http://go.microsoft.com/fwlink/?LinkID=733084) ahora.</span><span class="sxs-lookup"><span data-stu-id="fe8af-112">You can [download a copy of the EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="fe8af-113">Soporte técnico para el paquete de Service Fabric para Windows Server</span><span class="sxs-lookup"><span data-stu-id="fe8af-113">Get support for the Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="fe8af-114">Pregunte a la comunidad sobre el paquete independiente de Service Fabric para Windows Server en el [foro de Azure Service Fabric](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span><span class="sxs-lookup"><span data-stu-id="fe8af-114">Ask the community about the Service Fabric standalone package for Windows Server in the [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="fe8af-115">Abra una incidencia para obtener [soporte técnico profesional para Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span><span class="sxs-lookup"><span data-stu-id="fe8af-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="fe8af-116">Más información sobre el soporte técnico profesional de Microsoft[aquí](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="fe8af-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="fe8af-117">También puede obtener soporte técnico para este paquete como parte del [soporte técnico Premier de Microsoft](https://support.microsoft.com/en-us/premier).</span><span class="sxs-lookup"><span data-stu-id="fe8af-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="fe8af-118">Para más información, consulte [Opciones de soporte técnico de Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span><span class="sxs-lookup"><span data-stu-id="fe8af-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="fe8af-119">Para recopilar registros como soporte técnico, ejecute el [recopilador de registros independiente de Service Fabric](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="fe8af-119">To collect logs for support purposes, run the [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="fe8af-120">Descarga del paquete de Service Fabric para Windows Server</span><span class="sxs-lookup"><span data-stu-id="fe8af-120">Download the Service Fabric for Windows Server package</span></span>
<span data-ttu-id="fe8af-121">Para crear el clúster, use el paquete de Service Fabric para Windows Server (versión 2012 R2 y posteriores) que se encuentra aquí:</span><span class="sxs-lookup"><span data-stu-id="fe8af-121">To create the cluster, use the Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="fe8af-122">
[Vínculo de descarga del paquete independiente de Service Fabric de Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="fe8af-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="fe8af-123">Puede encontrar detalles sobre el contenido del paquete [aquí](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="fe8af-123">Find details on contents of the package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="fe8af-124">El paquete en tiempo de ejecución de Service Fabric se descarga automáticamente en el momento de la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="fe8af-124">The Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="fe8af-125">Si la implementación se realiza desde una máquina no está conectada a Internet, descargue el paquete en tiempo de ejecución fuera de banda desde aquí:</span><span class="sxs-lookup"><span data-stu-id="fe8af-125">If deploying from a machine not connected to the internet, please download the runtime package out of band from here:</span></span> <br><span data-ttu-id="fe8af-126">
[Vínculo de descarga del entorno de tiempo de ejecución de Service Fabric para Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="fe8af-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="fe8af-127">Puede encontrar ejemplos de configuración de clúster independiente en:</span><span class="sxs-lookup"><span data-stu-id="fe8af-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="fe8af-128">
[Ejemplos de configuración de clúster independiente](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="fe8af-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-the-cluster"></a><span data-ttu-id="fe8af-129">Creación de clústeres</span><span class="sxs-lookup"><span data-stu-id="fe8af-129">Create the cluster</span></span>
<span data-ttu-id="fe8af-130">Service Fabric se puede implementar en un clúster de desarrollo de una máquina mediante el archivo *ClusterConfig.Unsecure.DevCluster.json* que se incluye en los [ejemplos](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="fe8af-130">Service Fabric can be deployed to a one-machine development cluster by using the *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="fe8af-131">Desempaquete el paquete independiente en su máquina, copie el archivo de configuración de ejemplo en la máquina local y ejecute luego el script *CreateServiceFabricCluster.ps1* mediante una sesión de administrador de PowerShell, desde la carpeta del paquete independiente:</span><span class="sxs-lookup"><span data-stu-id="fe8af-131">Unpack the standalone package to your machine, copy the sample config file to the local machine, then run the *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from the standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="fe8af-132">Paso 1A: Creación de un clúster de desarrollo local poco seguro</span><span class="sxs-lookup"><span data-stu-id="fe8af-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="fe8af-133">Para detalles de solución de problemas, consulte la sección Configuración del entorno del artículo sobre el [planeamiento la preparación de la implementación del clúster](service-fabric-cluster-standalone-deployment-preparation.md).</span><span class="sxs-lookup"><span data-stu-id="fe8af-133">See the Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="fe8af-134">Si ya ha terminado de ejecutar los escenarios de desarrollo, puede quitar el clúster de Service Fabric de la máquina; para ello, consulte los pasos de la sección "[Eliminación de un clúster](#removecluster_anchor)".</span><span class="sxs-lookup"><span data-stu-id="fe8af-134">If you're finished running development scenarios, you can remove the Service Fabric cluster from the machine by referring to steps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="fe8af-135">Paso 1B: Creación de un clúster de varias máquinas</span><span class="sxs-lookup"><span data-stu-id="fe8af-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="fe8af-136">Después de haber realizado los pasos de planeamiento y preparación detallados en el siguiente vínculo, está listo para crear el clúster de producción mediante el archivo de configuración del clúster.</span><span class="sxs-lookup"><span data-stu-id="fe8af-136">After you have gone through the planning and preparation steps detailed at the below link, you are ready to create your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="fe8af-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) (Planeamiento y preparación del desarrollo del clúster)</span><span class="sxs-lookup"><span data-stu-id="fe8af-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="fe8af-138">Valide el archivo de configuración que se ha escrito ejecutando el script *TestConfiguration.ps1* desde la carpeta del paquete independiente:</span><span class="sxs-lookup"><span data-stu-id="fe8af-138">Validate the configuration file you have written by running the *TestConfiguration.ps1* script from the standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="fe8af-139">El resultado debería ser parecido al que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="fe8af-139">You should see output like below.</span></span> <span data-ttu-id="fe8af-140">Si el campo inferior "Pasado" se devuelve como "True", se han superado las comprobaciones de integridad y el clúster parece ser implementable según la configuración de entrada.</span><span class="sxs-lookup"><span data-stu-id="fe8af-140">If the bottom field "Passed" is returned as "True", sanity checks have passed and the cluster looks to be deployable based on the input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written to existing trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
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

2. <span data-ttu-id="fe8af-141">Cree el clúster: ejecute el script *CreateServiceFabricCluster.ps1* para implementar el clúster de Service Fabric en las máquinas de la configuración.</span><span class="sxs-lookup"><span data-stu-id="fe8af-141">Create the cluster:  Run the *CreateServiceFabricCluster.ps1* script to deploy the Service Fabric cluster across each machine in the configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="fe8af-142">Se escriben seguimientos de implementación en la máquina virtual/máquina física en la que ejecutó el script CreateServiceFabricCluster.ps1 de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe8af-142">Deployment traces are written to the VM/machine on which you ran the CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="fe8af-143">Estos seguimientos se pueden encontrar en la subcarpeta DeploymentTraces, que se encuentra en el directorio desde el que se ejecutó el script.</span><span class="sxs-lookup"><span data-stu-id="fe8af-143">These can be found in the subfolder DeploymentTraces, based in the directory from which the script was run.</span></span> <span data-ttu-id="fe8af-144">Para ver si Service Fabric se ha implementado correctamente en una máquina, busque los archivos instalados en el directorio FabricDataRoot, como se detalla en la sección FabricSettings del archivo de configuración del clúster (de forma predeterminada c:\ProgramData\SF).</span><span class="sxs-lookup"><span data-stu-id="fe8af-144">To see if Service Fabric was deployed correctly to a machine, find the installed files in the FabricDataRoot directory, as detailed in the cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="fe8af-145">También, los procesos FabricHost.exe y Fabric.exe se pueden ver ejecutando el Administrador de tareas.</span><span class="sxs-lookup"><span data-stu-id="fe8af-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="fe8af-146">Paso 1C: Creación de un clúster sin conexión (desconectado de internet)</span><span class="sxs-lookup"><span data-stu-id="fe8af-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="fe8af-147">El paquete en tiempo de ejecución de Service Fabric se descarga automáticamente durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="fe8af-147">The Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="fe8af-148">Al implementar un clúster en máquinas sin conexión a internet, debe descargar el paquete en tiempo de ejecución de Service Fabric por separado y proporcionar su ruta de acceso durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="fe8af-148">When deploying a cluster to machines not connected to the internet, you will need to download the Service Fabric runtime package separately, and provide the path to it at cluster creation.</span></span>
<span data-ttu-id="fe8af-149">El paquete en tiempo de ejecución se puede descargar por separado desde otra máquina conectada a internet, desde el [vínculo de descarga: Service Fabric en tiempo de ejecución para Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span><span class="sxs-lookup"><span data-stu-id="fe8af-149">The runtime package can be downloaded separately, from another machine connected to the internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="fe8af-150">Copie el paquete en tiempo de ejecución donde vaya a implementar el clúster desconectado y cree el clúster mediante la ejecución de `CreateServiceFabricCluster.ps1` con el parámetro `-FabricRuntimePackagePath` incluido, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="fe8af-150">Copy the runtime package to where you are deploying the offline cluster from, and create the cluster by running `CreateServiceFabricCluster.ps1` with the `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="fe8af-151">donde `.\ClusterConfig.json` y `.\MicrosoftAzureServiceFabric.cab` son las rutas de acceso a la configuración del clúster y el archivo .cab en tiempo de ejecución, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="fe8af-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are the paths to the cluster configuration and the runtime .cab file respectively.</span></span>


### <a name="step-2-connect-to-the-cluster"></a><span data-ttu-id="fe8af-152">Paso 2: Conexión al clúster</span><span class="sxs-lookup"><span data-stu-id="fe8af-152">Step 2: Connect to the cluster</span></span>
<span data-ttu-id="fe8af-153">Para conectarse a un clúster seguro, vea [Conexión a un clúster seguro](service-fabric-connect-to-secure-cluster.md) en Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fe8af-153">To connect to a secure cluster, see [Service fabric connect to secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="fe8af-154">Para conectarse a un clúster no seguro, ejecute el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fe8af-154">To connect to an unsecure cluster, run the following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="fe8af-155">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fe8af-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="fe8af-156">Paso 3: Incorporación de Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="fe8af-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="fe8af-157">Ahora puede conectarse al clúster con Service Fabric Explorer directamente desde una de las máquinas con http://localhost:19080/Explorer/index.html o de forma remota con http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span><span class="sxs-lookup"><span data-stu-id="fe8af-157">Now you can connect to the cluster with Service Fabric Explorer either directly from one of the machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="fe8af-158">Agregar y quitar nodos</span><span class="sxs-lookup"><span data-stu-id="fe8af-158">Add and remove nodes</span></span>
<span data-ttu-id="fe8af-159">Puede agregar o quitar nodos del clúster de Service Fabric independiente a medida que cambien las necesidades empresariales.</span><span class="sxs-lookup"><span data-stu-id="fe8af-159">You can add or remove nodes to your standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="fe8af-160">Lea [Incorporación o eliminación de nodos de un clúster de Service Fabric independiente](service-fabric-cluster-windows-server-add-remove-nodes.md) para obtener pasos detallados.</span><span class="sxs-lookup"><span data-stu-id="fe8af-160">See [Add or Remove nodes to a Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="fe8af-161">Eliminación de un clúster</span><span class="sxs-lookup"><span data-stu-id="fe8af-161">Remove a cluster</span></span>
<span data-ttu-id="fe8af-162">Para quitar un clúster, ejecute el script de PowerShell *RemoveServiceFabricCluster.ps1* desde la carpeta del paquete y proporcione la ruta al archivo de configuración JSON.</span><span class="sxs-lookup"><span data-stu-id="fe8af-162">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="fe8af-163">También puede especificar una ubicación para el registro que se va a eliminar.</span><span class="sxs-lookup"><span data-stu-id="fe8af-163">You can optionally specify a location for the log of the deletion.</span></span>

<span data-ttu-id="fe8af-164">Este script puede ejecutarse en cualquier máquina que tenga acceso de administrador a todas las máquinas que se muestran como nodos en el archivo de configuración del clúster.</span><span class="sxs-lookup"><span data-stu-id="fe8af-164">This script can be run on any machine that has administrator access to all the machines that are listed as nodes in the cluster configuration file.</span></span> <span data-ttu-id="fe8af-165">La máquina donde se ejecuta este script no tiene que formar parte del clúster.</span><span class="sxs-lookup"><span data-stu-id="fe8af-165">The machine that this script is run on does not have to be part of the cluster.</span></span>

```
# Removes Service Fabric from each machine in the configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from the current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-to-opt-out-of-it"></a><span data-ttu-id="fe8af-166">Datos de telemetría recopilados y cómo omitirlos</span><span class="sxs-lookup"><span data-stu-id="fe8af-166">Telemetry data collected and how to opt out of it</span></span>
<span data-ttu-id="fe8af-167">De forma predeterminada, el producto recopila datos de telemetría sobre el uso de Service Fabric para mejorar el producto.</span><span class="sxs-lookup"><span data-stu-id="fe8af-167">As a default, the product collects telemetry on the Service Fabric usage to improve the product.</span></span> <span data-ttu-id="fe8af-168">El Analizador de procedimientos recomendados que se ejecuta como parte de la instalación, comprueba la conectividad a [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span><span class="sxs-lookup"><span data-stu-id="fe8af-168">The Best Practice Analyzer that runs as a part of the setup checks for connectivity to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="fe8af-169">Si no está accesible, el programa de instalación genera un error, a menos que decida no participar en la telemetría.</span><span class="sxs-lookup"><span data-stu-id="fe8af-169">If it is not reachable, the setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="fe8af-170">La canalización de telemetría intenta cargar los datos siguientes en [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) una vez al día.</span><span class="sxs-lookup"><span data-stu-id="fe8af-170">The telemetry pipeline tries to upload the following data to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="fe8af-171">Es una carga de mejor esfuerzo y no tiene ningún impacto en la funcionalidad del clúster.</span><span class="sxs-lookup"><span data-stu-id="fe8af-171">It is a best-effort upload and has no impact on the cluster functionality.</span></span> <span data-ttu-id="fe8af-172">Solo se envía la telemetría desde el nodo que ejecuta el administrador de conmutación por error principal.</span><span class="sxs-lookup"><span data-stu-id="fe8af-172">The telemetry is only sent from the node that runs the failover manager primary.</span></span> <span data-ttu-id="fe8af-173">Ningún otro nodo envía telemetría.</span><span class="sxs-lookup"><span data-stu-id="fe8af-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="fe8af-174">La telemetría consta de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe8af-174">The telemetry consists of the following:</span></span>

* <span data-ttu-id="fe8af-175">Número de servicios</span><span class="sxs-lookup"><span data-stu-id="fe8af-175">Number of services</span></span>
* <span data-ttu-id="fe8af-176">Número de ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="fe8af-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="fe8af-177">Número de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="fe8af-177">Number of Applications</span></span>
* <span data-ttu-id="fe8af-178">Número de ApplicationUpgrades</span><span class="sxs-lookup"><span data-stu-id="fe8af-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="fe8af-179">Número de FailoverUnits</span><span class="sxs-lookup"><span data-stu-id="fe8af-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="fe8af-180">Número de InBuildFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="fe8af-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="fe8af-181">Número de UnhealthyFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="fe8af-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="fe8af-182">Número de réplicas</span><span class="sxs-lookup"><span data-stu-id="fe8af-182">Number of Replicas</span></span>
* <span data-ttu-id="fe8af-183">Número de InBuildReplicas</span><span class="sxs-lookup"><span data-stu-id="fe8af-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="fe8af-184">Número de StandByReplicas</span><span class="sxs-lookup"><span data-stu-id="fe8af-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="fe8af-185">Número de OfflineReplicas</span><span class="sxs-lookup"><span data-stu-id="fe8af-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="fe8af-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="fe8af-186">CommonQueueLength</span></span>
* <span data-ttu-id="fe8af-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="fe8af-187">QueryQueueLength</span></span>
* <span data-ttu-id="fe8af-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="fe8af-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="fe8af-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="fe8af-189">CommitQueueLength</span></span>
* <span data-ttu-id="fe8af-190">Número de nodos</span><span class="sxs-lookup"><span data-stu-id="fe8af-190">Number of Nodes</span></span>
* <span data-ttu-id="fe8af-191">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="fe8af-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="fe8af-192">ClusterId: se trata de un GUID generado aleatoriamente para cada clúster</span><span class="sxs-lookup"><span data-stu-id="fe8af-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="fe8af-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="fe8af-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="fe8af-194">Dirección IP de la máquina virtual o la máquina desde la que se carga la telemetría</span><span class="sxs-lookup"><span data-stu-id="fe8af-194">IP address of the virtual machine or machine from which the telemetry is uploaded</span></span>

<span data-ttu-id="fe8af-195">Para deshabilitar la telemetría, agregue lo siguiente al elemento *properties* en la configuración del clúster: *enableTelemetry: false*.</span><span class="sxs-lookup"><span data-stu-id="fe8af-195">To disable telemetry, add the following to *properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="fe8af-196">Características de versión preliminar incluidas en este paquete</span><span class="sxs-lookup"><span data-stu-id="fe8af-196">Preview features included in this package</span></span>
<span data-ttu-id="fe8af-197">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="fe8af-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="fe8af-198">Con la nueva [versión de GA del clúster independiente para Windows Server (versión 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), puede actualizar el clúster a versiones futuras, manual o automáticamente.</span><span class="sxs-lookup"><span data-stu-id="fe8af-198">Starting with the new [GA version of the standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster to future releases, manually or automatically.</span></span> <span data-ttu-id="fe8af-199">Consulte el documento [Actualización del clúster de Service Fabric independiente en Windows Server](service-fabric-cluster-upgrade-windows-server.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="fe8af-199">Refer to [Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fe8af-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fe8af-200">Next steps</span></span>
* [<span data-ttu-id="fe8af-201">Implementación y eliminación de aplicaciones con PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe8af-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="fe8af-202">Opciones de configuración de clústeres de Windows independientes</span><span class="sxs-lookup"><span data-stu-id="fe8af-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="fe8af-203">Incorporación o eliminación de nodos de un clúster de Service Fabric independiente</span><span class="sxs-lookup"><span data-stu-id="fe8af-203">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="fe8af-204">Actualización de nodos de un clúster de Service Fabric independiente</span><span class="sxs-lookup"><span data-stu-id="fe8af-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="fe8af-205">Creación de un clúster de Service Fabric independiente con máquinas virtuales de Azure con Windows</span><span class="sxs-lookup"><span data-stu-id="fe8af-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="fe8af-206">Proteger un clúster independiente en Windows mediante la seguridad de Windows</span><span class="sxs-lookup"><span data-stu-id="fe8af-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="fe8af-207">Protección de un clúster de Windows independiente mediante certificados</span><span class="sxs-lookup"><span data-stu-id="fe8af-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png

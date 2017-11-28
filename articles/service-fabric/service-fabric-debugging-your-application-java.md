---
title: "Depuración de la aplicación de Azure Service Fabric en Eclipse | Microsoft Docs"
description: "Mejore la confiabilidad y el rendimiento de los servicios mediante su desarrollo y depuración en Eclipse en un clúster de desarrollo local."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: f3bcee3794de35005bd387ecfae7e6707f3cb5ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="2d3fa-103">Depuración de la aplicación de Service Fabric para Java con Eclipse</span><span class="sxs-lookup"><span data-stu-id="2d3fa-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2d3fa-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="2d3fa-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="2d3fa-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="2d3fa-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="2d3fa-106">Inicie un clúster de desarrollo local siguiendo los pasos descritos en [Configurar el entorno de desarrollo de Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2d3fa-106">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="2d3fa-107">Actualice el archivo entryPoint.sh del servicio que desea depurar para que comience el proceso de Java con parámetros de depuración remota.</span><span class="sxs-lookup"><span data-stu-id="2d3fa-107">Update entryPoint.sh of the service you wish to debug, so that it starts the java process with remote debug parameters.</span></span> <span data-ttu-id="2d3fa-108">Este archivo se puede encontrar en la ubicación siguiente: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="2d3fa-108">This file can be found at the following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="2d3fa-109">En este ejemplo, el puerto 8001 está establecido para depuración.</span><span class="sxs-lookup"><span data-stu-id="2d3fa-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="2d3fa-110">Actualice el manifiesto de aplicación estableciendo el recuento de instancias o el recuento de réplicas para el servicio que está en depuración en 1.</span><span class="sxs-lookup"><span data-stu-id="2d3fa-110">Update the Application Manifest by setting the instance count or the replica count for the service that is being debugged to 1.</span></span> <span data-ttu-id="2d3fa-111">Esta configuración evita conflictos en el puerto que se usa para depuración.</span><span class="sxs-lookup"><span data-stu-id="2d3fa-111">This setting avoids conflicts for the port that is used for debugging.</span></span> <span data-ttu-id="2d3fa-112">Por ejemplo, para servicios sin estado, establezca ``InstanceCount="1"`` y, para los servicios con estado, establezca los tamaños del conjunto de réplicas mínimo y de destino en 1 de la manera siguiente: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="2d3fa-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set the target and min replica set sizes to 1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="2d3fa-113">Implemente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2d3fa-113">Deploy the application.</span></span>

5. <span data-ttu-id="2d3fa-114">En el IDE de Eclipse, seleccione **Run -> Debug Configurations -> Remote Java Application and input connection properties** (Ejecutar -> Configuraciones de depuración -> Aplicación Java remota y propiedades de conexión de entrada) y establezca las propiedades como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="2d3fa-114">In the Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set the properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="2d3fa-115">Establezca puntos de interrupción en los puntos deseados y depure la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2d3fa-115">Set breakpoints at desired points and debug the application.</span></span>

<span data-ttu-id="2d3fa-116">Si se bloquea la aplicación, puede que también desee habilitar los volcados de memoria.</span><span class="sxs-lookup"><span data-stu-id="2d3fa-116">If the application is crashing, you may also want to enable coredumps.</span></span> <span data-ttu-id="2d3fa-117">Ejecute ``ulimit -c`` en un shell y, si devuelve el valor 0, los volcados de memoria no están habilitados.</span><span class="sxs-lookup"><span data-stu-id="2d3fa-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="2d3fa-118">Para habilitar volcados de memoria ilimitados, ejecute el comando siguiente: ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="2d3fa-118">To enable unlimited coredumps, execute the following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="2d3fa-119">También podemos comprobar el estado con el comando ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="2d3fa-119">You can also verify the status using the command ``ulimit -a``.</span></span>  <span data-ttu-id="2d3fa-120">Si desea actualizar la ruta de acceso a la generación de volcado de memoria, ejecute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="2d3fa-120">If you wanted to update the coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="2d3fa-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2d3fa-121">Next steps</span></span>

* <span data-ttu-id="2d3fa-122">[Recopilación de registros con Diagnósticos de Azure de Linux](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="2d3fa-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="2d3fa-123">[Supervisión y diagnóstico de servicios localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2d3fa-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>

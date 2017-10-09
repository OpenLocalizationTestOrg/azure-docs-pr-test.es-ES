---
title: "aaaDebug la aplicación de tejido de servicio de Azure en Eclipse | Documentos de Microsoft"
description: "Mejorar Hola confiabilidad y rendimiento de los servicios mediante el desarrollo y depuración en Eclipse en un clúster de desarrollo local."
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
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="97786-103">Depuración de la aplicación de Service Fabric para Java con Eclipse</span><span class="sxs-lookup"><span data-stu-id="97786-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97786-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="97786-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="97786-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="97786-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="97786-106">Iniciar un clúster de desarrollo local siguiendo los pasos de hello en [configuración del entorno de desarrollo de Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="97786-106">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="97786-107">Actualizar entryPoint.sh del servicio de hello desea toodebug, para que se inicie el proceso de java de hello con parámetros de depuración remota.</span><span class="sxs-lookup"><span data-stu-id="97786-107">Update entryPoint.sh of hello service you wish toodebug, so that it starts hello java process with remote debug parameters.</span></span> <span data-ttu-id="97786-108">Este archivo puede encontrarse en hello ubicación siguiente: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="97786-108">This file can be found at hello following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="97786-109">En este ejemplo, el puerto 8001 está establecido para depuración.</span><span class="sxs-lookup"><span data-stu-id="97786-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="97786-110">Actualizar Hola el manifiesto de aplicación mediante el establecimiento de recuento de instancias de Hola o hello número de réplica para el servicio de Hola que se está depurando too1.</span><span class="sxs-lookup"><span data-stu-id="97786-110">Update hello Application Manifest by setting hello instance count or hello replica count for hello service that is being debugged too1.</span></span> <span data-ttu-id="97786-111">Esta configuración evita conflictos de puerto de Hola que se utiliza para la depuración.</span><span class="sxs-lookup"><span data-stu-id="97786-111">This setting avoids conflicts for hello port that is used for debugging.</span></span> <span data-ttu-id="97786-112">Por ejemplo, para los servicios sin estado, establezca ``InstanceCount="1"`` y servicios con estado de réplica de destino y min Hola conjunto establezca too1 tamaños de la manera siguiente: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="97786-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set hello target and min replica set sizes too1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="97786-113">Implementar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="97786-113">Deploy hello application.</span></span>

5. <span data-ttu-id="97786-114">Hola Eclipse IDE, seleccione **ejecución -> Debug Configurations -> aplicación Java remota y las propiedades de conexión de entrada** y establecer las propiedades de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="97786-114">In hello Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set hello properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="97786-115">Establecer puntos de interrupción en puntos deseados y depurar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="97786-115">Set breakpoints at desired points and debug hello application.</span></span>

<span data-ttu-id="97786-116">Si se bloquea la aplicación hello, también puede tooenable coredumps.</span><span class="sxs-lookup"><span data-stu-id="97786-116">If hello application is crashing, you may also want tooenable coredumps.</span></span> <span data-ttu-id="97786-117">Ejecute ``ulimit -c`` en un shell y, si devuelve el valor 0, los volcados de memoria no están habilitados.</span><span class="sxs-lookup"><span data-stu-id="97786-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="97786-118">tooenable coredumps ilimitados, ejecutar el siguiente comando de Hola: ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="97786-118">tooenable unlimited coredumps, execute hello following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="97786-119">También puede comprobar el estado de hello mediante comandos de hello ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="97786-119">You can also verify hello status using hello command ``ulimit -a``.</span></span>  <span data-ttu-id="97786-120">Si desea que la ruta de acceso de generación de tooupdate hello coredump, ejecute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="97786-120">If you wanted tooupdate hello coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="97786-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97786-121">Next steps</span></span>

* <span data-ttu-id="97786-122">[Recopilación de registros con Diagnósticos de Azure de Linux](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="97786-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="97786-123">[Supervisión y diagnóstico de servicios localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="97786-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>

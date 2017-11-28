---
title: aaaAzure Crear vista previa en el tejido de Docker servicio
description: "Azure Service Fabric acepta Docker Compose toomake de formato sea más fácil tooorchestrate los contenedores existentes mediante Service Fabric. Esta compatibilidad se encuentra actualmente en versión preliminar."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="b1d43-104">Compatibilidad con la aplicación Docker Compose en Azure Service Fabric (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="b1d43-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="b1d43-105">Docker usa hello [docker compose.yml](https://docs.docker.com/compose) archivo para definir el contenedor de varias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b1d43-105">Docker uses hello [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="b1d43-106">toomake lo fácil para clientes familiarizados con aplicaciones contenedor Docker tooorchestrate existentes en el tejido de servicio de Azure, hemos incluido soporte de vista previa para Docker Compose forma nativa en la plataforma de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1d43-106">toomake it easy for customers familiar with Docker tooorchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in hello platform.</span></span> <span data-ttu-id="b1d43-107">Service Fabric puede aceptar la versión 3 y posterior de los archivos `docker-compose.yml`.</span><span class="sxs-lookup"><span data-stu-id="b1d43-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="b1d43-108">Dado que esta compatibilidad está en versión preliminar, solo se admite un subconjunto de directivas de Compose.</span><span class="sxs-lookup"><span data-stu-id="b1d43-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="b1d43-109">Por ejemplo, no se admiten las actualizaciones de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b1d43-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="b1d43-110">Sin embargo, siempre puede quitar e implementar aplicaciones en lugar de actualizarlas.</span><span class="sxs-lookup"><span data-stu-id="b1d43-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="b1d43-111">toouse esta vista previa, crear el clúster con la versión 5.7 o posterior del tiempo de ejecución de hello Service Fabric a través de hello portal de Azure junto con hello correspondiente SDK.</span><span class="sxs-lookup"><span data-stu-id="b1d43-111">toouse this preview, create your cluster with version 5.7 or greater of hello Service Fabric runtime through hello Azure portal along with hello corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="b1d43-112">Esta característica se encuentra en versión preliminar y no se admite en producción.</span><span class="sxs-lookup"><span data-stu-id="b1d43-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="b1d43-113">Implementación de un archivo de Docker Compose en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b1d43-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="b1d43-114">Hello siguientes comandos crean una aplicación de Service Fabric (denominado `fabric:/TestContainerApp` en el anterior ejemplo de Hola), que puede supervisar y administrar como cualquier otra aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b1d43-114">hello following commands create a Service Fabric application (named `fabric:/TestContainerApp` in hello preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="b1d43-115">Puede usar el nombre de la aplicación especificada de Hola para consultas de estado.</span><span class="sxs-lookup"><span data-stu-id="b1d43-115">You can use hello specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="b1d43-116">Uso de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1d43-116">Use PowerShell</span></span>

<span data-ttu-id="b1d43-117">Crear una aplicación de redacción de tejido de servicio desde un archivo de docker compose.yml ejecutando el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="b1d43-117">Create a Service Fabric Compose application from a docker-compose.yml file by running hello following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="b1d43-118">`RegistryUserName`y `RegistryPassword` consulte toohello contenedor del registro username y password.</span><span class="sxs-lookup"><span data-stu-id="b1d43-118">`RegistryUserName` and `RegistryPassword` refer toohello container registry username and password.</span></span> <span data-ttu-id="b1d43-119">Después de haber completado la aplicación hello, puede comprobar su estado mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b1d43-119">After you've completed hello application, you can check its status by using hello following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="b1d43-120">toodelete Hola redactar aplicación a través de PowerShell, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b1d43-120">toodelete hello Compose application through PowerShell, use hello following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="b1d43-121">Uso de la CLI de Azure Service Fabric (sfctl)</span><span class="sxs-lookup"><span data-stu-id="b1d43-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="b1d43-122">Como alternativa, puede usar Hola siguiente comando de CLI de tejido de servicio:</span><span class="sxs-lookup"><span data-stu-id="b1d43-122">Alternatively, you can use hello following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="b1d43-123">Después de haber creado la aplicación hello, puede comprobar su estado mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b1d43-123">After you've created hello application, you can check its status by using hello following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="b1d43-124">Hola toodelete aplicación de redacción, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b1d43-124">toodelete hello Compose application, use hello following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="b1d43-125">Directivas de Compose admitidas</span><span class="sxs-lookup"><span data-stu-id="b1d43-125">Supported Compose directives</span></span>

<span data-ttu-id="b1d43-126">Esta vista previa admite un subconjunto de opciones de configuración de Hola desde el formato de versión 3 de redactar hello, incluidos Hola después a primitivas:</span><span class="sxs-lookup"><span data-stu-id="b1d43-126">This preview supports a subset of hello configuration options from hello Compose version 3 format, including hello following primitives:</span></span>

* <span data-ttu-id="b1d43-127">Services > Deploy > Replicas</span><span class="sxs-lookup"><span data-stu-id="b1d43-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="b1d43-128">Services > Deploy > Placement > Constraints</span><span class="sxs-lookup"><span data-stu-id="b1d43-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="b1d43-129">Services > Deploy > Resources > Limits</span><span class="sxs-lookup"><span data-stu-id="b1d43-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="b1d43-130">-cpu-shares</span><span class="sxs-lookup"><span data-stu-id="b1d43-130">-cpu-shares</span></span>
    * <span data-ttu-id="b1d43-131">-memory</span><span class="sxs-lookup"><span data-stu-id="b1d43-131">-memory</span></span>
    * <span data-ttu-id="b1d43-132">-memory-swap</span><span class="sxs-lookup"><span data-stu-id="b1d43-132">-memory-swap</span></span>
* <span data-ttu-id="b1d43-133">Services > Commands</span><span class="sxs-lookup"><span data-stu-id="b1d43-133">Services > Commands</span></span>
* <span data-ttu-id="b1d43-134">Services > Environment</span><span class="sxs-lookup"><span data-stu-id="b1d43-134">Services > Environment</span></span>
* <span data-ttu-id="b1d43-135">Services > Ports</span><span class="sxs-lookup"><span data-stu-id="b1d43-135">Services > Ports</span></span>
* <span data-ttu-id="b1d43-136">Services > Image</span><span class="sxs-lookup"><span data-stu-id="b1d43-136">Services > Image</span></span>
* <span data-ttu-id="b1d43-137">Services > Isolation (solo para Windows)</span><span class="sxs-lookup"><span data-stu-id="b1d43-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="b1d43-138">Services > Logging > Driver</span><span class="sxs-lookup"><span data-stu-id="b1d43-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="b1d43-139">Services > Logging > Driver > Options</span><span class="sxs-lookup"><span data-stu-id="b1d43-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="b1d43-140">Volumen e implementación > Volumen</span><span class="sxs-lookup"><span data-stu-id="b1d43-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="b1d43-141">Configurar clúster Hola para aplicar límites de recursos, como se describe en [regulador de recursos de Service Fabric](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="b1d43-141">Set up hello cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="b1d43-142">El resto de directivas de Docker Compose no se admiten en esta versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="b1d43-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="b1d43-143">Cálculo de ServiceDnsName</span><span class="sxs-lookup"><span data-stu-id="b1d43-143">ServiceDnsName computation</span></span>

<span data-ttu-id="b1d43-144">Si el nombre de servicio de Hola que especifique en un archivo de composición es un nombre de dominio completo (es decir, contiene un punto [.]), nombre DNS de hello registrado por Service Fabric es `<ServiceName>` (incluido el punto de hello).</span><span class="sxs-lookup"><span data-stu-id="b1d43-144">If hello service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), hello DNS name registered by Service Fabric is `<ServiceName>` (including hello dot).</span></span> <span data-ttu-id="b1d43-145">De lo contrario, cada segmento de ruta de acceso en nombre de la aplicación hello se convierte en una etiqueta de dominio en nombre DNS del servicio de hello, con el primer segmento de ruta de acceso Hola se convierta en etiqueta de dominio de nivel superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1d43-145">If not, each path segment in hello application name becomes a domain label in hello service DNS name, with hello first path segment becoming hello top-level domain label.</span></span>

<span data-ttu-id="b1d43-146">Por ejemplo, si Hola especifica el nombre de la aplicación es `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` sería Hola nombre DNS registrado.</span><span class="sxs-lookup"><span data-stu-id="b1d43-146">For example, if hello specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be hello registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="b1d43-147">Diferencias entre Compose (definición de instancia) y el modelo de aplicación de Service Fabric (definición de tipo)</span><span class="sxs-lookup"><span data-stu-id="b1d43-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="b1d43-148">Un archivo docker-compose.yml describe un conjunto implementable de contenedores que incluye sus propiedades y configuraciones.</span><span class="sxs-lookup"><span data-stu-id="b1d43-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="b1d43-149">Por ejemplo, archivo hello puede contener variables de entorno y puertos.</span><span class="sxs-lookup"><span data-stu-id="b1d43-149">For example, hello file can contain environment variables and ports.</span></span> <span data-ttu-id="b1d43-150">También puede especificar parámetros de implementación, como las restricciones de posición, los límites de recursos y los nombres DNS, en archivo de hello compose.yml de docker.</span><span class="sxs-lookup"><span data-stu-id="b1d43-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in hello docker-compose.yml file.</span></span>

<span data-ttu-id="b1d43-151">Hola [modelo de aplicaciones de Service Fabric](service-fabric-application-model.md) usa tipos de servicio y los tipos de aplicación, donde puede tener muchas instancias de aplicación de Hola mismo tipo.</span><span class="sxs-lookup"><span data-stu-id="b1d43-151">hello [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of hello same type.</span></span> <span data-ttu-id="b1d43-152">Por ejemplo, puede tener una instancia de aplicación por cliente.</span><span class="sxs-lookup"><span data-stu-id="b1d43-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="b1d43-153">Este modelo basado en el tipo es compatible con varias versiones del programa Hola a mismo tipo de aplicación que está registrado con hello en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="b1d43-153">This type-based model supports multiple versions of hello same application type that's registered with hello runtime.</span></span>

<span data-ttu-id="b1d43-154">Por ejemplo, un cliente puede tener una aplicación crea una instancia con tipo 1.0 de AppTypeA y cliente B puede tener otra aplicación que crea una instancia con hello mismo tipo y la versión.</span><span class="sxs-lookup"><span data-stu-id="b1d43-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with hello same type and version.</span></span> <span data-ttu-id="b1d43-155">Definir tipos de aplicación hello en los manifiestos de aplicación hello y especificar parámetros de nombre y la implementación de la aplicación hello cuando se crea la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b1d43-155">You define hello application types in hello application manifests, and you specify hello application name and deployment parameters when you create hello application.</span></span>

<span data-ttu-id="b1d43-156">Aunque este modelo ofrece flexibilidad, planeamos toosupport un modelo de implementación sea más sencillo y basados en instancias donde tipos son implícitos del archivo de manifiesto de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1d43-156">Although this model offers flexibility, we are also planning toosupport a simpler, instance-based deployment model where types are implicit from hello manifest file.</span></span> <span data-ttu-id="b1d43-157">En este modelo, cada aplicación obtiene su propio manifiesto independiente.</span><span class="sxs-lookup"><span data-stu-id="b1d43-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="b1d43-158">Esta iniciativa se va a trasladar a la versión preliminar agregando compatibilidad con el archivo docker-compose.yml, que es un formato de implementación basado en instancias.</span><span class="sxs-lookup"><span data-stu-id="b1d43-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1d43-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b1d43-159">Next steps</span></span>

* <span data-ttu-id="b1d43-160">Obtener información detallada acerca de hello [modelo de aplicaciones de Service Fabric](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="b1d43-160">Read up on hello [Service Fabric application model](service-fabric-application-model.md)</span></span>
* [<span data-ttu-id="b1d43-161">Introducción a la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b1d43-161">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

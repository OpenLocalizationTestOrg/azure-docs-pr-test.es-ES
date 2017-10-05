---
title: "Versión preliminar de Azure Service Fabric Docker Compose"
description: "Azure Service Fabric acepta el formato de Docker Compose para facilitar la organización de los contenedores existentes con Service Fabric. Esta compatibilidad se encuentra actualmente en versión preliminar."
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
ms.openlocfilehash: e05d1a3d6111e3bbc34008226bcd1fdf35935450
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="c08bf-104">Compatibilidad con la aplicación Docker Compose en Azure Service Fabric (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="c08bf-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="c08bf-105">Docker usa el archivo [docker compose.yml](https://docs.docker.com/compose) para definir aplicaciones de varios contenedores.</span><span class="sxs-lookup"><span data-stu-id="c08bf-105">Docker uses the [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="c08bf-106">Para que a los clientes familiarizados con Docker les sea más fácil organizar las aplicaciones de contenedores existentes en Azure Service Fabric, se ha incluido compatibilidad de versión preliminar para Docker Compose de forma nativa en la plataforma.</span><span class="sxs-lookup"><span data-stu-id="c08bf-106">To make it easy for customers familiar with Docker to orchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in the platform.</span></span> <span data-ttu-id="c08bf-107">Service Fabric puede aceptar la versión 3 y posterior de los archivos `docker-compose.yml`.</span><span class="sxs-lookup"><span data-stu-id="c08bf-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="c08bf-108">Dado que esta compatibilidad está en versión preliminar, solo se admite un subconjunto de directivas de Compose.</span><span class="sxs-lookup"><span data-stu-id="c08bf-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="c08bf-109">Por ejemplo, no se admiten las actualizaciones de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c08bf-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="c08bf-110">Sin embargo, siempre puede quitar e implementar aplicaciones en lugar de actualizarlas.</span><span class="sxs-lookup"><span data-stu-id="c08bf-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="c08bf-111">Para usar esta versión preliminar, cree el clúster con la versión 5.7 o superior del entorno en tiempo de ejecución de Service Fabric a través de Azure Portal junto con el SDK correspondiente.</span><span class="sxs-lookup"><span data-stu-id="c08bf-111">To use this preview, create your cluster with version 5.7 or greater of the Service Fabric runtime through the Azure portal along with the corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="c08bf-112">Esta característica se encuentra en versión preliminar y no se admite en producción.</span><span class="sxs-lookup"><span data-stu-id="c08bf-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="c08bf-113">Implementación de un archivo de Docker Compose en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c08bf-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="c08bf-114">Los siguientes comandos crean una aplicación de Service Fabric (llamada `fabric:/TestContainerApp` en el ejemplo anterior), la cual se puede supervisar y administrar como cualquier otra aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c08bf-114">The following commands create a Service Fabric application (named `fabric:/TestContainerApp` in the preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="c08bf-115">Puede usar el nombre de aplicación especificado para las consultas de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="c08bf-115">You can use the specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="c08bf-116">Uso de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c08bf-116">Use PowerShell</span></span>

<span data-ttu-id="c08bf-117">Cree una aplicación Compose de Service Fabric a partir de un archivo docker-compose.yml ejecutando el siguiente comando en PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c08bf-117">Create a Service Fabric Compose application from a docker-compose.yml file by running the following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="c08bf-118">`RegistryUserName` y `RegistryPassword` hacen referencia al nombre de usuario y la contraseña del registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="c08bf-118">`RegistryUserName` and `RegistryPassword` refer to the container registry username and password.</span></span> <span data-ttu-id="c08bf-119">Después de haber completado la aplicación, puede comprobar su estado mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c08bf-119">After you've completed the application, you can check its status by using the following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="c08bf-120">Para eliminar la aplicación Compose mediante PowerShell, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c08bf-120">To delete the Compose application through PowerShell, use the following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="c08bf-121">Uso de la CLI de Azure Service Fabric (sfctl)</span><span class="sxs-lookup"><span data-stu-id="c08bf-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="c08bf-122">También puede ejecutar el siguiente comando de la CLI de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="c08bf-122">Alternatively, you can use the following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="c08bf-123">Después de crear la aplicación, puede comprobar su estado mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c08bf-123">After you've created the application, you can check its status by using the following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="c08bf-124">Para eliminar la aplicación Compose, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c08bf-124">To delete the Compose application, use the following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="c08bf-125">Directivas de Compose admitidas</span><span class="sxs-lookup"><span data-stu-id="c08bf-125">Supported Compose directives</span></span>

<span data-ttu-id="c08bf-126">Esta versión preliminar admite un subconjunto de las opciones de configuración en el formato de la versión 3 de Compose, lo que incluye los siguientes primitivos:</span><span class="sxs-lookup"><span data-stu-id="c08bf-126">This preview supports a subset of the configuration options from the Compose version 3 format, including the following primitives:</span></span>

* <span data-ttu-id="c08bf-127">Services > Deploy > Replicas</span><span class="sxs-lookup"><span data-stu-id="c08bf-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="c08bf-128">Services > Deploy > Placement > Constraints</span><span class="sxs-lookup"><span data-stu-id="c08bf-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="c08bf-129">Services > Deploy > Resources > Limits</span><span class="sxs-lookup"><span data-stu-id="c08bf-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="c08bf-130">-cpu-shares</span><span class="sxs-lookup"><span data-stu-id="c08bf-130">-cpu-shares</span></span>
    * <span data-ttu-id="c08bf-131">-memory</span><span class="sxs-lookup"><span data-stu-id="c08bf-131">-memory</span></span>
    * <span data-ttu-id="c08bf-132">-memory-swap</span><span class="sxs-lookup"><span data-stu-id="c08bf-132">-memory-swap</span></span>
* <span data-ttu-id="c08bf-133">Services > Commands</span><span class="sxs-lookup"><span data-stu-id="c08bf-133">Services > Commands</span></span>
* <span data-ttu-id="c08bf-134">Services > Environment</span><span class="sxs-lookup"><span data-stu-id="c08bf-134">Services > Environment</span></span>
* <span data-ttu-id="c08bf-135">Services > Ports</span><span class="sxs-lookup"><span data-stu-id="c08bf-135">Services > Ports</span></span>
* <span data-ttu-id="c08bf-136">Services > Image</span><span class="sxs-lookup"><span data-stu-id="c08bf-136">Services > Image</span></span>
* <span data-ttu-id="c08bf-137">Services > Isolation (solo para Windows)</span><span class="sxs-lookup"><span data-stu-id="c08bf-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="c08bf-138">Services > Logging > Driver</span><span class="sxs-lookup"><span data-stu-id="c08bf-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="c08bf-139">Services > Logging > Driver > Options</span><span class="sxs-lookup"><span data-stu-id="c08bf-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="c08bf-140">Volumen e implementación > Volumen</span><span class="sxs-lookup"><span data-stu-id="c08bf-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="c08bf-141">Configure el clúster para exigir límites de recursos, como se describe en [Regulación de recursos de Service Fabric](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="c08bf-141">Set up the cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="c08bf-142">El resto de directivas de Docker Compose no se admiten en esta versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="c08bf-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="c08bf-143">Cálculo de ServiceDnsName</span><span class="sxs-lookup"><span data-stu-id="c08bf-143">ServiceDnsName computation</span></span>

<span data-ttu-id="c08bf-144">Si el nombre de servicio especificado en un archivo de Compose es un nombre de dominio completo (es decir, contiene un punto, [.]), el nombre DNS registrado por Service Fabric será `<ServiceName>` (incluido el punto).</span><span class="sxs-lookup"><span data-stu-id="c08bf-144">If the service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), the DNS name registered by Service Fabric is `<ServiceName>` (including the dot).</span></span> <span data-ttu-id="c08bf-145">En caso contrario, cada segmento de la ruta del nombre de aplicación se convierte en una etiqueta de dominio del nombre DNS del servicio, siendo el primer segmento de la ruta el que se convierte en la etiqueta de dominio de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="c08bf-145">If not, each path segment in the application name becomes a domain label in the service DNS name, with the first path segment becoming the top-level domain label.</span></span>

<span data-ttu-id="c08bf-146">Por ejemplo, si el nombre de aplicación especificado es `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` sería el nombre DNS registrado.</span><span class="sxs-lookup"><span data-stu-id="c08bf-146">For example, if the specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be the registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="c08bf-147">Diferencias entre Compose (definición de instancia) y el modelo de aplicación de Service Fabric (definición de tipo)</span><span class="sxs-lookup"><span data-stu-id="c08bf-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="c08bf-148">Un archivo docker-compose.yml describe un conjunto implementable de contenedores que incluye sus propiedades y configuraciones.</span><span class="sxs-lookup"><span data-stu-id="c08bf-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="c08bf-149">Por ejemplo, el archivo puede contener las variables de entorno y los puertos.</span><span class="sxs-lookup"><span data-stu-id="c08bf-149">For example, the file can contain environment variables and ports.</span></span> <span data-ttu-id="c08bf-150">También puede especificar parámetros de implementación como, por ejemplo, las restricciones de colocación, los límites de recursos y los nombres DNS, en el archivo docker-compose.yml.</span><span class="sxs-lookup"><span data-stu-id="c08bf-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in the docker-compose.yml file.</span></span>

<span data-ttu-id="c08bf-151">El [modelo de aplicación de Service Fabric](service-fabric-application-model.md) usa tipos de servicio y tipos de aplicación, en los que puede tener muchas instancias de aplicaciones del mismo tipo.</span><span class="sxs-lookup"><span data-stu-id="c08bf-151">The [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of the same type.</span></span> <span data-ttu-id="c08bf-152">Por ejemplo, puede tener una instancia de aplicación por cliente.</span><span class="sxs-lookup"><span data-stu-id="c08bf-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="c08bf-153">Este modelo basado en tipos admite varias versiones del mismo tipo de aplicación registrado con el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c08bf-153">This type-based model supports multiple versions of the same application type that's registered with the runtime.</span></span>

<span data-ttu-id="c08bf-154">Por ejemplo, un cliente A puede tener una aplicación con una instancia creada con el tipo 1.0 de AppTypeA y un cliente B puede tener otra aplicación con una instancia creada con el mismo tipo y versión.</span><span class="sxs-lookup"><span data-stu-id="c08bf-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with the same type and version.</span></span> <span data-ttu-id="c08bf-155">Los tipos de aplicación se definen en los manifiestos de aplicación, y se puede especificar el nombre de la aplicación y los parámetros de implementación al crear la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c08bf-155">You define the application types in the application manifests, and you specify the application name and deployment parameters when you create the application.</span></span>

<span data-ttu-id="c08bf-156">Aunque este modelo ofrece flexibilidad, está prevista la compatibilidad con un modelo más sencillo de implementación basado en instancias donde los tipos son implícitos en el archivo de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="c08bf-156">Although this model offers flexibility, we are also planning to support a simpler, instance-based deployment model where types are implicit from the manifest file.</span></span> <span data-ttu-id="c08bf-157">En este modelo, cada aplicación obtiene su propio manifiesto independiente.</span><span class="sxs-lookup"><span data-stu-id="c08bf-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="c08bf-158">Esta iniciativa se va a trasladar a la versión preliminar agregando compatibilidad con el archivo docker-compose.yml, que es un formato de implementación basado en instancias.</span><span class="sxs-lookup"><span data-stu-id="c08bf-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c08bf-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c08bf-159">Next steps</span></span>

* <span data-ttu-id="c08bf-160">Descripción del [modelo de aplicación de Service Fabric](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="c08bf-160">Read up on the [Service Fabric application model](service-fabric-application-model.md)</span></span>
* [<span data-ttu-id="c08bf-161">Introducción a la CLI de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c08bf-161">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

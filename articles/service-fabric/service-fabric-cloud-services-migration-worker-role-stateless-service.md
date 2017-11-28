---
title: "Conversión de aplicaciones de Azure Cloud Services en microservicios | Microsoft Docs"
description: "Esta guía compara los roles web y de trabajo de Servicios en la nube y los servicios sin estado de Service Fabric para ayudar a la migración desde Servicios en la nube a Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4ab1f83e88b262b1752300b2786340d9abca8154
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="guide-to-converting-web-and-worker-roles-to-service-fabric-stateless-services"></a><span data-ttu-id="66a81-103">Guía de conversión de roles web y de trabajo a servicios sin estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="66a81-103">Guide to converting Web and Worker Roles to Service Fabric stateless services</span></span>
<span data-ttu-id="66a81-104">Este artículo describe cómo migrar los roles web y de trabajo de los Servicios en la nube a los servicios sin estado de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="66a81-104">This article describes how to migrate your Cloud Services Web and Worker Roles to Service Fabric stateless services.</span></span> <span data-ttu-id="66a81-105">Se trata de la ruta de migración más sencilla desde los Servicios en la nube a Service Fabric para aquellas aplicaciones cuya arquitectura global va a permanecer más o menos igual.</span><span class="sxs-lookup"><span data-stu-id="66a81-105">This is the simplest migration path from Cloud Services to Service Fabric for applications whose overall architecture is going to stay roughly the same.</span></span>

## <a name="cloud-service-project-to-service-fabric-application-project"></a><span data-ttu-id="66a81-106">Proyecto de Servicios en la nube en comparación con proyecto de la aplicación de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="66a81-106">Cloud Service project to Service Fabric application project</span></span>
 <span data-ttu-id="66a81-107">Un proyecto de Servicio en la nube y un proyecto de la aplicación de Service Fabric tienen una estructura similar y ambos representan la unidad de implementación para la aplicación, es decir, cada uno de ellos define el paquete completo que se implementa para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="66a81-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent the deployment unit for your application - that is, they each define the complete package that is deployed to run your application.</span></span> <span data-ttu-id="66a81-108">Un proyecto de Servicio en la nube contiene uno o varios roles web o de trabajo.</span><span class="sxs-lookup"><span data-stu-id="66a81-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="66a81-109">De igual forma, un proyecto de la aplicación de Service Fabric contiene uno o más servicios.</span><span class="sxs-lookup"><span data-stu-id="66a81-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="66a81-110">La diferencia es que el proyecto de Servicio en la nube une la implementación de la aplicación con una implementación de máquina virtual y, por tanto, contiene valores de configuración de máquina virtual, mientras que el proyecto de la aplicación de Service Fabric solo define una aplicación que se va a implementar en un conjunto de máquinas virtuales existentes en un clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="66a81-110">The difference is that the Cloud Service project couples the application deployment with a VM deployment and thus contains VM configuration settings in it, whereas the Service Fabric Application project only defines an application that will be deployed to a set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="66a81-111">El propio clúster de Service Fabric solo se implementa una vez, a través de una plantilla de Resource Manager o a través de Azure Portal y se pueden implementar varias aplicaciones de Service Fabric en él.</span><span class="sxs-lookup"><span data-stu-id="66a81-111">The Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through the Azure portal, and multiple Service Fabric applications can be deployed to it.</span></span>

![Comparación de proyectos de Service Fabric y de Servicios en la nube][3]

## <a name="worker-role-to-stateless-service"></a><span data-ttu-id="66a81-113">Rol de trabajo a servicio sin estado</span><span class="sxs-lookup"><span data-stu-id="66a81-113">Worker Role to stateless service</span></span>
<span data-ttu-id="66a81-114">Conceptualmente, un rol de trabajo representa una carga de trabajo sin estado, lo que significa que cada instancia de la carga de trabajo es idéntica y las solicitudes se pueden enrutar a cualquier instancia en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="66a81-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of the workload is identical and requests can be routed to any instance at any time.</span></span> <span data-ttu-id="66a81-115">No se espera que cada instancia recuerde la solicitud anterior.</span><span class="sxs-lookup"><span data-stu-id="66a81-115">Each instance is not expected to remember the previous request.</span></span> <span data-ttu-id="66a81-116">El estado en el que opera la carga de trabajo es administrado por un almacén de estado externo, como Almacenamiento de tablas de Azure o Azure DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="66a81-116">State that the workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="66a81-117">En Service Fabric, este tipo de carga de trabajo se representa mediante un servicio sin estado.</span><span class="sxs-lookup"><span data-stu-id="66a81-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="66a81-118">La manera más sencilla de migrar un rol de trabajo a Service Fabric se puede realizar mediante la conversión de un código de rol de trabajo a un servicio sin estado.</span><span class="sxs-lookup"><span data-stu-id="66a81-118">The simplest approach to migrating a Worker Role to Service Fabric can be done by converting Worker Role code to a Stateless Service.</span></span>

![Rol de trabajo a servicio sin estado][4]

## <a name="web-role-to-stateless-service"></a><span data-ttu-id="66a81-120">Rol web a servicio sin estado</span><span class="sxs-lookup"><span data-stu-id="66a81-120">Web Role to stateless service</span></span>
<span data-ttu-id="66a81-121">Igual que el rol de trabajo, un rol web también representa una carga de trabajo sin estado y, por tanto, conceptualmente también se puede asignar a un servicio sin estado de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="66a81-121">Similar to Worker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped to a Service Fabric stateless service.</span></span> <span data-ttu-id="66a81-122">Sin embargo, a diferencia de los roles web, Service Fabric no admite IIS.</span><span class="sxs-lookup"><span data-stu-id="66a81-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="66a81-123">Para migrar una aplicación web desde un rol web a un servicio sin estado debe moverla primero a un marco web autohospedado que no dependa de IIS o System.Web, como ASP.NET Core 1.</span><span class="sxs-lookup"><span data-stu-id="66a81-123">To migrate a web application from a Web Role to a stateless service requires first moving to a web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="66a81-124">**Aplicación**</span><span class="sxs-lookup"><span data-stu-id="66a81-124">**Application**</span></span> | <span data-ttu-id="66a81-125">**Compatible**</span><span class="sxs-lookup"><span data-stu-id="66a81-125">**Supported**</span></span> | <span data-ttu-id="66a81-126">**Ruta de migración**</span><span class="sxs-lookup"><span data-stu-id="66a81-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="66a81-127">Formularios Web Forms ASP.NET</span><span class="sxs-lookup"><span data-stu-id="66a81-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="66a81-128">No</span><span class="sxs-lookup"><span data-stu-id="66a81-128">No</span></span> |<span data-ttu-id="66a81-129">Conversión a ASP.NET Core 1 MVC</span><span class="sxs-lookup"><span data-stu-id="66a81-129">Convert to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="66a81-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="66a81-130">ASP.NET MVC</span></span> |<span data-ttu-id="66a81-131">Con migración</span><span class="sxs-lookup"><span data-stu-id="66a81-131">With Migration</span></span> |<span data-ttu-id="66a81-132">Actualización a ASP.NET Core 1 MVC</span><span class="sxs-lookup"><span data-stu-id="66a81-132">Upgrade to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="66a81-133">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="66a81-133">ASP.NET Web API</span></span> |<span data-ttu-id="66a81-134">Con migración</span><span class="sxs-lookup"><span data-stu-id="66a81-134">With Migration</span></span> |<span data-ttu-id="66a81-135">Uso de servidor autohospedado o ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="66a81-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="66a81-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="66a81-136">ASP.NET Core 1</span></span> |<span data-ttu-id="66a81-137">Sí</span><span class="sxs-lookup"><span data-stu-id="66a81-137">Yes</span></span> |<span data-ttu-id="66a81-138">N/D</span><span class="sxs-lookup"><span data-stu-id="66a81-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="66a81-139">API de punto de entrada y ciclo de vida</span><span class="sxs-lookup"><span data-stu-id="66a81-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="66a81-140">Las API de rol de trabajo y las de los servicios de Service Fabric ofrecen puntos de entrada similares:</span><span class="sxs-lookup"><span data-stu-id="66a81-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="66a81-141">**Punto de entrada**</span><span class="sxs-lookup"><span data-stu-id="66a81-141">**Entry Point**</span></span> | <span data-ttu-id="66a81-142">**Rol de trabajo**</span><span class="sxs-lookup"><span data-stu-id="66a81-142">**Worker Role**</span></span> | <span data-ttu-id="66a81-143">**Servicio de Service Fabric.**</span><span class="sxs-lookup"><span data-stu-id="66a81-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="66a81-144">Processing</span><span class="sxs-lookup"><span data-stu-id="66a81-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="66a81-145">Inicio de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="66a81-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="66a81-146">N/D</span><span class="sxs-lookup"><span data-stu-id="66a81-146">N/A</span></span> |
| <span data-ttu-id="66a81-147">Detención de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="66a81-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="66a81-148">N/D</span><span class="sxs-lookup"><span data-stu-id="66a81-148">N/A</span></span> |
| <span data-ttu-id="66a81-149">Apertura del agente de escucha para las solicitudes de cliente</span><span class="sxs-lookup"><span data-stu-id="66a81-149">Open listener for client requests</span></span> |<span data-ttu-id="66a81-150">N/D</span><span class="sxs-lookup"><span data-stu-id="66a81-150">N/A</span></span> |<ul><li> <span data-ttu-id="66a81-151">`CreateServiceInstanceListener()` para sin estado</span><span class="sxs-lookup"><span data-stu-id="66a81-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="66a81-152">`CreateServiceReplicaListener()` para con estado</span><span class="sxs-lookup"><span data-stu-id="66a81-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="66a81-153">Rol de trabajo</span><span class="sxs-lookup"><span data-stu-id="66a81-153">Worker Role</span></span>
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="66a81-154">Servicio sin estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="66a81-154">Service Fabric Stateless Service</span></span>
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

<span data-ttu-id="66a81-155">Ambos tienen un reemplazo principal "Run" en el que se va a iniciar el procesamiento.</span><span class="sxs-lookup"><span data-stu-id="66a81-155">Both have a primary "Run" override in which to begin processing.</span></span> <span data-ttu-id="66a81-156">Los servicios de Service Fabric combinan `Run`, `Start`, y `Stop` en un único punto de entrada, `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="66a81-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="66a81-157">El servicio debe empezar a trabajar cuando empieza `RunAsync` y debe dejar de funcionar cuando se señala el token de cancelación del método `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="66a81-157">Your service should begin working when `RunAsync` starts, and should stop working when the `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="66a81-158">Hay varias diferencias claves entre el ciclo de vida y la duración de los servicios de roles de trabajo y los de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="66a81-158">There are several key differences between the lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="66a81-159">**Ciclo de vida:** la principal diferencia es que un rol de trabajo es una máquina virtual y, por tanto, su ciclo de vida está asociado al de la máquina virtual e incluye eventos para cuando se inicia y detiene dicha máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="66a81-159">**Lifecycle:** The biggest difference is that a Worker Role is a VM and so its lifecycle is tied to the VM, which includes events for when the VM starts and stops.</span></span> <span data-ttu-id="66a81-160">Un servicio de Service Fabric tiene un ciclo de vida que es independiente del ciclo de vida de la máquina virtual, por lo que no incluye eventos para cuando el equipo o máquina virtual host se inicia y se detiene, ya que no están relacionados.</span><span class="sxs-lookup"><span data-stu-id="66a81-160">A Service Fabric service has a lifecycle that is separate from the VM lifecycle, so it does not include events for when the host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="66a81-161">**Duración:`Run` Una instancia de rol de trabajo se reciclará si se sale del método** .</span><span class="sxs-lookup"><span data-stu-id="66a81-161">**Lifetime:** A Worker Role instance will recycle if the `Run` method exits.</span></span> <span data-ttu-id="66a81-162">No obstante, el método `RunAsync` en un servicio de Service Fabric se puede ejecutar hasta su finalización y la instancia de servicio permanecerá disponible.</span><span class="sxs-lookup"><span data-stu-id="66a81-162">The `RunAsync` method in a Service Fabric service however can run to completion and the service instance will stay up.</span></span> 

<span data-ttu-id="66a81-163">Service Fabric ofrece un punto de entrada de configuración de comunicación opcional para servicios que atienden las solicitudes de cliente.</span><span class="sxs-lookup"><span data-stu-id="66a81-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="66a81-164">Tanto RunAsync como el punto de entrada de comunicación son reemplazos opcionales en los servicios de Service Fabric. El servicio puede elegir entre solo atender a las solicitudes de cliente o solo ejecutar un bucle de procesamiento o ambas cosas, razón por la cual se permite al método RunAsync salir sin necesidad de reiniciar la instancia de servicio, ya que puede continuar atendiendo a las solicitudes de cliente.</span><span class="sxs-lookup"><span data-stu-id="66a81-164">Both the RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose to only listen to client requests, or only run a processing loop, or both - which is why the RunAsync method is allowed to exit without restarting the service instance, because it may continue to listen for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="66a81-165">API de la aplicación y entorno</span><span class="sxs-lookup"><span data-stu-id="66a81-165">Application API and environment</span></span>
<span data-ttu-id="66a81-166">La API del entorno de Servicios en la nube proporciona información y funcionalidad para la instancia de máquina virtual actual, así como información acerca de otras instancias de rol de VM.</span><span class="sxs-lookup"><span data-stu-id="66a81-166">The Cloud Services environment API provides information and functionality for the current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="66a81-167">Service Fabric proporciona información relacionada con su tiempo de ejecución y algo de información sobre el nodo en el que un servicio se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="66a81-167">Service Fabric provides information related to its runtime and some information about the node a service is currently running on.</span></span> 

| <span data-ttu-id="66a81-168">**Tarea del entorno**</span><span class="sxs-lookup"><span data-stu-id="66a81-168">**Environment Task**</span></span> | <span data-ttu-id="66a81-169">**Servicios en la nube**</span><span class="sxs-lookup"><span data-stu-id="66a81-169">**Cloud Services**</span></span> | <span data-ttu-id="66a81-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="66a81-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="66a81-171">Valores de configuración y notificación de cambios</span><span class="sxs-lookup"><span data-stu-id="66a81-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="66a81-172">Almacenamiento local</span><span class="sxs-lookup"><span data-stu-id="66a81-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="66a81-173">Información de punto de conexión</span><span class="sxs-lookup"><span data-stu-id="66a81-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="66a81-174">Instancia actual: `RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="66a81-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="66a81-175">Otros roles e instancia: `RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="66a81-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="66a81-176">`NodeContext` para la dirección del nodo actual</span><span class="sxs-lookup"><span data-stu-id="66a81-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="66a81-177">`FabricClient` y `ServicePartitionResolver` para la detección de punto de conexión de servicio</span><span class="sxs-lookup"><span data-stu-id="66a81-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="66a81-178">Emulación de entorno</span><span class="sxs-lookup"><span data-stu-id="66a81-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="66a81-179">N/D</span><span class="sxs-lookup"><span data-stu-id="66a81-179">N/A</span></span> |
| <span data-ttu-id="66a81-180">Evento de cambio simultáneo</span><span class="sxs-lookup"><span data-stu-id="66a81-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="66a81-181">N/D</span><span class="sxs-lookup"><span data-stu-id="66a81-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="66a81-182">Valores de configuración</span><span class="sxs-lookup"><span data-stu-id="66a81-182">Configuration settings</span></span>
<span data-ttu-id="66a81-183">Los valores de configuración de los Servicios en la nube se establecen para un rol de VM y se aplican a todas las instancias de ese rol de VM.</span><span class="sxs-lookup"><span data-stu-id="66a81-183">Configuration settings in Cloud Services are set for a VM role and apply to all instances of that VM role.</span></span> <span data-ttu-id="66a81-184">Estos valores son pares de clave-valor establecidos en los archivos Serviceconfiguration.*.cscfg a los que se puede acceder directamente a través de RoleEnvironment.</span><span class="sxs-lookup"><span data-stu-id="66a81-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="66a81-185">En Service Fabric, la configuración se aplica individualmente a cada servicio y a cada aplicación, en lugar de a una máquina virtual, ya que una máquina virtual puede hospedar varios servicios y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="66a81-185">In Service Fabric, settings apply individually to each service and to each application, rather than to a VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="66a81-186">Un servicio se compone de tres paquetes:</span><span class="sxs-lookup"><span data-stu-id="66a81-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="66a81-187">**Código:** contiene los archivos ejecutables de servicio, los archivos binarios, los archivos DLL y cualquier otro archivo necesario para que se ejecute un servicio.</span><span class="sxs-lookup"><span data-stu-id="66a81-187">**Code:** contains the service executables, binaries, DLLs, and any other files a service needs to run.</span></span>
* <span data-ttu-id="66a81-188">**Config:** todos los valores y archivos de configuración de un servicio.</span><span class="sxs-lookup"><span data-stu-id="66a81-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="66a81-189">**Datos:** los archivos de datos estáticos asociados al servicio.</span><span class="sxs-lookup"><span data-stu-id="66a81-189">**Data:** static data files associated with the service.</span></span>

<span data-ttu-id="66a81-190">Cada uno de estos paquetes puede tener versiones y actualizaciones independientes.</span><span class="sxs-lookup"><span data-stu-id="66a81-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="66a81-191">De forma similar a los Servicios en la nube, se puede acceder a un paquete de configuración mediante programación a través de una API y los eventos están disponibles para notificar al servicio de un cambio del paquete de configuración.</span><span class="sxs-lookup"><span data-stu-id="66a81-191">Similar to Cloud Services, a config package can be accessed programmatically through an API and events are available to notify the service of a config package change.</span></span> <span data-ttu-id="66a81-192">Se puede utilizar un archivo Settings.xml para la configuración de los pares clave-valor y el acceso mediante programación similar a la sección de configuración de aplicaciones de un archivo App.config.</span><span class="sxs-lookup"><span data-stu-id="66a81-192">A Settings.xml file can be used for key-value configuration and programmatic access similar to the app settings section of an App.config file.</span></span> <span data-ttu-id="66a81-193">Sin embargo, a diferencia de los Servicios en la nube, un paquete de configuración de Service Fabric puede contener todos los archivos de configuración en cualquier formato, ya sea en XML, JSON, YAML o en un formato binario personalizado.</span><span class="sxs-lookup"><span data-stu-id="66a81-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="66a81-194">Acceso a la configuración</span><span class="sxs-lookup"><span data-stu-id="66a81-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="66a81-195">Servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="66a81-195">Cloud Services</span></span>
<span data-ttu-id="66a81-196">Se puede acceder a los valores de configuración de Serviceconfiguration.*.cscfg a través de `RoleEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="66a81-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="66a81-197">Estas opciones están disponibles globalmente para todas las instancias de rol en la misma implementación del Servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="66a81-197">These settings are globally available to all role instances in the same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="66a81-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="66a81-198">Service Fabric</span></span>
<span data-ttu-id="66a81-199">Cada servicio tiene su propio paquete de configuración individual.</span><span class="sxs-lookup"><span data-stu-id="66a81-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="66a81-200">No hay ningún mecanismo integrado para los valores de configuración global al que puedan acceder todas las aplicaciones de un clúster.</span><span class="sxs-lookup"><span data-stu-id="66a81-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="66a81-201">Cuando utiliza el archivo de configuración especial Settings.xml de Service Fabric dentro de un paquete de configuración, los valores en Settings.xml se pueden reemplazar en el nivel de aplicación lo que permite la configuración en dicho nivel de aplicación.</span><span class="sxs-lookup"><span data-stu-id="66a81-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at the application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="66a81-202">Se puede acceder a los valores de configuración de cada instancia de servicio a través de `CodePackageActivationContext`del servicio.</span><span class="sxs-lookup"><span data-stu-id="66a81-202">Configuration settings are accesses within each service instance through the service's `CodePackageActivationContext`.</span></span>

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a><span data-ttu-id="66a81-203">Eventos de actualización de configuración</span><span class="sxs-lookup"><span data-stu-id="66a81-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="66a81-204">Servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="66a81-204">Cloud Services</span></span>
<span data-ttu-id="66a81-205">El evento `RoleEnvironment.Changed` se utiliza para notificar a todas las instancias de rol cuando se produce un cambio en el entorno, como un cambio de configuración.</span><span class="sxs-lookup"><span data-stu-id="66a81-205">The `RoleEnvironment.Changed` event is used to notify all role instances when a change occurs in the environment, such as a configuration change.</span></span> <span data-ttu-id="66a81-206">Esto se usa para consumir las actualizaciones de configuración sin reciclar las instancias de rol ni reiniciar un proceso de trabajo.</span><span class="sxs-lookup"><span data-stu-id="66a81-206">This is used to consume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get the list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="66a81-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="66a81-207">Service Fabric</span></span>
<span data-ttu-id="66a81-208">Cada uno de los tres tipos de paquete de un servicio, Código, Config y Datos, tienen eventos que notifican a una instancia de servicio cuando se actualiza, agrega o quita un paquete.</span><span class="sxs-lookup"><span data-stu-id="66a81-208">Each of the three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="66a81-209">Un servicio puede contener varios paquetes de cada tipo.</span><span class="sxs-lookup"><span data-stu-id="66a81-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="66a81-210">Por ejemplo, un servicio puede tener varios paquetes de configuración, cada uno individualmente con varias versiones y actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="66a81-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="66a81-211">Estos eventos están disponibles para consumir los cambios en los paquetes de servicio sin necesidad de reiniciar la instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="66a81-211">These events are available to consume changes in service packages without restarting the service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="66a81-212">Tareas de inicio</span><span class="sxs-lookup"><span data-stu-id="66a81-212">Startup tasks</span></span>
<span data-ttu-id="66a81-213">Las tareas de inicio son acciones que se realizan antes de que se inicie una aplicación.</span><span class="sxs-lookup"><span data-stu-id="66a81-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="66a81-214">Una tarea de inicio se utiliza normalmente para ejecutar scripts de configuración con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="66a81-214">A startup task is typically used to run setup scripts using elevated privileges.</span></span> <span data-ttu-id="66a81-215">Tanto Servicios en la nube como Service Fabric admiten tareas de inicio.</span><span class="sxs-lookup"><span data-stu-id="66a81-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="66a81-216">La principal diferencia estriba en que en los Servicios en la nube, una tarea de inicio está asociada a una máquina virtual porque forma parte de una instancia de rol, mientras que en Service Fabric una tarea de inicio se asocia a un servicio que no está asociado a ninguna máquina virtual concreta.</span><span class="sxs-lookup"><span data-stu-id="66a81-216">The main difference is that in Cloud Services, a startup task is tied to a VM because it is part of a role instance, whereas in Service Fabric a startup task is tied to a service, which is not tied to any particular VM.</span></span>

| <span data-ttu-id="66a81-217">Servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="66a81-217">Cloud Services</span></span> | <span data-ttu-id="66a81-218">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="66a81-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="66a81-219">Ubicación de configuración</span><span class="sxs-lookup"><span data-stu-id="66a81-219">Configuration location</span></span> |<span data-ttu-id="66a81-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="66a81-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="66a81-221">Privilegios</span><span class="sxs-lookup"><span data-stu-id="66a81-221">Privileges</span></span> |<span data-ttu-id="66a81-222">"limitados" o "elevados"</span><span class="sxs-lookup"><span data-stu-id="66a81-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="66a81-223">Secuenciación</span><span class="sxs-lookup"><span data-stu-id="66a81-223">Sequencing</span></span> |<span data-ttu-id="66a81-224">"simple", "segundo plano", "primer plano"</span><span class="sxs-lookup"><span data-stu-id="66a81-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="66a81-225">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="66a81-225">Cloud Services</span></span>
<span data-ttu-id="66a81-226">En Servicios en la nube se configura un punto de entrada de inicio por rol en ServiceDefintion.csdef.</span><span class="sxs-lookup"><span data-stu-id="66a81-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a><span data-ttu-id="66a81-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="66a81-227">Service Fabric</span></span>
<span data-ttu-id="66a81-228">En Service Fabric se configura un punto de entrada de inicio por servicio en ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="66a81-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a><span data-ttu-id="66a81-229">Nota acerca de un entorno de desarrollo</span><span class="sxs-lookup"><span data-stu-id="66a81-229">A note about development environment</span></span>
<span data-ttu-id="66a81-230">Los Servicios en la nube y Service Fabric se integran con Visual Studio mediante plantillas de proyecto y soporte para depuración, configuración e implementación tanto local como en Azure.</span><span class="sxs-lookup"><span data-stu-id="66a81-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and to Azure.</span></span> <span data-ttu-id="66a81-231">Los Servicios en la nube y Service Fabric también proporcionan un entorno de desarrollo local en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="66a81-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="66a81-232">La diferencia es que mientras que el tiempo de ejecución de desarrollo del Servicio en la nube emula el entorno de Azure en el que se ejecuta, Service Fabric no utiliza un emulador, sino que usa el tiempo de ejecución de Service Fabric completo.</span><span class="sxs-lookup"><span data-stu-id="66a81-232">The difference is that while the Cloud Service development runtime emulates the Azure environment on which it runs, Service Fabric does not use an emulator - it uses the complete Service Fabric runtime.</span></span> <span data-ttu-id="66a81-233">El entorno de Service Fabric que ejecuta en el equipo de desarrollo local es el mismo entorno que se ejecuta en producción.</span><span class="sxs-lookup"><span data-stu-id="66a81-233">The Service Fabric environment you run on your local development machine is the same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66a81-234">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="66a81-234">Next steps</span></span>
<span data-ttu-id="66a81-235">Conozca más información sobre Reliable Services de Service Fabric y las diferencias fundamentales entre los Servicios en la nube y la arquitectura de la aplicación de Service Fabric para aprender a aprovechar el conjunto completo de características de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="66a81-235">Read more about Service Fabric Reliable Services and the fundamental differences between Cloud Services and Service Fabric application architecture to understand how to take advantage of the full set of Service Fabric features.</span></span>

* [<span data-ttu-id="66a81-236">Introducción a Reliable Services de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="66a81-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="66a81-237">Guía conceptual acerca de las diferencias entre Servicios en la nube y Service Fabric</span><span class="sxs-lookup"><span data-stu-id="66a81-237">Conceptual guide to the differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png

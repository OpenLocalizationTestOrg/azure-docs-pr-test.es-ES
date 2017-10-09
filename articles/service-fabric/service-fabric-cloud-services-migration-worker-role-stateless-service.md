---
title: aaaConvert toomicroservices de aplicaciones de servicios de nube de Azure | Documentos de Microsoft
description: "Esta guía compara Web de servicios de nube y Roles de trabajo y Service Fabric servicios sin estado toohelp migran desde servicios en la nube tooService tejido."
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
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a><span data-ttu-id="2693b-103">Guía de tooconverting servicios Web y Roles de trabajo tooService tejido sin estado</span><span class="sxs-lookup"><span data-stu-id="2693b-103">Guide tooconverting Web and Worker Roles tooService Fabric stateless services</span></span>
<span data-ttu-id="2693b-104">Este artículo se describe cómo toomigrate los Roles de trabajador y Web de servicios de nube tooService tejido servicios sin estado.</span><span class="sxs-lookup"><span data-stu-id="2693b-104">This article describes how toomigrate your Cloud Services Web and Worker Roles tooService Fabric stateless services.</span></span> <span data-ttu-id="2693b-105">Se trata de ruta de migración más sencilla de hello de servicios en la nube tooService tejido para aplicaciones cuya arquitectura global va aproximadamente toostay Hola igual.</span><span class="sxs-lookup"><span data-stu-id="2693b-105">This is hello simplest migration path from Cloud Services tooService Fabric for applications whose overall architecture is going toostay roughly hello same.</span></span>

## <a name="cloud-service-project-tooservice-fabric-application-project"></a><span data-ttu-id="2693b-106">Proyecto de aplicación de tejido de tooService de proyecto de servicio de nube</span><span class="sxs-lookup"><span data-stu-id="2693b-106">Cloud Service project tooService Fabric application project</span></span>
 <span data-ttu-id="2693b-107">Un proyecto de servicio de nube y un proyecto de aplicación de tejido de servicio tienen una estructura similar y ambos unidad de implementación de hello representan para su aplicación, es decir, cada uno de ellos definen el paquete completo de Hola que es toorun implementado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2693b-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent hello deployment unit for your application - that is, they each define hello complete package that is deployed toorun your application.</span></span> <span data-ttu-id="2693b-108">Un proyecto de Servicio en la nube contiene uno o varios roles web o de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2693b-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="2693b-109">De igual forma, un proyecto de la aplicación de Service Fabric contiene uno o más servicios.</span><span class="sxs-lookup"><span data-stu-id="2693b-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="2693b-110">diferencia de Hello es que parejas de proyecto de servicio de nube de Hola Hola implementación de aplicación con una implementación de máquina virtual y, por tanto, contiene valores de configuración de máquina virtual, mientras que el proyecto de aplicación de servicio Fabric Hola solo define una aplicación que se va a implementar tooa el conjunto de máquinas virtuales existentes en un clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2693b-110">hello difference is that hello Cloud Service project couples hello application deployment with a VM deployment and thus contains VM configuration settings in it, whereas hello Service Fabric Application project only defines an application that will be deployed tooa set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="2693b-111">propio clúster de Service Fabric Hola solo se implementa una vez, ya sea a través de una plantilla de administrador de recursos o a través del portal de Azure de Hola y varias aplicaciones pueden ser de Service Fabric implementan tooit.</span><span class="sxs-lookup"><span data-stu-id="2693b-111">hello Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through hello Azure portal, and multiple Service Fabric applications can be deployed tooit.</span></span>

![Comparación de proyectos de Service Fabric y de Servicios en la nube][3]

## <a name="worker-role-toostateless-service"></a><span data-ttu-id="2693b-113">Servicio de toostateless de rol de trabajo</span><span class="sxs-lookup"><span data-stu-id="2693b-113">Worker Role toostateless service</span></span>
<span data-ttu-id="2693b-114">Conceptualmente, un rol de trabajo representa una carga de trabajo sin estado, lo que significa que todas las instancias de la carga de trabajo de hello es idéntica y las solicitudes pueden tener tooany enrutado instancia en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="2693b-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of hello workload is identical and requests can be routed tooany instance at any time.</span></span> <span data-ttu-id="2693b-115">Cada instancia no es solicitud anterior de hello tooremember esperado.</span><span class="sxs-lookup"><span data-stu-id="2693b-115">Each instance is not expected tooremember hello previous request.</span></span> <span data-ttu-id="2693b-116">Estado esa carga de trabajo de hello funciona en está administrado por un almacén de estado externo, como almacenamiento de tablas de Azure o base de datos de documentos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2693b-116">State that hello workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="2693b-117">En Service Fabric, este tipo de carga de trabajo se representa mediante un servicio sin estado.</span><span class="sxs-lookup"><span data-stu-id="2693b-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="2693b-118">Hola más simple enfoque toomigrating un tooService de rol de trabajo tejido puede realizarse mediante la conversión de código de rol de trabajo tooa servicio sin estado.</span><span class="sxs-lookup"><span data-stu-id="2693b-118">hello simplest approach toomigrating a Worker Role tooService Fabric can be done by converting Worker Role code tooa Stateless Service.</span></span>

![Rol de trabajo tooStateless servicio][4]

## <a name="web-role-toostateless-service"></a><span data-ttu-id="2693b-120">Servicio de rol toostateless Web</span><span class="sxs-lookup"><span data-stu-id="2693b-120">Web Role toostateless service</span></span>
<span data-ttu-id="2693b-121">TooWorker similar rol, un rol Web también representa una carga de trabajo sin estado y así conceptualmente demasiado puede ser asignado tooa servicio sin estado de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2693b-121">Similar tooWorker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped tooa Service Fabric stateless service.</span></span> <span data-ttu-id="2693b-122">Sin embargo, a diferencia de los roles web, Service Fabric no admite IIS.</span><span class="sxs-lookup"><span data-stu-id="2693b-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="2693b-123">toomigrate una aplicación web desde un servicio sin estado de rol Web tooa requiere primer marco web tooa móvil que puede ser hospeda a sí mismo y no depende de IIS o System.Web, por ejemplo, ASP.NET Core 1.</span><span class="sxs-lookup"><span data-stu-id="2693b-123">toomigrate a web application from a Web Role tooa stateless service requires first moving tooa web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="2693b-124">**Aplicación**</span><span class="sxs-lookup"><span data-stu-id="2693b-124">**Application**</span></span> | <span data-ttu-id="2693b-125">**Compatible**</span><span class="sxs-lookup"><span data-stu-id="2693b-125">**Supported**</span></span> | <span data-ttu-id="2693b-126">**Ruta de migración**</span><span class="sxs-lookup"><span data-stu-id="2693b-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2693b-127">Formularios Web Forms ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2693b-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="2693b-128">No</span><span class="sxs-lookup"><span data-stu-id="2693b-128">No</span></span> |<span data-ttu-id="2693b-129">Convertir tooASP.NET principales 1 MVC</span><span class="sxs-lookup"><span data-stu-id="2693b-129">Convert tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="2693b-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="2693b-130">ASP.NET MVC</span></span> |<span data-ttu-id="2693b-131">Con migración</span><span class="sxs-lookup"><span data-stu-id="2693b-131">With Migration</span></span> |<span data-ttu-id="2693b-132">Actualización tooASP.NET principales 1 MVC</span><span class="sxs-lookup"><span data-stu-id="2693b-132">Upgrade tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="2693b-133">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="2693b-133">ASP.NET Web API</span></span> |<span data-ttu-id="2693b-134">Con migración</span><span class="sxs-lookup"><span data-stu-id="2693b-134">With Migration</span></span> |<span data-ttu-id="2693b-135">Uso de servidor autohospedado o ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="2693b-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="2693b-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="2693b-136">ASP.NET Core 1</span></span> |<span data-ttu-id="2693b-137">Sí</span><span class="sxs-lookup"><span data-stu-id="2693b-137">Yes</span></span> |<span data-ttu-id="2693b-138">N/D</span><span class="sxs-lookup"><span data-stu-id="2693b-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="2693b-139">API de punto de entrada y ciclo de vida</span><span class="sxs-lookup"><span data-stu-id="2693b-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="2693b-140">Las API de rol de trabajo y las de los servicios de Service Fabric ofrecen puntos de entrada similares:</span><span class="sxs-lookup"><span data-stu-id="2693b-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="2693b-141">**Punto de entrada**</span><span class="sxs-lookup"><span data-stu-id="2693b-141">**Entry Point**</span></span> | <span data-ttu-id="2693b-142">**Rol de trabajo**</span><span class="sxs-lookup"><span data-stu-id="2693b-142">**Worker Role**</span></span> | <span data-ttu-id="2693b-143">**Servicio de Service Fabric.**</span><span class="sxs-lookup"><span data-stu-id="2693b-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2693b-144">Processing</span><span class="sxs-lookup"><span data-stu-id="2693b-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="2693b-145">Inicio de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2693b-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="2693b-146">N/D</span><span class="sxs-lookup"><span data-stu-id="2693b-146">N/A</span></span> |
| <span data-ttu-id="2693b-147">Detención de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2693b-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="2693b-148">N/D</span><span class="sxs-lookup"><span data-stu-id="2693b-148">N/A</span></span> |
| <span data-ttu-id="2693b-149">Apertura del agente de escucha para las solicitudes de cliente</span><span class="sxs-lookup"><span data-stu-id="2693b-149">Open listener for client requests</span></span> |<span data-ttu-id="2693b-150">N/D</span><span class="sxs-lookup"><span data-stu-id="2693b-150">N/A</span></span> |<ul><li> <span data-ttu-id="2693b-151">`CreateServiceInstanceListener()` para sin estado</span><span class="sxs-lookup"><span data-stu-id="2693b-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="2693b-152">`CreateServiceReplicaListener()` para con estado</span><span class="sxs-lookup"><span data-stu-id="2693b-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="2693b-153">Rol de trabajo</span><span class="sxs-lookup"><span data-stu-id="2693b-153">Worker Role</span></span>
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

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="2693b-154">Servicio sin estado de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2693b-154">Service Fabric Stateless Service</span></span>
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

<span data-ttu-id="2693b-155">Ambos tienen un reemplazo principal "ejecutar" procesamiento que toobegin.</span><span class="sxs-lookup"><span data-stu-id="2693b-155">Both have a primary "Run" override in which toobegin processing.</span></span> <span data-ttu-id="2693b-156">Los servicios de Service Fabric combinan `Run`, `Start`, y `Stop` en un único punto de entrada, `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="2693b-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="2693b-157">El servicio debe empezar a trabajar cuando `RunAsync` se inicia y debe dejar de funcionar cuando hello `RunAsync` se señaliza CancellationToken del método.</span><span class="sxs-lookup"><span data-stu-id="2693b-157">Your service should begin working when `RunAsync` starts, and should stop working when hello `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="2693b-158">Hay varias diferencias claves entre el ciclo de vida de Hola y duración de los servicios de Roles de trabajo y el tejido de servicio:</span><span class="sxs-lookup"><span data-stu-id="2693b-158">There are several key differences between hello lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="2693b-159">**Ciclo de vida:** diferencia estriba hello es que un rol de trabajo es una máquina virtual y por lo que su ciclo de vida relacionado toohello máquina virtual, que incluye eventos para cuando se inicia y detiene Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2693b-159">**Lifecycle:** hello biggest difference is that a Worker Role is a VM and so its lifecycle is tied toohello VM, which includes events for when hello VM starts and stops.</span></span> <span data-ttu-id="2693b-160">Un servicio de Service Fabric tiene un ciclo de vida que es independiente de ciclo de vida VM de hello, por lo que no incluye eventos para cuando Hola host VM o equipo se inicia y se detenga, tal y como no están relacionadas.</span><span class="sxs-lookup"><span data-stu-id="2693b-160">A Service Fabric service has a lifecycle that is separate from hello VM lifecycle, so it does not include events for when hello host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="2693b-161">**Duración:** se reciclará una instancia de rol de trabajo si hello `Run` sale del método.</span><span class="sxs-lookup"><span data-stu-id="2693b-161">**Lifetime:** A Worker Role instance will recycle if hello `Run` method exits.</span></span> <span data-ttu-id="2693b-162">Hola `RunAsync` método en un servicio de Service Fabric. sin embargo puede ejecutar toocompletion e instancia del servicio Hola estarán activos.</span><span class="sxs-lookup"><span data-stu-id="2693b-162">hello `RunAsync` method in a Service Fabric service however can run toocompletion and hello service instance will stay up.</span></span> 

<span data-ttu-id="2693b-163">Service Fabric ofrece un punto de entrada de configuración de comunicación opcional para servicios que atienden las solicitudes de cliente.</span><span class="sxs-lookup"><span data-stu-id="2693b-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="2693b-164">Hola Coredispatcher y punto de entrada de comunicación son reemplazos opcionales en servicios de Service Fabric - el servicio puede elegir tooonly solicitudes de tooclient de escucha, o solo ejecutar un bucle de procesamiento, o ambos - motivo por el cual hello Coredispatcher método se permite tooexit sin reiniciar la instancia de servicio de hello, ya que puede seguir toolisten para las solicitudes de cliente.</span><span class="sxs-lookup"><span data-stu-id="2693b-164">Both hello RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose tooonly listen tooclient requests, or only run a processing loop, or both - which is why hello RunAsync method is allowed tooexit without restarting hello service instance, because it may continue toolisten for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="2693b-165">API de la aplicación y entorno</span><span class="sxs-lookup"><span data-stu-id="2693b-165">Application API and environment</span></span>
<span data-ttu-id="2693b-166">entorno de servicios en la nube de Hello API proporciona información y funcionalidad para la instancia actual de VM de hello, así como información acerca de otras instancias de rol de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2693b-166">hello Cloud Services environment API provides information and functionality for hello current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="2693b-167">Service Fabric proporciona información relacionada con el tiempo de ejecución de tooits y alguna información sobre el nodo de hello un servicio se está ejecutando actualmente.</span><span class="sxs-lookup"><span data-stu-id="2693b-167">Service Fabric provides information related tooits runtime and some information about hello node a service is currently running on.</span></span> 

| <span data-ttu-id="2693b-168">**Tarea del entorno**</span><span class="sxs-lookup"><span data-stu-id="2693b-168">**Environment Task**</span></span> | <span data-ttu-id="2693b-169">**Servicios en la nube**</span><span class="sxs-lookup"><span data-stu-id="2693b-169">**Cloud Services**</span></span> | <span data-ttu-id="2693b-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="2693b-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2693b-171">Valores de configuración y notificación de cambios</span><span class="sxs-lookup"><span data-stu-id="2693b-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="2693b-172">Almacenamiento local</span><span class="sxs-lookup"><span data-stu-id="2693b-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="2693b-173">Información de punto de conexión</span><span class="sxs-lookup"><span data-stu-id="2693b-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="2693b-174">Instancia actual: `RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="2693b-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="2693b-175">Otros roles e instancia: `RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="2693b-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="2693b-176">`NodeContext` para la dirección del nodo actual</span><span class="sxs-lookup"><span data-stu-id="2693b-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="2693b-177">`FabricClient` y `ServicePartitionResolver` para la detección de punto de conexión de servicio</span><span class="sxs-lookup"><span data-stu-id="2693b-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="2693b-178">Emulación de entorno</span><span class="sxs-lookup"><span data-stu-id="2693b-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="2693b-179">N/D</span><span class="sxs-lookup"><span data-stu-id="2693b-179">N/A</span></span> |
| <span data-ttu-id="2693b-180">Evento de cambio simultáneo</span><span class="sxs-lookup"><span data-stu-id="2693b-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="2693b-181">N/D</span><span class="sxs-lookup"><span data-stu-id="2693b-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="2693b-182">Valores de configuración</span><span class="sxs-lookup"><span data-stu-id="2693b-182">Configuration settings</span></span>
<span data-ttu-id="2693b-183">Valores de configuración de servicios en la nube se establecen para un rol de VM y aplican tooall instancias de ese rol de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2693b-183">Configuration settings in Cloud Services are set for a VM role and apply tooall instances of that VM role.</span></span> <span data-ttu-id="2693b-184">Estos valores son pares de clave-valor establecidos en los archivos Serviceconfiguration.*.cscfg a los que se puede acceder directamente a través de RoleEnvironment.</span><span class="sxs-lookup"><span data-stu-id="2693b-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="2693b-185">En Service Fabric, configuración se aplica individualmente tooeach servicio y aplicación tooeach, en lugar de tooa de máquina virtual, ya que una máquina virtual puede hospedar varios servicios y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2693b-185">In Service Fabric, settings apply individually tooeach service and tooeach application, rather than tooa VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="2693b-186">Un servicio se compone de tres paquetes:</span><span class="sxs-lookup"><span data-stu-id="2693b-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="2693b-187">**Código:** contiene Hola ejecutables del servicio, los archivos binarios, archivos DLL y cualquier otro archivo de un servicio necesita toorun.</span><span class="sxs-lookup"><span data-stu-id="2693b-187">**Code:** contains hello service executables, binaries, DLLs, and any other files a service needs toorun.</span></span>
* <span data-ttu-id="2693b-188">**Config:** todos los valores y archivos de configuración de un servicio.</span><span class="sxs-lookup"><span data-stu-id="2693b-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="2693b-189">**Datos:** archivos de datos estáticos asociados con el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2693b-189">**Data:** static data files associated with hello service.</span></span>

<span data-ttu-id="2693b-190">Cada uno de estos paquetes puede tener versiones y actualizaciones independientes.</span><span class="sxs-lookup"><span data-stu-id="2693b-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="2693b-191">Servicios de tooCloud similares, un paquete de configuración pueden obtenerse mediante programación a través de una API y eventos se servicio de hello toonotify disponibles de un cambio de paquete de configuración.</span><span class="sxs-lookup"><span data-stu-id="2693b-191">Similar tooCloud Services, a config package can be accessed programmatically through an API and events are available toonotify hello service of a config package change.</span></span> <span data-ttu-id="2693b-192">Un archivo Settings.xml puede utilizarse para la configuración de valores de clave y acceso mediante programación similar toohello aplicación sección Configuración de un archivo App.config.</span><span class="sxs-lookup"><span data-stu-id="2693b-192">A Settings.xml file can be used for key-value configuration and programmatic access similar toohello app settings section of an App.config file.</span></span> <span data-ttu-id="2693b-193">Sin embargo, a diferencia de los Servicios en la nube, un paquete de configuración de Service Fabric puede contener todos los archivos de configuración en cualquier formato, ya sea en XML, JSON, YAML o en un formato binario personalizado.</span><span class="sxs-lookup"><span data-stu-id="2693b-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="2693b-194">Acceso a la configuración</span><span class="sxs-lookup"><span data-stu-id="2693b-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="2693b-195">Servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="2693b-195">Cloud Services</span></span>
<span data-ttu-id="2693b-196">Se puede acceder a los valores de configuración de Serviceconfiguration.*.cscfg a través de `RoleEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="2693b-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="2693b-197">Estas opciones están disponibles globalmente tooall instancias de rol en hello misma implementación del servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="2693b-197">These settings are globally available tooall role instances in hello same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="2693b-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2693b-198">Service Fabric</span></span>
<span data-ttu-id="2693b-199">Cada servicio tiene su propio paquete de configuración individual.</span><span class="sxs-lookup"><span data-stu-id="2693b-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="2693b-200">No hay ningún mecanismo integrado para los valores de configuración global al que puedan acceder todas las aplicaciones de un clúster.</span><span class="sxs-lookup"><span data-stu-id="2693b-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="2693b-201">Al usar archivo de configuración de Settings.xml especial del tejido de servicio dentro de un paquete de configuración, se pueden sobrescribir valores en Settings.xml a nivel de aplicación Hola, lo que permite valores de configuración de nivel de aplicación.</span><span class="sxs-lookup"><span data-stu-id="2693b-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at hello application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="2693b-202">Valores de configuración son accesos dentro de cada instancia de servicio a través del servicio de hello `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="2693b-202">Configuration settings are accesses within each service instance through hello service's `CodePackageActivationContext`.</span></span>

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

### <a name="configuration-update-events"></a><span data-ttu-id="2693b-203">Eventos de actualización de configuración</span><span class="sxs-lookup"><span data-stu-id="2693b-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="2693b-204">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="2693b-204">Cloud Services</span></span>
<span data-ttu-id="2693b-205">Hola `RoleEnvironment.Changed` evento es utilizado toonotify todas las instancias de rol cuando un cambio se produce en el entorno de hello, por ejemplo, un cambio de configuración.</span><span class="sxs-lookup"><span data-stu-id="2693b-205">hello `RoleEnvironment.Changed` event is used toonotify all role instances when a change occurs in hello environment, such as a configuration change.</span></span> <span data-ttu-id="2693b-206">Se trata de las actualizaciones de configuración de tooconsume usado sin reciclado de instancias de rol o reiniciar un proceso de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2693b-206">This is used tooconsume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="2693b-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2693b-207">Service Fabric</span></span>
<span data-ttu-id="2693b-208">Cada uno de los tres tipos de paquete hello en un servicio en código, configuración y datos - tienen eventos que notificar a una instancia de servicio cuando se actualiza, se agrega o se quita un paquete.</span><span class="sxs-lookup"><span data-stu-id="2693b-208">Each of hello three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="2693b-209">Un servicio puede contener varios paquetes de cada tipo.</span><span class="sxs-lookup"><span data-stu-id="2693b-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="2693b-210">Por ejemplo, un servicio puede tener varios paquetes de configuración, cada uno individualmente con varias versiones y actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="2693b-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="2693b-211">Estos eventos son cambios de tooconsume disponibles en los paquetes de servicio sin necesidad de reiniciar la instancia de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2693b-211">These events are available tooconsume changes in service packages without restarting hello service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="2693b-212">Tareas de inicio</span><span class="sxs-lookup"><span data-stu-id="2693b-212">Startup tasks</span></span>
<span data-ttu-id="2693b-213">Las tareas de inicio son acciones que se realizan antes de que se inicie una aplicación.</span><span class="sxs-lookup"><span data-stu-id="2693b-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="2693b-214">Una tarea de inicio es toorun normalmente se usan scripts de instalación con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="2693b-214">A startup task is typically used toorun setup scripts using elevated privileges.</span></span> <span data-ttu-id="2693b-215">Tanto Servicios en la nube como Service Fabric admiten tareas de inicio.</span><span class="sxs-lookup"><span data-stu-id="2693b-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="2693b-216">Hola principal diferencia es que en servicios en la nube, una tarea de inicio es tooa ligada VM porque forma parte de una instancia de rol, mientras que en Service Fabric una tarea de inicio es servicio de tooa relacionados, que no está ligada tooany máquina virtual concreta.</span><span class="sxs-lookup"><span data-stu-id="2693b-216">hello main difference is that in Cloud Services, a startup task is tied tooa VM because it is part of a role instance, whereas in Service Fabric a startup task is tied tooa service, which is not tied tooany particular VM.</span></span>

| <span data-ttu-id="2693b-217">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="2693b-217">Cloud Services</span></span> | <span data-ttu-id="2693b-218">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2693b-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2693b-219">Ubicación de configuración</span><span class="sxs-lookup"><span data-stu-id="2693b-219">Configuration location</span></span> |<span data-ttu-id="2693b-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="2693b-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="2693b-221">Privilegios</span><span class="sxs-lookup"><span data-stu-id="2693b-221">Privileges</span></span> |<span data-ttu-id="2693b-222">"limitados" o "elevados"</span><span class="sxs-lookup"><span data-stu-id="2693b-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="2693b-223">Secuenciación</span><span class="sxs-lookup"><span data-stu-id="2693b-223">Sequencing</span></span> |<span data-ttu-id="2693b-224">"simple", "segundo plano", "primer plano"</span><span class="sxs-lookup"><span data-stu-id="2693b-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="2693b-225">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="2693b-225">Cloud Services</span></span>
<span data-ttu-id="2693b-226">En Servicios en la nube se configura un punto de entrada de inicio por rol en ServiceDefintion.csdef.</span><span class="sxs-lookup"><span data-stu-id="2693b-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

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

### <a name="service-fabric"></a><span data-ttu-id="2693b-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2693b-227">Service Fabric</span></span>
<span data-ttu-id="2693b-228">En Service Fabric se configura un punto de entrada de inicio por servicio en ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="2693b-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

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

## <a name="a-note-about-development-environment"></a><span data-ttu-id="2693b-229">Nota acerca de un entorno de desarrollo</span><span class="sxs-lookup"><span data-stu-id="2693b-229">A note about development environment</span></span>
<span data-ttu-id="2693b-230">Servicios en la nube y tejido de servicio se integran con Visual Studio con plantillas de proyecto y la compatibilidad con la depuración, configurar e implementar ambos localmente y tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2693b-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and tooAzure.</span></span> <span data-ttu-id="2693b-231">Los Servicios en la nube y Service Fabric también proporcionan un entorno de desarrollo local en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="2693b-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="2693b-232">Hello diferencia es que mientras el servicio de nube en tiempo de ejecución de desarrollo emula Hola Hola entorno de Azure en el que se ejecuta, Service Fabric no usa un emulador, sino que usa el tiempo de ejecución de hello completo Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2693b-232">hello difference is that while hello Cloud Service development runtime emulates hello Azure environment on which it runs, Service Fabric does not use an emulator - it uses hello complete Service Fabric runtime.</span></span> <span data-ttu-id="2693b-233">Hello Service Fabric es de entorno que se ejecuta en el equipo de desarrollo local Hola mismo entorno que se ejecuta en producción.</span><span class="sxs-lookup"><span data-stu-id="2693b-233">hello Service Fabric environment you run on your local development machine is hello same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2693b-234">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2693b-234">Next steps</span></span>
<span data-ttu-id="2693b-235">Leer más sobre servicios confiables de tejido de servicio y las diferencias fundamentales de hello entre servicios en la nube y toounderstand de arquitectura de aplicación de Service Fabric cómo tootake aprovechar Hola completo conjunto de características de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2693b-235">Read more about Service Fabric Reliable Services and hello fundamental differences between Cloud Services and Service Fabric application architecture toounderstand how tootake advantage of hello full set of Service Fabric features.</span></span>

* [<span data-ttu-id="2693b-236">Introducción a Reliable Services de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2693b-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="2693b-237">Diferencias de toohello guía conceptual entre servicios en la nube y el tejido de servicio</span><span class="sxs-lookup"><span data-stu-id="2693b-237">Conceptual guide toohello differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png

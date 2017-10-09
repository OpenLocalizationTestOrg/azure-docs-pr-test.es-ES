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
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a>Guía de tooconverting servicios Web y Roles de trabajo tooService tejido sin estado
Este artículo se describe cómo toomigrate los Roles de trabajador y Web de servicios de nube tooService tejido servicios sin estado. Se trata de ruta de migración más sencilla de hello de servicios en la nube tooService tejido para aplicaciones cuya arquitectura global va aproximadamente toostay Hola igual.

## <a name="cloud-service-project-tooservice-fabric-application-project"></a>Proyecto de aplicación de tejido de tooService de proyecto de servicio de nube
 Un proyecto de servicio de nube y un proyecto de aplicación de tejido de servicio tienen una estructura similar y ambos unidad de implementación de hello representan para su aplicación, es decir, cada uno de ellos definen el paquete completo de Hola que es toorun implementado la aplicación. Un proyecto de Servicio en la nube contiene uno o varios roles web o de trabajo. De igual forma, un proyecto de la aplicación de Service Fabric contiene uno o más servicios. 

diferencia de Hello es que parejas de proyecto de servicio de nube de Hola Hola implementación de aplicación con una implementación de máquina virtual y, por tanto, contiene valores de configuración de máquina virtual, mientras que el proyecto de aplicación de servicio Fabric Hola solo define una aplicación que se va a implementar tooa el conjunto de máquinas virtuales existentes en un clúster de Service Fabric. propio clúster de Service Fabric Hola solo se implementa una vez, ya sea a través de una plantilla de administrador de recursos o a través del portal de Azure de Hola y varias aplicaciones pueden ser de Service Fabric implementan tooit.

![Comparación de proyectos de Service Fabric y de Servicios en la nube][3]

## <a name="worker-role-toostateless-service"></a>Servicio de toostateless de rol de trabajo
Conceptualmente, un rol de trabajo representa una carga de trabajo sin estado, lo que significa que todas las instancias de la carga de trabajo de hello es idéntica y las solicitudes pueden tener tooany enrutado instancia en cualquier momento. Cada instancia no es solicitud anterior de hello tooremember esperado. Estado esa carga de trabajo de hello funciona en está administrado por un almacén de estado externo, como almacenamiento de tablas de Azure o base de datos de documentos de Azure. En Service Fabric, este tipo de carga de trabajo se representa mediante un servicio sin estado. Hola más simple enfoque toomigrating un tooService de rol de trabajo tejido puede realizarse mediante la conversión de código de rol de trabajo tooa servicio sin estado.

![Rol de trabajo tooStateless servicio][4]

## <a name="web-role-toostateless-service"></a>Servicio de rol toostateless Web
TooWorker similar rol, un rol Web también representa una carga de trabajo sin estado y así conceptualmente demasiado puede ser asignado tooa servicio sin estado de Service Fabric. Sin embargo, a diferencia de los roles web, Service Fabric no admite IIS. toomigrate una aplicación web desde un servicio sin estado de rol Web tooa requiere primer marco web tooa móvil que puede ser hospeda a sí mismo y no depende de IIS o System.Web, por ejemplo, ASP.NET Core 1.

| **Aplicación** | **Compatible** | **Ruta de migración** |
| --- | --- | --- |
| Formularios Web Forms ASP.NET |No |Convertir tooASP.NET principales 1 MVC |
| ASP.NET MVC |Con migración |Actualización tooASP.NET principales 1 MVC |
| ASP.NET Web API |Con migración |Uso de servidor autohospedado o ASP.NET Core 1 |
| ASP.NET Core 1 |Sí |N/D |

## <a name="entry-point-api-and-lifecycle"></a>API de punto de entrada y ciclo de vida
Las API de rol de trabajo y las de los servicios de Service Fabric ofrecen puntos de entrada similares: 

| **Punto de entrada** | **Rol de trabajo** | **Servicio de Service Fabric.** |
| --- | --- | --- |
| Processing |`Run()` |`RunAsync()` |
| Inicio de máquina virtual |`OnStart()` |N/D |
| Detención de máquina virtual |`OnStop()` |N/D |
| Apertura del agente de escucha para las solicitudes de cliente |N/D |<ul><li> `CreateServiceInstanceListener()` para sin estado</li><li>`CreateServiceReplicaListener()` para con estado</li></ul> |

### <a name="worker-role"></a>Rol de trabajo
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

### <a name="service-fabric-stateless-service"></a>Servicio sin estado de Service Fabric
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

Ambos tienen un reemplazo principal "ejecutar" procesamiento que toobegin. Los servicios de Service Fabric combinan `Run`, `Start`, y `Stop` en un único punto de entrada, `RunAsync`. El servicio debe empezar a trabajar cuando `RunAsync` se inicia y debe dejar de funcionar cuando hello `RunAsync` se señaliza CancellationToken del método. 

Hay varias diferencias claves entre el ciclo de vida de Hola y duración de los servicios de Roles de trabajo y el tejido de servicio:

* **Ciclo de vida:** diferencia estriba hello es que un rol de trabajo es una máquina virtual y por lo que su ciclo de vida relacionado toohello máquina virtual, que incluye eventos para cuando se inicia y detiene Hola máquina virtual. Un servicio de Service Fabric tiene un ciclo de vida que es independiente de ciclo de vida VM de hello, por lo que no incluye eventos para cuando Hola host VM o equipo se inicia y se detenga, tal y como no están relacionadas.
* **Duración:** se reciclará una instancia de rol de trabajo si hello `Run` sale del método. Hola `RunAsync` método en un servicio de Service Fabric. sin embargo puede ejecutar toocompletion e instancia del servicio Hola estarán activos. 

Service Fabric ofrece un punto de entrada de configuración de comunicación opcional para servicios que atienden las solicitudes de cliente. Hola Coredispatcher y punto de entrada de comunicación son reemplazos opcionales en servicios de Service Fabric - el servicio puede elegir tooonly solicitudes de tooclient de escucha, o solo ejecutar un bucle de procesamiento, o ambos - motivo por el cual hello Coredispatcher método se permite tooexit sin reiniciar la instancia de servicio de hello, ya que puede seguir toolisten para las solicitudes de cliente.

## <a name="application-api-and-environment"></a>API de la aplicación y entorno
entorno de servicios en la nube de Hello API proporciona información y funcionalidad para la instancia actual de VM de hello, así como información acerca de otras instancias de rol de máquina virtual. Service Fabric proporciona información relacionada con el tiempo de ejecución de tooits y alguna información sobre el nodo de hello un servicio se está ejecutando actualmente. 

| **Tarea del entorno** | **Servicios en la nube** | **Service Fabric** |
| --- | --- | --- |
| Valores de configuración y notificación de cambios |`RoleEnvironment` |`CodePackageActivationContext` |
| Almacenamiento local |`RoleEnvironment` |`CodePackageActivationContext` |
| Información de punto de conexión |`RoleInstance` <ul><li>Instancia actual: `RoleEnvironment.CurrentRoleInstance`</li><li>Otros roles e instancia: `RoleEnvironment.Roles`</li> |<ul><li>`NodeContext` para la dirección del nodo actual</li><li>`FabricClient` y `ServicePartitionResolver` para la detección de punto de conexión de servicio</li> |
| Emulación de entorno |`RoleEnvironment.IsEmulated` |N/D |
| Evento de cambio simultáneo |`RoleEnvironment` |N/D |

## <a name="configuration-settings"></a>Valores de configuración
Valores de configuración de servicios en la nube se establecen para un rol de VM y aplican tooall instancias de ese rol de máquina virtual. Estos valores son pares de clave-valor establecidos en los archivos Serviceconfiguration.*.cscfg a los que se puede acceder directamente a través de RoleEnvironment. En Service Fabric, configuración se aplica individualmente tooeach servicio y aplicación tooeach, en lugar de tooa de máquina virtual, ya que una máquina virtual puede hospedar varios servicios y aplicaciones. Un servicio se compone de tres paquetes:

* **Código:** contiene Hola ejecutables del servicio, los archivos binarios, archivos DLL y cualquier otro archivo de un servicio necesita toorun.
* **Config:** todos los valores y archivos de configuración de un servicio.
* **Datos:** archivos de datos estáticos asociados con el servicio de Hola.

Cada uno de estos paquetes puede tener versiones y actualizaciones independientes. Servicios de tooCloud similares, un paquete de configuración pueden obtenerse mediante programación a través de una API y eventos se servicio de hello toonotify disponibles de un cambio de paquete de configuración. Un archivo Settings.xml puede utilizarse para la configuración de valores de clave y acceso mediante programación similar toohello aplicación sección Configuración de un archivo App.config. Sin embargo, a diferencia de los Servicios en la nube, un paquete de configuración de Service Fabric puede contener todos los archivos de configuración en cualquier formato, ya sea en XML, JSON, YAML o en un formato binario personalizado. 

### <a name="accessing-configuration"></a>Acceso a la configuración
#### <a name="cloud-services"></a>Servicios en la nube
Se puede acceder a los valores de configuración de Serviceconfiguration.*.cscfg a través de `RoleEnvironment`. Estas opciones están disponibles globalmente tooall instancias de rol en hello misma implementación del servicio de nube.

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a>Service Fabric
Cada servicio tiene su propio paquete de configuración individual. No hay ningún mecanismo integrado para los valores de configuración global al que puedan acceder todas las aplicaciones de un clúster. Al usar archivo de configuración de Settings.xml especial del tejido de servicio dentro de un paquete de configuración, se pueden sobrescribir valores en Settings.xml a nivel de aplicación Hola, lo que permite valores de configuración de nivel de aplicación.

Valores de configuración son accesos dentro de cada instancia de servicio a través del servicio de hello `CodePackageActivationContext`.

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

### <a name="configuration-update-events"></a>Eventos de actualización de configuración
#### <a name="cloud-services"></a>Cloud Services
Hola `RoleEnvironment.Changed` evento es utilizado toonotify todas las instancias de rol cuando un cambio se produce en el entorno de hello, por ejemplo, un cambio de configuración. Se trata de las actualizaciones de configuración de tooconsume usado sin reciclado de instancias de rol o reiniciar un proceso de trabajo.

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

#### <a name="service-fabric"></a>Service Fabric
Cada uno de los tres tipos de paquete hello en un servicio en código, configuración y datos - tienen eventos que notificar a una instancia de servicio cuando se actualiza, se agrega o se quita un paquete. Un servicio puede contener varios paquetes de cada tipo. Por ejemplo, un servicio puede tener varios paquetes de configuración, cada uno individualmente con varias versiones y actualizaciones. 

Estos eventos son cambios de tooconsume disponibles en los paquetes de servicio sin necesidad de reiniciar la instancia de servicio de Hola.

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a>Tareas de inicio
Las tareas de inicio son acciones que se realizan antes de que se inicie una aplicación. Una tarea de inicio es toorun normalmente se usan scripts de instalación con privilegios elevados. Tanto Servicios en la nube como Service Fabric admiten tareas de inicio. Hola principal diferencia es que en servicios en la nube, una tarea de inicio es tooa ligada VM porque forma parte de una instancia de rol, mientras que en Service Fabric una tarea de inicio es servicio de tooa relacionados, que no está ligada tooany máquina virtual concreta.

| Cloud Services | Service Fabric |
| --- | --- | --- |
| Ubicación de configuración |ServiceDefinition.csdef |
| Privilegios |"limitados" o "elevados" |
| Secuenciación |"simple", "segundo plano", "primer plano" |

### <a name="cloud-services"></a>Cloud Services
En Servicios en la nube se configura un punto de entrada de inicio por rol en ServiceDefintion.csdef. 

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

### <a name="service-fabric"></a>Service Fabric
En Service Fabric se configura un punto de entrada de inicio por servicio en ServiceManifest.xml:

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

## <a name="a-note-about-development-environment"></a>Nota acerca de un entorno de desarrollo
Servicios en la nube y tejido de servicio se integran con Visual Studio con plantillas de proyecto y la compatibilidad con la depuración, configurar e implementar ambos localmente y tooAzure. Los Servicios en la nube y Service Fabric también proporcionan un entorno de desarrollo local en tiempo de ejecución. Hello diferencia es que mientras el servicio de nube en tiempo de ejecución de desarrollo emula Hola Hola entorno de Azure en el que se ejecuta, Service Fabric no usa un emulador, sino que usa el tiempo de ejecución de hello completo Service Fabric. Hello Service Fabric es de entorno que se ejecuta en el equipo de desarrollo local Hola mismo entorno que se ejecuta en producción.

## <a name="next-steps"></a>Pasos siguientes
Leer más sobre servicios confiables de tejido de servicio y las diferencias fundamentales de hello entre servicios en la nube y toounderstand de arquitectura de aplicación de Service Fabric cómo tootake aprovechar Hola completo conjunto de características de Service Fabric.

* [Introducción a Reliable Services de Service Fabric](service-fabric-reliable-services-quick-start.md)
* [Diferencias de toohello guía conceptual entre servicios en la nube y el tejido de servicio](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png

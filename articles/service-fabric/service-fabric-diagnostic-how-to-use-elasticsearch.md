---
title: "Uso de Elasticsearch como almacén de seguimientos de aplicaciones de Service Fabric | Microsoft Docs"
description: "Describe cómo las aplicaciones de Service Fabric pueden usar ElasticSearch y Kibana para el almacenamiento, la indexación y la búsqueda de seguimientos de aplicaciones."
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: adegeo
editor: 
ms.assetid: e59b0c39-e468-4d9e-b453-d5f2a8ad20d8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: karolz@microsoft.com
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: 2d2ceceea131b41ad1a1735aaa2a859d035ab098
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-elasticsearch-as-a-service-fabric-application-trace-store"></a>Uso de ElasticSearch como almacén de seguimientos de aplicaciones de Service Fabric
## <a name="introduction"></a>Introducción
En este artículo se describe cómo las aplicaciones de [Azure Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric/) pueden usar **ElasticSearch** y **Kibana** para el almacenamiento, la indexación y la búsqueda de seguimientos de aplicaciones. [ElasticSearch](https://www.elastic.co/guide/index.html) es un motor de búsqueda y análisis de código abierto, distribuido, escalable y en tiempo real que resulta adecuado para esta tarea. Se puede instalar en máquinas virtuales de Windows o Linux que se ejecutan en Microsoft Azure. Elasticsearch puede procesar de forma eficiente seguimientos *estructurados* producidos con tecnologías como **Seguimiento de eventos para Windows (ETW)**.

El tiempo de ejecución de Service Fabric usa ETW para producir información de diagnóstico (seguimientos). También es el método recomendado para que las aplicaciones de Service Fabric produzcan su información de diagnóstico. El uso del mismo mecanismo permite correlacionar los seguimientos proporcionados por el sistema en tiempo de ejecución y los suministrados por la aplicación, y facilita la solución de problemas. Las plantillas de proyecto de Service Fabric en Visual Studio incluyen una API de registro (basada en la clase **EventSource** de .NET) que emite seguimientos de ETW de forma predeterminada. Para una descripción general del seguimiento de aplicaciones de Service Fabric mediante ETW, consulte [Supervisión y diagnóstico de servicios en una configuración de desarrollo de máquina local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

Para que los seguimientos aparezcan en ElasticSearch, deben capturarse en los nodos de clúster de Service Fabric en tiempo real (mientras se ejecuta la aplicación) y enviarse al punto de conexión de ElasticSearch. Hay dos opciones principales para la captura de seguimientos:

* **Captura de seguimientos en proceso**  
  La aplicación o, más concretamente, el proceso de servicio es responsable de enviar los datos de diagnóstico al almacén de seguimientos (ElasticSearch).
* **Captura de seguimientos fuera de proceso**  
  Un agente independiente captura los seguimientos de los procesos del servicio y los envía al almacén de seguimientos.

En el resto del artículo se describe cómo configurar ElasticSearch en Azure, se analizan los pros y los contras de ambas opciones de captura y se explica cómo configurar un servicio de Service Fabric para enviar datos a ElasticSearch.

## <a name="set-up-elasticsearch-on-azure"></a>Configuración de ElasticSearch en Azure
La manera más sencilla de configurar el servicio ElasticSearch en Azure es mediante las [**plantillas de Azure Resource Manager**](../azure-resource-manager/resource-group-overview.md). Hay disponible una [plantilla del Administrador de recursos de Azure de inicio rápido para ElasticSearch](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) en el repositorio de plantillas de inicio rápido de Azure. Esta plantilla usa cuentas de almacenamiento independiente para unidades de escalado (grupos de nodos). También puede aprovisionar nodos de cliente y de servidor independientes con distintas configuraciones y varios números de discos de datos adjuntos.

Aquí, se usa otra plantilla, llamada **ES-MultiNode** , del [repositorio de herramientas de diagnóstico de Azure](https://github.com/Azure/azure-diagnostics-tools). Esta plantilla es más fácil de usar y crea un clúster de Elasticsearch protegido mediante autenticación HTTP básica. Antes de continuar, descargue el repositorio de GitHub en su equipo (ya sea mediante la clonación de dicho repositorio o la descarga de un archivo ZIP). La plantilla ES-MultiNode se encuentra en la carpeta con el mismo nombre.

### <a name="prepare-a-machine-to-run-elasticsearch-installation-scripts"></a>Preparación de una máquina para ejecutar scripts de instalación de ElasticSearch
La manera más fácil de usar la plantilla ES-MultiNode es mediante un script de Azure PowerShell llamado `CreateElasticSearchCluster`. Para usar este script, debe instalar módulos de PowerShell y una herramienta llamada **openssl**. Esta es necesaria para crear una clave SSH que se puede usar para administrar el clúster de ElasticSearch de forma remota.

`CreateElasticSearchCluster` está diseñado para facilitar su uso con la plantilla ES-MultiNode en una máquina con Windows. Se puede usar la plantilla en una máquina que no sea de Windows, pero ese escenario queda fuera del ámbito de este artículo.

1. Si aún no lo hizo, instale los [**módulos de Azure PowerShell**](http://aka.ms/webpi-azps). Cuando se le pida, haga clic en **Ejecutar** y, después, en **Instalar**. Se requiere Azure PowerShell 1.3 o posterior.
2. La herramienta **openssl** se incluye en la distribución de [**Git para Windows**](http://www.git-scm.com/downloads). Si aún no lo hizo, instale [Git para Windows](http://www.git-scm.com/downloads) ahora. (las opciones de instalación predeterminadas son adecuadas).
3. Si Git está instalado pero no está incluido en la ruta de acceso del sistema, abra la ventana de Microsoft Azure PowerShell y ejecute los siguientes comandos:
   
    ```powershell
    $ENV:PATH += ";<Git installation folder>\usr\bin"
    $ENV:OPENSSL_CONF = "<Git installation folder>\usr\ssl\openssl.cnf"
    ```
   
    Reemplace `<Git installation folder>` por la ubicación de Git en su equipo; el valor predeterminado es **"C:\Archivos de programa\Git"**. No olvide el carácter de punto y coma al principio de la primera ruta de acceso.
4. Asegúrese de iniciar sesión en Azure (mediante el cmdlet [`Add-AzureRmAccount`](https://msdn.microsoft.com/library/mt619267.aspx) ) y de seleccionar la suscripción que se debe usar para crear el clúster de Elasticsearch. Puede comprobar que se ha seleccionado la suscripción correcta utilizando los cmdlets `Get-AzureRmContext` y `Get-AzureRmSubscription`.
5. Si aún no lo hizo, cambie el directorio actual a la carpeta ES-MultiNode.

### <a name="run-the-createelasticsearchcluster-script"></a>Ejecución del script CreateElasticSearchCluster
Antes de ejecutar el script, abra el archivo `azuredeploy-parameters.json` y compruebe o indique los valores de los parámetros del script. Se proporcionan los parámetros siguientes:

| Nombre de parámetro | Description |
| --- | --- |
| dnsNameForLoadBalancerIP |El nombre que se usa para crear el nombre DNS públicamente visible del clúster de Elasticsearch (anexando el dominio de la región de Azure al nombre proporcionado). Por ejemplo, si el valor de este parámetro es "myBigCluster" y la región de Azure elegida corresponde al oeste de EE. UU., el nombre DNS resultante del clúster será myBigCluster.westus.cloudapp.azure.com. <br /><br />Este nombre también sirve como raíz para los nombres de numerosos artefactos asociados con el clúster de Elasticsearch, como los nombres de nodos de datos. |
| adminUsername |Nombre de la cuenta de administrador para administrar el clúster de Elasticsearch (las claves SSH correspondientes se generan automáticamente). |
| dataNodeCount |Número de nodos del clúster de Elastic Search. La versión actual del script no distingue entre los nodos de datos y de consulta: todos los nodos representan ambos roles. El valor predeterminado son 3 nodos. |
| dataDiskSize |El tamaño de los discos de datos (en GB) que se va a asignar a cada nodo de datos. Cada nodo recibe 4 discos de datos dedicados exclusivamente al servicio Elasticsearch. |
| region |Nombre de la región de Azure donde se debe ubicar el clúster de Elastic Search. |
| esUserName |El nombre del usuario que se configura para acceder al clúster ES (de acuerdo con la autenticación HTTP básica). La contraseña no forma parte del archivo de parámetros y debe proporcionarse cuando se invoca el script `CreateElasticSearchCluster` . |
| vmSizeDataNodes |Tamaño de la máquina virtual de Azure para nodos de clúster de Elastic Search. El valor predeterminado es Standard_D2. |

Ya está preparado para ejecutar el script. Ejecute el siguiente comando:

```powershell
CreateElasticSearchCluster -ResourceGroupName <es-group-name> -Region <azure-region> -EsPassword <es-password>
```

donde 

| Nombre del parámetro de script | Description |
| --- | --- |
| `<es-group-name>` |El nombre del grupo de recursos de Azure que contendrá todos los recursos del clúster de Elasticsearch. |
| `<azure-region>` |El nombre de la región de Azure en la que se debe crear el clúster de Elasticsearch. |
| `<es-password>` |La contraseña del usuario de Elasticsearch. |

> [!NOTE]
> Si recibe una excepción NullReferenceException del cmdlet Test-AzureResourceGroup, significa que olvidó iniciar sesión en Azure (`Add-AzureRmAccount`).
> 
> 

Si recibe un error de ejecución del script y determina que la causa del error es un valor incorrecto del parámetro de plantilla, corrija el archivo de parámetros y ejecute de nuevo el script con un nombre de grupo de recursos distinto. También puede volver a usar el mismo nombre de grupo de recursos y hacer que el script limpie el antiguo agregando el parámetro `-RemoveExistingResourceGroup` a la invocación del script.

### <a name="result-of-running-the-createelasticsearchcluster-script"></a>Resultado de ejecutar el script CreateElasticSearchCluster
Después de ejecutar el script `CreateElasticSearchCluster`, se crearán los siguientes artefactos principales. En este ejemplo, se asume que ha usado "myBigCluster" como valor del parámetro `dnsNameForLoadBalancerIP` y que la región donde ha creado el clúster es el oeste de EE. UU.

| Artefacto | Nombre, ubicación y comentarios |
| --- | --- |
| Clave SSH para administración remota |Archivo myBigCluster.key (en el directorio desde el que se ejecutó CreateElasticSearchCluster). <br /><br />Este es el archivo de clave que se puede usar para conectar con el nodo de administración y, mediante este último, con los nodos de datos del clúster. |
| Nodo de administración |myBigCluster-admin.westus.cloudapp.azure.com  <br /><br />Una VM dedicada para la administración remota de clústeres de Elasticsearch, la única que permite conexiones SSH externas. Se ejecuta en la misma red virtual que todos los nodos de clúster de Elasticsearch, pero no ejecuta servicios Elasticsearch. |
| Nodos de datos |myBigCluster1 … myBigCluster*N* <br /><br />Nodos de datos que ejecutan servicios Elasticsearch y Kibana. Puede conectarse mediante SSH a cada nodo, pero solo mediante el nodo de administración. |
| Clúster Elasticsearch |http://myBigCluster.westus.cloudapp.azure.com/es/ <br /><br />El punto de conexión principal del clúster de Elasticsearch (observe el sufijo /es). Está protegido por autenticación HTTP básica (las credenciales son los parámetros esUserName/esPassword especificados en la plantilla ES-MultiNode). El clúster tiene también el complemento de encabezado instalado (http://myBigCluster.westus.cloudapp.azure.com/es/_plugin/head) para la administración básica de clústeres. |
| Servicio Kibana |http://myBigCluster.westus.cloudapp.azure.com <br /><br />El servicio Kibana está configurado para mostrar datos del clúster de Elasticsearch creado. Está protegido por las mismas credenciales de autenticación que el propio clúster. |

## <a name="in-process-versus-out-of-process-trace-capturing"></a>Captura de seguimientos en proceso frente a fuera de proceso
En la introducción mencionamos dos formas básicas de recopilar datos de diagnóstico: en proceso y fuera de proceso. Cada una tiene sus ventajas y desventajas.

Las ventajas de la **captura de seguimientos en proceso** son:

1. *Fácil configuración e implementación*
   
   * La configuración de recopilación de datos de diagnóstico es parte de la configuración de la aplicación. Es fácil mantenerla siempre "sincronizada" con el resto de la aplicación.
   * Se puede realizar fácilmente la configuración por aplicación o por servicio.
   * La captura de seguimientos fuera de proceso normalmente requiere una implementación y configuración independientes del agente de diagnóstico, lo que supone una tarea administrativa adicional y una posible fuente de errores. A menudo, la tecnología del agente particular permite solo una instancia del agente por máquina virtual (nodo). Esto significa que la configuración de recopilación de la configuración de diagnóstico se comparte entre todas las aplicaciones y servicios que se ejecutan en ese nodo.
2. *Flexibilidad*
   
   * La aplicación puede enviar los datos dondequiera que deban ir siempre que haya una biblioteca de cliente que admita el sistema de almacenamiento de datos de destino. Se pueden agregar tantos receptores nuevos como se desee.
   * Se pueden implementar reglas complejas de captura, filtrado y agregación de datos.
   * Una captura de seguimientos fuera de proceso a menudo está limitada por los receptores de datos que admite el agente. Algunos agentes se pueden ampliar.
3. *Acceso a los datos y el contexto internos de la aplicación*
   
   * El subsistema de diagnóstico que se ejecuta dentro del proceso de la aplicación o servicio puede ampliar fácilmente los seguimientos con información contextual.
   * En el método fuera de proceso, los datos se deben enviar a un agente mediante algún mecanismo de comunicación entre procesos, como el Seguimiento de eventos para Windows. Este mecanismo podría imponer limitaciones adicionales.

Las ventajas de la **captura de seguimientos fuera de proceso** son:

1. *Capacidad para supervisar la aplicación y recopilar volcados de memoria*
   
   * Se puede producir un error en la captura de seguimientos en proceso si la aplicación no se inicia o se bloquea. Un agente independiente tiene muchas más probabilidades de capturar información crucial de solución de problemas.<br /><br />
2. *Madurez, solidez y rendimiento probado*
   
   * Se sometió a rigurosas pruebas y refuerzos a un agente desarrollado por el proveedor de la plataforma (por ejemplo, el agente de Diagnósticos de Microsoft Azure).
   * Con la captura de seguimientos en proceso, hay que tener cuidado y asegurarse de que la actividad de envío de datos de diagnóstico desde un proceso de aplicación no interfiera con las tareas principales de la aplicación y no presente problemas de rendimiento o de temporización. Un agente que se ejecuta de forma independiente es menos propenso a estos problemas y está específicamente diseñado para limitar su impacto en el sistema.

Por supuesto, es posible combinar y beneficiarse de ambos enfoques; de hecho, puede que sea la mejor solución para muchas aplicaciones.

En este artículo, se usa la **biblioteca Microsoft.Diagnostic.Listeners** y la característica de captura de seguimientos en proceso para enviar datos desde una aplicación de Service Fabric hasta un clúster de Elasticsearch.

## <a name="use-the-listeners-library-to-send-diagnostic-data-to-elasticsearch"></a>Uso de la biblioteca de agentes de escucha para enviar datos de diagnóstico a ElasticSearch
La biblioteca Microsoft.Diagnostic.Listeners forma parte de la aplicación de clúster de Service Fabric de ejemplo. Para usarla:

1. Descargue [el ejemplo de PartyCluster](https://github.com/Azure-Samples/service-fabric-dotnet-management-party-cluster) desde GitHub.
2. Copie los proyectos Microsoft.Diagnostics.Listeners y Microsoft.Diagnostics.Listeners.Fabric (las carpetas completas) desde el directorio del ejemplo de PartyCluster a la carpeta de solución de la aplicación que se supone que debe enviar los datos a ElasticSearch.
3. Abra la solución de destino, haga clic con el botón derecho en el nodo de solución del Explorador de soluciones y elija **Agregar proyecto existente**. Agregue el proyecto Microsoft.Diagnostics.Listeners a la solución. Repita lo mismo para el proyecto Microsoft.Diagnostics.Listeners.Fabric.
4. Agregue una referencia de proyecto desde sus proyectos de servicio a los dos proyectos agregados (cada servicio que debe enviar datos a ElasticSearch deberá hacer referencia a Microsoft.Diagnostics.EventListeners y Microsoft.Diagnostics.EventListeners.Fabric).
   
    ![Referencias de proyecto a las bibliotecas Microsoft.Diagnostics.EventListeners y Microsoft.Diagnostics.EventListeners.Fabric.][1]

### <a name="service-fabric-general-availability-release-and-microsoftdiagnosticstracing-nuget-package"></a>Versión de disponibilidad general de Service Fabric y paquete NuGet Microsoft.Diagnostics.Tracing
Las aplicaciones creadas con la versión de disponibilidad general de Service Fabric (2.0.135, publicada el 31 de marzo de 2016) están destinadas a **.NET Framework 4.5.2**. Se trata de la última versión de .NET Framework compatible con Azure en el momento de publicar la versión de disponibilidad general. Lamentablemente, esta versión de Framework carece de ciertas API de EventListener que la biblioteca Microsoft.Diagnostics.Listeners necesita. Como EventSource (el componente que constituye la base de las API de registro en las aplicaciones de Fabric) y EventListener están estrechamente relacionados, cada proyecto que use la biblioteca Microsoft.Diagnostics.Listeners debe usar una implementación alternativa de EventSource, que la proporciona el **paquete NuGet Microsoft.Diagnostics.Tracing** creado por Microsoft. Este paquete es totalmente compatible con la versión anterior de EventSource incluida en Framework, por lo que no se necesitan cambios en el código salvo los cambios de espacio de nombres indicados.

Para empezar a usar la implementación para Microsoft.Diagnostics.Tracing de la clase EventSource, siga estos pasos para cada proyecto de servicio que necesite enviar datos a ElasticSearch:

1. Haga clic con el botón derecho en el proyecto de servicio y elija **Administrar paquetes NuGet**.
2. Cambie al origen del paquete nuget.org (si no está ya seleccionado) y busque "**Microsoft.Diagnostics.Tracing**".
3. Instale el paquete `Microsoft.Diagnostics.Tracing.EventSource` (y sus dependencias).
4. Abra el archivo **ServiceEventSource.cs** o **ActorEventSource.cs** en el proyecto de servicio y reemplace la directiva `using System.Diagnostics.Tracing` de la parte superior del archivo por la directiva `using Microsoft.Diagnostics.Tracing`.

No habrá que realizar estos pasos cuando **.NET Framework 4.6** sea compatible con Microsoft Azure.

### <a name="elasticsearch-listener-instantiation-and-configuration"></a>Configuración y creación de instancias del agente de escucha de ElasticSearch
El último paso para enviar datos de diagnóstico a Elastic Search es crear una instancia de `ElasticSearchListener` y configurarla con datos de conexión de Elasticsearch. El agente de escucha captura automáticamente todos los eventos generados mediante las clases EventSource definidas en el proyecto de servicio. Debe estar activa durante toda la vida del servicio, por lo que el mejor lugar para crearla es en el código de inicialización del servicio. Este es el aspecto que podría tener el código de inicialización para un servicio sin estado después de los cambios necesarios (las incorporaciones se indican en los comentarios que comienzan con `****`):

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Runtime;

// **** Add the following directives
using Microsoft.Diagnostics.EventListeners;
using Microsoft.Diagnostics.EventListeners.Fabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is the entry point of the service host process.
        /// </summary>        
        private static void Main()
        {
            try
            {
                // **** Instantiate ElasticSearchListener
                var configProvider = new FabricConfigurationProvider("ElasticSearchEventListener");
                ElasticSearchListener esListener = null;
                if (configProvider.HasConfiguration)
                {
                    esListener = new ElasticSearchListener(configProvider, new FabricHealthReporter("ElasticSearchEventListener"));
                }

                // The ServiceManifest.XML file defines one or more service type names.
                // Registering a service maps a service type name to a .NET type.
                // When Service Fabric creates an instance of this service type,
                // an instance of the class is created in this host process.

                ServiceRuntime.RegisterServiceAsync("Stateless1Type", 
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                // Prevents this host process from terminating so services keep running.
                Thread.Sleep(Timeout.Infinite);

                // **** Ensure that the ElasticSearchListner instance is not garbage-collected prematurely
                GC.KeepAlive(esListener);
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e);
                throw;
            }
        }
    }
}
```

Los datos de conexión de Elasticsearch deben colocarse en una sección independiente del archivo de configuración de servicio (**PackageRoot\Config\Settings.xml**). El nombre de la sección debe corresponder con el valor pasado al constructor `FabricConfigurationProvider` , por ejemplo:

```xml
<Section Name="ElasticSearchEventListener">
  <Parameter Name="serviceUri" Value="http://myBigCluster.westus.cloudapp.azure.com/es/" />
  <Parameter Name="userName" Value="(ES user name)" />
  <Parameter Name="password" Value="(ES user password)" />
  <Parameter Name="indexNamePrefix" Value="myapp" />
</Section>
```
Los valores de los parámetros `serviceUri`, `userName` y `password` corresponden a la dirección del punto de conexión de clúster Elasticsearch, al nombre de usuario Elasticsearch y a la contraseña, respectivamente. `indexNamePrefix` es el prefijo de los índices de Elasticsearch; la biblioteca Microsoft.Diagnostics.Listeners crea un nuevo índice para sus datos cada día.

### <a name="verification"></a>Comprobación
Eso es todo. Ahora, cada vez que se ejecute el servicio, empezará a enviar seguimientos al servicio Elasticsearch especificado en la configuración. Puede comprobarlo abriendo la IU de Kibana asociada a la instancia de Elasticsearch de destino. En nuestro ejemplo, la dirección de la página es http://myBigCluster.westus.cloudapp.azure.com/. Compruebe que los índices con el prefijo del nombre elegido para la instancia de `ElasticSearchListener` efectivamente se han creado y rellenado con datos.

![Kibana muestra eventos de aplicación de PartyCluster][2]

## <a name="next-steps"></a>Pasos siguientes
* [Más información sobre cómo diagnosticar y supervisar un servicio Service Fabric](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

<!--Image references-->
[1]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/listener-lib-references.png
[2]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/kibana.png

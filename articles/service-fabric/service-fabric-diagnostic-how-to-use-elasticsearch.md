---
title: "aaaUsing Elasticsearch como un almacén de seguimiento de aplicaciones de Service Fabric | Documentos de Microsoft"
description: "Describe cómo pueden utilizar las aplicaciones de Service Fabric toostore Elasticsearch y Kibana, índice y buscar a través de seguimientos de aplicaciones (registros)"
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
ms.openlocfilehash: b5977c54e69319e3caa376e44a02f971b66a3254
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-elasticsearch-as-a-service-fabric-application-trace-store"></a>Uso de ElasticSearch como almacén de seguimientos de aplicaciones de Service Fabric
## <a name="introduction"></a>Introducción
En este artículo se describe cómo las aplicaciones de [Azure Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric/) pueden usar **ElasticSearch** y **Kibana** para el almacenamiento, la indexación y la búsqueda de seguimientos de aplicaciones. [ElasticSearch](https://www.elastic.co/guide/index.html) es un motor de búsqueda y análisis de código abierto, distribuido, escalable y en tiempo real que resulta adecuado para esta tarea. Se puede instalar en máquinas virtuales de Windows o Linux que se ejecutan en Microsoft Azure. Elasticsearch puede procesar de forma eficiente seguimientos *estructurados* producidos con tecnologías como **Seguimiento de eventos para Windows (ETW)**.

ETW es utilizado por Service Fabric en tiempo de ejecución toosource información de diagnóstico (seguimientos). Es Hola método recomendado para toosource de las aplicaciones de Service Fabric su información de diagnóstico, demasiado. Uso de hello permite el mismo mecanismo para la correlación entre los seguimientos proporcionado por el tiempo de ejecución y proporcionada por la aplicación y hace más fácil solucionar. Plantillas de proyecto de Service Fabric en Visual Studio incluyen una API de registro (en función de hello .NET **EventSource** clase) que emite seguimientos de ETW de forma predeterminada. Para una descripción general del seguimiento de aplicaciones de Service Fabric mediante ETW, consulte [Supervisión y diagnóstico de servicios en una configuración de desarrollo de máquina local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

Para seguimientos de hello tooshow seguridad en Elasticsearch, necesitan toobe capturados en los nodos del clúster de Service Fabric hello en tiempo real (mientras se ejecuta la aplicación hello) y envía el punto de conexión de tooan Elasticsearch. Hay dos opciones principales para la captura de seguimientos:

* **Captura de seguimientos en proceso**  
  aplicación Hello, o más concretamente, el proceso de servicio, es responsable de envío de almacén de seguimiento de toohello de datos de diagnóstico de hello (Elasticsearch).
* **Captura de seguimientos fuera de proceso**  
  Un agente independiente es capturar seguimientos de los procesos de servicio de Hola y enviarlas después a almacén de seguimiento toohello.

A continuación, se describe cómo tratan de tooset seguridad Elasticsearch en Azure, los profesionales de TI de Hola e inconvenientes para las opciones de captura y explican cómo tooconfigure un tejido de servicio service toosend datos tooElasticsearch.

## <a name="set-up-elasticsearch-on-azure"></a>Configuración de ElasticSearch en Azure
Hola tooset de manera más sencillo servicio de Elasticsearch de hello en Azure es a través de [ **plantillas de Azure Resource Manager**](../azure-resource-manager/resource-group-overview.md). Hay disponible una [plantilla del Administrador de recursos de Azure de inicio rápido para ElasticSearch](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) en el repositorio de plantillas de inicio rápido de Azure. Esta plantilla usa cuentas de almacenamiento independiente para unidades de escalado (grupos de nodos). También puede aprovisionar nodos de cliente y de servidor independientes con distintas configuraciones y varios números de discos de datos adjuntos.

En este caso, usamos otra plantilla, llama a **ES multinodo** de hello [repositorio de herramientas de diagnóstico de Azure](https://github.com/Azure/azure-diagnostics-tools). Esta plantilla es más fácil toouse y crea un clúster de Elasticsearch protegido por la autenticación básica HTTP. Antes de continuar, debe descargar repositorio Hola desde el equipo de tooyour de GitHub (de clonación de repositorio de Hola o descargar un archivo zip). plantilla de Hello ES multinodo se encuentra en la carpeta Hola con hello mismo nombre.

### <a name="prepare-a-machine-toorun-elasticsearch-installation-scripts"></a>Preparar una máquina toorun Elasticsearch secuencias de comandos de instalación
Hello más fácil manera toouse hello ES multinodo plantilla es a través de un script de PowerShell de Azure proporcionado denominado `CreateElasticSearchCluster`. toouse este script, necesita tooinstall módulos de PowerShell y una herramienta denominada **openssl**. Hola este último se necesita para crear una clave SSH que puede ser utilizado tooadminister su clúster Elasticsearch remotamente.

`CreateElasticSearchCluster`secuencia de comandos está diseñado para facilitar su uso con plantilla hello ES multinodo desde un equipo Windows. Es posible toouse Hola plantilla en una máquina distinta de Windows, pero esa situación es más allá del ámbito de Hola de este artículo.

1. Si aún no lo hizo, instale los [**módulos de Azure PowerShell**](http://aka.ms/webpi-azps). Cuando se le pida, haga clic en **Ejecutar** y, después, en **Instalar**. Se requiere Azure PowerShell 1.3 o posterior.
2. Hola **openssl** herramienta se incluye en la distribución de Hola de [ **Git para Windows**](http://www.git-scm.com/downloads). Si aún no lo hizo, instale [Git para Windows](http://www.git-scm.com/downloads) ahora. (opciones de instalación predeterminadas de hello son correctos.)
3. Suponiendo que se ha instalado pero no se incluye en la ruta de acceso de sistema de hello Git, abra una ventana de Microsoft Azure PowerShell y ejecute hello siguientes comandos:
   
    ```powershell
    $ENV:PATH += ";<Git installation folder>\usr\bin"
    $ENV:OPENSSL_CONF = "<Git installation folder>\usr\ssl\openssl.cnf"
    ```
   
    Reemplace hello `<Git installation folder>` con la ubicación de Git de hello en el equipo; valor predeterminado de hello es **"C:\Program Files\Git"**. Tenga en cuenta carácter de punto y coma de hello en a partir de la primera ruta de acceso de Hola Hola.
4. Asegúrese de que ha iniciado sesión tooAzure (a través de [ `Add-AzureRmAccount` ](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet) y que ha seleccionado la suscripción de Hola que se debe usa toocreate el clúster de búsqueda elástico. Puede comprobar que se ha seleccionado la suscripción correcta utilizando los cmdlets `Get-AzureRmContext` y `Get-AzureRmSubscription`.
5. Si aún no lo ha hecho lo ha hecho, cambie la carpeta de toohello multinodo ES de directorio actual de Hola.

### <a name="run-hello-createelasticsearchcluster-script"></a>Ejecutar script de Hola CreateElasticSearchCluster
Antes de ejecutar script de Hola, abra hello `azuredeploy-parameters.json` de archivos y comprobar o proporcionar valores para parámetros de script de Hola. se proporciona Hola parámetros siguientes:

| Nombre de parámetro | Description |
| --- | --- |
| dnsNameForLoadBalancerIP |Hola nombre toocreate usado Hola sean visibles públicamente DNS para clúster de búsqueda elástico hello (anexando el nombre de toohello proporcionado de dominio de región de Azure de hello). Por ejemplo, si este valor de parámetro es "myBigCluster" y región de Azure Hola elegido es oeste de Estados Unidos, nombre DNS resultante de hello para el clúster de hello es myBigCluster.westus.cloudapp.azure.com. <br /><br />Este nombre también actúa como un nombre de raíz para muchos artefactos asociados a clúster de búsqueda flexible de hello, como nombres de nodo de datos. |
| adminUsername |nombre de Hola de cuenta de administrador de hello para la administración de clúster de búsqueda elástico hello (claves SSH correspondientes se generan automáticamente). |
| dataNodeCount |número de Hola de nodos de clúster de búsqueda elástico Hola. versión actual de Hola de script de Hola no distingue entre los nodos de datos y la consulta; todos los nodos desempeñan ambos roles. Nodos de too3 los valores predeterminados. |
| dataDiskSize |tamaño de Hola de los discos de datos (en GB) que se asigna a cada nodo de datos. Cada nodo recibe 4 discos de datos, exclusivamente dedicado tooElastic de servicio de búsqueda. |
| region |nombre de Hola de región de Azure donde debe estar ubicado del clúster de búsqueda elástico Hola. |
| esUserName |Hello nombre de usuario del usuario de Hola que esté había configurado toohave acceso tooES clúster (asunto tooHTTP la autenticación básica). Hello contraseña no forma parte del archivo de parámetros y debe proporcionarse al `CreateElasticSearchCluster` script es invocado. |
| vmSizeDataNodes |Hola tamaño de máquina virtual de Azure para nodos de clúster de búsqueda elástico. TooStandard_D2 de valores predeterminados. |

Ahora está listo toorun script de Hola. Emita el siguiente comando de hello:

```powershell
CreateElasticSearchCluster -ResourceGroupName <es-group-name> -Region <azure-region> -EsPassword <es-password>
```

donde 

| Nombre del parámetro de script | Descripción |
| --- | --- |
| `<es-group-name>` |nombre de Hola Hola Azure del grupo de recursos que contendrá todos los recursos de clúster de búsqueda elástico. |
| `<azure-region>` |nombre de Hola de hello región de Azure donde se debe crear el clúster de búsqueda elástico Hola. |
| `<es-password>` |contraseña de Hello para el usuario de búsqueda elástico Hola. |

> [!NOTE]
> Si recibe una excepción NullReferenceException del cmdlet de hello AzureResourceGroup de prueba, ha olvidado toolog en tooAzure (`Add-AzureRmAccount`).
> 
> 

Si se produce un error de ejecución de script de Hola y determina que el error de hello fue causado por un valor de parámetro de plantilla incorrecta, corrija el archivo de parámetros de Hola y vuelva a ejecutar el script de Hola con un nombre de grupo de recursos distinto. También puede volver a usar Hola el mismo nombre de grupo de recursos y tiene un script de Hola Hola antiguo de limpieza mediante la adición de hello `-RemoveExistingResourceGroup` invocación del parámetro toohello secuencia de comandos.

### <a name="result-of-running-hello-createelasticsearchcluster-script"></a>Resultado de la ejecución de secuencias de comandos de hello CreateElasticSearchCluster
Después de ejecutar hello `CreateElasticSearchCluster` secuencia de comandos, se creará Hola siguientes artefactos principales. En este ejemplo se supone que ha usado "myBigCluster" como valor de Hola de hello `dnsNameForLoadBalancerIP` parámetro y esa región Hola donde se ha creado el clúster de hello es oeste de Estados Unidos.

| Artefacto | Nombre, ubicación y comentarios |
| --- | --- |
| Clave SSH para administración remota |archivo de myBigCluster.key (en el directorio de Hola desde qué Hola se ejecutó CreateElasticSearchCluster). <br /><br />Este archivo de clave puede ser el nodo de administración de toohello tooconnect usado y (a través del nodo de administración de hello) toodata nodos de clúster de Hola. |
| Nodo de administración |myBigCluster-admin.westus.cloudapp.azure.com  <br /><br />Una máquina virtual dedicada para la administración remota de clúster Elasticsearch: Hola solo una que permite conexiones externas de SSH. Se ejecuta en hello mismo redes virtuales como todos los nodos del clúster hello Elasticsearch, pero no ejecutar ningún servicio de Elasticsearch. |
| Nodos de datos |myBigCluster1 … myBigCluster*N* <br /><br />Nodos de datos que ejecutan servicios Elasticsearch y Kibana. Puede conectarse a través de SSH tooeach nodo, pero solo a través del nodo de administración de Hola. |
| Clúster Elasticsearch |http://myBigCluster.westus.cloudapp.azure.com/es/ <br /><br />Hola extremo principal de clúster de hello Elasticsearch (sufijo de nota Hola/es). Está protegido por la autenticación básica HTTP (credenciales de hello eran Hola especificado esUserName/esPassword parámetros de plantilla de hello ES multinodo). clúster de Hello también tiene Hola head complemento instalado (http://myBigCluster.westus.cloudapp.azure.com/es/_plugin/head) para la administración de clúster básico. |
| Servicio Kibana |http://myBigCluster.westus.cloudapp.azure.com <br /><br />Hola Kibana servicio se configura tooshow datos de hello creado clúster Elasticsearch. Está protegida por hello mismas credenciales de autenticación Hola propio clúster. |

## <a name="in-process-versus-out-of-process-trace-capturing"></a>Captura de seguimientos en proceso frente a fuera de proceso
En la introducción de hello, mencionamos que dos aspectos fundamentales de recopilar datos de diagnóstico: en proceso y fuera de proceso. Cada una tiene sus ventajas y desventajas.

Ventajas del programa Hola a **capturar el seguimiento en proceso** incluyen:

1. *Fácil configuración e implementación*
   
   * configuración de Hola de recopilación de datos de diagnóstico es parte de la configuración de la aplicación hello. Es mantener tooalways fácil que "sincronizados" con hello resto de la aplicación hello.
   * Se puede realizar fácilmente la configuración por aplicación o por servicio.
   * Capturar el seguimiento de fuera de proceso, normalmente requiere una implementación independiente y la configuración del agente de diagnóstico de hello, que es una tarea administrativa adicional y un origen potencial de errores. tecnología de agente en particular de Hola a menudo permite solo una instancia de agente de Hola por máquina virtual (nodo). Esto significa que la configuración de colección de hello de la configuración de diagnóstico Hola se comparte entre todas las aplicaciones y servicios que se ejecutan en ese nodo.
2. *Flexibilidad*
   
   * aplicación Hello puede enviar datos de hello dondequiera que necesita toogo, siempre que hay una biblioteca de cliente que admite el sistema de almacenamiento de datos de Hola de destino. Se pueden agregar tantos receptores nuevos como se desee.
   * Se pueden implementar reglas complejas de captura, filtrado y agregación de datos.
   * Un seguimiento de fuera de proceso de captura a menudo está limitado por los receptores de datos de Hola que admite el agente de Hola. Algunos agentes se pueden ampliar.
3. *Contexto y obtener acceso a datos de aplicación de toointernal*
   
   * subsistema de diagnóstico de Hello ejecuta en proceso de aplicación o un servicio de hello puede ampliar fácilmente la seguimientos de hello junto con información contextual.
   * En el enfoque de fuera de proceso de hello, Hola se deben enviar datos tooan agente a través de algún mecanismo de comunicación entre procesos, como el seguimiento de eventos para Windows. Este mecanismo podría imponer limitaciones adicionales.

Ventajas del programa Hola a **seguimiento fuera de proceso de captura** incluyen:

1. *Hola capacidad toomonitor Hola aplicación y recopilar volcados de memoria*
   
   * Captura de seguimiento en curso pueden fallar si se produce un error toostart de aplicación hello o se bloquea. Un agente independiente tiene muchas más probabilidades de capturar información crucial de solución de problemas.<br /><br />
2. *Madurez, solidez y rendimiento probado*
   
   * Un agente desarrollado por un proveedor de la plataforma (por ejemplo, un agente de Microsoft Azure Diagnostics) ha estado sujeto toorigorous pruebas y la protección de batalla.
   * Con seguimiento de en proceso de captura, se debe tener cuidado tooensure que actividad hello de enviar los datos de diagnóstico desde un proceso de aplicación no interferir con las tareas principales de la aplicación hello ni presentar problemas de rendimiento o de tiempo. Un agente de ejecución de forma independiente es menos propensas a problemas de toothese y está específicamente diseñado toolimit su impacto en el sistema de Hola.

Es posible toocombine y se benefician de ambos enfoques. De hecho, podría ser mejor solución Hola para muchas aplicaciones.

Aquí usamos hello **Microsoft.Diagnostic.Listeners biblioteca** y seguimiento de hello en curso la captura de datos de toosend desde un clúster de Service Fabric aplicación tooan Elasticsearch.

## <a name="use-hello-listeners-library-toosend-diagnostic-data-tooelasticsearch"></a>Usar Hola agentes de escucha biblioteca toosend datos de diagnóstico tooElasticsearch
biblioteca de Microsoft.Diagnostic.Listeners Hello es parte de la aplicación de Service Fabric de ejemplo PartyCluster. toouse:

1. Descargar [muestra de Hola a PartyCluster](https://github.com/Azure-Samples/service-fabric-dotnet-management-party-cluster) desde GitHub.
2. Copiar hello Microsoft.Diagnostics.Listeners y Microsoft.Diagnostics.Listeners.Fabric proyectos (carpetas enteras) desde carpeta hello PartyCluster ejemplo directory toohello solución de aplicación Hola que se supone toosend Hola datos tooElasticsearch .
3. Abra la solución de destino de Hola, haga clic en el nodo de la solución de Hola Hola el Explorador de soluciones y elija **Agregar proyecto existente**. Agregar hello Microsoft.Diagnostics.Listeners proyecto toohello solución. Repita Hola igual para proyectos de Microsoft.Diagnostics.Listeners.Fabric Hola.
4. Agregar una referencia de proyecto de sus proyectos toohello dos agregado proyectos de servicio. (Cada servicio que se supone toosend datos tooElasticsearch debe hacer referencia a Microsoft.Diagnostics.EventListeners y Microsoft.Diagnostics.EventListeners.Fabric).
   
    ![Proyecto hace referencia a bibliotecas de Microsoft.Diagnostics.EventListeners.Fabric y tooMicrosoft.Diagnostics.EventListeners][1]

### <a name="service-fabric-general-availability-release-and-microsoftdiagnosticstracing-nuget-package"></a>Versión de disponibilidad general de Service Fabric y paquete NuGet Microsoft.Diagnostics.Tracing
Las aplicaciones creadas con la versión de disponibilidad general de Service Fabric (2.0.135, publicada el 31 de marzo de 2016) están destinadas a **.NET Framework 4.5.2**. Esta versión es hello más alto de .NET Framework compatible con Azure en tiempo de Hola de versión de GA Hola Hola. Por desgracia, esta versión de framework Hola carece de ciertas APIs EventListener ese hello Microsoft.Diagnostics.Listeners biblioteca necesita. Porque se acoplan estrechamente EventSource (componente de Hola que constituye Hola base del registro de las API en aplicaciones de tejido de) y EventListener, cada proyecto que utilice la biblioteca de hello Microsoft.Diagnostics.Listeners debe usar una implementación alternativa de EventSource. Esta implementación se proporciona por hello **paquete Microsoft.Diagnostics.Tracing Nuget**, creado por Microsoft. paquete de Hello es totalmente compatible con versiones anteriores con EventSource incluida en framework de hello, por lo que no hay cambios en el código deberían ser necesarios que no sea de cambios de espacio de nombres que se hace referencia.

toostart con hello Microsoft.Diagnostics.Tracing implementación de hello EventSource (clase), siga estos pasos para cada proyecto de servicio que necesita toosend datos tooElasticsearch:

1. Haga doble clic en el proyecto de servicio de Hola y elija **administrar paquetes de Nuget**.
2. Cambiar el origen del paquete toohello nuget.org (si no está ya seleccionada) y busque "**Microsoft.Diagnostics.Tracing**".
3. Instalar hello `Microsoft.Diagnostics.Tracing.EventSource` paquete (y sus dependencias).
4. Abra hello **ServiceEventSource.cs** o **ActorEventSource.cs** un archivo en el proyecto de servicio y reemplace hello `using System.Diagnostics.Tracing` directiva sobre archivo hello con hello `using Microsoft.Diagnostics.Tracing` directiva.

No será necesario realizar estos pasos una vez Hola **.NET Framework 4.6** es compatible con Microsoft Azure.

### <a name="elasticsearch-listener-instantiation-and-configuration"></a>Configuración y creación de instancias del agente de escucha de ElasticSearch
Hello paso final para el envío de datos de diagnóstico tooElasticsearch es toocreate una instancia de `ElasticSearchListener` y configúrelo con datos de la conexión de Elasticsearch. agente de escucha de Hello captura automáticamente todos los eventos provocados a través de las clases de EventSource definidas en el proyecto de servicio de Hola. Debe toobe activo durante la duración de hello del servicio de hello, para hello mejor colocar toocreate se encuentra en el código de inicialización del servicio de Hola. Aquí es el aspecto que podría código de inicialización de Hola para un servicio sin estado después de los cambios necesarios de hello (adiciones que se indican en los comentarios a partir de `****`):

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Runtime;

// **** Add hello following directives
using Microsoft.Diagnostics.EventListeners;
using Microsoft.Diagnostics.EventListeners.Fabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
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

                // hello ServiceManifest.XML file defines one or more service type names.
                // Registering a service maps a service type name tooa .NET type.
                // When Service Fabric creates an instance of this service type,
                // an instance of hello class is created in this host process.

                ServiceRuntime.RegisterServiceAsync("Stateless1Type", 
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                // Prevents this host process from terminating so services keep running.
                Thread.Sleep(Timeout.Infinite);

                // **** Ensure that hello ElasticSearchListner instance is not garbage-collected prematurely
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

Datos de conexión de Elasticsearch deberían colocarse en una sección independiente en el archivo de configuración de servicio de hello (**PackageRoot\Config\Settings.xml**). nombre de Hola de sección Hola debe corresponder valor toohello pasado toohello `FabricConfigurationProvider` constructor, por ejemplo:

```xml
<Section Name="ElasticSearchEventListener">
  <Parameter Name="serviceUri" Value="http://myBigCluster.westus.cloudapp.azure.com/es/" />
  <Parameter Name="userName" Value="(ES user name)" />
  <Parameter Name="password" Value="(ES user password)" />
  <Parameter Name="indexNamePrefix" Value="myapp" />
</Section>
```
Hola valores de `serviceUri`, `userName` y `password` parámetros corresponden a dirección de punto de conexión del clúster de toohello Elasticsearch, Elasticsearch nombre de usuario y contraseña, respectivamente. `indexNamePrefix`es el prefijo de Hola para los índices de Elasticsearch; biblioteca de Hello Microsoft.Diagnostics.Listeners crea un nuevo índice para sus datos diariamente.

### <a name="verification"></a>Comprobación
Eso es todo. Ahora, cada vez que se ejecuta el servicio de hello, iniciar el envío de servicio de seguimientos toohello Elasticsearch especificado en la configuración de Hola. Para comprobarlo, Hola de apertura que kibana UI asociado a la instancia de hello destino Elasticsearch. En nuestro ejemplo, la dirección de la página de hello es http://myBigCluster.westus.cloudapp.azure.com/. Compruebe que los índices con prefijo de nombre de hello elegido para hello `ElasticSearchListener` instancia realmente se han creado y rellenado con datos.

![Kibana muestra eventos de aplicación de PartyCluster][2]

## <a name="next-steps"></a>Pasos siguientes
* [Más información sobre cómo diagnosticar y supervisar un servicio Service Fabric](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

<!--Image references-->
[1]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/listener-lib-references.png
[2]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/kibana.png

---
title: "Agregación de eventos de servicio de Fabric con diagnósticos de Windows Azure aaaAzure | Documentos de Microsoft"
description: "Obtenga información sobre la agregación y la recopilación de eventos con WAD para la supervisión y el diagnóstico de clústeres de Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a>Recopilación y agregación de eventos con Azure Diagnostics de Windows
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Cuando se ejecuta un clúster de Azure Service Fabric, es un buena idea toocollect Hola inicia una sesión de todos los nodos de hello en una ubicación central. Tener registros de hello en una ubicación central le ayuda a analizar y solucionar problemas en el clúster o problemas en aplicaciones de Hola y servicios que se ejecutan en ese clúster.

Tooupload de una forma y recopilar registros es la extensión de diagnósticos de Windows Azure (WAD) de hello toouse, que carga tooAzure almacenamiento de registros pero también tiene Hola opción toosend registros tooAzure Application Insights o concentradores de eventos. También puede usar un proceso externo tooread Hola de eventos de almacenamiento y colocarlos en un producto de plataforma de análisis, como [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) u otra solución de análisis de registro.

## <a name="prerequisites"></a>Requisitos previos
Estas herramientas están tooperform usado alguna de las operaciones de hello en este documento:

* [Diagnósticos de Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (relacionadas con la tooAzure servicios en la nube, pero tiene buena información y ejemplos)
* [Administrador de recursos de Azure](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Cliente de Azure Resource Manager](https://github.com/projectkudu/ARMClient)
* [Plantilla de Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a>Orígenes de eventos y registros

### <a name="service-fabric-platform-events"></a>Eventos de plataforma de Service Fabric
Como se describe en [este artículo](service-fabric-diagnostics-event-generation-infra.md), Service Fabric se configura la con algunos canales de registro remoto, del que Hola siguientes canales fácilmente se configuran con WAD toosend supervisión y diagnóstico tooa almacenamiento tabla de datos o en otros lugares:
  * Los eventos operativos: operaciones de nivel superior que Hola Service Fabric realiza la plataforma. Algunos ejemplos son la creación de aplicaciones y servicios, los cambios de estado de nodo y la información sobre la actualización. Se emiten como registros de Seguimiento de eventos para Windows (ETW).
  * [Eventos del modelo de programación de Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
  * [Eventos del modelo de programación de Reliable Services](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a>Eventos de aplicación
 Eventos emitidos desde las aplicaciones y servicios de código y que se escribe mediante el uso de la clase de aplicación auxiliar de hello EventSource en hello proporcionan plantillas de Visual Studio. Para obtener más información sobre cómo se registra toowrite EventSource desde su aplicación, consulte [Monitor y diagnosticar los servicios en una configuración de desarrollo de equipo local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Implementar la extensión de diagnósticos de Hola
Hola primer paso en la recopilación de registros es toodeploy extensión de diagnósticos de hello en cada una de las máquinas virtuales de hello en clúster de Service Fabric Hola. extensión de diagnósticos de Hello recopila registros en cada máquina virtual y los carga toohello cuenta de almacenamiento que especifique. pasos de Hello varían ligeramente en función de si utiliza Hola portal de Azure o Azure Resource Manager. pasos de Hello también varían en función de si implementación hello es parte de la creación de clúster o de un clúster que ya existe. Echemos un vistazo a los pasos de Hola para cada escenario.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a>Implementar la extensión de diagnósticos de hello como parte de la creación del clúster a través del portal de Azure
toodeploy Hola diagnósticos extensión toohello máquinas virtuales en clúster de hello como parte de la creación del clúster, usa panel de configuración de diagnósticos de Hola se muestra en el siguiente de saludo de la imagen: asegúrese de que los diagnósticos está establecido demasiado**en** (Hola la configuración predeterminada) . Después de crear el clúster de hello, no se puede cambiar esta configuración mediante el portal de Hola.

![Configuración de diagnóstico de Azure en el portal de hello para la creación de clúster](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

Al crear un clúster mediante el portal de hello, recomendamos encarecidamente que descargue la plantilla de hello **antes de hacer clic en Aceptar** clúster de hello toocreate. Para obtener más información, consulte demasiado[configurar un clúster de Service Fabric mediante una plantilla de Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Necesitará toomake cambios de la plantilla de hello más tarde, debido a que no puede realizar algunos cambios mediante el portal de Hola.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Implementar la extensión de diagnósticos de hello como parte de la creación del clúster mediante el Administrador de recursos de Azure
toocreate un clúster mediante el Administrador de recursos, necesita hello tooadd diagnósticos JSON configuración toohello el Administrador de recursos completo del clúster plantilla antes de crear el clúster de Hola. Proporcionamos una plantilla de administrador de recursos de clúster de cinco VM de ejemplo con la configuración de diagnóstico agrega tooit como parte de nuestros ejemplos de la plantilla de administrador de recursos. Puede ver en esta ubicación en la Galería de ejemplos de Azure hello: [clúster de cinco nodos con el ejemplo de la plantilla de administrador de recursos de diagnóstico](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).

configuración de diagnósticos de hello toosee en plantilla de administrador de recursos de hello, archivo de azuredeploy.json de hello abierto y busque **IaaSDiagnostics**. un clúster con esta plantilla, seleccione hello toocreate **implementar tooAzure** botón está disponible en el vínculo anterior de Hola.

Como alternativa, puede descargar el ejemplo de Hola a Administrador de recursos, realizar cambios tooit y crear un clúster con la plantilla modificada hello mediante Hola `New-AzureRmResourceGroupDeployment` comando en una ventana de PowerShell de Azure. Vea Hola siguiente código para los parámetros de Hola que se pasan en el comando toohello. Para obtener información detallada sobre cómo toodeploy un recurso de grupo mediante el uso de PowerShell, vea el artículo de hello [implementar un grupo de recursos con la plantilla de Azure Resource Manager hello](../azure-resource-manager/resource-group-template-deploy.md).

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a>Implementar el clúster existente de hello diagnósticos extensión tooan
Si tiene un clúster existente que no tiene implementado de diagnóstico, o si desea toomodify una configuración existente, puede agregar o actualizar. Modificar plantilla de administrador de recursos de Hola que es usado toocreate Hola existente clúster o descargar plantilla de Hola desde el portal de hello, tal como se describió anteriormente. Modificar el archivo de template.json de hello realizando Hola siguiente las tareas.

Agregar una nueva plantilla de toohello de recursos de almacenamiento mediante la adición de la sección de recursos toohello.

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 A continuación, agregue parámetros toohello sección justo después de las definiciones de la cuenta de almacenamiento de hello, entre `supportLogStorageAccountName` y `vmNodeType0Name`. Reemplace el texto de marcador de posición de hello *aquí el nombre de cuenta de almacenamiento* con el nombre de Hola de cuenta de almacenamiento de Hola.

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
A continuación, actualice hello `VirtualMachineProfile` sección del archivo de template.json Hola agregando Hola siguiente código dentro de la matriz de extensiones de Hola. Ser seguro tooadd una coma al principio de Hola o al final de hello, según donde se inserta.

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

Después de modificar el archivo de hello template.json tal como se describe, volver a publicar la plantilla de administrador de recursos de Hola. Si se ha exportado la plantilla de hello, archivo de ejecución hello deploy.ps1 vuelve a publicar plantilla Hola. Después de realizar la implementación, asegúrese de que el estado **ProvisioningState** sea **Correcto**.

## <a name="collect-health-and-load-events"></a>Recopilar eventos de mantenimiento y carga

A partir de hello 5.4 versión de Service Fabric, eventos de métrica de mantenimiento y carga están disponibles para la colección. Estos eventos reflejan los eventos generados por el sistema de hello o tu código mediante el uso de mantenimiento de Hola o cargue las API de generación de informes como [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) o [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Esto permite agregar y ver el estado de mantenimiento del sistema en el tiempo, y generar alertas basadas en eventos de estado de mantenimiento o carga. tooview agregan estos eventos en el Visor de eventos de diagnóstico de Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000008" toohello lista de proveedores de ETW.

eventos de hello toocollect, modificar tooinclude de plantilla del Administrador de recursos de Hola

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="collect-reverse-proxy-events"></a>Recopilación de eventos de proxy inverso

A partir de hello 5.7 versión de Service Fabric, [proxy inverso](service-fabric-reverseproxy.md) eventos están disponibles para la colección.
Proxy inverso emite eventos en dos canales, un error que contiene eventos reflejar errores de procesamiento de solicitud y otros uno que contiene eventos detallados de todas las solicitudes de hello procesadas en el proxy inverso Hola Hola. 

1. Recopilar eventos de error: tooview agregan estos eventos en el Visor de eventos de diagnóstico de Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000010" toohello lista de proveedores de ETW.
eventos de hello toocollect de clústeres de Azure, modifique tooinclude de plantilla del Administrador de recursos de Hola

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. Recopilar todos los eventos de procesamiento de solicitud: Visor de eventos de diagnóstico de en Visual Studio, en la entrada de hello Microsoft ServiceFabric actualización Hola lista de proveedores ETW demasiado "Microsoft-ServiceFabric:4:0x4000000000000020".
Para los clústeres de Azure Service Fabric, modificar tooinclude de plantilla de administrador de recursos de Hola

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> Se recomienda toojudiciously habilitar recopilación de eventos de este canal ya que recopila todo el tráfico a través de proxy inverso de Hola y puede consumir rápidamente la capacidad de almacenamiento.

Para los clústeres de Azure Service Fabric, eventos de Hola desde todos los nodos de Hola se recopilan y agregan en hello SystemEventTable.
Para obtener la solución de problemas de eventos de proxy inverso de hello, consulte hello [Guía de diagnóstico de proxy inverso](service-fabric-reverse-proxy-diagnostics.md).

## <a name="collect-from-new-eventsource-channels"></a>Recopilar desde canales EventSource nuevos

registros de toocollect tooupdate diagnósticos de nuevos canales EventSource que representan una nueva aplicación que le sobre toodeploy, realizar Hola mismos pasos descritos anteriormente para la instalación de Hola de diagnósticos para un clúster existente.

Actualizar hello `EtwEventSourceProviderConfiguration` sección entradas del archivo de hello template.json tooadd para actualización con Hola Hola EventSource canales nuevos antes de aplicar la configuración de hello `New-AzureRmResourceGroupDeployment` comando de PowerShell. nombre de Hola Hola del origen de evento se define como parte de su código en un archivo generado por Visual Studio ServiceEventSource.cs Hola.

Por ejemplo, si el origen de eventos se denomina Mis Eventsource, agregar Hola siguientes eventos de código tooplace Hola de mi Eventsource en una tabla denominada MyDestinationTableName.

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

contadores de rendimiento de toocollect o registros de eventos, modificar plantilla de administrador de recursos de hello mediante ejemplos de hello en [crear una máquina virtual de Windows con la supervisión y el diagnóstico mediante una plantilla de Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). A continuación, volver a publicar plantilla del Administrador de recursos de Hola.

## <a name="collect-performance-counters"></a>Recopilar contadores de rendimiento

las métricas de rendimiento de toocollect desde el clúster, agregue tooyour de contadores de rendimiento de Hola "WadCfg > DiagnosticMonitorConfiguration" en la plantilla de administrador de recursos de hello para el clúster. Vea en [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) (Contadores de rendimiento de Service Fabric) los contadores de rendimiento que se recomienda recopilar.

Por ejemplo, aquí se establezca un contador de rendimiento, muestreado cada 15 segundos (Esto se puede cambiar y se indica a continuación Hola formato de "PT\<tiempo >\<unidad >", por ejemplo, PT3M se muestra en intervalos de tres minutos) y transfieren toohello tabla de almacenamiento adecuado cada minuto.

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
Si si está usando un receptor de Application Insights, tal y como se describe en la siguiente sección de Hola y desea que estas métricas tooshow seguridad en Application Insights, asegúrese de nombre de receptor de hello tooadd seguro en hello "receptores" sección como se indicó anteriormente. Además, considere la posibilidad de crear una tabla independiente toosend los contadores de rendimiento, por lo que no sobrecargue out Hola Hola de datos procedentes de otros canales de registro que se ha habilitado.


## <a name="send-logs-tooapplication-insights"></a>Enviar registros de visión tooApplication

Enviar tooApplication de datos de supervisión y diagnóstico de visión (AI) puede realizarse como parte de la configuración de WAD Hola. Si decide toouse AI para visualización y análisis de eventos, leer [análisis de eventos y la visualización con Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset seguridad un receptor de AI como parte de la "WadCfg".

## <a name="next-steps"></a>Pasos siguientes

Una vez que ha configurado correctamente los diagnósticos de Azure, verá los datos de las tablas de almacenamiento de registros de EventSource y Hola ETW. Si elige toouse OMS, Kibana o cualquier otro análisis y visualización de plataforma de datos que no esté configurado directamente en la plantilla de administrador de recursos de hello, asegúrese de tooset seguro de la plataforma de Hola de su elección tooread en los datos de Hola de estas tablas de almacenamiento. Es relativamente fácil hacerlo para OMS, como se explica en [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md) (Análisis de eventos y registro mediante OMS). Application Insights es un poco de un caso especial en este sentido, ya que puede configurarse como parte de la configuración de extensión de diagnósticos de hello, así que haga referencia toohello [artículo apropiado](service-fabric-diagnostics-event-analysis-appinsights.md) si elige toouse AI.

>[!NOTE]
>Actualmente no hay ningún evento de Hola de toofilter o limpiar de forma que se envía toohello tabla. Si no implementan un tooremove procesar los eventos de tabla de hello, tabla de hello seguirá toogrow. Actualmente, hay un ejemplo de un servicio de limpieza de datos ejecuta en hello [ejemplo guardián](https://github.com/Azure-Samples/service-fabric-watchdog-service), y se recomienda escribir uno para sí mismo, a menos que haya una buena razón para que los registros de toostore más allá de un plazo de 30 o 90 días.

* [Obtenga información acerca de cómo toocollect los contadores de rendimiento o de registros mediante el uso de Hola extensión de diagnósticos](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Análisis y visualización de eventos con Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)
* [Análisis y visualización de eventos con OMS](service-fabric-diagnostics-event-analysis-oms.md)
---
title: "registros de aaaCollect con el diagnóstico de Azure | Documentos de Microsoft"
description: "Este artículo describe cómo se registra tooset seguridad toocollect de diagnósticos de Azure desde un clúster de Service Fabric que se ejecuta en Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Recopilación de registros con Diagnósticos de Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Cuando se ejecuta un clúster de Azure Service Fabric, es un buena idea toocollect Hola inicia una sesión de todos los nodos de hello en una ubicación central. Tener registros de hello en una ubicación central le ayuda a analizar y solucionar problemas en el clúster o problemas en aplicaciones de Hola y servicios que se ejecutan en ese clúster.

Tooupload de una forma y recopilar registros es extensión de diagnósticos de Azure hello toouse, qué cargas registra tooAzure centros de eventos de Azure, Azure Application Insights o de almacenamiento. Hola registros no son tan útiles directamente en el almacenamiento o en centros de eventos. Pero puede usar un proceso externo tooread Hola de eventos de almacenamiento y colocarlos en un producto como [análisis de registros](../log-analytics/log-analytics-service-fabric.md) u otra solución de análisis de registro. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) tiene integrado un servicio integral de análisis y búsqueda de registros.

## <a name="prerequisites"></a>Requisitos previos
Use estas herramientas tooperform algunas de las operaciones de hello en este documento:

* [Diagnósticos de Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (relacionadas con la tooAzure servicios en la nube, pero tiene buena información y ejemplos)
* [Administrador de recursos de Azure](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Cliente de Azure Resource Manager](https://github.com/projectkudu/ARMClient)
* [Plantilla de Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a>Orígenes de registro que podría interesarle toocollect
* **Registros de Service Fabric**: emitidos desde Hola plataforma toostandard seguimiento de eventos para Windows (ETW) y EventSource los canales. Los registros pueden ser de uno de los varios tipos que hay:
  * Los eventos operativos: registros de operaciones que Hola Service Fabric realiza la plataforma. Algunos ejemplos son la creación de aplicaciones y servicios, los cambios de estado de nodo y la información sobre la actualización.
  * [Eventos del modelo de programación de Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
  * [Eventos del modelo de programación de Reliable Services](service-fabric-reliable-services-diagnostics.md)
* **Eventos de aplicación**: eventos emitidos desde el código de su servicio y que se escribe mediante el uso de clase de aplicación auxiliar de hello EventSource proporcionada en las plantillas de Visual Studio de Hola. Para obtener más información sobre cómo toowrite registros de la aplicación, consulte [Monitor y diagnosticar los servicios en una configuración de desarrollo de equipo local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Implementar la extensión de diagnósticos de Hola
Hola primer paso en la recopilación de registros es toodeploy extensión de diagnósticos de hello en cada una de las máquinas virtuales de hello en clúster de Service Fabric Hola. extensión de diagnósticos de Hello recopila registros en cada máquina virtual y los carga toohello cuenta de almacenamiento que especifique. pasos de Hello varían ligeramente en función de si utiliza Hola portal de Azure o Azure Resource Manager. pasos de Hello también varían en función de si implementación hello es parte de la creación de clúster o de un clúster que ya existe. Echemos un vistazo a los pasos de Hola para cada escenario.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a>Implementar la extensión de diagnósticos de hello como parte de la creación del clúster a través del portal de Hola
toodeploy Hola diagnósticos extensión toohello máquinas virtuales en clúster de hello como parte de la creación del clúster, utilice panel de configuración de diagnósticos de Hola se muestra en hello después de la imagen. tooenable Reliable Actors o servicios confiables recopilación de eventos, asegúrese de que diagnósticos está establecido demasiado**en** (Hola la configuración predeterminada). Después de crear el clúster de hello, no se puede cambiar esta configuración mediante el portal de Hola.

![Configuración de diagnóstico de Azure en el portal de hello para la creación de clúster](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

Hola equipo de soporte técnico de Azure *requiere* compatibilidad con registros toohelp resolver las solicitudes de soporte técnico que cree. Estos registros se recopilan en tiempo real y se almacenan en una de las cuentas de almacenamiento de hello creadas en el grupo de recursos de Hola. configuración de diagnóstico de Hello configura eventos de nivel de aplicación. Estos eventos incluyen [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) eventos, [servicios confiables](service-fabric-reliable-services-diagnostics.md) eventos y algunos toobe de eventos de Service Fabric de nivel de sistema almacenados en el almacenamiento de Azure.

Productos como [Elasticsearch](https://www.elastic.co/guide/index.html) o su propio proceso puede recopilar eventos de Hola de cuenta de almacenamiento de Hola. Actualmente no hay ningún evento de Hola de toofilter o limpiar de forma que se envía toohello tabla. Si no implementan un tooremove procesar los eventos de tabla de hello, tabla de hello seguirá toogrow.

Al crear un clúster mediante el portal de hello, recomendamos encarecidamente que descargue la plantilla de hello **antes de hacer clic en Aceptar** clúster de hello toocreate. Para obtener más información, consulte demasiado[configurar un clúster de Service Fabric mediante una plantilla de Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Necesitará toomake cambios de la plantilla de hello más tarde, debido a que no puede realizar algunos cambios mediante el portal de Hola.

Puede exportar plantillas desde el portal de hello mediante Hola pasos. Sin embargo, estas plantillas pueden ser más difícil toouse porque podría tienen valores null que les falta información necesaria.

1. Abra el grupo de recursos.
2. Seleccione **configuración** panel de configuración de toodisplay Hola.
3. Seleccione **implementaciones** panel de historial de implementación de toodisplay Hola.
4. Seleccione un detalles de implementación toodisplay Hola de implementación de Hola.
5. Seleccione **Exportar plantilla** panel de plantilla de toodisplay Hola.
6. Seleccione **guardar toofile** tooexport un archivo .zip que contiene la plantilla de hello, parámetros y archivos de PowerShell.

Después de exportar los archivos de hello, deberá toomake una modificación. Editar archivo de parameters.json de Hola y quitar hello **adminPassword** elemento. Esto hará que una petición de contraseña de hello al ejecutar el script de implementación de Hola. Si estás ejecutando script de implementación de hello, puede que tenga valores de parámetro con valor nulo de toofix.

Hola toouse descarga plantilla tooupdate una configuración:

1. Extraer tooa carpeta de contenido de hello en el equipo local.
2. Modificar Hola contenido tooreflect Hola nueva configuración.
3. Inicie PowerShell y cambie la carpeta toohello en la que extrajo el contenido de Hola.
4. Ejecutar **deploy.ps1** y rellene el identificador de suscripción de hello, nombre de grupo de recursos de hello (use Hola mismo configuración el nombre de hello tooupdate) y un nombre único de implementación.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Implementar la extensión de diagnósticos de hello como parte de la creación del clúster mediante el Administrador de recursos de Azure
toocreate un clúster mediante el Administrador de recursos, necesita hello tooadd diagnósticos JSON configuración toohello el Administrador de recursos completo del clúster plantilla antes de crear el clúster de Hola. Proporcionamos una plantilla de administrador de recursos de clúster de cinco VM de ejemplo con la configuración de diagnóstico agrega tooit como parte de nuestros ejemplos de la plantilla de administrador de recursos. Puede ver en esta ubicación en la Galería de ejemplos de Azure hello: [clúster de cinco nodos con el ejemplo de la plantilla de administrador de recursos de diagnóstico](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).

configuración de diagnósticos de hello toosee en plantilla de administrador de recursos de hello, archivo de azuredeploy.json de hello abierto y busque **IaaSDiagnostics**. un clúster con esta plantilla, seleccione hello toocreate **implementar tooAzure** botón está disponible en el vínculo anterior de Hola.

Como alternativa, puede descargar el ejemplo de Hola a Administrador de recursos, realizar cambios tooit y crear un clúster con la plantilla modificada hello mediante Hola `New-AzureRmResourceGroupDeployment` comando en una ventana de PowerShell de Azure. Vea Hola siguiente código para los parámetros de Hola que se pasan en el comando toohello. Para obtener información detallada sobre cómo toodeploy un recurso de grupo mediante el uso de PowerShell, vea el artículo de hello [implementar un grupo de recursos con la plantilla de Azure Resource Manager hello](../azure-resource-manager/resource-group-template-deploy.md).

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

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

## <a name="update-diagnostics-toocollect-health-and-load-events"></a>Actualizar los eventos de estado y la carga de toocollect de diagnóstico

A partir de hello 5.4 versión de Service Fabric, eventos de métrica de mantenimiento y carga están disponibles para la colección. Estos eventos reflejan los eventos generados por el sistema de hello o tu código mediante el uso de mantenimiento de Hola o cargue las API de generación de informes como [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) o [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Esto permite agregar y ver el estado de mantenimiento del sistema en el tiempo, y generar alertas basadas en eventos de estado de mantenimiento o carga. tooview agregan estos eventos en el Visor de eventos de diagnóstico de Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000008" toohello lista de proveedores de ETW.

eventos de hello toocollect, modificar tooinclude de plantilla de administrador de recursos de Hola

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

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a>Actualizar toocollect de diagnóstico y carga los registros de nuevos canales EventSource
registros de toocollect tooupdate diagnósticos de nuevos canales EventSource que representan una nueva aplicación que le sobre toodeploy, realizar Hola mismos pasos en hello [sección anterior](#deploywadarm) para la configuración de diagnósticos de una existente clúster.

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

## <a name="next-steps"></a>Pasos siguientes
toounderstand con más detalle qué eventos debe buscar al solucionar problemas, consulte los eventos de diagnóstico Hola emitidos para [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) y [servicios confiables](service-fabric-reliable-services-diagnostics.md).

## <a name="related-articles"></a>Artículos relacionados
* [Obtenga información acerca de cómo toocollect los contadores de rendimiento o de registros mediante el uso de Hola extensión de diagnósticos](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Service Fabric solution in Log Analytics](../log-analytics/log-analytics-service-fabric.md) (Solución de Service Fabric en Log Analytics)


---
title: "almacenamiento de blobs de aaaUse para IIS y la tabla de almacenamiento para los eventos de análisis de registros de Azure | Documentos de Microsoft"
description: "Análisis de registros pueden leer registros de Hola para servicios de Azure que escriben tootable almacenamiento de diagnóstico o registros de IIS que se escriban tooblob almacenamiento."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a>Uso de Azure Blob Storage para el almacenamiento de tablas de Azure e IIS de eventos con Log Analytics

Análisis de registros pueden leer los registros de Hola para hello después servicios que escriben diagnósticos tootable tooblob escrito almacenamiento de registros de almacenamiento o IIS:

* Clústeres de Service Fabric (versión preliminar)
* Máquinas virtuales
* Roles web y de trabajo

Antes de que Log Analytics pueda recopilar los datos de estos recursos, es necesario habilitar Diagnósticos de Azure.

Una vez que se habilitan los diagnósticos, puede usar Hola portal de Azure o PowerShell configurar registros de análisis de registros toocollect Hola.

Diagnósticos de Azure es una extensión de Azure que permite toocollect de datos de diagnóstico de un rol de trabajo, el rol web o la máquina virtual se ejecuta en Azure. datos de Hola se almacenan en una cuenta de almacenamiento de Azure y, a continuación, se pueden recopilar mediante el análisis de registros.

Para el análisis de registros toocollect estos registros de diagnósticos de Azure, registros de hello deben estar en hello ubicaciones siguientes:

| Tipo de registro | Tipo de recurso | La ubicación |
| --- | --- | --- |
| Registros IIS |Máquinas virtuales <br> Roles web <br> Roles de trabajo |wad-iis-logfiles (Blob Storage) |
| syslog |Máquinas virtuales |LinuxsyslogVer2v0 (Table Storage) |
| Eventos operativos de Service Fabric |Nodos de Service Fabric |WADServiceFabricSystemEventTable |
| Service Fabric Reliable Actor Events |Nodos de Service Fabric |WADServiceFabricReliableActorEventTable |
| Service Fabric Reliable Service Events |Nodos de Service Fabric |WADServiceFabricReliableServiceEventTable |
| Registros de eventos de Windows |Nodos de Service Fabric <br> Máquinas virtuales <br> Roles web <br> Roles de trabajo |WADWindowsEventLogsTable (Table Storage) |
| Registros de ETW de Windows |Nodos de Service Fabric <br> Máquinas virtuales <br> Roles web <br> Roles de trabajo |WADETWEventTable (Table Storage) |

> [!NOTE]
> Los registros de IIS de Sitios web Azure no son compatibles actualmente.
>
>

Para máquinas virtuales, tiene la opción de hello de la instalación de hello [agente de análisis de registros](log-analytics-azure-vm-extension.md) en la visión adicional de tooenable de máquina virtual. Además toobeing tooanalyze capaz de los registros de IIS y registros de eventos, puede realizar análisis adicionales como seguimiento de cambios de configuración, evaluación de SQL y evaluación de actualizaciones.

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a>Habilitación de Diagnósticos de Azure en una máquina virtual para la recopilación de registros de IIS y de eventos
Hola de uso siguiendo el procedimiento tooenable diagnósticos de Azure en una máquina virtual para la colección mediante el portal de Microsoft Azure Hola de registros de IIS y el registro de eventos.

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a>tooenable diagnósticos de Azure en una máquina virtual con hello portal de Azure
1. Instalar agente de máquina virtual de hello cuando se crea una máquina virtual. Si ya existe una máquina virtual de hello, compruebe que Hola que ya está instalado el agente de máquina virtual.

   * En Hola portal de Azure, navegue toohello virtual machine, seleccione **configuración opcional**, a continuación, **diagnósticos** y establecer **estado** demasiado**en**.

     Al finalizar, Hola VM tiene la extensión de diagnósticos de Azure de hello instalada y en ejecución. Esta extensión se encarga de recopilar datos de diagnóstico.
2. Habilite la supervisión y configure el registro de eventos en una máquina virtual existente. Puede habilitar el diagnóstico en hello nivel de máquina virtual. tooenable diagnósticos y, a continuación, configurar el registro de eventos, realice Hola pasos:

   1. Seleccione Hola máquina virtual.
   2. Haga clic en **Supervisión**.
   3. Haga clic en **Diagnósticos**.
   4. Conjunto hello **estado** demasiado**ON**.
   5. Seleccione cada registro de diagnósticos que desea toocollect.
   6. Haga clic en **Aceptar**.

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a>Activación de Diagnósticos de Azure en un rol web para la recopilación de eventos y registros de IIS
Consulte demasiado[cómo tooEnable diagnósticos en un servicio de nube](../cloud-services/cloud-services-dotnet-diagnostics.md) para conocer los pasos generales acerca de cómo habilitar diagnósticos de Azure. Estas instrucciones Hola utilizan esta información y personalizarla para su uso con análisis de registros.

Con el diagnóstico de Azure habilitado:

* Registros de IIS se almacenan de forma predeterminada, con los datos transferidos en el intervalo de transferencia de scheduledTransferPeriod Hola.
* Los registros de eventos de Windows no se transfieren de forma predeterminada.

### <a name="tooenable-diagnostics"></a>diagnóstico de tooenable
tooenable registros de eventos de Windows o toochange Hola scheduledTransferPeriod, configure diagnósticos de Azure mediante el archivo de configuración de hello XML (diagnostics.wadcfg), como se muestra en [paso 4: crear el archivo de configuración de diagnóstico e instalar Hola extensión](../cloud-services/cloud-services-dotnet-diagnostics.md)

Hello siguiente archivo de configuración de ejemplo recopila registros de IIS y todos los eventos de aplicación hello y registros del sistema:

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

Asegúrese de que ConfigurationSettings especifica una cuenta de almacenamiento, como en el siguiente ejemplo de Hola:

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

Hola **AccountName** y **AccountKey** valores se encuentran en hello portal de Azure en el panel de cuenta de almacenamiento de hello, bajo administrar claves de acceso. Protocolo de Hola de cadena de conexión de hello debe ser **https**.

Una vez que se aplica la configuración de diagnóstico actualizada hello tooyour servicio en la nube y se está escribiendo tooAzure almacenamiento de información de diagnóstico, tú eres listo tooconfigure análisis de registros.

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a>Usar registros de Azure toocollect portal Hola desde el almacenamiento de Azure
Puede usar los registros de Hola de toocollect de hello tooconfigure portal Azure análisis de registros para hello después de los servicios de Azure:

* Clústeres de Service Fabric
* Máquinas virtuales
* Roles web y de trabajo

Hola portal de Azure, navegar por el área de trabajo de análisis de registros tooyour y realizar Hola siguientes tareas:

1. Haga clic en *Storage accounts logs* (Registros de las cuentas de almacenamiento)
2. Haga clic en hello *agregar* tarea
3. Seleccionar cuenta de almacenamiento de Hola que contiene registros de diagnósticos de Hola
   * Esta cuenta puede ser una cuenta de almacenamiento clásico o una cuenta de almacenamiento de Azure Resource Manager
4. Seleccione Hola desea toocollect registros para el tipo de datos
   * Opciones de Hello son registros de IIS; Eventos; Syslog (Linux); Registros ETW; Eventos de Service Fabric
5. valor de Hello para el origen se rellena automáticamente en función de hello, tipo de datos y no se puede cambiar
6. Haga clic en Aceptar toosave Hola configuración

Repita los pasos 2 a 6 para los tipos de cuentas y los datos de almacenamiento adicional que desee toocollect de análisis de registros.

En aproximadamente 30 minutos, es capaz de toosee datos de cuenta de almacenamiento de hello en análisis de registros. Sólo verá los datos que se escriben toostorage después de aplica la configuración de Hola. Análisis de registros no leen datos preexistentes Hola de cuenta de almacenamiento de Hola.

> [!NOTE]
> portal de Hello no valida que Hola origen existe en la cuenta de almacenamiento de Hola o si se está escribiendo datos nuevos.
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a>Habilitación de Diagnósticos de Azure en una máquina virtual para la recopilación de registros de IIS y de eventos con PowerShell
Hola de uso de los pasos de [tooindex de análisis de registros de configuración de diagnósticos de Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread diagnósticos de Azure que se escriben tootable almacenamiento.

Con Azure PowerShell puede especificar con mayor precisión los eventos de Hola que se escriben tooAzure almacenamiento.
Para obtener más información, vea[Habilitación de Diagnósticos en Azure](../virtual-machines-dotnet-diagnostics.md).

Puede habilitar y actualizar los diagnósticos de Azure mediante el siguiente script de PowerShell de Hola.
También puede utilizar este script con una configuración de registro personalizada.
Modificar la cuenta de almacenamiento de hello script tooset Hola, nombre del servicio y nombre de máquina virtual.
script de Hola usa cmdlets para máquinas virtuales clásicas.

Revisar Hola siguiendo el ejemplo de script, cópielo, modifíquelo según sea necesario, guarde el ejemplo de Hola como un archivo de script de PowerShell y, a continuación, ejecute el script de Hola.

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a>Pasos siguientes
* [Recopilación de registros y métricas de los servicios de Azure](log-analytics-azure-storage.md) para los servicios compatibles de Azure.
* [Habilitar soluciones](log-analytics-add-solutions.md) visión tooprovide datos Hola.
* [Usar consultas de búsqueda](log-analytics-log-searches.md) tooanalyze datos de saludo.

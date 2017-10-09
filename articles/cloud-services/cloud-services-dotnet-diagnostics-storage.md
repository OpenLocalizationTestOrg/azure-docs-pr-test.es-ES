---
title: "aaaStore y ver datos de diagnóstico en almacenamiento de Azure | Documentos de Microsoft"
description: "Obtención de datos de diagnóstico de Azure en Almacenamiento de Azure y su visualización"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a>Almacenamiento y visualización de los datos de diagnóstico en Almacenamiento de Azure
Datos de diagnóstico no se almacenan de forma permanente a menos que transfiera emulador de almacenamiento de Microsoft Azure toohello o tooAzure almacenamiento. Una vez que se encuentren almacenados, los datos se pueden ver con una de las diversas herramientas disponibles.

## <a name="specify-a-storage-account"></a>Especificación de una cuenta de almacenamiento
Especificar cuenta de almacenamiento de Hola que desea que toouse en el archivo ServiceConfiguration.cscfg de Hola. información de la cuenta de Hello se define como una cadena de conexión en un valor de configuración. Hello en el ejemplo siguiente se muestra hello cadena de conexión predeterminado creado para un nuevo proyecto de servicio de nube en Visual Studio:

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

Puede cambiar esta información de cuenta de tooprovide de cadena de conexión para una cuenta de almacenamiento de Azure.

Según el tipo de saludo de datos de diagnóstico que se están recopilando, diagnósticos de Azure usa servicio de Blob de Hola o servicio de la tabla de Hola. Hello tabla siguiente muestran los orígenes de datos de Hola que se conservan y su formato.

| Origen de datos | Formato de almacenamiento |
| --- | --- |
| Registros de Azure |Tabla |
| Registros de IIS 7.0 |Blob |
| Registros de infraestructura de diagnóstico de Azure |Tabla |
| Registros de seguimiento de solicitudes con error |Blob |
| Registros de eventos de Windows |Tabla |
| Contadores de rendimiento |Tabla |
| Volcados de memoria |Blob |
| Registros de errores personalizados |Blob |

## <a name="transfer-diagnostic-data"></a>Transferencia de datos de diagnóstico
SDK 2.5 y versiones posteriores, datos de diagnóstico de hello solicitud tootransfer pueden producirse a través de archivo de configuración de Hola. Puede transferir datos de diagnóstico a intervalos programados, como se especifica en configuración de Hola.

Para SDK 2.4 y anteriores pueden solicitar datos de diagnóstico de hello tootransfer a través del archivo de configuración de hello como mediante programación. enfoque de programación de Hello también permite a transferencias a petición toodo.

> [!IMPORTANT]
> Cuando la transferencia de datos de diagnóstico tooan cuenta de almacenamiento de Azure, se incurre en costos para los recursos de almacenamiento de Hola que usa los datos de diagnóstico.
> 
> 

## <a name="store-diagnostic-data"></a>Almacenamiento de datos de diagnóstico
Datos de registro se almacenan en almacenamiento de Blob o tabla con hello después de nombres:

**Tablas**

* **WadLogsTable** : registros escritos en código mediante el agente de escucha de seguimiento de Hola.
* **WADDiagnosticInfrastructureLogsTable** : monitor de diagnóstico y cambios de configuración.
* **WADDirectoriesTable** – directorios ese monitor de diagnóstico de hello está supervisando.  Esto incluye los registros de IIS, los registros de solicitudes con error de IIS y los directorios personalizados.  ubicación de Hola Hola blob del archivo de registro se especifica en el campo de contenedor de Hola y nombre de hello del blob de hello es en el campo RelativePath de Hola.  campo AbsolutePath de Hello indica Hola ubicación y el nombre de archivo hello tal como se encontraban en hello máquina virtual de Azure.
* **WADPerformanceCountersTable** : contadores de rendimiento.
* **WADWindowsEventLogsTable** : registros de eventos de Windows.

**Blobs**

* **wad-control-container** : (solo para SDK 2.4 y anteriores) contiene archivos de configuración XML de Hola que controla Hola diagnósticos de Azure.
* **wad-iis-failedreqlogfiles** : contiene información de registros de solicitudes con error de IIS.
* **wad-iis-logfiles** : contiene información acerca de los registros de IIS.
* **"custom"** : contenedor personalizado basado en la configuración de directorios supervisados por el monitor de diagnóstico de Hola.  nombre de Hola de este contenedor de blob se especificará en WADDirectoriesTable.

## <a name="tools-tooview-diagnostic-data"></a>Datos de diagnóstico de tooview de herramientas
Varias herramientas son datos de Hola de tooview disponibles una vez transferido toostorage. Por ejemplo:

* Explorador de servidores de Visual Studio: si ha instalado hello Azure Tools para Microsoft Visual Studio, puede usar nodo de almacenamiento de Azure de hello en el Explorador de servidores tooview blob y tabla de datos de solo lectura de las cuentas de almacenamiento de Azure. Puede mostrar datos de la cuenta del emulador de almacenamiento local y también desde cuentas de almacenamiento que haya creado para Azure. Para obtener más información, consulte [Exploración y administración de recursos de almacenamiento con el Explorador de servidores](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente que permite trabajar tooeasily con los datos de almacenamiento de Azure en Linux, Windows y OSX.
* [Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) incluye Azure Diagnostics Manager que permite tooview, descargar y administrar datos de diagnóstico de hello recopilados por aplicaciones de Hola que se ejecutan en Azure.

## <a name="next-steps"></a>Pasos siguientes
[Flujo de Hola de seguimiento en una aplicación de servicios en la nube con diagnósticos de Azure](cloud-services-dotnet-diagnostics-trace-flow.md)


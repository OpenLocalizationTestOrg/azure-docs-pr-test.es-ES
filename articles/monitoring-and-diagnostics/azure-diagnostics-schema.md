---
title: "Historial y versiones del esquema de configuración de la extensión Azure Diagnostics | Microsoft Docs"
description: "Se utiliza para recopilar contadores de rendimiento en Azure Virtual Machines, conjuntos de escalado de máquinas virtuales, Service Fabric y Cloud Services."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/16/2017
ms.author: robb
ms.openlocfilehash: 119e8a237f24cdc80a1ab8e376f2b308c9eada05
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a>Historial y versiones del esquema de configuración de la extensión Azure Diagnostics
Esta página es un índice de las versiones del esquema de la extensión Azure Diagnostics que se incluyen como parte de Microsoft Azure SDK.  

> [!NOTE]
> La extensión Azure Diagnostics es el componente que se usa para recopilar los contadores de rendimiento y otras estadísticas de los siguientes recursos:
> - Máquinas virtuales de Azure 
> - Conjuntos de escalado de máquina virtual
> - Service Fabric 
> - Cloud Services 
> - Grupos de seguridad de red
> 
> Esta página solo es pertinente si está usando uno de estos servicios.

La extensión Azure Diagnostics se usa con otros productos de diagnósticos de Microsoft, como Azure Monitor, Application Insights y Log Analytics. Para obtener más información, consulte el artículo de [información general de herramientas de supervisión de Microsoft](monitoring-overview.md).

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a>Gráfico de envío de las versiones de Azure Diagnostics y de Azure SDK  

|Versión del SDK de Azure | Versión de la extensión Diagnostics | Modelo|  
|------------------|-------------------------------|------|  
|1.x               |1.0                            |complemento|  
|2.0 - 2.4         |1.0                            |complemento|  
|2.5               |1.2                            |extensión|  
|2.6               |1.3                            |"|  
|2.7               |1.4                            |"|  
|2.8               |1.5                            |"|  
|2.9               |1.6                            |"|
|2.96              |1.7                            |"|
|2.96              |1.8                            |"|
|2.96              |1.8.1                          |"|
|2.96              |1.9                            |"|



 La versión 1.0 de Azure Diagnostics se incluyó por primera vez en un modelo de complemento, lo que significa que, al instalar Azure SDK, obtuvo la versión de Azure Diagnostics que se incluía con el producto.  

 A partir de SDK 2.5 (versión 1.2 de Diagnósticos), Diagnósticos de Azure pasó a un modelo de extensión. Las herramientas para usar las características nuevas solo estaban disponibles en las versiones más recientes de Azure SDK, pero cualquier servicio que use Azure Diagnostics seleccionaría la versión de envío más reciente directamente desde Azure. Por ejemplo, cualquier usuario que siga usando SDK 2.5 estaría cargando la versión más reciente que se muestra en la tabla anterior, sin importar si usan las características más recientes.  

## <a name="schemas-index"></a>Índice de esquemas  
Las distintas versiones de Azure Diagnostics utilizan esquemas de configuración diferentes. 

[Esquema de configuración de Diagnósticos 1.0](azure-diagnostics-schema-1dot0.md)  

[Esquema de configuración de Diagnósticos 1.2](azure-diagnostics-schema-1dot2.md)  

[Esquema de configuración de Diagnósticos 1.3 y versiones posteriores](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a>Historial de versiones


### <a name="diagnostics-extension-19"></a>Extensión Diagnostics 1.9 
Se agregó compatibilidad con Docker.


### <a name="diagnostics-extension-181"></a>Extensión Diagnostics 1.8.1 
Puede especificar un token de SAS en lugar de una clave de cuenta de almacenamiento en la configuración privada. Si se proporciona un token de SAS, se omite la clave de cuenta de almacenamiento.


```json
{
    "storageAccountName": "diagstorageaccount",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    }
}
```

```xml
<PrivateConfig>
    <StorageAccount name="diagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    <SecondaryStorageAccounts>
        <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
</PrivateConfig>
```


### <a name="diagnostics-extension-18"></a>Extensión Diagnostics 1.8 
Se agregó StorageType a PublicConfig. Puede ser *Table*, *Blob* y *TableAndBlob*. *Table* es el valor predeterminado.


```json
{
    "WadCfg": {
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```xml
<PublicConfig>
    <WadCfg />
    <StorageAccount>diagstorageaccount</StorageAccount>
    <StorageType>TableAndBlob</StorageType>
</PublicConfig>
```


### <a name="diagnostics-extension-17"></a>Extensión Diagnostics 1.7 
Se agregó la capacidad de enrutar a EventHub.

### <a name="diagnostics-extension-15"></a>Extensión Diagnostics 1.5
Se agregaron el elemento Sinks y la capacidad de enviar datos de diagnóstico a [Application Insights](../application-insights/app-insights-cloudservices.md), lo que permitió diagnosticar de forma más sencilla los problemas tanto en la aplicación como en la infraestructura y el sistema.

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a>Azure SDK 2.6 y extensión Diagnostics 1.3 
Para los proyectos de Cloud Service en Visual Studio, se realizaron los siguientes cambios. (Estos cambios también se aplican a las versiones posteriores del SDK de Azure.)

* El emulador local ahora es compatible con diagnósticos. Esto significa que puede recopilar datos de diagnóstico y asegurarse de que su aplicación crea los seguimientos correctos mientras desarrolla y realiza pruebas en Visual Studio. La cadena de conexión `UseDevelopmentStorage=true` habilita la colección de datos de diagnóstico mientras ejecuta el proyecto de servicio en la nube en Visual Studio mediante el emulador de almacenamiento de Azure. Todos los datos de diagnóstico se recopilan en la cuenta de almacenamiento (Almacenamiento de desarrollo).
* La cadena de conexión de la cuenta de almacenamiento de diagnóstico (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) se almacena una vez más en el archivo de configuración de servicio (.cscfg). En Azure SDK 2.5 se especificó la cuenta de almacenamiento de diagnóstico en el archivo diagnostics.wadcfgx.

Existen algunas diferencias importantes entre el funcionamiento de la cadena de conexión en Azure SDK 2.4 y Azure SDK 2.6 y versiones posteriores.

* En Azure SDK 2.4 y versiones anteriores, la cadena de conexión se usaba como tiempo de ejecución mediante el complemento de diagnóstico para obtener la información de la cuenta de almacenamiento para la transferencia de registros de diagnóstico.
* En Azure SDK 2.6 y versiones posteriores, Visual Studio usa la cadena de conexión de diagnóstico para configurar la extensión de diagnóstico con la información de la cuenta de almacenamiento adecuada durante la publicación. La cadena de conexión le permite definir las cuentas de almacenamiento diferentes para diferentes configuraciones de servicio que Visual Studio usará al publicar. Sin embargo, porque ya no está disponible el complemento de diagnóstico (después de Azure SDK 2.5), el archivo .cscfg por sí solo no puede habilitar la extensión de diagnóstico. Debe habilitar la extensión por separado a través de herramientas como Visual Studio o PowerShell.
* Para simplificar el proceso de configuración de la extensión de diagnósticos con PowerShell, la salida del paquete de Visual Studio también contiene el XML de configuración pública para la extensión de diagnósticos para cada rol. Visual Studio usa la cadena de conexión de diagnósticos para rellenar la información de la cuenta de almacenamiento presente en la configuración pública. Los archivos de configuración públicas se crean en la carpeta Extensiones y siguen el patrón PaaSDiagnostics<RoleName>.PubConfig.xml. Cualquier implementación basada en PowerShell puede usar este patrón para asignar cada configuración a un rol.
* El portal de Azure también usa la cadena de conexión del archivo .cscfg para obtener acceso a los datos de diagnóstico, por lo que puede aparecer en la pestaña **Supervisión** . La cadena de conexión es necesaria para configurar el servicio para que muestre los datos de supervisión detallada en el portal.

#### <a name="migrating-projects-to-azure-sdk-26-and-later"></a>Migración de proyectos a Azure SDK 2.6 y versiones posteriores
Al migrar de Azure SDK 2.5 a Azure SDK 2.6 o versiones posteriores, si tenía una cuenta de almacenamiento de diagnósticos especificada en el archivo .wadcfgx, permanecerá allí. Para aprovechar la flexibilidad de utilizar cuentas de almacenamiento diferentes para distintas configuraciones de almacenamiento, tendrá que agregar manualmente la cadena de conexión al proyecto. Si está migrando un proyecto de Azure SDK 2.4 o una versión anterior a Azure SDK 2.6, se conservarán las cadenas de conexión de diagnóstico. Sin embargo, tenga en cuenta los cambios en cómo se tratan las cadenas de conexión en Azure SDK 2.6 tal como se especifica en la sección anterior.

#### <a name="how-visual-studio-determines-the-diagnostics-storage-account"></a>Cómo determina Visual Studio la cuenta de almacenamiento de diagnósticos
* Si se especifica una cadena de conexión de diagnóstico en el archivo .cscfg, Visual Studio lo usa para configurar la extensión de diagnóstico al publicar y al generar los archivos xml de configuración pública durante el empaquetado.
* Si no se especifica ninguna cadena de conexión de diagnóstico en el archivo .cscfg, Visual Studio recurre a usar la cuenta de almacenamiento especificada en el archivo .wadcfgx para configurar la extensión de diagnóstico al publicar, y a generar los archivos xml de configuración pública durante el empaquetado.
* La cadena de conexión de diagnóstico del archivo .cscfg tiene prioridad sobre la cuenta de almacenamiento del archivo .wadcfgx. Si se especifica una cadena de conexión de diagnóstico en el archivo .cscfg, Visual Studio la usa y omite la cuenta de almacenamiento en .wadcfgx.

#### <a name="what-does-the-update-development-storage-connection-strings-checkbox-do"></a>¿Qué hace la casilla "Actualizar las cadenas de conexión de almacenamiento de desarrollo..."?
La casilla **Actualizar las cadenas de conexión de almacenamiento de desarrollo para el diagnóstico y el almacenamiento en caché con las credenciales de la cuenta de almacenamiento de Microsoft Azure al publicar en Microsoft Azure** le ofrece una manera cómoda de actualizar cualquier cadena de conexión de cuenta de almacenamiento de desarrollo con la cuenta de almacenamiento de Azure especificada durante la publicación.

Por ejemplo, supongamos que activa esta casilla y la cadena de conexión de diagnóstico especifica `UseDevelopmentStorage=true`. Al publicar el proyecto en Azure, Visual Studio actualizará automáticamente la cadena de conexión de diagnóstico con la cuenta de almacenamiento que especificó en el Asistente para publicación. Sin embargo, si se especificó una cuenta de almacenamiento real como la cadena de conexión de diagnóstico, se usará dicha cuenta en su lugar.

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Diferencias de funcionalidad de diagnóstico entre Azure SDK 2.4 y versiones anteriores y Azure SDK 2.5 y versiones posteriores
Si está actualizando su proyecto de Azure SDK 2.4 a Azure SDK 2.5 o versiones posteriores, debe tener en cuenta las siguientes diferencias de funcionalidad de diagnóstico.

* **Las API de configuración están desusadas** : la configuración mediante programación del diagnóstico está disponible en Azure SDK 2.4 o versiones anteriores, pero está en desuso en Azure SDK 2.5 y versiones posteriores. Si la configuración de diagnóstico está definida actualmente en el código, deberá volver a definir esa configuración desde el principio en el proyecto migrado para que el diagnóstico siga funcionando. El archivo de configuración de diagnóstico de Azure SDK 2.4 es diagnostics.wadcfg y diagnostics.wadcfgx, para Azure SDK 2.5 y versiones posteriores.
* **El diagnóstico para aplicaciones de servicio en la nube solo se puede configurar en el nivel de rol, no en el nivel de instancia.**
* **Cada vez que implementa la aplicación, se actualiza la configuración de diagnóstico** : esto puede provocar problemas de paridad si cambia la configuración de diagnóstico del Explorador de servidores y luego vuelve a implementar la aplicación.
* **En Azure SDK 2.5 y versiones posteriores, los volcados de memoria se configuran en el archivo de configuración de diagnóstico, no en el código** : si tiene volcados de memoria configurados en el código, tendrá que transferir manualmente la configuración del código al archivo de configuración, porque los volcados de memoria no se transfieren durante la migración a Azure SDK 2.6.


---
title: "aaaAzure diagnósticos versiones de esquema de configuración de extensión y el historial | Documentos de Microsoft"
description: "Contadores de rendimiento de toocollecting relevante en máquinas virtuales de Azure, conjuntos de escalas de máquina virtual, Service Fabric y servicios en la nube."
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
ms.openlocfilehash: 854ad118f660810aa38703670284794d658142c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a>Historial y versiones del esquema de configuración de la extensión Azure Diagnostics
Esta página los índices versiones de esquema de extensión de diagnósticos de Azure se incluyen como parte de hello SDK de Microsoft Azure.  

> [!NOTE]
> Hola extensión de diagnósticos de Azure es el componente de hello usa toocollect los contadores de rendimiento y otras estadísticas de:
> - Máquinas virtuales de Azure 
> - Conjuntos de escalado de máquina virtual
> - Service Fabric 
> - Cloud Services 
> - Grupos de seguridad de red
> 
> Esta página solo es pertinente si está usando uno de estos servicios.

Hola extensión de diagnósticos de Azure se usa con otros productos de diagnósticos de Microsoft como Monitor de Azure, Application Insights y análisis de registros. Para obtener más información, consulte el artículo de [información general de herramientas de supervisión de Microsoft](monitoring-overview.md).

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



 Diagnósticos de Azure versión 1.0 incluyó por primera vez en un modelo de complemento, lo que significa que, cuando instala hello Azure SDK, que obtuvo versión Hola de diagnósticos de Azure que viene con el producto.  

 A partir de SDK 2.5 (versión 1.2 de diagnósticos), diagnósticos de Azure se ha producido un modelo de extensión de tooan. nuevas características de Hello herramientas tooutilize sólo estaban disponibles en versiones más recientes de los SDK de Azure, pero cualquier servicio mediante Diagnósticos de Azure seleccionará la última versión trasvase de hello directamente desde Azure. Por ejemplo, cualquier usuario sigue usando SDK 2.5 haría que cargue versión más reciente de Hola que se muestra en la tabla anterior de hello, todo ello sin importar si usan características más recientes de Hola.  

## <a name="schemas-index"></a>Índice de esquemas  
Las distintas versiones de Azure Diagnostics utilizan esquemas de configuración diferentes. 

[Esquema de configuración de Diagnósticos 1.0](azure-diagnostics-schema-1dot0.md)  

[Esquema de configuración de Diagnósticos 1.2](azure-diagnostics-schema-1dot2.md)  

[Esquema de configuración de Diagnósticos 1.3 y versiones posteriores](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a>Historial de versiones


### <a name="diagnostics-extension-19"></a>Extensión Diagnostics 1.9 
Se agregó compatibilidad con Docker.


### <a name="diagnostics-extension-181"></a>Extensión Diagnostics 1.8.1 
Puede especificar un token SAS en lugar de una clave de cuenta de almacenamiento en la configuración privada de Hola. Si no se proporciona un token de SAS, se omite la clave de cuenta de almacenamiento de Hola.


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
Agregado tooPublicConfig de tipo de almacenamiento. Puede ser *Table*, *Blob* y *TableAndBlob*. *Tabla* es Hola predeterminado.


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
Hola agregado capacidad tooroute tooEventHub.

### <a name="diagnostics-extension-15"></a>Extensión Diagnostics 1.5
Agrega Hola receptores hello y elemento de datos de diagnóstico de capacidad toosend demasiado[Application Insights](../application-insights/app-insights-cloudservices.md) lo que sea más fáciles problemas toodiagnose a través de la aplicación, así como el nivel de sistema y la infraestructura de Hola.

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a>Azure SDK 2.6 y extensión Diagnostics 1.3 
Para los proyectos de servicio en la nube en Visual Studio, Hola siguientes cambios se realizaron. (Estos cambios también aplican toolater versiones del SDK de Azure.)

* un emulador local Hola ahora es compatible con diagnósticos. Esto significa que puede recopilar datos de diagnóstico y asegúrese de que la aplicación está creando Hola seguimientos correctos mientras está desarrollando y pruebas en Visual Studio. cadena de conexión de Hola `UseDevelopmentStorage=true` habilita la recopilación de datos de diagnóstico mientras se ejecuta el proyecto de servicio de nube en Visual Studio mediante Hola emulador de almacenamiento de Azure. Todos los datos de diagnóstico se recopilan en la cuenta de almacenamiento de hello (almacenamiento de desarrollo).
* cadena de conexión de la cuenta para la almacenamiento de diagnósticos Hello (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) se almacena una vez más en el archivo de configuración (.cscfg) del servicio de Hola. En Azure SDK 2.5 cuenta de almacenamiento de diagnósticos de Hola se especificó en el archivo de hello diagnostics.wadcfgx.

Hay algunas diferencias importantes entre la cadena de conexión de hello trabajado en Azure SDK 2.4 y versiones anteriores y cómo funciona en Azure SDK 2.6 y versiones posteriores.

* En Azure SDK 2.4 y versiones anteriores, cadena de conexión de hello usado como un tiempo de ejecución por información de cuenta de almacenamiento de Hola de hello diagnósticos complemento tooget para transferir los registros de diagnóstico.
* En Azure SDK 2.6 y versiones posteriores, se utiliza la cadena de conexión de diagnósticos de Hola por extensión de diagnósticos de Visual Studio tooconfigure Hola con la información de cuenta de almacenamiento apropiada de Hola durante la publicación. cadena de conexión de Hello le permite definir las cuentas de almacenamiento distintas para diferentes configuraciones del servicio que va a usar Visual Studio al publicar. Sin embargo, porque ya no está disponible el complemento de diagnóstico de hello (después de Azure SDK 2.5), archivo de .cscfg de hello por sí mismo no puede habilitar Hola extensión de diagnósticos. Tiene la extensión de hello tooenable por separado mediante herramientas como Visual Studio o PowerShell.
* proceso de hello toosimplify de configuración de extensión de diagnósticos de hello con PowerShell, salida del paquete Hola desde Visual Studio también contiene Hola pública XML de configuración de extensión de diagnósticos de Hola para cada rol. Visual Studio usa Hola conexión cadena toopopulate Hola almacenamiento cuenta información de diagnóstico está presente en la configuración pública de Hola. archivos de configuración pública de Hola se crean en la carpeta de extensiones de Hola y seguir Hola patrón PaaSDiagnostics. <RoleName>. PubConfig.xml. Las implementaciones basadas en PowerShell pueden usar este patrón toomap cada rol tooa de configuración.
* Hello cadena de conexión en el archivo de .cscfg de hello también la usan datos de diagnóstico de Azure tooaccess portal Hola Hola para que pueda aparecer en hello **supervisión** cadena de conexión de pestaña hello es necesario tooconfigure Hola servicio tooshow detallado datos de supervisión en el portal de Hola.

#### <a name="migrating-projects-tooazure-sdk-26-and-later"></a>Migrar proyectos tooAzure SDK 2.6 y versiones posterior
Al migrar desde Azure SDK 2.5 tooAzure SDK 2.6 o versiones posteriores, si tuviera una cuenta de almacenamiento de diagnósticos especificada en el archivo .wadcfgx de hello, a continuación, permanecerá allí. cuentas de tootake aprovechar la flexibilidad de hello del uso de almacenamiento diferente para distintas configuraciones de almacenamiento, tendrá que toomanually Agregar proyecto de tooyour de cadena de conexión de Hola. Si está migrando un proyecto de Azure SDK 2.4 o anterior tooAzure SDK 2.6, Hola, a continuación, se conservan las cadenas de conexión de diagnóstico. Sin embargo, tenga en cuenta los cambios de hello en cómo se tratan las cadenas de conexión en Azure SDK 2.6 tal como se especifica en la sección anterior de Hola.

#### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Cómo Visual Studio determina la cuenta de almacenamiento de diagnósticos de Hola
* Si se especifica una cadena de conexión de diagnóstico en el archivo de .cscfg de hello, Visual Studio utiliza extensión de diagnósticos de hello tooconfigure al publicar y al generar archivos xml de configuración pública de Hola durante el empaquetado.
* Si no se especifica ninguna cadena de conexión de diagnóstico en el archivo de .cscfg de hello, a continuación, Visual Studio vuelve cuenta de almacenamiento de hello toousing especificada en hello wadcfgx tooconfigure Hola diagnósticos extensión de archivo al publicar y generar Hola público archivos xml de configuración al empaquetar.
* cadena de conexión de diagnósticos de Hello en el archivo de .cscfg de hello tiene prioridad sobre la cuenta de almacenamiento de hello en el archivo .wadcfgx de Hola. Si es una cadena de conexión de diagnósticos especificado en el archivo de .cscfg de hello, a continuación, Visual Studio usa y omite la cuenta de almacenamiento de hello en wadcfgx.

#### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>¿Qué does Hola "Actualizar cadenas de conexión de almacenamiento de desarrollo..." desarrollo..."?
Hola casilla **actualizar cadenas de conexión de almacenamiento de desarrollo para diagnóstico y almacenamiento en caché con las credenciales de cuenta de almacenamiento de Microsoft Azure al publicar tooMicrosoft Azure** le ofrece una manera cómoda de tooupdate cualquier cadenas de conexión de cuenta de almacenamiento de desarrollo con la cuenta de almacenamiento de Azure Hola especificada durante la publicación.

Por ejemplo, suponga que activa esta casilla y especifica la cadena de conexión de diagnósticos de hello `UseDevelopmentStorage=true`. Cuando publica hello tooAzure de proyecto, Visual Studio actualizará automáticamente cadena de conexión de diagnósticos de Hola con cuenta de almacenamiento de Hola que especificó en el Asistente para publicación de Hola. Sin embargo, si se especificó una cuenta de almacenamiento real como cadena de conexión de diagnósticos de hello, a continuación, dicha cuenta se utiliza en su lugar.

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Diferencias de funcionalidad de diagnóstico entre Azure SDK 2.4 y versiones anteriores y Azure SDK 2.5 y versiones posteriores
Si va a actualizar el proyecto de Azure SDK 2.4 tooAzure SDK 2.5 o versiones posteriores, debe tener en hello cuenta después de las diferencias de funcionalidad de diagnóstico.

* **Las API de configuración están desusadas** : la configuración mediante programación del diagnóstico está disponible en Azure SDK 2.4 o versiones anteriores, pero está en desuso en Azure SDK 2.5 y versiones posteriores. Si su configuración de diagnóstico está definida actualmente en el código, deberá tooreconfigure estos valores desde cero en el proyecto migrado de hello en orden para trabajar de tookeep de diagnóstico. archivo de configuración de diagnósticos de Hola para Azure SDK 2.4 es diagnostics.wadcfg y diagnostics.wadcfgx para Azure SDK 2.5 y versiones posteriores.
* **Los diagnósticos para aplicaciones de servicio de nube solo pueden configurarse en el nivel de rol de hello, no en el nivel de instancia de Hola.**
* **Cada vez que implementa la aplicación, se actualiza la configuración de diagnóstico de Hola** : Esto puede causar problemas de paridad si cambia la configuración de diagnóstico del explorador de servidores y, a continuación, volver a implementar la aplicación.
* **En Azure SDK 2.5 y versiones posteriores, los volcados de memoria se configuran en el archivo de configuración de diagnósticos de hello, no en el código** : si tiene volcados de memoria configurados en el código, deberá volver configuración de Hola de transferencia de toomanually toohello configuración archivo de código, no se transfieren porque volcados de Hola durante la migración de hello tooAzure SDK 2.6.


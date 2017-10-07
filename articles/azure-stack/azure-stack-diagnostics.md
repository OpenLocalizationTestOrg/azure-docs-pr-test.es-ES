---
title: aaaDiagnostics en la pila de Azure | Documentos de Microsoft
description: "Cómo archivos de registro de toocollect para el diagnóstico en la pila de Azure"
services: azure-stack
documentationcenter: 
author: adshar
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: adshar
ms.openlocfilehash: a4a5ddf29e75df710e9fae366d6ac16e6fb36d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-diagnostics-tools"></a>Herramientas de diagnóstico de Azure Stack
 
Azure Stack es una gran colección de componentes que funcionan juntos e interactúan entre sí. Todos estos componentes generan sus propios registros únicos, lo que significa que los problemas de diagnóstico pueden convertirse rápidamente en una tarea difícil, especialmente en el caso de los errores procedentes de varios componentes que interactúan en Azure Stack. 

Nuestras herramientas de diagnóstico ayudan a asegurarse de que el mecanismo de recopilación de registro de hello es fácil y eficaz. Hello siguiente diagrama muestra cómo iniciar herramientas de recopilación en los trabajos de la pila de Azure:

![Herramientas de recopilación de registros](media/azure-stack-diagnostics/image01.png)
 
 
## <a name="trace-collector"></a>Recopilador de seguimiento
 
Hola recopilador de seguimiento está habilitado de forma predeterminada. Lo continuamente se ejecuta en segundo plano de Hola y recopila todos los registros de seguimiento de eventos para Windows (ETW) de servicios de componentes en la pila de Azure y almacenarlos en un recurso compartido local. 

son las siguientes de Hello tooknow aspectos importantes sobre Hola recopilador de seguimiento:
 
* Hola recopilador de seguimiento se ejecuta sin interrupción con límites de tamaño de forma predeterminada. Hola tamaño máximo predeterminado permitido para cada archivo (200 MB) es **no** un tamaño límite. Se produce una comprobación de tamaño periódicamente (actualmente cada 10 minutos) y si el archivo actual de hello es > = 200 MB, se guarda y se genera un nuevo archivo. También hay un límite (configurable) de 8 GB en tamaño total del archivo de hello generado por sesión de eventos. Una vez que se alcanza este límite, se eliminan los archivos más antiguos de hello cuando se crean nuevos.
* Hay un límite de edad de 5 días en los registros de Hola. Este límite también es configurable. 
* Cada componente define las propiedades de configuración de seguimiento de Hola a través de un archivo JSON. Hola JSON archivos se almacenan en `C:\TraceCollector\Configuration`. Si es necesario, estos archivos se pueden editar los límites de antigüedad y el tamaño de hello toochange de hello recopilan registros. Archivos de toothese de cambios requieren un reinicio de hello *el recopilador de seguimiento de pila de Microsoft Azure* servicio para hello cambia tootake efecto.
* Hello en el ejemplo siguiente se es un archivo JSON de configuración de seguimiento para las operaciones de FabricRingServices de hello XRP VM: 

```
{
    "LogFile": 
    {
        "SessionName": "FabricRingServicesOperationsLogSession",
        "FileName": "\\\\SU1FileServer\\SU1_ManagementLibrary_1\\Diagnostics\\FabricRingServices\\Operations\\AzureStack.Common.Infrastructure.Operations.etl",
        "RollTimeStamp": "00:00:00",
        "MaxDaysOfFiles": "5",
        "MaxSizeInMB": "200",
        "TotalSizeInMB": "5120"
    },
    "EventSources":
    [
        {"Name": "Microsoft-AzureStack-Common-Infrastructure-ResourceManager" },
        {"Name": "Microsoft-OperationManager-EventSource" },
        {"Name": "Microsoft-Operation-EventSource" }
    ]
}
```

* **MaxDaysOfFiles**

    Este parámetro controla la edad de Hola de tookeep de archivos. Los archivos más antiguos se eliminan.
* **MaxSizeInMB**

    Este parámetro controla el umbral de tamaño de Hola para un único archivo. Si se alcanza el tamaño de hello, se crea un nuevo archivo .etl.
* **TotalSizeInMB**

    Este parámetro controla el tamaño total de Hola de hello .etl archivos generados a partir de una sesión de eventos. Si el tamaño total del archivo de hello es mayor que este valor de parámetro, se eliminan los archivos antiguos.
  
## <a name="log-collection-tool"></a>Herramienta de recopilación de registros
 
comando de PowerShell de Hola `Get-AzureStackLog` puede ser usado toocollect registros de todos los componentes de hello en un entorno de pila de Azure. Los guarda en archivos ZIP en una ubicación definida por el usuario. Si nuestro technical ajuste a las necesidades de equipo su toohelp registros solucionar un problema, puede pedirle toorun esta herramienta.

> [!CAUTION]
> Estos archivos de registro pueden contener información de identificación personal (PII). Tenga esto en cuenta antes de publicar los archivos de registro.
 
Actualmente, recopilamos Hola siguientes tipos de registro:
*   **Registros de implementación de Azure Stack**
*   **Registros de eventos de Windows**
*   **Registros de Panther**

     problemas de creación de VM de tootroubleshoot.
*   **Registros de clúster**
*   **Registros de diagnóstico de almacenamiento**
*   **Registros de ETW**

    Estos se recopilan por hello recopilador de seguimiento y almacenados en un recurso compartido desde el que se `Get-AzureStackLog` recuperarlas.
 
tooidentify todos Hola registros que se recopilan de todos los componentes de hello, consulte toohello `<Logs>` etiquetas en el archivo de configuración de cliente hello ubicados en `C:\EceStore\<Guid>\<GuidWithMaxFileSize>`.
 
### <a name="toorun-get-azurestacklog"></a>Get-AzureStackLog toorun
1.  Inicie sesión como AzureStack\AzureStackAdmin en host Hola.
2.  Abra una ventana de PowerShell como administrador.
3.  Ejecute `Get-AzureStackLog`.  

    **Ejemplos**

    - Recopilar todos los registros de todos los roles:

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs`

    - Recopilar registros de los roles VirtualMachines y BareMetal:

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal`

    - Recopilar registros de roles VirtualMachines y BareMetal, con fecha de filtrado de archivos de registro de hello últimas 8 horas:

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal -FromDate (Get-Date).AddHours(-8) -ToDate (Get-Date)`

Si hello `FromDate` y `ToDate` no se especifican parámetros, los registros se recopilan para hello últimas 4 horas de forma predeterminada.

Actualmente no se puede usar hello `FilterByRole` recopilación de registros de parámetro toofilter por hello siguientes roles:

|   |   |   |
| - | - | - |
| `ACSMigrationService`     | `ACSMonitoringService`   | `ACSSettingsService` |
| `ACS`                     | `ACSFabric`              | `ACSFrontEnd`        |
| `ACSTableMaster`          | `ACSTableServer`         | `ACSWac`             |
| `ADFS`                    | `ASAppGateway`           | `BareMetal`          |
| `BRP`                     | `CA`                     | `CPI`                |
| `CRP`                     | `DeploymentMachine`      | `DHCP`               |
|`Domain`                   | `ECE`                    | `ECESeedRing`        |        
| `FabricRing`              | `FabricRingServices`     | `FRP`                |
|` Gateway`                 | `HealthMonitoring`       | `HRP`                |               
| `IBC`                     | `InfraServiceController` | `KeyVaultAdminResourceProvider`|
| `KeyVaultControlPlane`    | `KeyVaultDataPlane`      | `NC`                 |            
| `NonPrivilegedAppGateway` | `NRP`                    | `SeedRing`           |
| `SeedRingServices`        | `SLB`                    | `SQL`                |     
| `SRP`                     | `Storage`                | `StorageController`  |
| `URP`                     | `UsageBridge`            | `VirtualMachines`    |  
| `WAS`                     | `WASPUBLIC`              | `WDS`                |


Toonote algunas cosas:

* Este comando tardará un rato en recopilar los registros en función de los registros del rol que se recopilen. Factores incluyen hello duración especificada para la recopilación de registros y números de Hola de nodos en el entorno de Azure pila Hola.
* Una vez finalizada la recopilación de registros, compruebe la carpeta nueva hello en hello `-OutputPath` los parámetros especificados en el comando de Hola.
* Un archivo denominado `Get-AzureStackLog_Output.log` se crea en la carpeta de Hola que contiene los archivos zip Hola e incluye la salida del comando hello, que se puede usar para solucionar problemas de errores en la colección de registros.
* Cada rol tiene sus registros dentro de un archivo ZIP individual. 
* tooinvestigate un error específico, pueden resultar necesario registros de más de un componente.
    -   Sistema y registros de eventos para todas las máquinas virtuales de infraestructura se recopilan en hello *VirtualMachines* rol.
    -   Sistema y registros de eventos para todos los hosts se recopilan en hello *BareMetal* rol.
    -   Registros de eventos de clúster de conmutación por error y Hyper-V se recopilan en hello *almacenamiento* rol.
    -   Registros de ACS se recopilan en hello *almacenamiento* y *ACS* roles.
* Para obtener más detalles, puede hacer referencia a toohello archivo de configuración de cliente. Investigar hello `<Logs>` etiquetas para distintas funciones de Hola.

> [!NOTE]
> Le estamos aplique tamaño y edad limita los registros de toohello tal y como resulta esencial tooensure un uso eficaz de los toomake de espacio de almacenamiento seguro no obtener congestiona con registros se recopilan. Dicho esto, cuando se diagnostica un problema a menudo necesitará registros que no exista ya debido a límites de toothese que se apliquen. Por lo tanto, es **recomienda** la descarga de su espacio de almacenamiento externo de tooan registros (una cuenta de almacenamiento de Azure público, un dispositivo de almacenamiento local adicional etc.) cada 8 horas too12 y mantenerlos existe para 1-3 meses en función de los requisitos.


## <a name="next-steps"></a>Pasos siguientes
[Solución de problemas de Microsoft Azure Stack](azure-stack-troubleshooting.md)

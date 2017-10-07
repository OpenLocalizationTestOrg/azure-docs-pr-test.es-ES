---
title: "aaaTroubleshoot el programa de instalación de clúster de Service Fabric local | Documentos de Microsoft"
description: "En este artículo se trata de un conjunto de sugerencias para solucionar problemas de su clúster de desarrollo local"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a>Solución de problemas de instalación del clúster de desarrollo local
Si experimenta un problema al interactuar con el clúster de desarrollo local de Azure Service Fabric, revise Hola siguiendo las sugerencias sobre posibles soluciones.

## <a name="cluster-setup-failures"></a>Errores de instalación de clúster
### <a name="cannot-clean-up-service-fabric-logs"></a>No se pueden limpiar los registros de Service Fabric
#### <a name="problem"></a>Problema
Mientras se ejecuta la secuencia de comandos de hello DevClusterSetup, verá un error similar al siguiente:

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a>Solución
Cerrar ventana actual de PowerShell de Hola y abrir una nueva ventana de PowerShell como administrador. Ahora debe ser capaz de toosuccessfully ejecutar script de Hola.

## <a name="cluster-connection-failures"></a>Errores de conexión del clúster
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a>Los cmdlets de PowerShell de Service Fabric no se reconocen en Azure PowerShell
#### <a name="problem"></a>Problema
Si intentas toorun cualquiera de hello cmdlets de PowerShell de tejido de servicio, como `Connect-ServiceFabricCluster` en una ventana de PowerShell de Azure, se produce un error, que indica que no se reconoce el cmdlet Hola. motivo Hello es que Azure PowerShell utiliza la versión de 32 bits de Hola de Windows PowerShell (incluso en versiones de sistema operativo de 64 bits), mientras que Hola cmdlets de Service Fabric solo funcionan en entornos de 64 bits.

#### <a name="solution"></a>Solución
Ejecute siempre los cmdlets de Service Fabric directamente desde Windows PowerShell.

> [!NOTE]
> versión más reciente de Hola de PowerShell de Azure no crea un acceso directo especial, por lo que ya no debería ocurrir.
> 
> 

### <a name="type-initialization-exception"></a>Excepción de inicialización de tipo
#### <a name="problem"></a>Problema
Cuando se conecta el clúster de toohello en PowerShell, consulte error Hola TypeInitializationException para System.Fabric.Common.AppTrace.

#### <a name="solution"></a>Solución
La variable de ruta de acceso no se estableció correctamente durante la instalación. Cierre la sesión de Windows y vuelva a iniciarla. Esto actualiza la ruta de acceso.

### <a name="cluster-connection-fails-with-object-is-closed"></a>Se produce un error de conexión del clúster con el mensaje "El objeto está cerrado"
#### <a name="problem"></a>Problema
Se produce un error en una llamada tooConnect-ServiceFabricCluster con un error similar al siguiente:

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a>Solución
Cerrar ventana actual de PowerShell de Hola y abrir una nueva ventana de PowerShell como administrador. Ahora debe poder conectarse toosuccessfully.

### <a name="fabric-connection-denied-exception"></a>Excepción de conexión de tejido denegada
#### <a name="problem"></a>Problema
Cuando se depura desde Visual Studio, se obtiene un error FabricConnectionDeniedException.

#### <a name="solution"></a>Solución
Este error suele producirse cuando intenta toostart un proceso de host de servicio manualmente, en lugar de permitir Hola Service Fabric en tiempo de ejecución toostart lo automáticamente.

Asegúrese de que no tenga ningún proyecto de servicio establecido como proyecto de inicio de la solución. Solo los proyectos de aplicación de Service Fabric deben establecerse como proyectos de inicio.

> [!TIP]
> Si, después de la instalación, el clúster local empieza toobehave anormalmente, pueden restablecer mediante la aplicación de bandeja del sistema de hello clúster local Administrador. Esta forma se elimina Hola clúster existente y configurar uno nuevo. Tenga en cuenta que todas las aplicaciones implementadas y los datos asociados también se quitan.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* [Comprensión y solución de problemas de clústeres con informes de mantenimiento del sistema](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Visualización del clúster mediante el Explorador de Service Fabric](service-fabric-visualizing-your-cluster.md)


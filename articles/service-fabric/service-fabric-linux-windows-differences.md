---
title: aaaAzure Service Fabric diferencias entre Windows y Linux | Documentos de Microsoft
description: Diferencias entre hello Azure Service Fabric Preview en Linux y Azure Service Fabric en Windows.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 7a16a440dfc8d9006e274f46951be1562e6f10d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a>Diferencias entre Service Fabric en Linux (versión preliminar) y Windows (disponible con carácter general)

Dado que Service Fabric en Linux está en versión preliminar, hay varias características que se admiten en Windows, pero aún no en Linux. Finalmente, conjuntos de características de hello estará en paridad cuando Service Fabric en Linux está generalmente disponible. En las próximas versiones, esta distancia se reducirá. Hello siguientes existen diferencias entre hello más reciente disponible versiones (es decir, entre la versión 5.6 en Windows y la versión 5.5 en Linux): 

* Colecciones confiables (y servicios con estado confiables) 
* ReverseProxy 
* Instalador independiente 
* Validación del esquema XML para archivos de manifiesto 
* Redireccionamiento de la consola 
* Hola servicio de análisis de errores (FAS)
* Docker Compose y controladores de volúmenes y de registro para contenedores 
* Regulación de recursos para contenedores y servicios 
* Servicio DNS
* Compatibilidad con Azure Active Directory
* Comandos de la CLI equivalentes a ciertos comandos de Powershell 
* Solo un subconjunto de comandos de Powershell se puede ejecutar en un clúster de Linux (tal y como se expande en la sección siguiente de hello).

>[!NOTE]
>El redireccionamiento de la consola no se admite en los clústeres de producción, ni siquiera en Windows.

Las herramientas de desarrollo también son diferentes en Windows y Linux. VisualStudio, Powershell, VSTS, and ETW se usan en Windows, mientras que Yeoman, Eclipse, Jenkins, y LTTng se usan en Linux.

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a>Cmdlets de PowerShell que no funcionan en un clúster de Service Fabric para Linux

* Invoke-ServiceFabricChaosTestScenario
* Invoke-ServiceFabricFailoverTestScenario
* Invoke-ServiceFabricPartitionDataLoss
* Invoke-ServiceFabricPartitionQuorumLoss
* Restart-ServiceFabricPartition
* Start-ServiceFabricNode
* Stop-ServiceFabricNode
* Get-ServiceFabricImageStoreContent
* Get-ServiceFabricChaosReport
* Get-ServiceFabricNodeTransitionProgress
* Get-ServiceFabricPartitionDataLossProgress
* Get-ServiceFabricPartitionQuorumLossProgress
* Get-ServiceFabricPartitionRestartProgress
* Get-ServiceFabricTestCommandStatusList
* Remove-ServiceFabricTestState
* Start-ServiceFabricChaos
* Start-ServiceFabricNodeTransition
* Start-ServiceFabricPartitionDataLoss
* Start-ServiceFabricPartitionQuorumLoss
* Start-ServiceFabricPartitionRestart
* Stop-ServiceFabricChaos
* Stop-ServiceFabricTestCommand
* Cmd
* Get-ServiceFabricNodeConfiguration
* Get-ServiceFabricClusterConfiguration
* Get-ServiceFabricClusterConfigurationUpgradeStatus
* Get-ServiceFabricPackageDebugParameters
* New-ServiceFabricPackageDebugParameter
* New-ServiceFabricPackageSharingPolicy
* Add-ServiceFabricNode
* Copy-ServiceFabricClusterPackage
* Get-ServiceFabricRuntimeSupportedVersion
* Get-ServiceFabricRuntimeUpgradeVersion
* New-ServiceFabricCluster
* New-ServiceFabricNodeConfiguration
* Remove-ServiceFabricCluster
* Remove-ServiceFabricClusterPackage
* Remove-ServiceFabricNodeConfiguration
* Test-ServiceFabricClusterManifest
* Test-ServiceFabricConfiguration
* Update-ServiceFabricNodeConfiguration
* Approve-ServiceFabricRepairTask
* Complete-ServiceFabricRepairTask
* Get-ServiceFabricRepairTask
* Invoke-ServiceFabricDecryptText
* Invoke-ServiceFabricEncryptSecret
* Invoke-ServiceFabricEncryptText
* Invoke-ServiceFabricInfrastructureCommand
* Invoke-ServiceFabricInfrastructureQuery
* Remove-ServiceFabricRepairTask
* Start-ServiceFabricRepairTask
* Stop-ServiceFabricRepairTask
* Update-ServiceFabricRepairTaskHealthPolicy



## <a name="next-steps"></a>Pasos siguientes
* [Prepare your development environment on Linux](service-fabric-get-started-linux.md)
* [Prepare your development environment on OSX](service-fabric-get-started-mac.md)
* [Creación e implementación de la primera aplicación de Java para Service Fabric en Linux con Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Creación e implementación de la primera aplicación de Java para Service Fabric con el complemento de Eclipse para Service Fabric](service-fabric-get-started-eclipse.md)
* [Creación de su primera aplicación de CSharp en Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
* [Usar las aplicaciones de hello CLI de tejido de servicio toomanage](service-fabric-application-lifecycle-sfctl.md)

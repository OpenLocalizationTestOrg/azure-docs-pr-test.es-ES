---
title: "Actualización de la aplicación: parámetros de actualización | Microsoft Docs"
description: "Describe los parámetros relacionados tooupgrading una aplicación de Service Fabric, incluyendo mantenimiento comprobaciones tooperform y directivas tooautomatically deshacer Hola actualización."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a4170ac6-192e-44a8-b93d-7e39c92a347e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: abd0ba48c223be9aa0909c7a0100ba5986430db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-upgrade-parameters"></a>Parámetros de actualización de la aplicación
Este artículo describe Hola actualización varios parámetros que se aplican durante el saludo de una aplicación de Azure Service Fabric. parámetros de Hello incluyen hello nombre y la versión de la aplicación hello. Son botones que controlan los tiempos de espera de Hola y comprobaciones de mantenimiento que se aplican durante la actualización de Hola y especifican directivas de Hola que deben aplicarse cuando se produce un error en una actualización.

<br>

| Parámetro | Description |
| --- | --- |
| ApplicationName |Nombre de aplicación Hola que se está actualizando. Ejemplos: fabric:/VisualObjects, fabric:/ClusterMonitor |
| TargetApplicationTypeVersion |versión de Hola del tipo de aplicación Hola que Hola destinos de actualización. |
| FailureAction |acción de Hello realizada por Service Fabric cuando se produce un error en la actualización de Hola. aplicación Hello puede revertirse versión anterior a la actualización de toohello (revertir) o actualización de hello puede detenerse en el dominio de actualización actual Hola. En este último caso hello, modo de actualización de hello también es tooManual modificada. Los valores permitidos son los modos de reversión y manual. |
| HealthCheckWaitDurationSec |Hola toowait de tiempo (en segundos) después de la actualización de hello terminó en el dominio de actualización de hello antes de Service Fabric evalúa el estado de saludo de la aplicación hello. Esta duración también puede considerarse como una aplicación debe estar en ejecución antes de que se puede considerar correcto de tiempo de Hola. Si pasa la comprobación de mantenimiento de hello, el proceso de actualización de hello sigue toohello siguiente dominio de actualización.  Si se produce un error en la comprobación de mantenimiento de hello, Service Fabric espera un intervalo (Hola UpgradeHealthCheckInterval) antes de reintentar la comprobación de mantenimiento de hello nuevamente hasta hello que healthcheckretrytimeout se alcanza. valor predeterminado de Hola y recomendado es de 0 segundos. |
| HealthCheckRetryTimeoutSec |duración de Hello (en segundos) que Service Fabric continúa tooperform de evaluación de mantenimiento antes de declarar la actualización de hello como no superado. valor predeterminado de Hello es 600 segundos. Esta duración se inicia tras alcanzarse HealthCheckWaitDuration. Dentro de este HealthCheckRetryTimeout, Service Fabric podría realizar varias comprobaciones de mantenimiento del estado de la aplicación hello. valor predeterminado de Hello es de 10 minutos y debe personalizarse adecuadamente para la aplicación. |
| HealthCheckStableDurationSec |Hola tooverify de duración (en segundos) que aplicación hello es estable antes de mover toohello siguiente dominio de actualización o completar Hola actualización. Esta duración de espera es tooprevent utilizado no se detectan cambios de estado correcto después de realiza la comprobación de mantenimiento de Hola. valor predeterminado de Hello es de 120 segundos y debe personalizarse adecuadamente para la aplicación. |
| UpgradeDomainTimeoutSec |Tiempo máximo (en segundos) para actualizar un solo dominio de actualización. Si se alcanza este tiempo de espera, actualización de Hola se detiene y continúa basándose en la configuración de Hola para UpgradeFailureAction. nunca es el valor predeterminado de Hello (infinito) y debe personalizarse adecuadamente para la aplicación. |
| UpgradeTimeout |Un tiempo de espera (en segundos) que se aplica para la actualización completa de Hola. Si se alcanza este tiempo de espera, Hola actualización se detiene y se desencadena UpgradeFailureAction. nunca es el valor predeterminado de Hello (infinito) y debe personalizarse adecuadamente para la aplicación. |
| UpgradeHealthCheckInterval |frecuencia de Hola que se comprueba el estado de mantenimiento de Hola. Este parámetro se especifica en hello ClusterManager sección de hello *clúster* *manifiesto*y no se especifica como parte del cmdlet de actualización de Hola. valor de Hello predeterminado es 60 segundos. |

<br>

## <a name="service-health-evaluation-during-application-upgrade"></a>Evaluación de estado del servicio durante la actualización de la aplicación
<br>
criterios de evaluación de mantenimiento de Hello son opcionales. Si no se especifican los criterios de evaluación de mantenimiento de hello cuando se inicia una actualización, Service Fabric usa las directivas de mantenimiento de aplicación Hola especificadas en hello ApplicationManifest.xml de instancia de la aplicación hello.

<br>

| Parámetro | Description |
| --- | --- |
| ConsiderWarningAsError |El valor predeterminado es False. Tratar los eventos de estado de advertencia de hello para la aplicación hello como errores al evaluar el estado de Hola de aplicación de Hola durante la actualización. De forma predeterminada, Service Fabric no evalúa errores de toobe de eventos de estado de advertencia (errores), por lo que Hola actualización puede continuar incluso si no hay eventos de advertencia. |
| MaxPercentUnhealthyDeployedApplications |El valor predeterminado y recomendado es 0. Especifique el número máximo de Hola de las aplicaciones implementadas (vea hello [sección Mantenimiento](service-fabric-health-introduction.md)) que pueden estar mal estado antes de aplicación hello se considera incorrecto y se produce un error Hola actualización. Este parámetro define el estado de la aplicación hello en el nodo de Hola y ayuda a detecta problemas durante la actualización. Por lo general, réplicas de Hola de aplicación hello obtener toohello con equilibrio de carga otro nodo, lo que permite correcto, por lo que tooproceed actualización Hola Hola tooappear de aplicación. Mediante la especificación de un mantenimiento MaxPercentUnhealthyDeployedApplications estricta, Service Fabric puede detectar un problema con el paquete de aplicación Hola más rápido y ayudar a producir un error de actualización rápida. |
| MaxPercentUnhealthyServices |El valor predeterminado y recomendado es 0. Especificar número máximo de hello de servicios en la instancia de la aplicación hello que puede estar mal estado antes de aplicación hello se considera incorrecto y se produce un error de actualización de Hola. |
| MaxPercentUnhealthyPartitionsPerService |El valor predeterminado y recomendado es 0. Especificar número máximo de Hola de particiones en un servicio que puede ser incorrecto antes de que el servicio de Hola se considera incorrecto. |
| MaxPercentUnhealthyReplicasPerPartition |El valor predeterminado y recomendado es 0. Especificar número máximo de Hola de réplicas de partición que puede estar mal estado antes de hello partición se considera incorrecto. |
| UpgradeReplicaSetCheckTimeout |**Servicio sin estado**--dentro de un solo dominio de actualización, Service Fabric intenta tooensure que instancias adicionales de servicio de hello están disponibles. Si el recuento de instancias de destino de hello es superior a uno, Service Fabric espera toobe de más de una instancia disponible, valor de tiempo de espera máximo de tooa. Este tiempo de espera se especifica mediante la propiedad de UpgradeReplicaSetCheckTimeout Hola. Si se agota el tiempo de espera de hello, Service Fabric continúa con la actualización de hello, independientemente del número de Hola de instancias de servicio. Si el recuento de instancias de destino de hello es uno, Service Fabric no espera e inmediatamente continúa con la actualización de Hola. **Servicio con estado**--dentro de un solo dominio de actualización, Service Fabric intenta tooensure que Hola réplica conjunto tiene un quórum. Tejido de servicio espera un toobe de quórum disponible, valor de tiempo de espera máximo de tooa (especificado por la propiedad de hello UpgradeReplicaSetCheckTimeout). Si se agota el tiempo de espera de hello, Service Fabric continúa con la actualización de hello, independientemente del quórum. Este valor se establece en Nunca (infinito) si avanza, y en 900 segundos si retrocede. |
| ForceRestart |Si actualiza una configuración o un paquete de datos sin actualizar el código de servicio de hello, servicio de Hola se reinicia solo si hello ForceRestart propiedad se establece tootrue. Una vez completada la actualización de hello, Service Fabric notifica al servicio Hola que está disponible un nuevo paquete de configuración o un paquete de datos. servicio de Hello es responsable de aplicar los cambios de Hola. Si es necesario, puede reiniciar el servicio de Hola propio. |

<br>
<br>
Hola MaxPercentUnhealthyServices MaxPercentUnhealthyPartitionsPerService, criterios y MaxPercentUnhealthyReplicasPerPartition se pueden especificar por tipo de servicio para una instancia de la aplicación. Configurar estos parámetros por servicio permite una servicios de aplicación toocontain diferentes tipos con directivas de evaluación diferentes. Por ejemplo, un tipo de servicio de pasarela sin estado puede tener un MaxPercentUnhealthyPartitionsPerService distinto de un tipo de servicio del motor con estado para una instancia de aplicación determinada.

## <a name="next-steps"></a>Pasos siguientes
[actualización de aplicaciones usando Visual Studio](service-fabric-application-upgrade-tutorial.md) ofrece información para actualizar una aplicación mediante Visual Studio.

[actualización de aplicaciones mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) se explica en detalle lo que tiene que hacer para actualizar una aplicación mediante PowerShell.

[Actualización de la aplicación mediante la CLI de Service Fabric en Linux](service-fabric-application-lifecycle-sfctl.md#upgrade-application) le lleva por los pasos para actualizar una aplicación mediante la CLI de Service Fabric.

[Actualización de la aplicación mediante el complemento de Eclipse para Service Fabric](service-fabric-get-started-eclipse.md#upgrade-your-service-fabric-java-application)

Hacer que las actualizaciones de la aplicación sea compatible por el aprendizaje cómo toouse [serialización de datos](service-fabric-application-upgrade-data-serialization.md).

Obtenga información acerca de cómo toouse funcionalidad avanzada al actualizar la aplicación, se hace referencia demasiado[temas avanzados](service-fabric-application-upgrade-advanced.md).

Solucione problemas habituales en las actualizaciones de aplicaciones, se hace referencia a pasos toohello en [solución de problemas de las actualizaciones de aplicaciones](service-fabric-application-upgrade-troubleshooting.md).

---
title: "actualización de hello aaaConfigure de una aplicación de Service Fabric | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure Hola configuración para actualizar una aplicación de Service Fabric mediante Microsoft Visual Studio."
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a>Configurar la actualización de Hola de una aplicación de Service Fabric en Visual Studio
Visual Studio tools para Azure Service Fabric proporcionan compatibilidad con la actualización para la publicación toolocal o clústeres remotos. Hay tres escenarios en que desea tooupgrade la versión más reciente de tooa de aplicación en lugar de reemplazar la aplicación hello durante las pruebas y depuración:

* Datos de la aplicación no se perderán durante la actualización de Hola.
* Disponibilidad permanece alta, por lo que no habrá ninguna interrupción del servicio durante la actualización de hello, si no hay suficientes instancias de servicio que se extienden desde los dominios de actualización.
* Pueden ejecutarse las pruebas en una aplicación mientras se realiza la actualización.

## <a name="parameters-needed-tooupgrade"></a>Parámetros necesitan tooupgrade
Puede elegir entre dos tipos de implementación: normal o actualización. Una implementación regular borra cualquier información de implementación anterior y los datos en el clúster de hello, mientras que una implementación de actualización conserva. Cuando se actualiza una aplicación de Service Fabric en Visual Studio, necesita tooprovide de parámetros de actualización de la aplicación y las directivas de comprobación de mantenimiento. Actualización de la aplicación los parámetros ayudan a controlar actualización hello, mientras que las directivas de comprobación de mantenimiento determinan si la actualización de hello tuvo éxito. Consulte [Actualización de la aplicación de Service Fabric: parámetros de actualización](service-fabric-application-upgrade-parameters.md) para obtener más información.

Existen tres modos de actualización: *Monitored*, *UnmonitoredAuto* y *UnmonitoredManual*.

* Una actualización de supervisión de automatiza la actualización de Hola y aplicación de comprobación de estado.
* Una actualización UnmonitoredAuto automatiza la actualización de hello, pero omite la comprobación de estado de aplicación de Hola.
* Al realizar una actualización de UnmonitoredManual, necesita toomanually actualizar cada dominio de actualización.

Cada modo de actualización requiere diferentes conjuntos de parámetros. Vea [parámetros de actualización de la aplicación](service-fabric-application-upgrade-parameters.md) toolearn más información acerca de las opciones de actualización disponibles Hola.

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a>Actualización de la aplicación de Service Fabric en Visual Studio
Si usas tooupgrade herramientas de Visual Studio Service Fabric Hola una aplicación de Service Fabric, puede especificar un toobe de proceso de publicar una actualización en lugar de una implementación regular marcando hello **actualizar la aplicación hello** comprobar cuadro.

### <a name="tooconfigure-hello-upgrade-parameters"></a>parámetros de actualización de hello tooconfigure
1. Haga clic en hello **configuración** casilla de verificación toohello siguiente botón. Hola **editar parámetros actualizar** aparece el cuadro de diálogo. Hola **editar parámetros actualizar** cuadro de diálogo admite modos de actualización de hello supervisado, UnmonitoredAuto y UnmonitoredManual.
2. Seleccione modo de actualización de Hola que desee toouse y, a continuación, rellene cuadrícula de parámetros de Hola.

    Cada parámetro tiene valores predeterminados. parámetro opcional de Hola *DefaultServiceTypeHealthPolicy* toma una entrada de la tabla hash. Este es un ejemplo del formato de entrada de tabla de hash y Hola para *DefaultServiceTypeHealthPolicy*:

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    *ServiceTypeHealthPolicyMap* es otro parámetro opcional que toma una entrada de la tabla hash en hello siguiendo el formato:

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    Este es un ejemplo real:

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. Si selecciona el modo de actualización de UnmonitoredManual, debe iniciar una toocontinue de consola de PowerShell manualmente y finalizar el proceso de actualización de Hola. Consulte demasiado[actualización de la aplicación de Service Fabric: temas avanzados](service-fabric-application-upgrade-advanced.md) toolearn manual cómo actualizar works.

## <a name="upgrade-an-application-by-using-powershell"></a>Actualización de una aplicación mediante PowerShell
Puede usar cmdlets de PowerShell tooupgrade una aplicación de Service Fabric. Consulte [Tutorial sobre la actualización de aplicaciones de Service Fabric](service-fabric-application-upgrade-tutorial.md) y [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) para obtener información detallada.

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a>Especificar una directiva de comprobación de mantenimiento en el archivo de manifiesto de aplicación Hola
Cada servicio en una aplicación de Service Fabric puede tener sus propios parámetros de directiva de mantenimiento que reemplazar los valores predeterminados de Hola. Puede proporcionar estos valores de parámetro en el archivo de manifiesto de aplicación Hola.

Hello en el ejemplo siguiente se muestra cómo tooapply un único estado de la comprobación de directiva de cada servicio en el manifiesto de aplicación Hola.

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de cómo implementar una aplicación, vea [Implementación de una aplicación existente en Azure Service Fabric](service-fabric-deploy-existing-app.md).
---
title: "aaaReport y comprobación de mantenimiento con Azure Service Fabric | Documentos de Microsoft"
description: "Obtenga información acerca de cómo informes de mantenimiento de toosend desde el código de servicio y cómo proporciona el estado de hello toocheck de su servicio mediante el uso de herramientas de supervisión de estado de Hola que Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a>Notificación y comprobación del estado del servicio
Cuando los servicios encuentran problemas, los incidentes de corrección de capacidad toorespond tooand e interrupciones depende de sus capacidad toodetect Hola problemas rápidamente. Si notificar problemas y errores de servicio de mantenimiento de Azure Service Fabric toohello desde el código de servicio, puede usar herramientas que Service Fabric proporciona el estado de mantenimiento de hello toocheck de supervisión de estado estándar.

Hay tres formas que puede crear informes de estado del servicio de hello:

* Mediante los objetos [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) o [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).  
  Puede usar hello `Partition` y `CodePackageActivationContext` objetos de estado de hello tooreport de elementos que forman parte del contexto actual de Hola. Por ejemplo, código que se ejecuta como parte de una réplica puede notificar el estado solo en esa réplica, partición de Hola que pertenece y aplicación Hola que forma parte de.
* Mediante `FabricClient`.   
  Puede usar `FabricClient` tooreport mantenimiento del código del servicio Hola si el clúster hello no está [segura](service-fabric-cluster-security.md) o si el servicio de saludo se está ejecutando con privilegios de administrador. La mayoría de los escenarios reales no usan clústeres no seguros ni proporcionan privilegios de administrador. Con `FabricClient`, puede notificar el estado en cualquier entidad que forma parte del clúster de Hola. Lo ideal es que, sin embargo, código de servicio sólo enviará informes que están relacionados tooits propio estado.
* Usar hello las API de REST en el clúster de hello, aplicación, aplicación implementada, servicio, paquete de servicio, partición, réplica o niveles de nodos. Puede tratarse de mantenimiento de tooreport usado desde dentro de un contenedor.

Este artículo le guiará a través de un ejemplo en el que informa del estado del código del servicio Hola. ejemplo de Hola también muestra cómo herramientas Hola proporcionadas por Service Fabric pueden ser usado toocheck Hola estado. En este artículo es toobe previsto en un estado de toohello introducción rápida a las capacidades de Service Fabric de supervisión. Para obtener más información, puede leer serie de Hola de artículos detallados sobre el estado que comienzan con hello vínculo final Hola de este artículo.

## <a name="prerequisites"></a>Requisitos previos
Debe tener instalado el siguiente hello:

* Visual Studio 2015 o Visual Studio 2017
* SDK de Service Fabric

## <a name="toocreate-a-local-secure-dev-cluster"></a>toocreate un clúster local desarrollo seguro
* Abra PowerShell con privilegios de administrador y ejecute hello siguientes comandos:

![Comandos que muestran cómo toocreate un clúster de desarrollo seguro](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a>toodeploy una aplicación y comprobar su estado
1. Abra Visual Studio como administrador.
2. Crear un proyecto mediante el uso de hello **servicio con estado** plantilla.
   
    ![Creación de una aplicación de Service Fabric con servicio con estado](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. Presione **F5** toorun aplicación de hello en modo de depuración. aplicación Hello es toohello implementado de clúster local.
4. Una vez que se ejecuta la aplicación hello, haga clic en el icono de administrador de clústeres Local de hello en el área de notificación de Hola y seleccione **administrar clúster Local** de tooopen de menú contextual de hello Service Fabric Explorer.
   
    ![Apertura del explorador de Service Fabric desde el área de notificación](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. estado de la aplicación Hello debe mostrarse como se muestra en esta imagen. En este momento, la aplicación hello deben funcionar correctamente sin errores.
   
    ![Aplicación correcta en el explorador de Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. También puede comprobar el estado de hello mediante PowerShell. Puede usar ```Get-ServiceFabricApplicationHealth``` toocheck el estado de una aplicación y se pueden usar ```Get-ServiceFabricServiceHealth``` toocheck estado del servicio. Hola informe de mantenimiento para hello misma aplicación en PowerShell está en esta imagen.
   
    ![Aplicación correcta en PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a>código de servicio de tooadd personalizada del estado eventos tooyour
las plantillas de proyecto de Service Fabric Hello en Visual Studio contienen código de ejemplo. Hello pasos siguientes muestran cómo puede crear informes de eventos de estado personalizado desde el código de servicio. Estos informes se muestran automáticamente en las herramientas estándar de Hola que proporciona Service Fabric, como explorador de Service Fabric y vista de estado de portal de Azure, PowerShell de supervisión de estado.

1. Vuelva a abrir la aplicación hello que creó en Visual Studio o cree una nueva aplicación mediante el uso de hello **servicio con estado** plantilla de Visual Studio.
2. Abra el archivo de hello Stateful1.cs y encontrar Hola `myDictionary.TryGetValueAsync` llamar a en hello `RunAsync` método. Puede ver que este método devuelve un `result` que contiene Hola valor actual del contador de hello porque lógica de las claves hello en esta aplicación es tookeep un ejecución de recuento. Si se tratara de una aplicación real, y si falta de Hola de resultado representa un error, sería aconsejable tooflag ese evento.
3. tooreport un evento de mantenimiento cuando falta de Hola de resultado representa un error, agregue Hola pasos.
   
    a. Agregar hello `System.Fabric.Health` espacio de nombres toohello Stateful1.cs archivo.
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    b. Agregar Hola siguiente código después de hello `myDictionary.TryGetValueAsync` llamar a
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    Informamos sobre el estado de la réplica porque se está informando desde un servicio con estado. Hola `HealthInformation` parámetro almacena información sobre el problema de estado de Hola que se va a notificar.
   
    Si ha creado un servicio sin estado, usar hello después de código
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. Si el servicio se ejecuta con privilegios de administrador o si hello clúster no está [segura](service-fabric-cluster-security.md), también puede usar `FabricClient` tooreport estado tal como se muestra en hello pasos.  
   
    a. Crear hello `FabricClient` instancia después de hello `var myDictionary` declaración.
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    b. Agregar Hola siguiente código después de hello `myDictionary.TryGetValueAsync` llamar.
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. Vamos a simular este error y se muestre en herramientas de supervisión de estado de Hola. Error de hello toosimulate, comenta la primera línea de hello en estado de hello informa del código que agregó anteriormente. Después Comente la primera línea de hello, código de hello se parecerá al siguiente ejemplo de Hola.
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   Este código activa informe de mantenimiento de hello cada vez que `RunAsync` se ejecuta. Después de cambiar hello, presione **F5** aplicación de hello toorun.
6. Después de que se ejecuta la aplicación hello, abra estado de Service Fabric Explorer toocheck Hola de aplicación hello. En esta ocasión, Service Fabric Explorer muestra que la aplicación hello es incorrecto. Esto es debido a error de hello devuelto desde el código de hello que agregamos previamente.
   
    ![Aplicación no correcta en el explorador de Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. Si selecciona la réplica principal de hello en la vista de árbol de Hola de Service Fabric Explorer, verá que **estado** indica un error, demasiado. Explorador de Service Fabric también muestra el informe de mantenimiento de hello detalles que agregan toohello `HealthInformation` parámetro en el código de hello. Puede ver Hola mismos informes de mantenimiento en PowerShell y Hola portal de Azure.
   
    ![Estado de réplica del explorador de Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

Este informe permanece en el Administrador de mantenimiento de hello hasta que sea reemplazado por otro informe o hasta que se elimine esta réplica. Dado que no se estableció `TimeToLive` para este informe de mantenimiento en hello `HealthInformation` objeto, informe de hello nunca caduca.

Se recomienda que se debería notificar mantenimiento en el nivel más granular de hello, que en este caso es réplica Hola. También se puede informar sobre el estado en `Partition`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

estado de tooreport `Application`, `DeployedApplication`, y `DeployedServicePackage`, utilice `CodePackageActivationContext`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a>Pasos siguientes
* [Profundización en el estado de Service Fabric](service-fabric-health-introduction.md)
* [API de REST para informar el estado del servicio](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [API de REST para informar el estado de la aplicación](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)


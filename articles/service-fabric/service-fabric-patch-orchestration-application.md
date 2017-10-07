---
title: "aplicación de orquestación de revisión de Service Fabric aaaAzure | Documentos de Microsoft"
description: "Aplicación tooautomate de funcionamiento de la aplicación de revisiones de sistema en un clúster de Service Fabric."
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a>Hola revisión sistema operativo Windows en el clúster de Service Fabric

aplicación de orquestación de revisión de Hello es una aplicación de Azure Service Fabric que automatiza la aplicación de revisiones en un clúster de Service Fabric en Azure sin tiempo de inactividad de sistema de operativo.

aplicación de orquestación de revisión de Hello proporciona siguiente hello:

- **Instalación automática de actualizaciones de sistema operativo**. Las actualizaciones de sistema operativo se descargan e instalan automáticamente. Los nodos de clúster se reinician según sea necesario sin tiempo de inactividad del clúster.

- **Integración de la aplicación de revisiones y el estado del clúster**. Al aplicar las actualizaciones, aplicación de orquestación de revisión de hello supervisa el estado de Hola Hola de nodos de clúster. Los nodos de clúster se actualizan de uno en uno o por dominio de actualización. Si estado Hola de clúster de hello deja de funcionar debido proceso de revisión de toohello, aplicación de revisiones es detenido tooprevent agravar el problema de Hola.

## <a name="internal-details-of-hello-app"></a>Detalles internos de la aplicación hello

aplicación de orquestación de revisión de Hello se compone de hello siguientes subcomponentes:

- **Coordinator Service**: este servicio con estado es responsable de:
    - Coordinar el trabajo de actualización de Windows de hello en clúster completo Hola.
    - Almacenando el resultado de hello operaciones completadas que Windows Update.
- **Node Agent Service**: es un servicio sin estado que se ejecuta en todos los nodos del clúster de Service Fabric. servicio de Hello es responsable de:
    - Arranque Hola servicio NT de agente de nodo.
    - Hola servicio NT de agente de nodo de supervisión.
- **Node Agent NTService**: este servicio de Windows NT se ejecuta con privilegios elevados (SYSTEM). En cambio, Hola nodo servicio de agente y Hola servicio Coordinador de ejecutan en un privilegio de nivel inferior (servicio de red). servicio de Hello es responsable de realizar Hola después de trabajos de Windows Update en todos los nodos de clúster de hello:
    - Deshabilitar las actualizaciones automáticas de Windows en el nodo de Hola.
    - Descarga e instalación de Windows Update según usuario Hola de toohello directiva ha proporcionado.
    - Reiniciar post de máquina de hello instalación de Windows Update.
    - Cargar resultados de Hola de toohello de las actualizaciones de Windows servicio de coordinador.
    - Realizar un informe de estado en caso de error en la operación después de agotar todos los reintentos.

> [!NOTE]
> Hola revisión orquestación aplicación usa Hola Service Fabric reparar toodisable de servicio de sistema de administrador o permitir que el nodo de Hola y realiza comprobaciones de estado. tarea de reparación de Hello creada por Hola revisión orquestación aplicación pistas Hola progreso de la actualización de Windows para cada nodo.

## <a name="prerequisites"></a>Requisitos previos

### <a name="minimum-supported-service-fabric-runtime-version"></a>Versión mínima admitida del runtime de Service Fabric

#### <a name="azure-clusters"></a>Clústeres de Azure
se debe ejecutar la aplicación de orquestación de revisión de Hello en Azure clústeres que tienen v5.5 de versión de Service Fabric en tiempo de ejecución o una versión posterior.

#### <a name="standalone-on-premises-clusters"></a>Clústeres locales independientes
se debe ejecutar la aplicación de orquestación de revisión de Hello en clústeres independientes que tengan v5.6 de versión de Service Fabric en tiempo de ejecución o una versión posterior.

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a>Habilitar el servicio de administrador de reparación de hello (si ya no se está ejecutando)

aplicación de orquestación de revisión de Hello requiere Hola reparación manager system service toobe habilitado en el clúster de Hola.

#### <a name="azure-clusters"></a>Clústeres de Azure

Clústeres de Azure en el nivel de durabilidad plata Hola tienen Hola reparar servicio manager habilitada de forma predeterminada. Clústeres de Azure en el nivel de durabilidad gold Hola que no tenga o servicio de administrador de reparación de hello habilitado, dependiendo de cuándo se crearon esos clústeres. Clústeres de Azure en el nivel de durabilidad bronce hello, de forma predeterminada, no es necesario Hola reparar habilitado el servicio de administrador. Si ya está habilitado el servicio de hello, puede ver que se ejecuta en la sección de servicios de sistema de Hola Hola Service Fabric Explorer.

##### <a name="azure-portal"></a>Azure Portal
Puede habilitar el Administrador de reparación de portal de Azure en tiempo de Hola de configuración de clúster. Seleccione `Include Repair Manager` opción `Add on features` en tiempo de Hola de configuración del clúster.
![Imagen de la habilitación del administrador de reparaciones de Azure Portal](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)

##### <a name="azure-resource-manager-template"></a>Plantilla del Administrador de recursos de Azure
O bien puede usar hello [plantilla de Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable servicio de administrador de reparación de hello en clústeres de Service Fabric existentes y nuevos. Obtener plantilla hello para el clúster de Hola que desea toodeploy. Puede usar plantillas de ejemplo de Hola o crear una plantilla personalizada que el Administrador de recursos. 

tooenable Hola reparación manager service mediante [plantilla de Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):

1. En primer lugar, compruebe que hello `apiversion` se establece demasiado`2017-07-01-preview` para hello `Microsoft.ServiceFabric/clusters` recursos, como se muestra en el siguiente fragmento de código de hello. Si es diferente, deberá hello tooupdate `apiVersion` toohello valor `2017-07-01-preview`:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Ahora habilitar el servicio de administrador de reparación de hello agregando Hola siguientes `addonFeatures` sección tras hello `fabricSettings` sección:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Después de haber actualizado la plantilla de clúster con estos cambios, aplicarlos y permitir que actualización de Hola a finalizar. Ahora puede ver ejecutan en el clúster de servicio del sistema de administrador de reparación Hola. Se denomina `fabric:/System/RepairManagerService` en la sección de servicios de sistema de Hola Hola Service Fabric Explorer. 

### <a name="standalone-on-premises-clusters"></a>Clústeres locales independientes

Puede usar hello [valores de configuración de clúster de Windows independiente](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable servicio de administrador de reparación de hello en clúster de Service Fabric nueva y existente.

servicio de administrador de reparación de Hola tooenable:

1. En primer lugar, compruebe que hello `apiversion` en [las configuraciones de clúster General](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) se establece demasiado`04-2017` o superior:

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. Ahora habilitar el servicio de administrador de reparación agregando Hola siguientes `addonFeaturres` sección tras hello `fabricSettings` sección tal y como se muestra a continuación:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Actualizar el manifiesto de clúster con estos cambios, usar manifiesto de clúster de hello actualiza [crear un nuevo clúster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) o [configuración de clúster de actualización hello](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration). Una vez Hola clúster se ejecuta con el manifiesto de clúster actualizados, ahora puede ver ejecutan en el clúster, que se denomina de servicio del sistema de administrador de reparación hello `fabric:/System/RepairManagerService`, en la sección en el Explorador de Service Fabric hello de servicios del sistema.

### <a name="disable-automatic-windows-update-on-all-nodes"></a>Deshabilitar las actualizaciones automáticas de Windows en todos los nodos

Actualizaciones automáticas de Windows podrían provocar la pérdida tooavailability porque varios nodos de clúster pueden reiniciar más Hola mismo tiempo. aplicación de orquestación de revisión de Hello, de forma predeterminada, los intentos toodisable Hola actualizaciones automáticas de Windows en cada nodo del clúster. Sin embargo, si administra la configuración de Hola por un administrador o la directiva de grupo, se recomienda Hola configuración directiva demasiado "notificar antes de descargar" explícitamente de Windows Update.

### <a name="optional-enable-azure-diagnostics"></a>Opcional: habilitar Azure Diagnostics

Los clústeres que ejecutan la versión `5.6.220.9494`, y versiones posteriores, del entorno en tiempo de ejecución de Service Fabric, recopilan registros de aplicación de orquestación de revisiones como parte de los registros de Service Fabric.
Puede omitir este paso si el clúster se ejecuta en la versión `5.6.220.9494`, y versiones posteriores, del entorno en tiempo de ejecución de Service Fabric.

Para los clústeres que ejecutan la versión de Service Fabric en tiempo de ejecución menor que `5.6.220.9494`, registros de aplicación de orquestación de revisión de hello se recopilan localmente en cada uno de los nodos del clúster Hola.
Se recomienda que configure los registros de diagnósticos de Azure tooupload desde ubicación central de todos los nodos tooa.

Para más información sobre Azure Diagnostics, vea [Recopilar de registros con Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).

Registros de aplicación de orquestación de revisión de hello se generan en hello después proveedor fijo identificadores:

- e39b723c-590c-4090-abb0-11e3e6616346
- fc0028ff-bfdc-499f-80dc-ed922c52c5e9
- 24afa313-0d3b-4c7c-b485-1047fd964b60
- 05dc046c-60e9-4ef7-965e-91660adffa68

En el Administrador de recursos plantilla goto `EtwEventSourceProviderConfiguration` sección en `WadCfg` y agregue Hola siguientes entradas:

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> Si el clúster de Service Fabric tiene varios tipos de nodo, se debe agregar la sección anterior de Hola para Hola todos los `WadCfg` secciones.

## <a name="download-hello-app-package"></a>Descargar paquete de la aplicación hello

Descargar la aplicación hello de hello [vínculo de descarga](https://go.microsoft.com/fwlink/P/?linkid=849590).

## <a name="configure-hello-app"></a>Configurar la aplicación hello

Hola comportamiento de aplicación de orquestación de revisión de hello puede ser toomeet configurado sus necesidades. Invalidar los valores predeterminados de Hola pasando en el parámetro de la aplicación hello durante la creación de la aplicación o actualización. Se pueden proporcionar parámetros de la aplicación mediante la especificación de `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` o `New-ServiceFabricApplication` cmdlets.

|**Parámetro**        |**Tipo**                          | **Detalles**|
|:-|-|-|
|MaxResultsToCache    |long                              | Número máximo de resultados de Windows Update que deben almacenarse en caché. <br>El valor predeterminado es 3000 suponiendo que: <br> - El número de nodos es 20. <br> - El número de actualizaciones en un nodo al mes es cinco. <br> - El número de resultados por cada operación es 10. <br> -Deben almacenarse resultados de hello últimos tres meses. |
|TaskApprovalPolicy   |Enum <br> { NodeWise, UpgradeDomainWise }                          |TaskApprovalPolicy indica la directiva de hello toobe utilizada por actualizaciones de Windows hello servicio Coordinador tooinstall de nodos de clúster de Service Fabric Hola.<br>                         Los valores permitidos son: <br>                                                           <b>NodeWise</b>. Windows Update se instala en un nodo cada vez. <br>                                                           <b>UpgradeDomainWise</b>. Windows Update se instala en un dominio de actualización cada vez. (En hello máximo, todos los nodos de Hola que pertenece el dominio de actualización tooan pueden ir de Windows Update).
|LogsDiskQuotaInMB   |long  <br> (Valor predeterminado: 1024)               |Tamaño máximo de los registros de la aplicación de orquestación de revisiones en MB que se pueden almacenar de forma persistente y local en un nodo.
| WUQuery               | cadena<br>(Valor predeterminado: "IsInstalled=0")                | Consultar tooget actualizaciones de Windows. Para más información, vea [WuQuery](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx).
| InstallWindowsOSOnlyUpdates | Booleano <br> (Valor predeterminado: True)                 | Esta marca permite operativo toobe de las actualizaciones del sistema instalado Windows.            |
| WUOperationTimeOutInMinutes | int <br>(Valor predeterminado: 90)                   | Especifica el tiempo de espera de Hola para cualquier operación de actualización de Windows (búsqueda o descargar o instalar). Si no se realiza una operación Hola dentro de Hola tiempo de espera especificado, se anula.       |
| WURescheduleCount     | int <br> (Valor predeterminado: 5)                  | número máximo de Hola de veces servicio Hola reprograma Hola Windows update en caso de error de una operación de forma persistente.          |
| WURescheduleTimeInMinutes | int <br>(Valor predeterminado: 30) | intervalo de saludo en qué Hola servicio reprograma la actualización de Windows hello en caso de error persiste. |
| WUFrequency           | Cadena separada por comas (Valor predeterminado: "Weekly, Wednesday, 7:00:00")     | frecuencia de Hello para la instalación de Windows Update. Hola formato y los posibles valores son: <br>-   Monthly, DD,HH:MM:SS, por ejemplo, Monthly, 5,12:22:32. <br> - Weekly, DÍA,HH:MM:SS, por ejemplo, Weekly, Martes, 12:22:32.  <br> -   Daily, HH:MM:SS, por ejemplo, Daily, 12:22:32.  <br> -  None indica que no debe realizarse Windows Update.  <br><br> Tenga en cuenta que todos los tiempos de hello en UTC.|
| AcceptWindowsUpdateEula | Booleano <br>(Valor predeterminado: true) | Al establecer esta marca, aplicación hello acepta Hola acuerdo de licencia de por el usuario final para Windows Update en nombre del propietario de la máquina de Hola Hola.              |

> [!TIP]
> Si desea que Windows Update toohappen inmediatamente, establezca `WUFrequency` toohello relativa momento de la implementación de aplicación. Por ejemplo, suponga que tiene una aplicación hello prueba de nodo de cinco clústeres y el plan toodeploy a aproximadamente 5:00 P.M. hora UTC. Si asume que la implementación o actualización de la aplicación hello toma 30 minutos en Hola Hola máximo, establezca WUFrequency como "Todos los días, 17:30:00".

## <a name="deploy-hello-app"></a>Implementar la aplicación hello

1. Finalizar todos los clústeres de hello tooprepare de hello pasos previos necesarios.
2. Implementar la aplicación de orquestación de revisión de hello como cualquier otra aplicación de Service Fabric. Puede implementar la aplicación hello mediante PowerShell. Siga los pasos de hello en [implementar y quitar aplicaciones con PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).
3. aplicación de Hola de tooconfigure en tiempo de Hola de implementación, pase hello `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet. Para su comodidad, hemos proporcionado Hola script Deploy.ps1 junto con la aplicación hello. script de Hola toouse:

    - Conectar el clúster de Service Fabric tooa mediante `Connect-ServiceFabricCluster`.
    - Ejecutar script de PowerShell de hello Deploy.ps1 con hello adecuado `ApplicationParameter` valor.

> [!NOTE]
> Tenga en hello script de Hola y de carpeta de la aplicación hello PatchOrchestrationApplication mismo directorio.

## <a name="upgrade-hello-app"></a>Actualizar la aplicación hello

tooupgrade una aplicación existente de orquestación de revisión con PowerShell, siga los pasos de hello en [actualización de la aplicación de Service Fabric mediante PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).

## <a name="remove-hello-app"></a>Quitar aplicación hello

aplicación de hello tooremove, siga los pasos de hello en [implementar y quitar aplicaciones con PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).

Para su comodidad, hemos proporcionado Hola script Undeploy.ps1 junto con la aplicación hello. script de Hola toouse:

  - Conectar el clúster de Service Fabric tooa mediante ```Connect-ServiceFabricCluster```.

  - Ejecutar script de PowerShell de hello Undeploy.ps1.

> [!NOTE]
> Tenga en hello script de Hola y de carpeta de la aplicación hello PatchOrchestrationApplication mismo directorio.

## <a name="view-hello-windows-update-results"></a>Ver los resultados de actualización de Windows hello

aplicación de orquestación de revisión de Hello expone el usuario toohello resultados históricos de las API de REST toodisplay Hola. Un ejemplo de Hola resultado JSON:
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
Si no hay ninguna actualización está programada todavía, el resultado de hello JSON está vacío.

Inicie sesión en el clúster de toohello tooquery Windows Update resultados. A continuación, averiguar la dirección de la réplica de hello para el elemento primario de Hola de hello servicio Coordinador de y alcanza Hola URL desde el Explorador de hello: http://&lt;IP de réplica&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.

extremo REST de Hello para el servicio Coordinador de hello tiene un puerto dinámico. toocheck Hola URL exacta, consulte toohello Service Fabric Explorer. Por ejemplo, están disponibles en los resultados de hello `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.

![Imagen de punto de conexión REST](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


Si está habilitado el proxy inverso de hello en clúster de hello, puede tener acceso URL Hola desde fuera de clúster de hello así.
Hola de punto de conexión que necesita toobe aciertos es http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.

proxy inverso de hello tooenable en clúster de hello, siga los pasos de hello en [proxy en Azure Service Fabric inverso](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy). 

> 
> [!WARNING]
> Después de configura el proxy inverso de hello, todos los servicios en clúster de hello micro que exponen un extremo HTTP son direccionables desde fuera de clúster de Hola.

## <a name="diagnosticshealth-events"></a>Eventos de diagnóstico y mantenimiento

### <a name="collect-patch-orchestration-app-logs"></a>Recopilar los registros de la aplicación de orquestación de revisiones

Los registros de aplicación de orquestación de revisiones se recopilan como parte de los registros de Service Fabric en la versión del runtime `5.6.220.9494` y versiones posteriores.
Para los clústeres que ejecutan la versión en tiempo de ejecución de Service Fabric inferior a `5.6.220.9494`, se pueden recopilar registros mediante uno de los siguientes métodos de Hola.

#### <a name="locally-on-each-node"></a>Localmente en cada nodo

Los registros se recopilan localmente en cada nodo de clúster de Service Fabric si la versión del entorno en tiempo de ejecución de Service Fabric es inferior a la `5.6.220.9494`. Hola Hola registros de ubicación tooaccess es \[Service Fabric\_instalación\_unidad\]:\\PatchOrchestrationApplication\\registros.

Por ejemplo, si Service Fabric se instala en la unidad D, ruta de acceso de hello es D:\\PatchOrchestrationApplication\\registros.

#### <a name="central-location"></a>Ubicación central

Si diagnósticos de Azure está configurado como parte de los pasos de requisitos previos, registros de aplicación de orquestación de revisión de hello están disponibles en el almacenamiento de Azure.

### <a name="health-reports"></a>Informes de mantenimiento

aplicación de orquestación de revisión de Hello también publica los informes de mantenimiento contra Hola servicio Coordinador u Hola nodo servicio de agente en hello casos siguientes:

#### <a name="a-windows-update-operation-failed"></a>Error en la operación de Windows Update

Si se produce un error en una operación de actualización de Windows en un nodo, se genera un informe de mantenimiento contra Hola nodo servicio de agente. Detalles de informe de mantenimiento de hello contienen nombre de nodo problemático Hola.

Después de aplicar revisiones se completó correctamente en el nodo problemático hello, informe de Hola se borra automáticamente.

#### <a name="hello-node-agent-ntservice-is-down"></a>Hola servicio NT de agente de nodo está inactivo

Si Hola servicio NT de agente de nodo está inactivo en un nodo, se genera un informe de mantenimiento de nivel de advertencia contra Hola nodo servicio de agente.

#### <a name="hello-repair-manager-service-is-not-enabled"></a>servicio de administrador de reparación de Hello no está habilitado

Si no se encuentra el servicio de administrador de reparación de hello en clúster de hello, se genera un informe de mantenimiento de nivel de advertencia para hello servicio Coordinador.

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

P: **¿Por qué veo mi clúster en un estado de error cuando se ejecuta la aplicación de orquestación de hello revisión?**

A. Durante el proceso de instalación de hello, aplicación de orquestación de revisión de hello deshabilita o reinicia nodos, lo que pueden producir temporalmente en estado de Hola de clúster de hello bajan.

Se basa en la directiva de hello para la aplicación hello, ya sea un nodo puede bajar durante una operación de aplicación de revisiones *o* todo un dominio de actualización puede desplazarse hacia abajo al mismo tiempo.

Extremo de Hola de hello instalación de Windows Update, Hola nodos se vuelve a habilitar después del reinicio.

En el siguiente ejemplo de Hola, clúster de hello produjo un estado de error de tooan temporalmente porque estaban apagados de dos nodos y Hola MaxPercentageUnhealthNodes directiva se ha infringido. error de Hello es temporal hasta que Hola aplicar revisiones operación está en curso.

![Imagen de clúster en mal estado](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

Si persiste el problema de hello, consulte la sección de solución de problemas de toohello.

P: **La aplicación de orquestación de revisiones está en estado de advertencia**

A. Compruebe toosee si un informe de estado registrado con la aplicación hello es la causa de Hola. Por lo general, la advertencia de hello contiene detalles del problema de Hola. Si el problema de hello es transitorio, aplicación hello es esperado tooauto-recuperación de este estado.

P: **¿Qué puedo hacer si el clúster está en mal estado y se necesita una actualización de sistema operativo urgentes toodo?**

A. aplicación de orquestación de revisión de Hello no instalar actualizaciones al clúster de hello está en mal estado. Intente toobring el clúster tooa estado correcto toounblock Hola revisión orquestación aplicación flujo de trabajo.

P: **¿Por qué aplicar revisiones a través de clústeres tardan tanto tiempo toorun?**

A. tiempo de Hello sea necesario mediante la aplicación de orquestación de revisión de hello depende principalmente de hello siguientes factores:

- Directiva de Hola de hello servicio del coordinador. 
  - Hola directiva predeterminada, `NodeWise`, da como resultado un solo nodo de aplicación de revisiones a la vez. Especialmente en el caso de hello de clústeres más grandes, se recomienda que realice hello `UpgradeDomainWise` directiva tooachieve más rápido aplicar revisiones a través de clústeres.
- número de Hola de actualizaciones disponibles para su descarga e instalación. 
- Hola toodownload tiempo promedio necesario e instale una actualización, lo que no debe tener más de un par de horas.
- Hola rendimiento de hello VM y ancho de banda de red.

P: **¿Por qué veo algunas actualizaciones en los resultados de Windows Update obtenidos a través de la api de REST, pero no se admite con hello historial de Windows Update en el equipo?**

A. Algunas actualizaciones de producto necesitan toobe comprueba en su historial de actualización/revisión respectivos. Por ejemplo: Las actualizaciones de Windows Defender no se muestran en el historial de Windows Update en Windows Server 2016.

## <a name="disclaimers"></a>Declinación de responsabilidades

- aplicación de orquestación de revisión de Hello acepta Hola acuerdo de licencia de por el usuario final de Windows Update en nombre de usuario de Hola. Si lo desea, configuración de hello puede desactivarse en la configuración de Hola de aplicación hello.

- aplicación de orquestación de revisión de Hello recopila telemetría tootrack uso y el rendimiento. telemetría de la aplicación Hello sigue configuración Hola de configuración de telemetría de hello Service Fabric en tiempo de ejecución (que está activada de forma predeterminada).

## <a name="troubleshooting"></a>Solución de problemas

### <a name="a-node-is-not-coming-back-tooup-state"></a>Un nodo no es ir los tooup estado

**nodo de Hello podría bloquearse en un estado deshabilitado porque**:

Hay una comprobación de seguridad pendiente. tooremedy esta situación, asegúrese de que hay suficientes nodos están disponibles en un estado correcto.

**nodo de Hello podría bloquearse en un estado deshabilitado porque**:

- nodo de Hola se ha deshabilitado manualmente.
- nodo de Hola se deshabilitó debido tooan trabajo de infraestructura de Azure en curso.
- nodo de Hello deshabilitó temporalmente por nodo de hello de la orquestación aplicación Hola revisión toopatch.

**Hello nodo podría bloquearse en un estado inactivo porque**:

- nodo de Hola se puso en un estado inactivo manualmente.
- nodo de saludo se está llevando a cabo un reinicio (que podría ser desencadenado por la aplicación de orquestación de revisión de hello).
- nodo de Hello está inactivo debido tooa defectuoso VM o equipo o red problemas de conectividad.

### <a name="updates-were-skipped-on-some-nodes"></a>Las actualizaciones se omitieron en algunos nodos

aplicación de orquestación de revisión de Hello intenta tooinstall una actualización correspondiente toohello reprogramación directiva de Windows. servicio de Hello trata de nodo de hello toorecover y omitir la directiva de aplicación de hello actualización correspondiente toohello.

En tal caso, se genera un informe de estado de nivel de advertencia contra Hola nodo servicio de agente. resultado de Hello de Windows Update también contiene hello es posible que el error de Hola.

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a>estado de Hola de clúster de Hola va tooerror mientras instala la actualización de Hola

Una actualización de Windows defectuosa puede acabar con estado de Hola de una aplicación o un clúster en un nodo concreto o un dominio de actualización. aplicación de orquestación de revisión de Hello interrumpe las operaciones posteriores de Windows Update hasta que el clúster Hola nuevo es correcto.

Un administrador debe intervenir y determinar por qué aplicación hello o clúster pasara a ser incorrecto debido a tooWindows Update.

## <a name="release-notes-"></a>Notas de la versión:

### <a name="version-110"></a>Versión 1.1.0
- Versión pública

### <a name="version-111"></a>Versión 1.1.1
- Se ha corregido un error en SetupEntryPoint de NodeAgentService que impedía la instalación de NodeAgentNTService.

### <a name="version-120-latest"></a>Versión 1.2.0 (más reciente)

- Correcciones de errores en el flujo de trabajo de reinicio del sistema.
- Corrección de errores en la creación de las tareas de RM pendientes toowhich comprobación de mantenimiento durante la preparación de las tareas de reparación no estaba sucediendo según lo previsto.
- Modo de inicio de hello modificada para servicio de windows POANodeSvc automática toodelayed-automáticamente.

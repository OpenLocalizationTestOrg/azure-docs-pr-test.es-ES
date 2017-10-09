---
title: "configuración de clúster de Azure Service Fabric aaaChange | Documentos de Microsoft"
description: "Este artículo describe la configuración de fabric Hola y Hola tejido actualización las directivas que se pueden personalizar."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 7ced36bf-bd3f-474f-a03a-6ebdbc9677e2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: chackdan
ms.openlocfilehash: a8b125f7b4a02547cf4bcf2c936d0c7f1686c1a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-service-fabric-cluster-settings-and-fabric-upgrade-policy"></a>Personalización de la configuración de un clúster de Service Fabric y una directiva de actualización de Fabric
Este documento explica cómo toocustomize Hola diversas configuraciones de tejido y directiva de actualización de fabric de hello para el clúster de Service Fabric. Puede personalizarlos en el portal de Hola o usando una plantilla de Azure Resource Manager.

> [!NOTE]
> No todos los valores pueden estar disponibles a través del portal de Hola. En caso de una configuración que se muestran a continuación no está disponible a través del portal de hello personalizarlo usando una plantilla de Azure Resource Manager.
> 

## <a name="customizing-service-fabric-cluster-settings-using-azure-resource-manager-templates"></a>Personalización de un clúster de Service Fabric mediante plantillas de Azure Resource Manager
Hola los pasos siguientes muestran cómo una nueva configuración de tooadd *MaxDiskQuotaInMB* toohello *diagnósticos* sección.

1. Vaya toohttps://resources.azure.com
2. Navegar por suscripción tooyour expandiendo suscripciones -> -> grupos de recursos Microsoft.ServiceFabric -> su nombre de clúster
3. En hello esquina superior derecha, seleccione "Lectura/escritura"
4. Seleccione Editar y actualizar hello `fabricSettings` elemento JSON y agregue un nuevo elemento

```
      {
        "name": "Diagnostics",
        "parameters": [
          {
            "name": "MaxDiskQuotaInMB",
            "value": "65536"
          }
        ]
      }
```

## <a name="fabric-settings-that-you-can-customize"></a>Configuración de Fabric que se puede personalizar
Estos son la configuración de Fabric Hola que se puede personalizar:

### <a name="section-name-diagnostics"></a>Nombre de sección: Diagnostics
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| ConsumerInstances |String |lista de Hola de instancias de consumidor DCA. |
| ProducerInstances |String |lista de Hola de instancias del productor DCA. |
| AppEtwTraceDeletionAgeInDays |Int, el valor predeterminado es 3. |Número de días transcurridos los cuales se eliminarán los archivos ETL antiguos que contienen seguimientos de ETW de aplicación. |
| AppDiagnosticStoreAccessRequiresImpersonation |Bool, el valor predeterminado es true. |Si no se requiere la suplantación al obtener acceso a diagnóstico almacena en nombre de la aplicación hello. |
| MaxDiskQuotaInMB |Int, el valor predeterminado es 65 536. |Cuota de disco en MB para archivos de registro de Windows Fabric. |
| DiskFullSafetySpaceInMB |Int, el valor predeterminado es 1024. |Espacio en disco restante en tooprotect MB del uso por DCA. |
| ApplicationLogsFormatVersion |Int, el valor predeterminado es 0. |Versión del formato de registros de aplicación. Los valores admitidos son 0 y 1. Versión 1 incluye más campos de registro de eventos ETW de Hola que versión 0. |
| ClusterId |String |Identificador único de Hello del clúster de Hola. Se genera cuando se crea un clúster Hola. |
| EnableTelemetry |Bool, el valor predeterminado es true. |Esto queda tooenable o deshabilitar la telemetría. |
| EnableCircularTraceSession |Bool, el valor predeterminado es false. |La marca indica si se deben usar sesiones de seguimiento circulares. |

### <a name="section-name-traceetw"></a>Nombre de sección: Trace/Etw
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| Nivel |Int, el valor predeterminado es 4. |El nivel de seguimiento de eventos puede adoptar los valores 1, 2, 3, 4. toobe admitida debe mantener el nivel de seguimiento de hello en 4 |

### <a name="section-name-performancecounterlocalstore"></a>Nombre de sección: PerformanceCounterLocalStore
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| IsEnabled |Bool, el valor predeterminado es true. |La marca indica si está habilitada la colección de contadores de rendimiento en el nodo local. |
| SamplingIntervalInSeconds |Int, el valor predeterminado es 60. |Intervalo de muestreo para los contadores de rendimiento que se recolectarán. |
| Counters |String |Lista separada por comas de toocollect de contadores de rendimiento. |
| MaxCounterBinaryFileSizeInMB |Int, el valor predeterminado es 1. |Tamaño máximo (en MB) de cada archivo binario de contador de rendimiento. |
| NewCounterBinaryFileCreationIntervalInMinutes |Int, el valor predeterminado es 10. |Intervalo máximo (en segundos) después del cual se crea un nuevo archivo binario de contador de rendimiento. |

### <a name="section-name-setup"></a>Nombre de sección: Setup
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| FabricDataRoot |string |Directorio raíz de datos de Service Fabric. El valor predeterminado para Azure es d:\svcfab. |
| FabricLogRoot |string |Directorio raíz del registro de Service Fabric. Aquí es donde se colocan los seguimientos y registros de SF. |
| ServiceRunAsAccountName |String |nombre de cuenta de Hello en qué servicio de host de tejido toorun. |
| ServiceStartupType |String |tipo de inicio de Hello del servicio de host de tejido de Hola. |
| SkipFirewallConfiguration |Bool, el valor predeterminado es false. |Especifica si la configuración del firewall debe toobe establecido por el sistema de Hola o no. Solo aplicable si usa Firewall de Windows. Si usas firewalls de terceros, debe abrir puertos de Hola para toouse de sistema y las aplicaciones de Hola |

### <a name="section-name-transactionalreplicator"></a>Nombre de sección: TransactionalReplicator
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| MaxCopyQueueSize |Uint, el valor predeterminado es 16384. |Se trata de valor máximo de hello define el tamaño inicial de Hola para cola de Hola que mantiene las operaciones de replicación. Tenga en cuenta que debe ser una potencia de 2. Si en tiempo de ejecución Hola cola sigue creciendo toothis operaciones de tamaño se limitarán entre replicadores de hello principal y secundaria. |
| BatchAcknowledgementInterval | Tiempo en segundos, el valor predeterminado es 0,015. | Especifique el intervalo de tiempo en segundos. Determina la cantidad de Hola de tiempo que Hola replicador espera después de recibir una operación antes de enviar una confirmación de nuevo. Otras operaciones que recibió durante este período de tiempo tendrán sus confirmaciones enviados en un único mensaje -> reducir el tráfico de red pero potencialmente reducen el rendimiento de Hola de Replicador de Hola. |
| MaxReplicationMessageSize |Uint, el valor predeterminado es 52 428 800. | Tamaño máximo de mensaje de las operaciones de replicación. El valor predeterminado es 50 MB. |
| ReplicatorAddress |string, el valor predeterminado es "localhost:0". | punto de conexión de Hello en forma de cadena-'IP: Port' que es utilizado por las conexiones de hello Replicador de Windows Fabric tooestablish con otras réplicas en las operaciones de recepción/toosend de orden. |
| InitialPrimaryReplicationQueueSize |Uint, el valor predeterminado es 64. | Este valor define el tamaño inicial de Hola para cola de Hola que mantiene las operaciones de replicación de hello en hello principal. Tenga en cuenta que debe ser una potencia de 2.|
| MaxPrimaryReplicationQueueSize |Uint, el valor predeterminado es 8192. |Se trata de hello número máximo de operaciones que podría existir en la cola de replicación principal Hola. Tenga en cuenta que debe ser una potencia de 2. |
| MaxPrimaryReplicationQueueMemorySize |Uint, el valor predeterminado es 0. |Se trata de un valor máximo de Hola de cola de replicación principal hello en bytes. |
| InitialSecondaryReplicationQueueSize |Uint, el valor predeterminado es 64. |Este valor define el tamaño inicial de Hola para cola de Hola que mantiene las operaciones de replicación de hello en hello secundaria. Tenga en cuenta que debe ser una potencia de 2. |
| MaxSecondaryReplicationQueueSize |Uint, el valor predeterminado es 16384. |Se trata de hello número máximo de operaciones que podría existir en la cola de replicación secundaria Hola. Tenga en cuenta que debe ser una potencia de 2. |
| MaxSecondaryReplicationQueueMemorySize |Uint, el valor predeterminado es 0. |Se trata de un valor máximo de Hola de cola de replicación secundaria de hello en bytes. |
| SecondaryClearAcknowledgedOperations |Bool, el valor predeterminado es false. |BOOL que controla si las operaciones de hello en replicador secundaria Hola se borran una vez que se confirmen toohello principal (vaciado toohello disco). Configuración de que este tooTRUE puede dar lugar a lecturas de disco adicional en la nueva réplica principal de hello, durante la detección de réplicas después de una conmutación por error. |
| MaxMetadataSizeInKB |Int, el valor predeterminado es 4. |Tamaño máximo de hello metadatos de la secuencia de registro. |
| MaxRecordSizeInKB |Uint, el valor predeterminado es 1024. | Tamaño máximo de un registro de secuencia de registro. |
| CheckpointThresholdInMB |Int, el valor predeterminado es 50. |Cuando el uso de registro de hello supera este valor, se iniciará un punto de control. |
| MaxAccumulatedBackupLogSizeInMB |Int, el valor predeterminado es 800. |El tamaño máximo acumulado (en MB) de los registros de copia de seguridad de una cadena de registros de copia de seguridad determinada. Una solicitudes de copia de seguridad incremental se producirá un error si la copia de seguridad incremental de hello generaría un registro de copia de seguridad que puede provocar que los registros de copia de seguridad de hello acumulado desde el número de toobe relevante copia de seguridad completa de hello mayor que este tamaño. En tales casos, el usuario es necesario tootake una copia de seguridad completa. |
| MaxWriteQueueDepthInKB |Int, el valor predeterminado es 0. | Int durante un máximo de escritura profundidad de cola dicho registrador de núcleo de hello puede usar como se especifica en kilobytes de registro de hello que está asociado a esta réplica. Este valor es el número máximo de Hola de bytes que pueden estar pendientes durante las actualizaciones básicas del registrador. Puede ser 0 para hello principales del registrador toocompute un valor adecuado o un múltiplo de 4. |
| SharedLogId |String |Identificador de registro compartido. Es un GUID y debe ser único para cada registro compartido. |
| SharedLogPath |String |Registro de ruta de acceso toohello compartido. Si este valor está vacío, se usa del registro compartidas Hola predeterminado. |
| SlowApiMonitoringDuration |Tiempo en segundos, el valor predeterminado es 300. | Especifique la duración de la API antes de que se desencadene el evento de mantenimiento de advertencia.|
| MinLogSizeInMB |Int, el valor predeterminado es 0. |Tamaño mínimo del registro transaccional de Hola. registro de Hello no se permitirán tootruncate tooa tamaño por debajo de este valor. 0 indica que Replicador Hola determinará el tamaño mínimo del registro de hello según la configuración de tooother. Al aumentar este valor aumenta la posibilidad de Hola de hacer las copias parciales y copias de seguridad incrementales desde posibilidades relevantes de entradas de registro que se va a truncar disminuye. |

### <a name="section-name-fabricclient"></a>Nombre de sección: FabricClient
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| NodeAddresses |string, el valor predeterminado es "". |Una colección de direcciones (las cadenas de conexión) en nodos diferentes que pueden ser utilizado toocommunicate con Hola Hola Naming Service. Hola inicialmente que cliente conecta al seleccionar una de las direcciones de hello aleatoriamente. Si se proporciona más de una cadena de conexión y se produce un error en una conexión debido a una comunicación o un error de tiempo de espera; Hello cliente cambia dirección del próximo toouse Hola secuencialmente. Vea la sección de reintento de dirección del servicio de nomenclatura de Hola para obtener más información sobre semántica de reintentos. |
| ConnectionInitializationTimeout |Tiempo en segundos, el valor predeterminado es 2. |Especifique el intervalo de tiempo en segundos. Intervalo de tiempo de espera de conexión para cada cliente tiempo intenta tooopen una puerta de enlace de conexión toohello. |
| PartitionLocationCacheLimit |Int, el valor predeterminado es 100 000. |Número de particiones que se almacenan en caché para la resolución del servicio (establecer too0 para no establecer ningún límite). |
| ServiceChangePollInterval |Tiempo en segundos, el valor predeterminado es 120. |Especifique el intervalo de tiempo en segundos. intervalo de saludo entre sondeos consecutivos para servicio cambia de puerta de enlace de hello cliente toohello para devoluciones de llamada de las notificaciones de cambio de servicio registrado. |
| KeepAliveIntervalInSeconds |Int, el valor predeterminado es 20. |intervalo de saludo en qué hello FabricClient transporte envía la puerta de enlace de mensajes de mantenimiento toohello. Para 0; keepAlive está deshabilitado. Debe ser un valor positivo. |
| HealthOperationTimeout. |Tiempo en segundos, el valor predeterminado es 120. |Especifique el intervalo de tiempo en segundos. tiempo de espera de Hola para un mensaje de informe enviado tooHealth Manager. |
| HealthReportSendInterval. |Tiempo en segundos, el valor predeterminado es 30. |Especifique el intervalo de tiempo en segundos. intervalo de saludo en qué componente de informes envía acumulado mantenimiento informa tooHealth Manager. |
| HealthReportRetrySendInterval |Tiempo en segundos, el valor predeterminado es 30. |Especifique el intervalo de tiempo en segundos. intervalo de saludo en qué componente de informes vuelve a enviar acumulado mantenimiento informa tooHealth Manager. |
| RetryBackoffInterval |Tiempo en segundos, el valor predeterminado es 3. |Especifique el intervalo de tiempo en segundos. Hola intervalo de interrupción antes de reintentar la operación de Hola. |
| MaxFileSenderThreads |Uint, el valor predeterminado es 10. |número máximo de Hola de archivos que se transfieren en paralelo. |

### <a name="section-name-common"></a>Nombre de sección: Common
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| PerfMonitorInterval |Tiempo en segundos, el valor predeterminado es 1. |Especifique el intervalo de tiempo en segundos. Intervalo de supervisión del rendimiento. Configuración too0 o valor negativo deshabilita la supervisión. |

### <a name="section-name-healthmanager"></a>Nombre de sección: HealthManager
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| EnableApplicationTypeHealthEvaluation |Bool, el valor predeterminado es false. |Directiva de evaluación de mantenimiento del clúster: habilita la evaluación de mantenimiento de tipos por aplicación. |

### <a name="section-name-fabricnode"></a>Nombre de sección: FabricNode
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| StateTraceInterval |Tiempo en segundos, el valor predeterminado es 300. |Especifique el intervalo de tiempo en segundos. intervalo de saludo para el seguimiento del estado del nodo en cada nodo y los nodos en FM/FMM. |

### <a name="section-name-nodedomainids"></a>Nombre de sección: NodeDomainIds
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| UpgradeDomainId |string, el valor predeterminado es "". |Describe el dominio de actualización de hello al que pertenece un nodo. |
| PropertyGroup |NodeFaultDomainIdCollection |Describe los dominios de error Hola que pertenece un nodo. dominio de error de Hola se define mediante un URI que describe la ubicación de hello del nodo de hello en el centro de datos de Hola.  URI de dominio de error son de hello formato fd: / fd/seguido de un segmento de ruta de acceso URI.|

### <a name="section-name-nodeproperties"></a>Nombre de sección: NodeProperties
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| PropertyGroup |NodePropertyCollectionMap |Una colección de pares de clave y valor de cadena para las propiedades de nodo. |

### <a name="section-name-nodecapacities"></a>Nombre de sección: NodeCapacities
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| PropertyGroup |NodeCapacityCollectionMap |Una colección de funcionalidades de nodo para diferentes métricas. |

### <a name="section-name-fabricnode"></a>Nombre de sección: FabricNode
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| StartApplicationPortRange |Int, el valor predeterminado es 0. |Inicio de puertos de la aplicación hello administrados por el subsistema de hospedaje. Requerido si EndpointFilteringEnabled es true en Hosting. |
| EndApplicationPortRange |Int, el valor predeterminado es 0. |Final (no inclusive) de puertos de la aplicación hello administrados por el subsistema de hospedaje. Requerido si EndpointFilteringEnabled es true en Hosting. |
| ClusterX509StoreName |string, el valor predeterminado es "My". |Nombre del almacén de certificados X.509 que contiene el certificado de clúster para proteger la comunicación dentro del clúster. |
| ClusterX509FindType |string, el valor predeterminado es "FindByThumbprint". |Indica cómo especifica toosearch para el certificado de clúster en el almacén de hello ClusterX509StoreName admite valores: "FindByThumbprint"; "FindBySubjectName" con "FindBySubjectName"; Cuando hay varias coincidencias; Hola con caducidad más lejana Hola se utiliza. |
| ClusterX509FindValue |string, el valor predeterminado es "". |Valor de filtro de búsqueda usa toolocate certificado de clúster. |
| ClusterX509FindValueSecondary |string, el valor predeterminado es "". |Valor de filtro de búsqueda usa toolocate certificado de clúster. |
| ServerAuthX509StoreName |string, el valor predeterminado es "My". |Nombre del almacén de certificados X.509 que contiene el certificado de servidor para el servicio de entrada. |
| ServerAuthX509FindType |string, el valor predeterminado es "FindByThumbprint". |Indica cómo toosearch para el certificado de servidor hello almacén especificado por valor ServerAuthX509StoreName admite: FindByThumbprint; FindBySubjectName. |
| ServerAuthX509FindValue |string, el valor predeterminado es "". |Valor de filtro de búsqueda usa el certificado de servidor toolocate. |
| ServerAuthX509FindValueSecondary |string, el valor predeterminado es "". |Valor de filtro de búsqueda usa el certificado de servidor toolocate. |
| ClientAuthX509StoreName |string, el valor predeterminado es "My". |Nombre del almacén de certificados X.509 de Hola que contiene el certificado para el rol de administrador predeterminado FabricClient. |
| ClientAuthX509FindType |string, el valor predeterminado es "FindByThumbprint". |Indica cómo toosearch de certificado en el almacén de hello especificado por valor ClientAuthX509StoreName admite: FindByThumbprint; FindBySubjectName. |
| ClientAuthX509FindValue |string, el valor predeterminado es "". | Valor de filtro de búsqueda usa toolocate certificado para el rol de administrador predeterminado FabricClient. |
| ClientAuthX509FindValueSecondary |string, el valor predeterminado es "". |Valor de filtro de búsqueda usa toolocate certificado para el rol de administrador predeterminado FabricClient. |
| UserRoleClientX509StoreName |string, el valor predeterminado es "My". |Nombre del almacén de certificados X.509 de Hola que contiene el certificado para el rol de usuario predeterminado FabricClient. |
| UserRoleClientX509FindType |string, el valor predeterminado es "FindByThumbprint". |Indica cómo toosearch de certificado en el almacén de hello especificado por valor UserRoleClientX509StoreName admite: FindByThumbprint; FindBySubjectName. |
| UserRoleClientX509FindValue |string, el valor predeterminado es "". |Valor de filtro de búsqueda usa toolocate certificado para el rol de usuario predeterminado FabricClient. |
| UserRoleClientX509FindValueSecondary |string, el valor predeterminado es "". |Valor de filtro de búsqueda usa toolocate certificado para el rol de usuario predeterminado FabricClient. |

### <a name="section-name-paas"></a>Nombre de sección: Paas
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| ClusterId |string, el valor predeterminado es "". |Almacén de certificados X509 usado por Fabric para la protección de la configuración. |

### <a name="section-name-fabrichost"></a>Nombre de sección: FabricHost
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| StopTimeout |Tiempo en segundos, el valor predeterminado es 300. |Especifique el intervalo de tiempo en segundos. Hola tiempo de espera para la activación del servicio hospedado; desactivación y la actualización. |
| StartTimeout |Tiempo en segundos, el valor predeterminado es 300. |Especifique el intervalo de tiempo en segundos. Tiempo de espera de inicio de fabricactivationmanager. |
| ActivationRetryBackoffInterval |Tiempo en segundos, el valor predeterminado es 5. |Especifique el intervalo de tiempo en segundos. Intervalo de interrupción en cada caso de error de activación; en cada activación continua sistema Hola de error volverá a intentar la activación de Hola para seguridad toohello MaxActivationFailureCount. intervalo de reintento de Hello en cada intento es un producto de activación continua hello y error retroceso intervalo de activación. |
| ActivationMaxRetryInterval |Tiempo en segundos, el valor predeterminado es 300. |Especifique el intervalo de tiempo en segundos. Intervalo de reintento máximo para la activación. En cada reintento de hello error continua intervalo se calcula como mínimo (ActivationMaxRetryInterval; Recuento de errores continuos * ActivationRetryBackoffInterval). |
| ActivationMaxFailureCount |Int, el valor predeterminado es 10. |Se trata de recuento máximo de hello para el que el sistema volverá a intentar activación errores antes de desistir. |
| EnableServiceFabricAutomaticUpdates |Bool, el valor predeterminado es false. |Se trata de una actualización automática de tejido tooenable a través de Windows Update. |
| EnableServiceFabricBaseUpgrade |Bool, el valor predeterminado es false. |Se trata de actualización de base de tooenable de servidor. |
| EnableRestartManagement |Bool, el valor predeterminado es false. |Se trata de reiniciar el servidor tooenable. |


### <a name="section-name-failovermanager"></a>Nombre de sección: FailoverManager
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| UserReplicaRestartWaitDuration |Tiempo en segundos, el valor predeterminado es 60.0 * 30. |Especifique el intervalo de tiempo en segundos. Cuando una réplica persistente deja de funcionar; Windows Fabric espera esta duración de hello réplica toocome copia de seguridad antes de crear nuevas réplicas de reemplazo (lo que requieran una copia del estado de hello). |
| QuorumLossWaitDuration |Tiempo en segundos, el valor predeterminado es MaxValue. |Especifique el intervalo de tiempo en segundos. Se trata de duración máxima de hello para el que se permite un toobe de partición en un estado de pérdida del quórum. Si hay partición hello en pérdida de quórum después de esta duración; partición de Hola se recuperarán de la pérdida de quórum a considerar Hola hacia abajo de réplicas como perdida. Tenga en cuenta que esto puede provocar una pérdida de datos. |
| UserStandByReplicaKeepDuration |Tiempo en segundos, el valor predeterminado es 3600,0 * 24 * 7 |Especifique el intervalo de tiempo en segundos. Cuando una réplica persistente vuelve de un estado inactivo, puede que ya se haya reemplazado. Este temporizador determina cuánto tiempo Hola FM mantendrá la réplica en espera de hello antes de descartarlo. |
| UserMaxStandByReplicaCount |Int, el valor predeterminado es 1. |número máximo de Hello predeterminado de réplicas StandBy que Hola sistema mantiene para los servicios de usuario. |

### <a name="section-name-namingservice"></a>Nombre de sección: NamingService
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| TargetReplicaSetSize |Int, el valor predeterminado es 7. |número de Hola de réplica se establece para cada partición del almacén del servicio de nomenclatura de Hola. Aumentar el número Hola de réplica conjuntos aumenta Hola nivel de confiabilidad para obtener información de Hola Hola escribir el nombre del almacén del servicio; reduce el cambio de Hola que Hola información se perderá como resultado errores de nodo; con un costo de aumento de carga en Windows Fabric y Hola tiempo de toma tooperform actualizaciones toohello nomenclatura datos.|
|MinReplicaSetSize | Int, el valor predeterminado es 3. | número mínimo de Hola de réplicas del servicio de nombres requeridos toowrite en toocomplete una actualización. Si hay menos réplicas que este activo Hola Hola de sistema confiabilidad sistema deniega el almacén del servicio de nomenclatura de actualizaciones toohello hasta que se restauran las réplicas. Este valor nunca debe ser mayor que hello TargetReplicaSetSize. |
|ReplicaRestartWaitDuration | Tiempo en segundos, el valor predeterminado es (60.0 * 30).| Especifique el intervalo de tiempo en segundos. Cuando una réplica del servicio de nomenclatura deja de funcionar, el temporizador se inicia.  Cuando venza Hola FM comenzará réplicas de hello tooreplace que están inactivos (no aún tenerlos en cuenta perdido). |
|QuorumLossWaitDuration | Tiempo en segundos, el valor predeterminado es MaxValue. | Especifique el intervalo de tiempo en segundos. Cuando un servicio de nomenclatura entra en pérdida de cuórum, este temporizador se inicia.  Cuando venza Hola FM considerará Hola hacia abajo de réplicas como perdida; quórum y el intento de toorecover. Tenga en cuenta que esto puede dar lugar a la pérdida de datos. |
|StandByReplicaKeepDuration | Tiempo en segundos, el valor predeterminado es 3600.0 * 2. | Especifique el intervalo de tiempo en segundos. Cuando una réplica del servicio de nomenclatura vuelve de un estado inactivo, puede que ya se haya reemplazado.  Este temporizador determina cuánto tiempo Hola FM mantendrá la réplica en espera de hello antes de descartarlo. |
|PlacementConstraints | string, el valor predeterminado es "". | Restricción de selección de ubicación para Hola Naming Service. |
|ServiceDescriptionCacheLimit | Int, el valor predeterminado es 0. | número máximo de Hola de entradas que se mantienen en caché de descripción del servicio de hello LRU en Hola Naming Service de almacén (establecer too0 para no establecer ningún límite). |
|RepairInterval | Tiempo en segundos, el valor predeterminado es 5. | Especifique el intervalo de tiempo en segundos. Intervalo de en qué Hola iniciará nomenclatura reparar incoherencias entre el propietario de la entidad de Hola y nombre. |
|MaxNamingServiceHealthReports | Int, el valor predeterminado es 10. | número máximo de Hola de operaciones lentas que almacenan los nombres de servicio de informes incorrecto al mismo tiempo. Si es 0, se envían todas las operaciones lentas. |
| MaxMessageSize |Int, el valor predeterminado es 4*1024*1024. |tamaño máximo del mensaje de Hola para la comunicación de nodo de cliente cuando se usa la nomenclatura. Mitigación de ataque de DOS; el valor predeterminado es 4 MB. |
| MaxFileOperationTimeout |Tiempo en segundos, el valor predeterminado es 30. |Especifique el intervalo de tiempo en segundos. Hola tiempo de espera máximo permitido para la operación de servicio de almacén de archivos. Las solicitudes que especifiquen un tiempo de espera mayor se rechazarán. |
| MaxOperationTimeout |Tiempo en segundos, el valor predeterminado es 600. |Especifique el intervalo de tiempo en segundos. Hola tiempo de espera máximo permitido para las operaciones de cliente. Las solicitudes que especifiquen un tiempo de espera mayor se rechazarán. |
| MaxClientConnections |Int, el valor predeterminado es 1000. |Hola número máximo permitido de conexiones de cliente por puerta de enlace. |
| ServiceNotificationTimeout |Tiempo en segundos, el valor predeterminado es 30. |Especifique el intervalo de tiempo en segundos. tiempo de espera de Hello utilizado para entregar el contenido de cliente del servicio de notificaciones toohello. |
| MaxOutstandingNotificationsPerClient |Int, el valor predeterminado es 1000. |número máximo de Hola de notificaciones pendientes antes de un registro de cliente se forzó el cierre la puerta de enlace de Hola. |
| MaxIndexedEmptyPartitions |Int, el valor predeterminado es 1000. |número máximo de Hola de particiones vacías que vaya a permanecer indiza en memoria caché de la notificación de hello para la sincronización de reconexión de los clientes. Índice de hello en sentido ascendente de versión de búsqueda se quitará cualquier partición vacía por encima de este número. Volver a conectar los clientes puede sincronizarse aún y recibir actualizaciones perdidas partición vacía; pero el protocolo de sincronización de hello es más caro. |
| GatewayServiceDescriptionCacheLimit |Int, el valor predeterminado es 0. |número máximo de Hola de entradas que se mantienen en caché de descripción del servicio de hello LRU en Hola Naming Gateway (establecer too0 para no establecer ningún límite). |
| PartitionCount |Int, el valor predeterminado es 3. |número de Hola de particiones de hello Naming Service almacén toobe creado. Cada partición posee una clave de una única partición que corresponde el índice de tooits; claves de partición así [0; PartitionCount) existe. Se estableció el creciente número de Hola de particiones aumenta de servicio de nomenclatura escala Hola Hola Naming Service puede realizar en reduciendo la cantidad media de Hola de los datos mantenidos por todas las réplicas de copias de seguridad; con un costo de incremento en el uso de recursos (desde PartitionCount * deben mantenerse ReplicaSetSize réplicas de servicio).|

### <a name="section-name-runas"></a>Nombre de sección: RunAs
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| RunAsAccountName |string, el valor predeterminado es "". |Indica el nombre de cuenta de ejecución de Hola. Solo es necesario para el tipo de cuenta "DomainUser" o "ManagedServiceAccount". Los valores válidos son "domain\user" o "user@domain". |
|RunAsAccountType|string, el valor predeterminado es "". |Indica el tipo de cuenta de RunAs Hola. Es necesario para cualquier sección RunAs. Valores válidos son "DomainUser/NetworkService/ManagedServiceAccount/LocalSystem".|
|RunAsPassword|string, el valor predeterminado es "". |Indica la contraseña de la cuenta de hello RunAs. Solo es necesario para el tipo de cuenta "DomainUser". |

### <a name="section-name-runasfabric"></a>Nombre de sección: RunAs_Fabric
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| RunAsAccountName |string, el valor predeterminado es "". |Indica el nombre de cuenta de ejecución de Hola. Solo es necesario para el tipo de cuenta "DomainUser" o "ManagedServiceAccount". Los valores válidos son "domain\user" o "user@domain". |
|RunAsAccountType|string, el valor predeterminado es "". |Indica el tipo de cuenta de RunAs Hola. Es necesario para cualquier sección RunAs. Valores válidos son "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem". |
|RunAsPassword|string, el valor predeterminado es "". |Indica la contraseña de la cuenta de hello RunAs. Solo es necesario para el tipo de cuenta "DomainUser". |

### <a name="section-name-runashttpgateway"></a>Nombre de sección: RunAs_HttpGateway
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| RunAsAccountName |string, el valor predeterminado es "". |Indica el nombre de cuenta de ejecución de Hola. Solo es necesario para el tipo de cuenta "DomainUser" o "ManagedServiceAccount". Los valores válidos son "domain\user" o "user@domain". |
|RunAsAccountType|string, el valor predeterminado es "". |Indica el tipo de cuenta de RunAs Hola. Es necesario para cualquier sección RunAs. Valores válidos son "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem". |
|RunAsPassword|string, el valor predeterminado es "". |Indica la contraseña de la cuenta de hello RunAs. Solo es necesario para el tipo de cuenta "DomainUser". |

### <a name="section-name-runasdca"></a>Nombre de sección: RunAs_DCA
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| RunAsAccountName |string, el valor predeterminado es "". |Indica el nombre de cuenta de ejecución de Hola. Solo es necesario para el tipo de cuenta "DomainUser" o "ManagedServiceAccount". Los valores válidos son "domain\user" o "user@domain". |
|RunAsAccountType|string, el valor predeterminado es "". |Indica el tipo de cuenta de RunAs Hola. Es necesario para cualquier sección RunAs. Valores válidos son "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem". |
|RunAsPassword|string, el valor predeterminado es "". |Indica la contraseña de la cuenta de hello RunAs. Solo es necesario para el tipo de cuenta "DomainUser". |

### <a name="section-name-httpgateway"></a>Nombre de sección: HttpGateway
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
|IsEnabled|Bool, el valor predeterminado es false. | Habilita/deshabilita Hola httpgateway. Httpgateway está deshabilitado de forma predeterminada y esta configuración debe toobe conjunto tooenable se. |
|ActiveListeners |Uint, el valor predeterminado es 50. | Número de cola del servidor de lecturas toopost toohello http. Esta opción controla Hola número de solicitudes simultáneas que se puede satisfacer mediante hello HttpGateway. |
|MaxEntityBodySize |Uint, el valor predeterminado es 4 194 304. |  Proporciona el tamaño máximo de Hola Hola del cuerpo de que se puede esperar de una solicitud http. El valor predeterminado es 4 MB. Httpgateway no atenderá una solicitud si el tamaño del cuerpo es mayor que su valor. El tamaño mínimo del fragmento de lectura es 4096 bytes. Por lo que esto tiene toobe > = 4096. |
|HttpGatewayHealthReportSendInterval |Tiempo en segundos, el valor predeterminado es 30. | Especifique el intervalo de tiempo en segundos. intervalo de saludo en qué Hola puerta de enlace de Http envía acumulados tooHealth de informes de estado Manager. |

### <a name="section-name-ktllogger"></a>Nombre de sección: KtlLogger
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
|AutomaticMemoryConfiguration |Int, el valor predeterminado es 1. | Marca que indica si la configuración de memoria Hola debería configurar automática y dinámica. Si cero valores de configuración de memoria de hello, a continuación, se utilizan directamente y no cambian según las condiciones del sistema. Si uno, a continuación, memoria de Hola se configura automáticamente y pueden cambiar según las condiciones del sistema. |
|WriteBufferMemoryPoolMinimumInKB |Int, el valor predeterminado es 8 388 608. |número de Hola de KB tooinitially asignar para el bloque de memoria de búfer de escritura de Hola. Use 0 tooindicate ningún límite predeterminado debe ser coherente con SharedLogSizeInMB siguiente. |
|WriteBufferMemoryPoolMaximumInKB | Int, el valor predeterminado es 0. |Hola número de KB tooallow Hola escritura toogrow de bloque de memoria de búfer hasta. No use 0 tooindicate ningún límite. |
|MaximumDestagingWriteOutstandingInKB | Int, el valor predeterminado es 0. | número de Hola de KB tooallow hello comparte tooadvance de registro por delante de registro dedicado Hola. No use 0 tooindicate ningún límite.
|SharedLogPath |string, el valor predeterminado es "". | Ruta de acceso y nombre toolocation tooplace compartido contenedor de registro. Use "" para utilizar la ruta de acceso predeterminada en la raíz de datos de Fabric. |
|SharedLogId |string, el valor predeterminado es "". |GUID único del contenedor de registros compartidos. Use "" si utiliza la ruta de acceso predeterminada en la raíz de datos de Fabric. |
|SharedLogSizeInMB |Int, el valor predeterminado es 8192. | número de Hola de tooallocate MB en el contenedor de registro compartido Hola. |

### <a name="section-name-applicationgatewayhttp"></a>Nombre de sección: ApplicationGateway/Http
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
|IsEnabled |Bool, el valor predeterminado es false. | Habilita/deshabilita Hola HttpApplicationGateway. HttpApplicationGateway está deshabilitado de forma predeterminada y esta configuración debe toobe conjunto tooenable se. |
|NumberOfParallelOperations | Uint, el valor predeterminado es 5000 | Número de cola del servidor de lecturas toopost toohello http. Esta opción controla Hola número de solicitudes simultáneas que se puede satisfacer mediante hello HttpGateway. |
|DefaultHttpRequestTimeout |Tiempo en segundos. El valor predeterminado es 120 |Especifique el intervalo de tiempo en segundos.  Da tiempo de espera de solicitud de saludo predeterminado para las solicitudes de http de Hola que se procesan en la puerta de enlace de aplicaciones de hello http. |
|ResolveServiceBackoffInterval |Tiempo en segundos, el valor predeterminado es 5. |Especifique el intervalo de tiempo en segundos.  Proporciona el intervalo de retroceso de predeterminado de hello antes de intentar una operación de servicio de resolución errores. |
|BodyChunkSize |Uint, el valor predeterminado es 16384. |  Proporciona Hola tamaño de fragmento de hello en bytes usa cuerpo de hello tooread. |
|GatewayAuthCredentialType |string, el valor predeterminado es "None" | Indica el tipo hello de toouse de credenciales de seguridad en valores válidos de punto de conexión de puerta de enlace de aplicación de hello http son "ninguno / X 509. |
|GatewayX509CertificateStoreName |string, el valor predeterminado es "My". | Nombre del almacén de certificados X.509 que contiene el certificado de puerta de enlace de aplicaciones HTTP. |
|GatewayX509CertificateFindType |string, el valor predeterminado es "FindByThumbprint". | Indica cómo toosearch de certificado en el almacén de hello especificado por valor GatewayX509CertificateStoreName admite: FindByThumbprint; FindBySubjectName. |
|GatewayX509CertificateFindValue | string, el valor predeterminado es "". | Valor de filtro de búsqueda usa el certificado de puerta de enlace de aplicación toolocate Hola http. Este certificado se configura en el punto de conexión de hello https y también puede ser usado tooverify Hola identidad de aplicación hello si necesaria para los servicios de Hola. Primero se busca FindValue y, si no existe, se busca FindValueSecondary. |
|GatewayX509CertificateFindValueSecondary | string, el valor predeterminado es "". |Valor de filtro de búsqueda usa el certificado de puerta de enlace de aplicación toolocate Hola http. Este certificado se configura en el punto de conexión de hello https y también puede ser usado tooverify Hola identidad de aplicación hello si necesaria para los servicios de Hola. Primero se busca FindValue y, si no existe, se busca FindValueSecondary.|

### <a name="section-name-management"></a>Nombre de sección: Management
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| ImageStoreConnectionString |SecureString | Toohello de cadena de conexión raíz para el almacén de imágenes. |
| ImageStoreMinimumTransferBPS | Int, el valor predeterminado es 1024. |velocidad de transferencia mínima de Hello entre clústeres de Hola y ImageStore. Este valor es el tiempo de espera de toodetermine usado hello cuando obtiene acceso a Hola ImageStore externo. Cambie este valor solo si latencia Hola entre clústeres de Hola y ImageStore es alta tooallow más tiempo para toodownload de clúster de Hola de Hola ImageStore externo. |
|AzureStorageMaxWorkerThreads | Int, el valor predeterminado es 25. | número máximo de Hola de subprocesos de trabajo en paralelo. |
|AzureStorageMaxConnections | Int, el valor predeterminado es 5000. | número máximo de Hola de almacenamiento de tooazure de conexiones simultáneas. |
|AzureStorageOperationTimeout | Tiempo en segundos, el valor predeterminado es 6000. | Especifique el intervalo de tiempo en segundos. Tiempo de espera para xstore operación toocomplete. |
|ImageCachingEnabled | Bool, el valor predeterminado es true. | Esta configuración permite tooenable o deshabilitar el almacenamiento en caché. |
|DisableChecksumValidation | Bool, el valor predeterminado es false. | Esta configuración permite que nos tooenable o deshabilitar la validación de suma de comprobación durante el aprovisionamiento de la aplicación. |
|DisableServerSideCopy | Bool, el valor predeterminado es false. | Esta configuración habilita o deshabilita la copia del lado servidor del paquete de aplicación en el almacén de imágenes de Hola durante el aprovisionamiento de la aplicación. |

### <a name="section-name-healthmanagerclusterhealthpolicy"></a>Nombre de sección: HealthManager/ClusterHealthPolicy
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| ConsiderWarningAsError |Bool, el valor predeterminado es false. |Directiva de evaluación de mantenimiento del clúster: las advertencias se tratan como errores. |
| MaxPercentUnhealthyNodes | Int, el valor predeterminado es 0. |Directiva de evaluación de mantenimiento del clúster: porcentaje máximo de nodos mal estado permitido para hello clúster toobe correcto. |
| MaxPercentUnhealthyApplications | Int, el valor predeterminado es 0. |Directiva de evaluación de mantenimiento del clúster: porcentaje máximo de aplicaciones en mal estado permitido para hello clúster toobe correcto. |
|MaxPercentDeltaUnhealthyNodes | Int, el valor predeterminado es 10. |Directiva de evaluación de estado de actualización de clúster: porcentaje máximo de nodos de mal estado delta permitido para hello clúster toobe correcto. |
|MaxPercentUpgradeDomainDeltaUnhealthyNodes | Int, el valor predeterminado es 15. |Directiva de evaluación de estado de actualización de clúster: porcentaje máximo de diferencias de los nodos incorrecto en un dominio de actualización permitido para hello clúster toobe correcto.|

### <a name="section-name-faultanalysisservice"></a>Nombre de sección: FaultAnalysisService
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| TargetReplicaSetSize |Int, el valor predeterminado es 0. |Hola NOT_PLATFORM_UNIX_START TargetReplicaSetSize para FaultAnalysisService. |
| MinReplicaSetSize |Int, el valor predeterminado es 0. |Hola MinReplicaSetSize para FaultAnalysisService. |
| ReplicaRestartWaitDuration |Tiempo en segundos, el valor predeterminado es 60 minutos.|Especifique el intervalo de tiempo en segundos. Hola ReplicaRestartWaitDuration para FaultAnalysisService. |
| QuorumLossWaitDuration | Tiempo en segundos, el valor predeterminado es MaxValue. |Especifique el intervalo de tiempo en segundos. Hola QuorumLossWaitDuration para FaultAnalysisService. |
| StandByReplicaKeepDuration| Tiempo en segundos, el valor predeterminado es (60*24*7) minutos. |Especifique el intervalo de tiempo en segundos. Hola StandByReplicaKeepDuration para FaultAnalysisService. |
| PlacementConstraints | string, el valor predeterminado es "".| Hola PlacementConstraints para FaultAnalysisService. |
| StoredActionCleanupIntervalInSeconds | Int, el valor predeterminado es 3600. |Se trata de la frecuencia con hello almacén se limpiarán.  Solo se quitarán las acciones en estado terminal y que se han completado como mínimo hace CompletedActionKeepDurationInSeconds. |
| CompletedActionKeepDurationInSeconds | Int, el valor predeterminado es 604 800. | Se trata de aproximadamente cuánto tookeep las acciones que se encuentran en un estado terminal.  Esto también depende StoredActionCleanupIntervalInSeconds; Puesto que Hola trabajo toocleanup sólo se realiza en ese intervalo. 604800 es 7 días. |
| StoredChaosEventCleanupIntervalInSeconds | Int, el valor predeterminado es 3600. |Se trata de la frecuencia con hello almacén se van a auditar para la limpieza; Si el número de Hola de eventos es más de 30000; limpieza de Hello activará. |

### <a name="section-name-filestoreservice"></a>Nombre de sección: FileStoreService
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| NamingOperationTimeout |Tiempo en segundos, el valor predeterminado es 60. |Especifique el intervalo de tiempo en segundos. tiempo de espera de Hola para realizar la operación de asignación de nombres. |
| QueryOperationTimeout | Tiempo en segundos, el valor predeterminado es 60. |Especifique el intervalo de tiempo en segundos. tiempo de espera de Hola para realizar la operación de consulta. |
| MaxCopyOperationThreads | Uint, el valor predeterminado es 0. | número máximo de Hola de archivos paralelo puede copiar esa base de datos secundaria del objeto principal. "0" == número de núcleos. |
| MaxFileOperationThreads | Uint, el valor predeterminado es 100. | número máximo de Hola de subprocesos paralelos permitidos tooperform FileOperations (copiar o mover) Hola principal. "0" == número de núcleos. |
| MaxStoreOperations | Uint, el valor predeterminado es 4096. |número máximo de Hola de operaciones de transcation almacén paralelo permitido en la principal. "0" == número de núcleos. |
| MaxRequestProcessingThreads | Uint, el valor predeterminado es 200. |Hola permite número máximo de subprocesos paralelos tooprocess solicitudes Hola principal. "0" == número de núcleos. |
| MaxSecondaryFileCopyFailureThreshold | Uint, el valor predeterminado es 25.| número máximo de Hola de reintentos de copia de archivo en hello secundaria antes de desistir. |
| AnonymousAccessEnabled | Bool, el valor predeterminado es true. |Habilitar o deshabilitar toohello acceso anónimo que filestoreservice comparte. |
| PrimaryAccountType | string, el valor predeterminado es "". |Hola principal AccountType de Hola tooACL principal Hola FileStoreService comparte. |
| PrimaryAccountUserName | string, el valor predeterminado es "". |nombre de usuario de los recursos compartidos de hello tooACL principal hello FileStoreService cuenta principal de Hola. |
| PrimaryAccountUserPassword | SecureString, el valor predeterminado es empty. |contraseña de la cuenta principal de Hola de Hola tooACL principal Hola FileStoreService comparte. |
| FileStoreService | PrimaryAccountNTLMPasswordSecret | SecureString, el valor predeterminado es empty. | secreto de contraseña de Hola que usa como valor de inicialización toogenerated misma contraseña cuando se usa la autenticación NTLM. |
| PrimaryAccountNTLMX509StoreLocation | string, el valor predeterminado es "LocalMachine".| ubicación del almacén de Hola de hello X509 certificado usado toogenerate HMAC en hello PrimaryAccountNTLMPasswordSecret cuando se usa la autenticación NTLM. |
| PrimaryAccountNTLMX509StoreName | string, el valor predeterminado es "MY".| nombre del almacén de Hola de hello X509 certificado usado toogenerate HMAC en hello PrimaryAccountNTLMPasswordSecret cuando se usa la autenticación NTLM. |
| PrimaryAccountNTLMX509Thumbprint | string, el valor predeterminado es "".|Hola huella digital del certificado usado toogenerate HMAC de hello X509 en hello PrimaryAccountNTLMPasswordSecret cuando se usa la autenticación NTLM. |
| SecondaryAccountType | string, el valor predeterminado es "".| Hola secundaria AccountType de Hola tooACL principal Hola FileStoreService comparte. |
| SecondaryAccountUserName | string, el valor predeterminado es "".| nombre de usuario de los recursos compartidos de hello tooACL principal hello FileStoreService cuenta secundaria de Hola. |
| SecondaryAccountUserPassword | SecureString, el valor predeterminado es empty. |contraseña de la cuenta secundaria de Hola de Hola tooACL principal Hola FileStoreService comparte.  |
| SecondaryAccountNTLMPasswordSecret | SecureString, el valor predeterminado es empty. | secreto de contraseña de Hola que usa como valor de inicialización toogenerated misma contraseña cuando se usa la autenticación NTLM. |
| SecondaryAccountNTLMX509StoreLocation | string, el valor predeterminado es "LocalMachine". |ubicación del almacén de Hola de hello X509 certificado usado toogenerate HMAC en hello SecondaryAccountNTLMPasswordSecret cuando se usa la autenticación NTLM. |
| SecondaryAccountNTLMX509StoreName | string, el valor predeterminado es "MY". |nombre del almacén de Hola de hello X509 certificado usado toogenerate HMAC en hello SecondaryAccountNTLMPasswordSecret cuando se usa la autenticación NTLM. |
| SecondaryAccountNTLMX509Thumbprint | string, el valor predeterminado es "".| Hola huella digital del certificado usado toogenerate HMAC de hello X509 en hello SecondaryAccountNTLMPasswordSecret cuando se usa la autenticación NTLM. |

### <a name="section-name-imagestoreservice"></a>Nombre de sección: ImageStoreService
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| Enabled |Bool, el valor predeterminado es false. |Hola marca habilitado para ImageStoreService. |
| TargetReplicaSetSize | Int, el valor predeterminado es 7. |Hola TargetReplicaSetSize para ImageStoreService. |
| MinReplicaSetSize | Int, el valor predeterminado es 3. |Hola MinReplicaSetSize para ImageStoreService. |
| ReplicaRestartWaitDuration | Tiempo en segundos, el valor predeterminado es 60.0 * 30. | Especifique el intervalo de tiempo en segundos. Hola ReplicaRestartWaitDuration para ImageStoreService. |
| QuorumLossWaitDuration | Tiempo en segundos, el valor predeterminado es MaxValue. | Especifique el intervalo de tiempo en segundos. Hola QuorumLossWaitDuration para ImageStoreService. |
| StandByReplicaKeepDuration | Tiempo en segundos, el valor predeterminado es 3600.0 * 2. | Especifique el intervalo de tiempo en segundos. Hola StandByReplicaKeepDuration para ImageStoreService. |
| PlacementConstraints | string, el valor predeterminado es "". | Hola PlacementConstraints para ImageStoreService. |
| ClientUploadTimeout | Tiempo en segundos, el valor predeterminado es 1800. |Especifique el intervalo de tiempo en segundos. Valor de tiempo de espera para la carga de nivel superior solicitar el servicio de almacenamiento de tooImage. |
| ClientCopyTimeout | Tiempo en segundos, el valor predeterminado es 1800. | Especifique el intervalo de tiempo en segundos. Valor de tiempo de espera para la copia de nivel superior solicitar el servicio de almacenamiento de tooImage. |
| ClientDownloadTimeout | Tiempo en segundos, el valor predeterminado es 1800. | Especifique el intervalo de tiempo en segundos. Valor de tiempo de espera de descarga de nivel superior solicitar el servicio de almacenamiento de tooImage |
| ClientListTimeout | Tiempo en segundos, el valor predeterminado es 600. | Especifique el intervalo de tiempo en segundos. Valor de tiempo de espera de la lista de nivel superior solicitar el servicio de almacenamiento de tooImage. |
| ClientDefaultTimeout | Tiempo en segundos, el valor predeterminado es 180. | Especifique el intervalo de tiempo en segundos. Valor de tiempo de espera para todas las solicitudes de no carga/no-descarga (por ejemplo, existe; eliminar) tooImage el servicio de almacenamiento. |

### <a name="section-name-imagestoreclient"></a>Nombre de sección: ImageStoreClient
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| ClientUploadTimeout |Tiempo en segundos, el valor predeterminado es 1800. | Especifique el intervalo de tiempo en segundos. Valor de tiempo de espera para la carga de nivel superior solicitar el servicio de almacenamiento de tooImage. |
| ClientCopyTimeout | Tiempo en segundos, el valor predeterminado es 1800. | Especifique el intervalo de tiempo en segundos. Valor de tiempo de espera para la copia de nivel superior solicitar el servicio de almacenamiento de tooImage. |
|ClientDownloadTimeout | Tiempo en segundos, el valor predeterminado es 1800. | Especifique el intervalo de tiempo en segundos. Valor de tiempo de espera de descarga de nivel superior solicitar el servicio de almacenamiento de tooImage. |
|ClientListTimeout | Tiempo en segundos, el valor predeterminado es 600. |Especifique el intervalo de tiempo en segundos. Valor de tiempo de espera de la lista de nivel superior solicitar el servicio de almacenamiento de tooImage. |
|ClientDefaultTimeout | Tiempo en segundos, el valor predeterminado es 180. | Especifique el intervalo de tiempo en segundos. Valor de tiempo de espera para todas las solicitudes de no carga/no-descarga (por ejemplo, existe; eliminar) tooImage el servicio de almacenamiento. |

### <a name="section-name-tokenvalidationservice"></a>Nombre de sección: TokenValidationService
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| Proveedores |string, el valor predeterminado es "DSTS". |Lista separada por comas de tooenable de proveedores de validación del token (proveedores válidos son: DSTS; AAD). Actualmente solo se puede habilitar un único proveedor cada vez. |

### <a name="section-name-upgradeorchestrationservice"></a>Nombre de sección: UpgradeOrchestrationService
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| TargetReplicaSetSize |Int, el valor predeterminado es 0. |Hola TargetReplicaSetSize para UpgradeOrchestrationService. |
| MinReplicaSetSize |Int, el valor predeterminado es 0. | Hola MinReplicaSetSize para UpgradeOrchestrationService.
| ReplicaRestartWaitDuration | Tiempo en segundos, el valor predeterminado es 60 minutos.| Especifique el intervalo de tiempo en segundos. Hola ReplicaRestartWaitDuration para UpgradeOrchestrationService. |
| QuorumLossWaitDuration | Tiempo en segundos, el valor predeterminado es MaxValue. | Especifique el intervalo de tiempo en segundos. Hola QuorumLossWaitDuration para UpgradeOrchestrationService. |
| StandByReplicaKeepDuration | Tiempo en segundos, el valor predeterminado es 60*24*7 minutos. | Especifique el intervalo de tiempo en segundos. Hola StandByReplicaKeepDuration para UpgradeOrchestrationService. |
| PlacementConstraints | string, el valor predeterminado es "". | Hola PlacementConstraints para UpgradeOrchestrationService. |
| AutoupgradeEnabled | Bool, el valor predeterminado es true. | Sondeo automático y acción de actualización basados en un archivo de estado de objetivo. |
| UpgradeApprovalRequired | Bool, el valor predeterminado es false. | Actualización del código toomake configuración requerir aprobación del administrador antes de continuar. |

### <a name="section-name-upgradeservice"></a>Nombre de sección: UpgradeService
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| PlacementConstraints |string, el valor predeterminado es "". |Hola PlacementConstraints para el servicio de actualización. |
| TargetReplicaSetSize | Int, el valor predeterminado es 3. | Hola TargetReplicaSetSize para UpgradeService. |
| MinReplicaSetSize | Int, el valor predeterminado es 2. | Hola MinReplicaSetSize para UpgradeService. |
| CoordinatorType | string, el valor predeterminado es "WUTest".| Hola CoordinatorType para UpgradeService. |
| BaseUrl | string, el valor predeterminado es "". |BaseUrl para UpgradeService. |
| ClusterId | string, el valor predeterminado es "". | ClusterId para UpgradeService. |
| X509StoreName | string, el valor predeterminado es "My".| X509StoreName para UpgradeService. |
| X509StoreLocation | string, el valor predeterminado es "". | X509StoreLocation para UpgradeService. |
| X509FindType | string, el valor predeterminado es "".| X509FindType para UpgradeService. |
| X509FindValue | string, el valor predeterminado es "". | X509FindValue para UpgradeService. |
| X509SecondaryFindValue | string, el valor predeterminado es "". | X509SecondaryFindValue para UpgradeService. |
| OnlyBaseUpgrade | Bool, el valor predeterminado es false. | OnlyBaseUpgrade para UpgradeService. |
| TestCabFolder | string, el valor predeterminado es "". | TestCabFolder para UpgradeService. |

### <a name="section-name-securityclientaccess"></a>Nombre de sección: Security/ClientAccess
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| CreateName |string, el valor predeterminado es "Admin". |Configuración de seguridad para la creación de URI de nomenclatura. |
| DeleteName |string, el valor predeterminado es "Admin". |Configuración de seguridad para la eliminación de URI de nomenclatura. |
| PropertyWriteBatch |string, el valor predeterminado es "Admin". |Configuración de seguridad para operaciones de escritura de la propiedad de nomenclatura. |
| CreateService |string, el valor predeterminado es "Admin". | Configuración de seguridad para la creación del servicio. |
| CreateServiceFromTemplate |string, el valor predeterminado es "Admin". |Configuración de seguridad para la creación de servicios a partir de una plantilla. |
| UpdateService |string, el valor predeterminado es "Admin". |Configuración de seguridad para actualizaciones de servicio. |
| DeleteService  |string, el valor predeterminado es "Admin". |Configuración de seguridad para eliminación de servicio. |
| ProvisionApplicationType |string, el valor predeterminado es "Admin". | Configuración de seguridad para aprovisionamiento de tipos de aplicaciones. |
| CreateApplication |string, el valor predeterminado es "Admin". | Configuración de seguridad para creación de aplicaciones. |
| DeleteApplication |string, el valor predeterminado es "Admin". | Configuración de seguridad para eliminación de aplicaciones. |
| UpgradeApplication |string, el valor predeterminado es "Admin". | Configuración de seguridad para iniciar o interrumpir actualizaciones de aplicaciones. |
| RollbackApplicationUpgrade |string, el valor predeterminado es "Admin". | Configuración de seguridad para revertir actualizaciones de aplicaciones. |
| UnprovisionApplicationType |string, el valor predeterminado es "Admin". | Configuración de seguridad para dejar de aprovisionar tipos de aplicación. |
| MoveNextUpgradeDomain |string, el valor predeterminado es "Admin". | Configuración de seguridad para reanudar actualizaciones de aplicaciones con un dominio de actualización explícito. |
| ReportUpgradeHealth |string, el valor predeterminado es "Admin". | Configuración de seguridad para reanudar las actualizaciones de aplicaciones con el progreso de la actualización actual Hola. |
| ReportHealth |string, el valor predeterminado es "Admin". | Configuración de seguridad para mantenimiento de informes. |
| ProvisionFabric |string, el valor predeterminado es "Admin". | Configuración de seguridad para aprovisionamiento de MSI o del manifiesto de clúster. |
| UpgradeFabric |string, el valor predeterminado es "Admin". | Configuración de seguridad para iniciar actualizaciones del clúster. |
| RollbackFabricUpgrade |string, el valor predeterminado es "Admin". | Configuración de seguridad para revertir actualizaciones del clúster. |
| UnprovisionFabric |string, el valor predeterminado es "Admin". | Configuración de seguridad para dejar de aprovisionar MSI o el manifiesto de clúster. |
| MoveNextFabricUpgradeDomain |string, el valor predeterminado es "Admin". | Configuración de seguridad para reanudar actualizaciones del clúster con un dominio de actualización explícito. |
| ReportFabricUpgradeHealth |string, el valor predeterminado es "Admin". | Configuración de seguridad para reanudar las actualizaciones de clúster con el progreso de la actualización actual Hola. |
| StartInfrastructureTask |string, el valor predeterminado es "Admin". | Configuración de seguridad para iniciar tareas de infraestructura. |
| FinishInfrastructureTask |string, el valor predeterminado es "Admin". | Configuración de seguridad para finalizar tareas de infraestructura. |
| ActivateNode |string, el valor predeterminado es "Admin". | Configuración de seguridad para activación de un nodo. |
| DeactivateNode |string, el valor predeterminado es "Admin". | Configuración de seguridad para desactivación de un nodo. |
| DeactivateNodesBatch |string, el valor predeterminado es "Admin". | Configuración de seguridad para desactivación de varios nodos. |
| RemoveNodeDeactivations |string, el valor predeterminado es "Admin". | Configuración de seguridad para revertir la desactivación en varios nodos. |
| GetNodeDeactivationStatus |string, el valor predeterminado es "Admin". | Configuración de seguridad para comprobar el estado de desactivación. |
| NodeStateRemoved |string, el valor predeterminado es "Admin". | Configuración de seguridad para notificar el estado quitado del nodo. |
| RecoverPartition |string, el valor predeterminado es "Admin". | Configuración de seguridad recuperar una partición. |
| RecoverPartitions |string, el valor predeterminado es "Admin". | Configuración de seguridad para recuperar particiones. |
| RecoverServicePartitions |string, el valor predeterminado es "Admin". | Configuración de seguridad para recuperar particiones de servicio. |
| RecoverSystemPartitions |string, el valor predeterminado es "Admin". | Configuración de seguridad para recuperar particiones de servicio del sistema. |
| ReportFault |string, el valor predeterminado es "Admin". | Configuración de seguridad para informes de error. |
| InvokeInfrastructureCommand |string, el valor predeterminado es "Admin". | Configuración de seguridad para comandos de administración de tareas de infraestructura. |
| FileContent |string, el valor predeterminado es "Admin". | Transferencia de archivos de cliente (toocluster externo) del almacén de configuración de seguridad de imagen. |
| FileDownload |string, el valor predeterminado es "Admin". | Configuración de seguridad para inicio de descarga (toocluster externo) para el archivo de cliente de almacén de imagen de. |
| InternalList |string, el valor predeterminado es "Admin". | Configuración de seguridad para operación de lista de archivos de cliente del almacén de imágenes (interno). |
| Eliminar |string, el valor predeterminado es "Admin". | Configuración de seguridad para operación de eliminación del cliente del almacén de imágenes. |
| Cargar |string, el valor predeterminado es "Admin". | Configuración de seguridad para operación de carga del cliente del almacén de imágenes. |
| GetStagingLocation |string, el valor predeterminado es "Admin". | Configuración de seguridad para recuperación de la ubicación de almacenamiento temporal del cliente del almacén de imágenes. |
| GetStoreLocation |string, el valor predeterminado es "Admin". | Configuración de seguridad para recuperación de la ubicación del almacén de clientes del almacén de imágenes. |
| NodeControl |string, el valor predeterminado es "Admin". | Configuración de seguridad para inicio, detención y reinicio de nodos. |
| CodePackageControl |string, el valor predeterminado es "Admin". | Configuración de seguridad para reiniciar paquetes de código. |
| UnreliableTransportControl |string, el valor predeterminado es "Admin". | Transporte no confiable para agregar y quitar comportamientos. |
| MoveReplicaControl |string, el valor predeterminado es "Admin". | Mueva la réplica. |
| PredeployPackageToNode |string, el valor predeterminado es "Admin". | API previas a la implementación. |
| StartPartitionDataLoss |string, el valor predeterminado es "Admin". | Provoca la pérdida de datos en una partición. |
| StartPartitionQuorumLoss |string, el valor predeterminado es "Admin". | Provoca la pérdida de cuórum en una partición. |
| StartPartitionRestart |string, el valor predeterminado es "Admin". | Reinicia simultáneamente algunas o todas las réplicas de Hola de una partición. |
| CancelTestCommand |string, el valor predeterminado es "Admin". | Cancela un comando de prueba específico, si se está ejecutando. |
| StartChaos |string, el valor predeterminado es "Admin". | Inicia Chaos, si no se ha iniciado. |
| StopChaos |string, el valor predeterminado es "Admin". | Detiene Chaos, si se ha iniciado. |
| StartNodeTransition |string, el valor predeterminado es "Admin". | Configuración de seguridad para iniciar una transición de nodo. |
| StartClusterConfigurationUpgrade |string, el valor predeterminado es "Admin". | Produce StartClusterConfigurationUpgrade en una partición. |
| GetUpgradesPendingApproval |string, el valor predeterminado es "Admin". | Produce GetUpgradesPendingApproval en una partición. |
| StartApprovedUpgrades |string, el valor predeterminado es "Admin". | Produce StartApprovedUpgrades en una partición. |
| Ping |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para pings de cliente. |
| Consultar |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para consultas. |
| NameExists |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para comprobaciones de existencia de URI de nomenclatura. |
| EnumerateSubnames |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para enumeración de URI de nomenclatura. |
| EnumerateProperties |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para enumeración de propiedad de nomenclatura. |
| PropertyReadBatch |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para operaciones de lectura de propiedad de nomenclatura. |
| GetServiceDescription |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para notificaciones de servicio de sondeo largo y descripciones de servicio de lectura. |
| ResolveService |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para resolución de servicio basada en reclamaciones. |
| ResolveNameOwner |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para resolver propietario de URI de nomenclatura. |
| ResolvePartition |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para resolver servicios del sistema. |
| ServiceNotifications |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para notificaciones del servicio basadas en eventos. |
| PrefixResolveService |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para resolución de prefijo de servicio basada en reclamaciones. |
| GetUpgradeStatus |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para sondeo de estado de actualización de aplicaciones. |
| GetFabricUpgradeStatus |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para sondeo de estado de actualización del clúster. |
| InvokeInfrastructureQuery |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para consultar tareas de infraestructura. |
| Enumerar |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para operación de lista de archivos de cliente del almacén de imágenes. |
| ResetPartitionLoad |string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para restablecer una carga para una unidad de conmutación por error. |
| ToggleVerboseServicePlacementHealthReporting | string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para alternar informes de mantenimiento detallados de ubicación de servicio. |
| GetPartitionDataLossProgress | string, el valor predeterminado es "Admin\.|\|User" | Captura el progreso de Hola para una llamada de api de pérdida de datos de invocación. |
| GetPartitionQuorumLossProgress | string, el valor predeterminado es "Admin\.|\|User" | Captura el progreso de Hola para una llamada de api de pérdida de quórum de invoke. |
| GetPartitionRestartProgress | string, el valor predeterminado es "Admin\.|\|User" | Captura el progreso de Hola para una llamada de api de la partición de reinicio. |
| GetChaosReport | string, el valor predeterminado es "Admin\.|\|User" | Captura el estado de Hola de caos dentro de un intervalo de tiempo determinado. |
| GetNodeTransitionProgress | string, el valor predeterminado es "Admin\.|\|User" | Configuración de seguridad para obtener el progreso en un comando de transición de nodo. |
| GetClusterConfigurationUpgradeStatus | string, el valor predeterminado es "Admin\.|\|User" | Produce GetClusterConfigurationUpgradeStatus en una partición. |
| GetClusterConfiguration | string, el valor predeterminado es "Admin\.|\|User" | Produce GetClusterConfiguration en una partición. |

### <a name="section-name-reconfigurationagent"></a>Nombre de sección: ReconfigurationAgent
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| ApplicationUpgradeMaxReplicaCloseDuration | Tiempo en segundos, el valor predeterminado es 900. |Especifique el intervalo de tiempo en segundos. duración de Hola por qué Hola sistema esperará antes de terminar de hosts de servicio que tengan réplicas que están bloqueadas en Cerrar. |
| ServiceApiHealthDuration | Tiempo en segundos, el valor predeterminado es 30 minutos. | Especifique el intervalo de tiempo en segundos. ServiceApiHealthDuration define cuánto tiempo se espere una toorun de API de servicio antes de que se informe incorrecto. |
| ServiceReconfigurationApiHealthDuration | Tiempo en segundos, el valor predeterminado es 30. | Especifique el intervalo de tiempo en segundos. ServiceReconfigurationApiHealthDuration define cuánto tiempo Hola antes de un servicio en la reconfiguración notifica como incorrecto. |
| PeriodicApiSlowTraceInterval | Tiempo en segundos, el valor predeterminado es 5 minutos. | Especifique el intervalo de tiempo en segundos. PeriodicApiSlowTraceInterval define el intervalo de saludo sobre el que se se redibuja lenta llamadas de API por el monitor de la API de Hola. |
| NodeDeactivationMaxReplicaCloseDuration | Tiempo en segundos, el valor predeterminado es 900. | Especifique el intervalo de tiempo en segundos. Hola toowait tiempo máximo antes de terminar un host de servicio que está bloqueando la desactivación de nodo. |
| FabricUpgradeMaxReplicaCloseDuration | Tiempo en segundos, el valor predeterminado es 900. | Especifique el intervalo de tiempo en segundos. RA de duración máxima de Hello esperará antes de terminar el host del servicio de réplica que no se está cerrando. |
| IsDeactivationInfoEnabled | Bool, el valor predeterminado es true. | Determina si RA utiliza información de desactivación para llevar a cabo elecciones nuevo principal para los clústeres nuevo esta configuración debe establecerse tootrue para clústeres existentes que se están actualizando, consulte las notas de la versión de Hola acerca de cómo tooenable esto. |

### <a name="section-name-placementandloadbalancing"></a>Nombre de sección: PlacementAndLoadBalancing
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| TraceCRMReasons |Bool, el valor predeterminado es true. |Especifica si tootrace motivos para CRM emitió canal de movimientos toohello eventos operativos. |
| ValidatePlacementConstraint | Bool, el valor predeterminado es true. | Especifica si no se valida hello PlacementConstraint expresión para un servicio cuando se actualiza ServiceDescription un servicio. |
| PlacementConstraintValidationCacheSize | Int, el valor predeterminado es 10 000. | Hola a límites de tamaño de tabla de hello utilizado para la validación rápida y almacenamiento en caché de expresiones de restricción de selección de ubicación. |
|VerboseHealthReportLimit | Int, el valor predeterminado es 20. | Define Hola número de veces que una réplica tiene toogo sin colocar antes de que se emite una advertencia de estado para ella (si el informe de estado detallado está habilitado). |
|ConstraintViolationHealthReportLimit | Int, el valor predeterminado es 50. | Define el número de hello tiempo restricción infringiendo réplica toobe de forma persistente sin corregir antes de que se llevan a cabo diagnósticos y se emiten los informes de mantenimiento de datos. |
|DetailedConstraintViolationHealthReportLimit | Int, el valor predeterminado es 200. | Define el número de Hola de tiempos de restricción infringiendo réplica tiene toobe forma persistente sin corregir antes de que se llevan a cabo diagnósticos y se emiten los informes de estado detallada. |
|DetailedVerboseHealthReportLimit | Int, el valor predeterminado es 200. | Define Hola número de veces que una réplica sin colocar tiene toobe forma persistente sin colocar antes de que se emiten los informes de estado detallada. |
|ConsecutiveDroppedMovementsHealthReportLimit | Int, el valor predeterminado es 20. | Define el número de Hola de veces consecutivas que emitió ResourceBalancer movimientos se quitan antes de que se llevan a cabo diagnósticos y se emiten advertencias de mantenimiento. Negativo: no se emiten advertencias bajo esta condición. |
|DetailedNodeListLimit | Int, el valor predeterminado es 15. | Define el número de Hola de nodos por restricción tooinclude antes de truncamiento en hello que informa de réplica sin colocar. |
|DetailedPartitionListLimit | Int, el valor predeterminado es 15. | Define el número de Hola de particiones por cada entrada de diagnóstico para un tooinclude restricción antes de truncamiento de diagnóstico. |
|DetailedDiagnosticsInfoListLimit | Int, el valor predeterminado es 15. | Define el número de Hola de entradas de diagnósticos (con información detallada) por restricción tooinclude antes de truncamiento en los diagnósticos.|
|PLBRefreshGap | Tiempo en segundos, el valor predeterminado es 1. | Especifique el intervalo de tiempo en segundos. Define la cantidad mínima de Hola de tiempo que debe transcurrir antes de PLB actualiza el estado de nuevo. |
|MinPlacementInterval | Tiempo en segundos, el valor predeterminado es 1. | Especifique el intervalo de tiempo en segundos. Define la cantidad mínima de Hola de tiempo que debe transcurrir antes de dos ciclos de selección de ubicación consecutivos. |
|MinConstraintCheckInterval | Tiempo en segundos, el valor predeterminado es 1. | Especifique el intervalo de tiempo en segundos. Define la cantidad mínima de Hola de tiempo que debe transcurrir antes de que dos restricción consecutivos protejan ciclos. |
|MinLoadBalancingInterval | Tiempo en segundos, el valor predeterminado es 5. | Especifique el intervalo de tiempo en segundos. Define la cantidad mínima de Hola de tiempo que debe transcurrir antes de dos ciclos de equilibrio consecutivos. |
|BalancingDelayAfterNodeDown | Tiempo en segundos, el valor predeterminado es 120. |Especifique el intervalo de tiempo en segundos. No inicie actividades de equilibrio dentro de este período después de un evento de inactividad de nodos. |
|BalancingDelayAfterNewNode | Tiempo en segundos, el valor predeterminado es 120. |Especifique el intervalo de tiempo en segundos. No inicie actividades de equilibrio dentro de este período después de agregar un nuevo nodo. |
|ConstraintFixPartialDelayAfterNodeDown | Tiempo en segundos, el valor predeterminado es 120. | Especifique el intervalo de tiempo en segundos. No resuelva infracciones FaultDomain y UpgradeDomain dentro de este período después de un evento de inactividad de nodos. |
|ConstraintFixPartialDelayAfterNewNode | Tiempo en segundos, el valor predeterminado es 120. | Especifique el intervalo de tiempo en segundos. No resuelva infracciones de restricciones FaultDomain y UpgradeDomain dentro de este período después de agregar un nuevo nodo. |
|GlobalMovementThrottleThreshold | Uint, el valor predeterminado es 1000. | Número máximo de movimientos permitidos en Hola fase equilibrio en hello último intervalo indicado por GlobalMovementThrottleCountingInterval. |
|GlobalMovementThrottleThresholdForPlacement | Uint, el valor predeterminado es 0. | Número máximo de movimientos permite en fase de selección de ubicación Hola último intervalo indicado por GlobalMovementThrottleCountingInterval.0 indica sin límite.|
|GlobalMovementThrottleThresholdForBalancing | Uint, el valor predeterminado es 0. | Número máximo de movimientos permitidos en fase de equilibrio en hello último intervalo indicado por GlobalMovementThrottleCountingInterval. 0 indica sin límite. |
|GlobalMovementThrottleCountingInterval | Tiempo en segundos, el valor predeterminado es 600. | Especifique el intervalo de tiempo en segundos. Indicar longitud Hola de hello más allá del intervalo de qué tootrack por movimientos de réplica de dominio (que se usa junto con GlobalMovementThrottleThreshold). Se puede establecer too0 tooignore global limitación por completo. |
|MovementPerPartitionThrottleThreshold | Uint, el valor predeterminado es 50. | Sin equilibrio relacionados con movimiento tendrá lugar para una partición si el número de Hola de equilibrio de movimientos relacionados para las réplicas de esa partición ha alcanzado o superado MovementPerFailoverUnitThrottleThreshold Hola últimos intervalo indicado por MovementPerPartitionThrottleCountingInterval. |
|MovementPerPartitionThrottleCountingInterval | Tiempo en segundos, el valor predeterminado es 600. | Especifique el intervalo de tiempo en segundos. Indicar longitud Hola de hello más allá del intervalo de los movimientos de la réplica de tootrack para cada partición (que se usa junto con MovementPerPartitionThrottleThreshold). |
|PlacementSearchTimeout | Tiempo en segundos, el valor predeterminado es 0.5. | Especifique el intervalo de tiempo en segundos. Al ubicar servicios, busque como máximo este período antes de devolver un resultado. |
|UseMoveCostReports | Bool, el valor predeterminado es false. | Indica al elemento de costo de hello LB tooignore Hola de hello función; de puntuación número potencialmente grande de movimientos para la mejor ubicación equilibrada resultante. |
|PreventTransientOvercommit | Bool, el valor predeterminado es false. | Determina debe PLB contar inmediatamente en los recursos que se liberarán por movimientos de hello iniciado. De forma predeterminada; PLB puede iniciar el movimiento out y pase hello sobrecargar el mismo nodo que puede crear transitorio. Configuración evitará que este parámetro tootrue los tipo de overcommits y se deshabilitará la desfragmentación de petición (también conocido como placementWithMove). |
|InBuildThrottlingEnabled | Bool, el valor predeterminado es false. | Determinar si está habilitada la limitación de hello en compilación. |
|InBuildThrottlingAssociatedMetric | string, el valor predeterminado es "". | Hola había asociado nombre de la métrica de esta limitación. |
|InBuildThrottlingGlobalMaxValue | Int, el valor predeterminado es 0. |número máximo de Hola de réplicas de la compilación de permiten globalmente. |
|SwapPrimaryThrottlingEnabled | Bool, el valor predeterminado es false.| Determinar si está habilitada la limitación principal de intercambio de Hola. |
|SwapPrimaryThrottlingAssociatedMetric | string, el valor predeterminado es "".| Hola había asociado nombre de la métrica de esta limitación. |
|SwapPrimaryThrottlingGlobalMaxValue | Int, el valor predeterminado es 0. | número máximo de Hola de réplicas de intercambio principal permitida globalmente. |
|PlacementConstraintPriority | Int, el valor predeterminado es 0. | Determina la prioridad de Hola de restricción de selección de ubicación: 0: disco duro; 1: software; negativo: pasar por alto. |
|PreferredLocationConstraintPriority | Int, el valor predeterminado es 2.| Determina la prioridad de Hola de restricción de ubicación preferida: 0: disco duro; 1: software; 2: optimización; negativo: pasar por alto |
|CapacityConstraintPriority | Int, el valor predeterminado es 0. | Determina la prioridad de Hola de restricción de capacidad: 0: disco duro; 1: software; negativo: pasar por alto. |
|AffinityConstraintPriority | Int, el valor predeterminado es 0. | Determina la prioridad de Hola de restricción de afinidad: 0: disco duro; 1: software; negativo: pasar por alto. |
|FaultDomainConstraintPriority | Int, el valor predeterminado es 0. | Determina la prioridad de Hola de restricción de dominio de error: 0: disco duro; 1: software; negativo: pasar por alto. |
|UpgradeDomainConstraintPriority | Int, el valor predeterminado es 1.| Determina la prioridad de Hola de restricción de dominio de actualización: 0: disco duro; 1: software; negativo: pasar por alto. |
|ScaleoutCountConstraintPriority | Int, el valor predeterminado es 0. | Determina la prioridad de Hola de restricción de recuento de ampliación: 0: disco duro; 1: software; negativo: pasar por alto. |
|ApplicationCapacityConstraintPriority | Int, el valor predeterminado es 0. | Determina la prioridad de Hola de restricción de capacidad: 0: disco duro; 1: software; negativo: pasar por alto. |
|MoveParentToFixAffinityViolation | Bool, el valor predeterminado es false. | Configuración que determina si las réplicas primaria pueden ser movido toofix restricciones de afinidad.|
|MoveExistingReplicaForPlacement | Bool, el valor predeterminado es true. |Configuración que determina si toomove réplica existente durante la selección. |
|UseSeparateSecondaryLoad | Bool, el valor predeterminado es true. | Valor que determina si se deben usar cargas secundarias diferentes. |
|PlaceChildWithoutParent | Bool, el valor predeterminado es true. | Valor que determina si puede colocarse la réplica de servicio secundaria si no hay ninguna réplica principal activa. |
|PartiallyPlaceServices | Bool, el valor predeterminado es true. | Determina si todas las réplicas de servicio del clúster se colocarán "todo o nada" dados los nodos adecuados limitados para ellas.|
|InterruptBalancingForAllFailoverUnitUpdates | Bool, el valor predeterminado es false. | Determina si cualquier tipo de actualización de las unidades de conmutación por error debe interrumpir la ejecución rápida o lenta del equilibrio. Si se especifica "false", la ejecución del equilibrio se interrumpirá si FailoverUnit: se crea o elimina, tiene réplicas que faltan, ha cambiado la ubicación de la réplica principal o ha cambiado el número de réplicas. La ejecución del equilibrio NO se interrumpirá en otros casos: si FailoverUnit: tiene réplicas adicionales, ha cambiado cualquier marca de réplica, ha cambiado solo la versión de partición o en cualquier otro caso. |

### <a name="section-name-security"></a>Nombre de sección: Seguridad
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| ClusterProtectionLevel |Ninguno o EncryptAndSign |Ninguno (valor predeterminado) para clústeres no seguros, EncryptAndSign para clústeres seguros. |

### <a name="section-name-hosting"></a>Nombre de sección: Hospedaje
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| ServiceTypeRegistrationTimeout |Tiempo en segundos, el valor predeterminado es 300. |Tiempo máximo permitido para hello ServiceType toobe registrado con el tejido |
| ServiceTypeDisableFailureThreshold |Número entero, el valor predeterminado es 1. |Éste es el umbral de Hola para hello recuento de errores después del cual FailoverManager (FM) es una notificación toodisable el tipo de servicio de hello en ese nodo y pruebe un nodo diferente para la ubicación. |
| ActivationRetryBackoffInterval |Tiempo en segundos, el valor predeterminado es 5. |Intervalo de interrupción en cada caso de error de activación; En cada caso de error de activación continua, reintentos de sistema de Hola Hola activación para la toohello MaxActivationFailureCount. intervalo de reintento de Hello en cada intento es un producto de activación continua hello y error retroceso intervalo de activación. |
| ActivationMaxRetryInterval |Tiempo en segundos, el valor predeterminado es 300. |En cada caso de error de activación continua, reintentos de sistema de Hola Hola activación para la tooActivationMaxFailureCount. ActivationMaxRetryInterval especifica el intervalo de tiempo de espera antes de un reintento después de cada error de activación. |
| ActivationMaxFailureCount |Número entero, el valor predeterminado es 10. |Número de veces que los reintentos del sistema no lograron la activación antes de desistir. |

### <a name="section-name-failovermanager"></a>Nombre de sección: FailoverManager
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| PeriodicLoadPersistInterval |Tiempo en segundos, el valor predeterminado es 10 |Esto determina con qué frecuencia Hola comprobación FM para los informes nuevos de carga |

### <a name="section-name-federation"></a>Nombre de sección: Federación
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| LeaseDuration |Tiempo en segundos, el valor predeterminado es 30. |Duración de una concesión entre un nodo y sus vecinos. |
| LeaseDurationAcrossFaultDomain |Tiempo en segundos, el valor predeterminado es 30. |Duración de una concesión entre un nodo y sus vecinos entre dominios de error. |

### <a name="section-name-clustermanager"></a>Nombre de sección: ClusterManager
| **Parámetro** | **Valores permitidos** | **Orientación o breve descripción** |
| --- | --- | --- |
| UpgradeStatusPollInterval |Tiempo en segundos, el valor predeterminado es 60. |frecuencia de Hola de sondeo de estado de actualización de la aplicación. Este valor determina la velocidad de Hola de actualización para cualquier llamada GetApplicationUpgradeProgress |
| UpgradeHealthCheckInterval |Tiempo en segundos, el valor predeterminado es 60. |frecuencia de Hello del estado de mantenimiento comprueba durante las actualizaciones de una de las aplicaciones supervisadas |
| FabricUpgradeStatusPollInterval |Tiempo en segundos, el valor predeterminado es 60. |frecuencia de Hola de sondeo de estado de actualización de Fabric. Este valor determina la velocidad de Hola de actualización para cualquier llamada GetFabricUpgradeProgress |
| FabricUpgradeHealthCheckInterval |Tiempo en segundos, el valor predeterminado es 60. |frecuencia de Hola de comprobación de estado de mantenimiento durante una actualización de Fabric supervisada |
|InfrastructureTaskProcessingInterval | Tiempo en segundos, el valor predeterminado es 10 |Especifique el intervalo de tiempo en segundos. intervalo de procesamiento de Hello usado por máquina de Estados de procesamiento de la tarea de infraestructura de Hola. |
|TargetReplicaSetSize |Int, el valor predeterminado es 7. |Hola TargetReplicaSetSize para ClusterManager. |
|MinReplicaSetSize |Int, el valor predeterminado es 3. |Hola MinReplicaSetSize para ClusterManager. |
|ReplicaRestartWaitDuration |Tiempo en segundos, el valor predeterminado es (60.0 * 30).|Especifique el intervalo de tiempo en segundos. Hola ReplicaRestartWaitDuration para ClusterManager. |
|QuorumLossWaitDuration |Tiempo en segundos, el valor predeterminado es MaxValue. | Especifique el intervalo de tiempo en segundos. Hola QuorumLossWaitDuration para ClusterManager. |
|StandByReplicaKeepDuration | Tiempo en segundos, el valor predeterminado es (3600.0 * 2).|Especifique el intervalo de tiempo en segundos. Hola StandByReplicaKeepDuration para ClusterManager. |
|PlacementConstraints | string, el valor predeterminado es "". |Hola PlacementConstraints para ClusterManager. |
|SkipRollbackUpdateDefaultService | Bool, el valor predeterminado es false. |Hola CM omitirá la reversión servicios predeterminado actualizado durante la reversión de actualización de aplicación. |
|EnableDefaultServicesUpgrade | Bool, el valor predeterminado es false. |Habilita la actualización de servicios predeterminados durante la actualización de aplicaciones. Las descripciones de servicios predeterminados se deben sobrescribir después de la actualización. |
|InfrastructureTaskHealthCheckWaitDuration |Tiempo en segundos, el valor predeterminado es 0.| Especifique el intervalo de tiempo en segundos. cantidad de Hola de toowait de tiempo antes de iniciar las comprobaciones de mantenimiento después de una tarea de la infraestructura de posprocesamiento. |
|InfrastructureTaskHealthCheckStableDuration | Tiempo en segundos, el valor predeterminado es 0.| Especifique el intervalo de tiempo en segundos. cantidad de Hola de mantenimiento ha pasado de hora tooobserve consecutivos comprueba antes de que el procesamiento posterior a la de una tarea de infraestructura finalice correctamente. Al observarse una comprobación de mantenimiento con error, se restablecerá este temporizador. |
|InfrastructureTaskHealthCheckRetryTimeout | Tiempo en segundos, el valor predeterminado es 60. |Especifique el intervalo de tiempo en segundos. cantidad de Hola de toospend tiempo reintentar las comprobaciones de mantenimiento con error durante el procesamiento posterior a la de una tarea de infraestructura. Al observarse una comprobación de mantenimiento pasada, se restablecerá este temporizador. |
|ImageBuilderTimeoutBuffer |Tiempo en segundos, el valor predeterminado es 3. |Especifique el intervalo de tiempo en segundos. cantidad de Hola de tooallow de tiempo para el cliente toohello tooreturn de Image Builder tiempo de espera concreto errores. Si este búfer es demasiado pequeño; a continuación, Hola caduca antes de que el servidor de Hola y obtiene un error genérico de tiempo de espera. |
|MinOperationTimeout | Tiempo en segundos, el valor predeterminado es 60. |Especifique el intervalo de tiempo en segundos. Hola mínimo tiempo de espera global para las operaciones de ClusterManager de procesamiento internamente. |
|MaxOperationTimeout |Tiempo en segundos, el valor predeterminado es MaxValue. | Especifique el intervalo de tiempo en segundos. Hola global tiempo de espera máximo para las operaciones de ClusterManager de procesamiento internamente. |
|MaxTimeoutRetryBuffer | Tiempo en segundos, el valor predeterminado es 600. |Especifique el intervalo de tiempo en segundos. Hola tiempo de espera de operación máximo al reintentar internamente a pagar es tootimeouts <Original Timeout>  +  <MaxTimeoutRetryBuffer>. El tiempo de espera adicional se agrega en incrementos de MinOperationTimeout. |
|MaxCommunicationTimeout |Tiempo en segundos, el valor predeterminado es 600. |Especifique el intervalo de tiempo en segundos. Hola tiempo de espera máximo para la comunicación interna entre ClusterManager y otros servicios del sistema (es decir, Servicio de nombres; El Administrador de conmutación por error y etcetera). Este tiempo de espera debe ser inferior al valor global de MaxOperationTimeout (ya que podría haber muchas comunicaciones entre los componentes del sistema para cada operación de cliente). |
|MaxDataMigrationTimeout |Tiempo en segundos, el valor predeterminado es 600. |Especifique el intervalo de tiempo en segundos. Hola tiempo de espera máximo para las operaciones de recuperación de migración de datos después de que ha llevado a cabo una actualización de Fabric. |
|MaxOperationRetryDelay |Tiempo en segundos, el valor predeterminado es 5.| Especifique el intervalo de tiempo en segundos. retraso máximo de Hola para reintentos internos cuando se producen errores. |
|ReplicaSetCheckTimeoutRollbackOverride |Tiempo en segundos, el valor predeterminado es 1200. | Especifique el intervalo de tiempo en segundos. Si ReplicaSetCheckTimeout se establece el valor máximo de toohello de DWORD; a continuación, que se invalide con el valor de Hola de esta configuración para los fines de Hola de reversión. nunca se invalida el valor de Hello utilizado para puesta al día. |
|ImageBuilderJobQueueThrottle |Int, el valor predeterminado es 10. |Limitación de recuento de subprocesos para la cola de trabajo del proxy de Image Builder en solicitudes de aplicación. |

## <a name="next-steps"></a>Pasos siguientes
Lea estos artículos para más información sobre la administración de clúster:

[Agregar o quitar certificados del clúster de Azure ](service-fabric-cluster-security-update-certs-azure.md) 


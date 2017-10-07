---
title: "configuración de ReliableDictionaryActorStateProvider aaaChange en Azure microservicios | Documentos de Microsoft"
description: "Obtenga información sobre cómo configurar los actores con estado de Azure Service Fabric del tipo ReliableDictionaryActorStateProvider."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: 79b48ffa-2474-4f1c-a857-3471f9590ded
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 44c85a41c90a17669ba874401d7921c94e7be9ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--reliabledictionaryactorstateprovider"></a>Configuración de Reliable Actors: ReliableDictionaryActorStateProvider
Puede modificar configuración predeterminada de Hola de ReliableDictionaryActorStateProvider cambiando hello settings.xml archivo generado en la raíz del paquete de Visual Studio hello en carpeta de configuración de hello para el actor especificado Hola.

en tiempo de ejecución de Hello Azure Service Fabric busca nombres de sección predefinida en el archivo de hello settings.xml y consume los valores de configuración de Hola durante la creación de hello subyacente componentes en tiempo de ejecución.

> [!NOTE]
> Hacer **no** eliminar o modificar los nombres de sección de Hola de hello siguiendo configuraciones en el archivo settings.xml hello que se genera en hello solución de Visual Studio.
> 
> 

También hay una configuración global que afecta a la configuración de Hola de ReliableDictionaryActorStateProvider.

## <a name="global-configuration"></a>Configuración global
configuración global de Hola se especifica en el manifiesto de clúster de Hola de clúster de hello en hello KtlLogger sección. Permite la configuración de Hola compartida ubicación y tamaño más Hola memoria global límites del registro utilizado por el registrador de Hola. Tenga en cuenta que los cambios en el manifiesto de clúster de hello afectan a todos los servicios que utilizan ReliableDictionaryActorStateProvider y servicios con estado confiables.

manifiesto de clúster de Hello es un único archivo XML que contiene la configuración y las configuraciones que se aplican tooall nodos y los servicios en clúster de Hola. archivo Hello normalmente se denomina ClusterManifest.xml. Puede ver manifiesto de clúster de hello para el clúster mediante comandos de powershell de hello ServiceFabricClusterManifest Get.

### <a name="configuration-names"></a>Nombres de configuración
| Nombre | Unidad | Valor predeterminado | Comentarios |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |Kilobytes |8388608 |Número mínimo de tooallocate KB en modo de kernel para el registrador de hello escribir bloque de memoria de búfer. Este bloque de memoria se utiliza para almacenar en caché información de estado antes de escribir toodisk. |
| WriteBufferMemoryPoolMaximumInKB |Kilobytes |Ilimitado |Bloque de memoria del búfer de escritura de tamaño máximo toowhich Hola registrador puede crecer. |
| SharedLogId |GUID |"" |Especifica un toouse GUID único para identificar el archivo hello predeterminado de registro compartido usado por todos los servicios de confianza en todos los nodos de clúster de Hola que no especifican hello SharedLogId en su configuración específica del servicio. Si se especifica SharedLogId, también se debe especificar SharedLogPath. |
| SharedLogPath |Nombre de ruta de acceso completo |"" |Especifica la ruta de acceso completa de Hola donde hello comparte el archivo de registro usado por todos los servicios de confianza en todos los nodos de clúster de Hola que no especifican hello SharedLogPath en su configuración específica del servicio. Sin embargo, si se especifica SharedLogPath, también se debe especificar SharedLogId. |
| SharedLogSizeInMB |Megabytes |8192 |Especifica el número de Hola de MB de espacio en disco toostatically asignar para registro de hello compartido. valor de Hello debe ser 2048 o superior. |

### <a name="sample-cluster-manifest-section"></a>Ejemplo de sección de manifiesto de clúster
```xml
   <Section Name="KtlLogger">
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
     <Parameter Name="SharedLogSizeInMB" Value="16383"/>
   </Section>
```

### <a name="remarks"></a>Comentarios
registrador de Hello tiene un grupo global de la memoria asignada de memoria del núcleo no paginada que proporciona servicios de confianza tooall disponible en un nodo para almacenar en caché datos de estado antes de que se escriban toohello registro dedicados asociado con la réplica de un servicio confiable de Hola. tamaño del grupo de Hola se controla mediante hello WriteBufferMemoryPoolMinimumInKB y la configuración de WriteBufferMemoryPoolMaximumInKB. WriteBufferMemoryPoolMinimumInKB especifica ambos Hola tamaño inicial de este bloque de memoria y el bloque de hello menor tamaño toowhich hello memoria puede reducir. WriteBufferMemoryPoolMaximumInKB es el bloque de hello mayor tamaño toowhich hello memoria puede alcanzar. Cada réplica de un servicio confiable que está abierto puede aumentar el tamaño de Hola de bloque de memoria de Hola por una cantidad de sistema determinada la tooWriteBufferMemoryPoolMaximumInKB. Si no hay más demanda de memoria de bloque de memoria de Hola que está disponible, las solicitudes de memoria se retrasará hasta que haya memoria disponible. Por lo tanto, si el bloque de memoria de búfer de escritura de hello es demasiado pequeño para una configuración concreta, a continuación, rendimiento puede verse afectado.

configuraciones de SharedLogId y SharedLogPath de Hola siempre son utilizados toodefine juntos Hola GUID y ubicación predeterminada de hello comparte registros para todos los nodos de clúster de Hola. registro de Hello predeterminado compartido se utiliza para todos los servicios de confianza que no se especifican los valores de hello en hello settings.xml servicio concreto de Hola. Para obtener el mejor rendimiento, compartido archivos de registro deben colocarse en discos que se usan únicamente para la contención de tooreduce del archivo de registro de hello compartido.

SharedLogSizeInMB especifica la cantidad de Hola de toopreallocate de espacio en disco para registro de hello predeterminado compartido en todos los nodos.  No es necesario SharedLogId y SharedLogPath toobe especificado en el orden de toobe SharedLogSizeInMB especificado.

## <a name="replicator-security-configuration"></a>Configuración de seguridad del replicador
Las configuraciones de seguridad de Replicador son canal de comunicación de hello toosecure utilizado que se usa durante la replicación. Esto significa que los servicios no pueden ver el tráfico de replicación de todas las demás, datos hello asegurar que ofrezca alta disponibilidad también están seguras.
De forma predeterminada, una sección de configuración de seguridad vacía impide la seguridad de la replicación.

### <a name="section-name"></a>Nombre de sección
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Configuración de replicador
Las configuraciones de Replicador son Replicador de hello tooconfigure utilizado que se encarga de hacer que sea el estado del proveedor de estado de Actor Hola altamente confiable replicar y conservar el estado de hello localmente.
configuración predeterminada de Hello generado por la plantilla de Visual Studio de Hola y debe ser suficiente. Esta sección trata sobre las configuraciones adicionales que están disponibles tootune Replicador de Hola.

### <a name="section-name"></a>Nombre de sección
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Nombres de configuración
| Nombre | Unidad | Valor predeterminado | Comentarios |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Segundos |0.015 |Período de tiempo para que Replicador de hello en espera secundaria de hello después de recibir una operación antes de devolver una confirmación toohello principal. Otro toobe de confirmaciones envía para las operaciones se procesan dentro de este intervalo se envían como una respuesta. |
| ReplicatorEndpoint |N/D |Ningún valor predeterminado: parámetro obligatorio |Dirección IP y puerto que Hola principal/secundario replicador utilizará toocommunicate con otros replicadores Hola conjunto de réplica. Esto debe hacer referencia a un punto de conexión del recurso TCP en el manifiesto del servicio Hola. Consulte demasiado[recursos del manifiestos de servicio](service-fabric-service-manifest-resources.md) tooread más acerca de cómo definir recursos de punto de conexión en el manifiesto del servicio. |
| MaxReplicationMessageSize |Bytes |50 MB |Tamaño máximo de los datos de replicación que se puede transmitir en un único mensaje. |
| MaxPrimaryReplicationQueueSize |Número de operaciones |8192 |Número máximo de operaciones en la cola principal Hola. Una operación se libera después de Replicador de hello principal recibe confirmación de todos los replicadores de hello secundaria. Este valor debe ser mayor que 64 y una potencia de 2. |
| MaxSecondaryReplicationQueueSize |Número de operaciones |16384 |Número máximo de operaciones en la cola secundaria Hola. Una operación se libera después de que su estado pase a ser de alta disponibilidad mediante persistencia. Este valor debe ser mayor que 64 y una potencia de 2. |
| CheckpointThresholdInMB |MB |200 |Cantidad de espacio de archivo de registro después de que el estado de hello es punto de comprobación. |
| MaxRecordSizeInKB |KB |1024 |Tamaño del registro más grande que Hola Replicador se puede escribir en el registro de hello. Este valor debe ser un múltiplo de 4 y superior a 16. |
| OptimizeLogForLowerDiskUsage |Booleano |true |Cuando sea true, el registro de hello se configura para que hello archivos de registro específico de la réplica se creación utilizando un archivo disperso de NTFS. Esto reduce el uso de espacio en disco real de hello para el archivo hello. Cuando sea false, archivo hello se crea con una asignación fija, que proporcionan un mejor rendimiento de escritura Hola. |
| SharedLogId |GUID |"" |Especifica un toouse guid único para identificar el archivo de registro compartido Hola usar con esta réplica. Normalmente, los servicios no deben usar esta opción de configuración. Sin embargo, si se especifica SharedLogId, también se debe especificar SharedLogPath. |
| SharedLogPath |Nombre de ruta de acceso completo |"" |Especifica la ruta de acceso completa de Hola donde se creará el archivo de registro compartido hello para esta réplica. Normalmente, los servicios no deben usar esta opción de configuración. Sin embargo, si se especifica SharedLogPath, también se debe especificar SharedLogId. |

## <a name="sample-configuration-file"></a>Archivo de configuración de muestra
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="180" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```

## <a name="remarks"></a>Comentarios
parámetro de Hello BatchAcknowledgementInterval controla la latencia de replicación. Un valor de '0' genera Hola menor latencia posible, costo de Hola de rendimiento (más mensajes de confirmación se deben enviar y procesar, que contiene menos confirmaciones).
Hello mayor valor de Hola para BatchAcknowledgementInterval, Hola Hola superior general rendimiento de replicación, costo de Hola de mayor latencia de la operación. Esto traduce directamente toohello latencia de confirmaciones de transacciones.

Hola CheckpointThresholdInMB parámetro controles Hola cantidad de espacio en disco que Hola replicador puede utilizar información de estado de toostore en archivo de registro dedicado de la réplica de Hola. Aumentar este valor superior al tooa que predeterminado Hola podría dar lugar a tiempos más rápidos de reconfiguración cuando una réplica nueva se agrega el conjunto de toohello. Esto es debido a toohello transferencia de estado parcial que tiene lugar debido toohello disponibilidad del historial más de las operaciones en el registro de hello. Potencialmente, esto puede aumentar el tiempo de recuperación de Hola de una réplica después de un bloqueo.

Si establece OptimizeForLowerDiskUsage tootrue, espacio de archivo de registro será provista en exceso para que las réplicas activas pueden almacenar más información de estado en sus archivos de registro, mientras que las réplicas inactivas utiliza menos espacio en disco. Esto hace posible toohost varias réplicas en un nodo. Si establece OptimizeForLowerDiskUsage toofalse, información de estado de saludo se escribe archivos de registro de toohello más rápidamente.

configuración de Hello MaxRecordSizeInKB define tamaño máximo de Hola de un registro que se puede escribir en el archivo de registro de hello replicador Hola. En la mayoría de los casos, el tamaño de registro de 1024 KB Hola predeterminado es óptimo. Sin embargo, si el servicio de hello provoca gran parte de toobe de elementos de datos de la información de estado de hello, este valor que tenga toobe aumentado. Hay pocas ventajas en lo MaxRecordSizeInKB inferior a 1024, como registros más pequeños sólo utilizan Hola espacio necesario para el registro más pequeño de Hola. Esperamos que este valor deberá toobe cambiar solo en casos poco frecuentes.

configuración de SharedLogId y SharedLogPath de Hello siempre es toomake junto usa un servicio, use un registro compartido independiente del registro de hello predeterminada compartida de nodo de Hola. Para obtener mayor eficacia, servicios tantos como sea posible deben especificar Hola mismas compartida de registro. Archivos de registro compartido deben estar ubicados en discos que se utilizan únicamente para el archivo de registro compartido en hello, contención de movimiento de los cabezales de tooreduce. Esperamos que estos valores necesitaría toobe cambiar solo en casos poco frecuentes.


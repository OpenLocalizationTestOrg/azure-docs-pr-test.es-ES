---
title: aaaConfigure confiable Azure microservicios | Documentos de Microsoft
description: "Obtenga información sobre cómo configurar Reliable Services con estado en Service Fabric."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: vturecek
ms.assetid: 9f72373d-31dd-41e3-8504-6e0320a11f0e
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 1e9c2890b62890a777561f25c04dc0fd11db9f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-stateful-reliable-services"></a>Configurar Reliable Services con estado
Hay dos conjuntos de valores de configuración para los servicios de confianza. Un conjunto es global para todos los servicios de confianza en el clúster de hello, mientras que otro conjunto hello es tooa específico de servicio confiable determinado.

## <a name="global-configuration"></a>Configuración global
configuración de servicio confiable global de Hola se especifica en el manifiesto de clúster de Hola de clúster de hello en hello KtlLogger sección. Permite la configuración de Hola compartida ubicación y tamaño más Hola memoria global límites del registro utilizado por el registrador de Hola. manifiesto de clúster de Hello es un único archivo XML que contiene la configuración y las configuraciones que se aplican tooall nodos y los servicios en clúster de Hola. archivo Hello normalmente se denomina ClusterManifest.xml. Puede ver manifiesto de clúster de hello para el clúster mediante comandos de powershell de hello ServiceFabricClusterManifest Get.

### <a name="configuration-names"></a>Nombres de configuración
| Nombre | Unidad | Valor predeterminado | Comentarios |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |Kilobytes |8388608 |Número mínimo de tooallocate KB en modo de kernel para el registrador de hello escribir bloque de memoria de búfer. Este bloque de memoria se utiliza para almacenar en caché información de estado antes de escribir toodisk. |
| WriteBufferMemoryPoolMaximumInKB |Kilobytes |Ilimitado |Bloque de memoria del búfer de escritura de tamaño máximo toowhich Hola registrador puede crecer. |
| SharedLogId |GUID |"" |Especifica un toouse GUID único para identificar el archivo hello predeterminado de registro compartido usado por todos los servicios de confianza en todos los nodos de clúster de Hola que no especifican hello SharedLogId en su configuración específica del servicio. Si se especifica SharedLogId, también se debe especificar SharedLogPath. |
| SharedLogPath |Nombre de ruta de acceso completo |"" |Especifica la ruta de acceso completa de Hola donde hello comparte el archivo de registro usado por todos los servicios de confianza en todos los nodos de clúster de Hola que no especifican hello SharedLogPath en su configuración específica del servicio. Sin embargo, si se especifica SharedLogPath, también se debe especificar SharedLogId. |
| SharedLogSizeInMB |Megabytes |8192 |Especifica el número de Hola de MB de espacio en disco toostatically asignar para registro de hello compartido. valor de Hello debe ser 2048 o superior. |

En Azure ARM o plantilla JSON en local, ejemplo de Hola siguiente muestra cómo toochange Hola Hola compartido registro de transacciones obtiene crea tooback las recopilaciones confiables para los servicios con estado.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="sample-local-developer-cluster-manifest-section"></a>Sección de manifiesto de clúster del desarrollador local de ejemplo
Si desea toochange esto en el entorno de desarrollo local, necesita tooedit Hola local clustermanifest.xml archivo.

```xml
   <Section Name="KtlLogger">
     <Parameter Name="SharedLogSizeInMB" Value="4096"/>
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
   </Section>
```

### <a name="remarks"></a>Comentarios
registrador de Hello tiene un grupo global de la memoria asignada de memoria del núcleo no paginada que proporciona servicios de confianza tooall disponible en un nodo para almacenar en caché datos de estado antes de que se escriban toohello registro dedicados asociado con la réplica de un servicio confiable de Hola. tamaño del grupo de Hola se controla mediante hello WriteBufferMemoryPoolMinimumInKB y la configuración de WriteBufferMemoryPoolMaximumInKB. WriteBufferMemoryPoolMinimumInKB especifica ambos Hola tamaño inicial de este bloque de memoria y el bloque de hello menor tamaño toowhich hello memoria puede reducir. WriteBufferMemoryPoolMaximumInKB es el bloque de hello mayor tamaño toowhich hello memoria puede alcanzar. Cada réplica de un servicio confiable que está abierto puede aumentar el tamaño de Hola de bloque de memoria de Hola por una cantidad de sistema determinada la tooWriteBufferMemoryPoolMaximumInKB. Si no hay más demanda de memoria de bloque de memoria de Hola que está disponible, las solicitudes de memoria se retrasará hasta que haya memoria disponible. Por lo tanto, si el bloque de memoria de búfer de escritura de hello es demasiado pequeño para una configuración concreta, a continuación, rendimiento puede verse afectado.

configuraciones de SharedLogId y SharedLogPath de Hola siempre son utilizados toodefine juntos Hola GUID y ubicación predeterminada de hello comparte registros para todos los nodos de clúster de Hola. registro de Hello predeterminado compartido se utiliza para todos los servicios de confianza que no se especifican los valores de hello en hello settings.xml servicio concreto de Hola. Para obtener el mejor rendimiento, compartido archivos de registro deben colocarse en discos que se usan únicamente para la contención de tooreduce del archivo de registro de hello compartido.

SharedLogSizeInMB especifica la cantidad de Hola de toopreallocate de espacio en disco para registro de hello predeterminado compartido en todos los nodos.  No es necesario SharedLogId y SharedLogPath toobe especificado en el orden de toobe SharedLogSizeInMB especificado.

## <a name="service-specific-configuration"></a>Configuración específica por servicio
Puede modificar las configuraciones predeterminadas de estado confiable de servicios mediante el paquete de configuración de hello (configuración) u Hola implementación del servicio (código).

* **Configuración** -configuración mediante el paquete de configuración Hola se consigue cambiando hello Settings.xml archivo que se genera en la raíz del paquete de Microsoft Visual Studio hello en carpeta de configuración de Hola para cada servicio en la aplicación hello.
* **Código** -configuración a través del código se logra creando una ReliableStateManager mediante un objeto ReliableStateManagerConfiguration con conjunto de opciones adecuadas de Hola.

De forma predeterminada, el tiempo de ejecución de hello Azure Service Fabric busca nombres de sección predefinida en el archivo de hello Settings.xml y utiliza los valores de configuración de Hola durante la creación de hello subyacente componentes en tiempo de ejecución.

> [!NOTE]
> Hacer **no** eliminar los nombres de sección de Hola de hello siguiendo configuraciones en el archivo Settings.xml hello que se genera en la solución de Visual Studio de Hola a menos que piense tooconfigure su servicio a través del código.
> Cambiar el nombre de los nombres de paquete o una sección de configuración de hello requerirá un cambio en el código al configurar hello ReliableStateManager.
> 
> 

### <a name="replicator-security-configuration"></a>Configuración de seguridad del replicador
Las configuraciones de seguridad de Replicador son canal de comunicación de hello toosecure utilizado que se usa durante la replicación. Esto significa que los servicios no serán toosee capaz de proteger sus respectivas tráfico de replicación, asegurándose de que los datos de Hola que ofrezca alta disponibilidad son también. De forma predeterminada, una sección de configuración de seguridad vacía impide la seguridad de la replicación.

### <a name="default-section-name"></a>Nombre de sección predeterminado
ReplicatorSecurityConfig

> [!NOTE]
> toochange este nombre de sección, invalidación hello replicatorSecuritySectionName parámetro toohello ReliableStateManagerConfiguration constructor al crear hello ReliableStateManager para este servicio.
> 
> 

### <a name="replicator-configuration"></a>Configuración de replicador
Las configuraciones de Replicador configurar Replicador de Hola que es responsable de tomar Hola con estado del estado del servicio confiable de gran confiabilidad por replicar y conservar el estado de hello localmente.
configuración predeterminada de Hello generado por la plantilla de Visual Studio de Hola y debe ser suficiente. Esta sección trata sobre las configuraciones adicionales que están disponibles tootune Replicador de Hola.

### <a name="default-section-name"></a>Nombre de sección predeterminado
ReplicatorConfig

> [!NOTE]
> toochange este nombre de sección, invalidación hello replicatorSettingsSectionName parámetro toohello ReliableStateManagerConfiguration constructor al crear hello ReliableStateManager para este servicio.
> 
> 

### <a name="configuration-names"></a>Nombres de configuración
| Nombre | Unidad | Valor predeterminado | Comentarios |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Segundos |0.015 |Período de tiempo para que Replicador de hello en espera secundaria de hello después de recibir una operación antes de devolver una confirmación toohello principal. Otro toobe de confirmaciones envía para las operaciones se procesan dentro de este intervalo se envían como una respuesta. |
| ReplicatorEndpoint |N/D |Ningún valor predeterminado: parámetro obligatorio |Dirección IP y puerto que Hola principal/secundario replicador utilizará toocommunicate con otros replicadores Hola conjunto de réplica. Esto debe hacer referencia a un punto de conexión del recurso TCP en el manifiesto del servicio Hola. Consulte demasiado[recursos del manifiestos de servicio](service-fabric-service-manifest-resources.md) tooread más acerca de cómo definir recursos de punto de conexión en un manifiesto de servicio. |
| MaxPrimaryReplicationQueueSize |Número de operaciones |8192 |Número máximo de operaciones en la cola principal Hola. Una operación se libera después de Replicador de hello principal recibe confirmación de todos los replicadores de hello secundaria. Este valor debe ser mayor que 64 y una potencia de 2. |
| MaxSecondaryReplicationQueueSize |Número de operaciones |16384 |Número máximo de operaciones en la cola secundaria Hola. Una operación se libera después de que su estado pase a ser de alta disponibilidad mediante persistencia. Este valor debe ser mayor que 64 y una potencia de 2. |
| CheckpointThresholdInMB |MB |50 |Cantidad de espacio de archivo de registro después de que el estado de hello es punto de comprobación. |
| MaxRecordSizeInKB |KB |1024 |Tamaño del registro más grande que Hola Replicador se puede escribir en el registro de hello. Este valor debe ser un múltiplo de 4 y superior a 16. |
| MinLogSizeInMB |MB |0 (sistema determinado) |Tamaño mínimo del registro transaccional de Hola. registro de Hello no se permitirán tootruncate tooa tamaño por debajo de este valor. 0 indica que Replicador Hola determinará el tamaño mínimo del registro de hello. Al aumentar este valor aumenta la posibilidad de Hola de hacer las copias parciales y copias de seguridad incrementales desde posibilidades relevantes de entradas de registro que se va a truncar disminuye. |
| TruncationThresholdFactor |Factor |2 |Determina a qué tamaño del registro de hello, se activará el truncamiento. El umbral de truncamiento se determina multiplicando el valor de MinLogSizeInMB por TruncationThresholdFactor. El valor de TruncationThresholdFactor debe ser mayor que 1. El valor de MinLogSizeInMB * TruncationThresholdFactor debe ser menor que MaxStreamSizeInMB. |
| ThrottlingThresholdFactor |Factor |4 |Determina en el tamaño del registro de hello, réplica de hello comenzará está limitando. El umbral de limitación (en MB) se determina mediante Max((MinLogSizeInMB ThrottlingThresholdFactor),(CheckpointThresholdInMB ThrottlingThresholdFactor)). El valor del umbral de limitación (en MB) debe ser mayor que el de truncamiento (en MB). El valor del umbral de truncamiento (en MB) debe ser menor que el de MaxStreamSizeInMB. |
| MaxAccumulatedBackupLogSizeInMB |MB |800 |El tamaño máximo acumulado (en MB) de los registros de copia de seguridad de una cadena de registros de copia de seguridad determinada. Una solicitudes de copia de seguridad incremental se producirá un error si la copia de seguridad incremental de hello generaría un registro de copia de seguridad que puede provocar que los registros de copia de seguridad de hello acumulado desde el número de toobe relevante copia de seguridad completa de hello mayor que este tamaño. En tales casos, el usuario es necesario tootake una copia de seguridad completa. |
| SharedLogId |GUID |"" |Especifica un toouse GUID único para identificar el archivo de registro compartido Hola usar con esta réplica. Normalmente, los servicios no deben usar esta opción de configuración. Sin embargo, si se especifica SharedLogId, también se debe especificar SharedLogPath. |
| SharedLogPath |Nombre de ruta de acceso completo |"" |Especifica la ruta de acceso completa de Hola donde se creará el archivo de registro compartido hello para esta réplica. Normalmente, los servicios no deben usar esta opción de configuración. Sin embargo, si se especifica SharedLogPath, también se debe especificar SharedLogId. |
| SlowApiMonitoringDuration |Segundos |300 |Establece el intervalo para las llamadas de API administradas de supervisión de Hola. Ejemplo: función de devolución de llamada de copia de seguridad proporcionada por el usuario. Después de que transcurra el intervalo de saludo, se enviará un informe de estado de advertencia toohello servicio de mantenimiento. |

### <a name="sample-configuration-via-code"></a>Ejemplo de configuración mediante código
```csharp
class Program
{
    /// <summary>
    /// This is hello entry point of hello service host process.
    /// </summary>
    static void Main()
    {
        ServiceRuntime.RegisterServiceAsync("HelloWorldStatefulType",
            context => new HelloWorldStateful(context, 
                new ReliableStateManager(context, 
        new ReliableStateManagerConfiguration(
                        new ReliableStateManagerReplicatorSettings()
            {
                RetryInterval = TimeSpan.FromSeconds(3)
                        }
            )))).GetAwaiter().GetResult();
    }
}    
```
```csharp
class MyStatefulService : StatefulService
{
    public MyStatefulService(StatefulServiceContext context, IReliableStateManagerReplica stateManager)
        : base(context, stateManager)
    { }
    ...
}
```


### <a name="sample-configuration-file"></a>Archivo de configuración de ejemplo
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="ReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="ReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="512" />
   </Section>
   <Section Name="ReplicatorSecurityConfig">
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


### <a name="remarks"></a>Comentarios
BatchAcknowledgementInterval controla la latencia de replicación. Un valor de '0' genera Hola menor latencia posible, costo de Hola de rendimiento (más mensajes de confirmación se deben enviar y procesar, que contiene menos confirmaciones).
Hello mayor valor de Hola para BatchAcknowledgementInterval, Hola Hola superior general rendimiento de replicación, costo de Hola de mayor latencia de la operación. Esto traduce directamente toohello latencia de confirmaciones de transacciones.

valor de Hola para CheckpointThresholdInMB controles Hola cantidad de espacio que Hola replicador puede utilizar información de estado de toostore en archivo de registro dedicado de la réplica de Hola. Aumentar este valor superior al tooa que predeterminado Hola podría dar lugar a tiempos más rápidos de reconfiguración cuando una réplica nueva se agrega el conjunto de toohello. Esto es debido a toohello transferencia de estado parcial que tiene lugar debido toohello disponibilidad del historial más de las operaciones en el registro de hello. Potencialmente, esto puede aumentar el tiempo de recuperación de Hola de una réplica después de un bloqueo.

configuración de Hello MaxRecordSizeInKB define tamaño máximo de Hola de un registro que se puede escribir en el archivo de registro de hello replicador Hola. En la mayoría de los casos, el tamaño de registro de 1024 KB Hola predeterminado es óptimo. Sin embargo, si el servicio de hello provoca gran parte de toobe de elementos de datos de la información de estado de hello, este valor que tenga toobe aumentado. Hay pocas ventajas en lo MaxRecordSizeInKB inferior a 1024, como registros más pequeños sólo utilizan Hola espacio necesario para el registro más pequeño de Hola. Esperamos que este valor deberá toobe cambiado en solo casos poco frecuentes.

configuración de SharedLogId y SharedLogPath de Hello siempre es toomake junto usa un servicio, use un registro compartido independiente del registro de hello predeterminada compartida de nodo de Hola. Para obtener mayor eficacia, servicios tantos como sea posible deben especificar Hola mismas compartida de registro. Archivos de registro compartido deben estar ubicados en discos que se usan únicamente para la contención de movimiento de los cabezales de hello compartido del registro archivo tooreduce. Esperamos que este valor deberá toobe cambiado en solo casos poco frecuentes.

## <a name="next-steps"></a>Pasos siguientes
* [Depuración de la aplicación del Service Fabric en Visual Studio](service-fabric-debugging-your-application.md)
* [Referencia para desarrolladores de servicios confiables](https://msdn.microsoft.com/library/azure/dn706529.aspx)


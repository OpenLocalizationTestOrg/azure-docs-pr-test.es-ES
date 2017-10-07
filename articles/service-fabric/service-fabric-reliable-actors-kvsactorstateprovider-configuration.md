---
title: "configuración de KVSActorStateProvider aaaChange en Azure microservicios | Documentos de Microsoft"
description: "Obtenga información sobre cómo configurar los actores con estado de Azure Service Fabric de tipo KVSActorStateProvider."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: e003512678556e68a8926b1b9c6c28d9ae3979d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--kvsactorstateprovider"></a>Configuración de Reliable Actors: KVSActorStateProvider
Puede modificar configuración predeterminada de Hola de KVSActorStateProvider cambiando hello settings.xml archivo que se genera en la raíz del paquete de Microsoft Visual Studio hello en carpeta de configuración de hello para el actor especificado Hola.

en tiempo de ejecución de Hello Azure Service Fabric busca nombres de sección predefinida en el archivo de hello settings.xml y consume los valores de configuración de Hola durante la creación de hello subyacente componentes en tiempo de ejecución.

> [!NOTE]
> Hacer **no** eliminar o modificar los nombres de sección de Hola de hello siguiendo configuraciones en el archivo settings.xml hello que se genera en hello solución de Visual Studio.
> 
> 

## <a name="replicator-security-configuration"></a>Configuración de seguridad del replicador
Las configuraciones de seguridad de Replicador son canal de comunicación de hello toosecure utilizado que se usa durante la replicación. Esto significa que los servicios no pueden ver sus respectivas tráfico de replicación, garantizar que los datos de Hola que ofrezca alta disponibilidad también están seguros.
De forma predeterminada, una sección de configuración de seguridad vacía impide la seguridad de la replicación.

### <a name="section-name"></a>Nombre de sección
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Configuración de replicador
Las configuraciones de Replicador configurar Replicador de Hola que se encarga de hacer que el estado del proveedor de estado de Actor Hola gran confiabilidad.
configuración predeterminada de Hello generado por la plantilla de Visual Studio de Hola y debe ser suficiente. Esta sección trata sobre las configuraciones adicionales que están disponibles tootune Replicador de Hola.

### <a name="section-name"></a>Nombre de sección
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Nombres de configuración
| Nombre | Unidad | Valor predeterminado | Comentarios |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Segundos |0.015 |Período de tiempo para que Replicador de hello en espera secundaria de hello después de recibir una operación antes de devolver una confirmación toohello principal. Otro toobe de confirmaciones envía para las operaciones se procesan dentro de este intervalo se envían como una respuesta. |
| ReplicatorEndpoint |N/D |Ningún valor predeterminado: parámetro obligatorio |Dirección IP y puerto que Hola principal/secundario replicador utilizará toocommunicate con otros replicadores Hola conjunto de réplica. Esto debe hacer referencia a un punto de conexión del recurso TCP en el manifiesto del servicio Hola. Consulte demasiado[recursos del manifiestos de servicio](service-fabric-service-manifest-resources.md) tooread más acerca de cómo definir recursos de punto de conexión en el manifiesto del servicio Hola. |
| RetryInterval |Segundos |5 |Período de tiempo después de que Replicador de hello volver a transmite un mensaje si no recibe una confirmación para una operación. |
| MaxReplicationMessageSize |Bytes |50 MB |Tamaño máximo de los datos de replicación que se puede transmitir en un único mensaje. |
| MaxPrimaryReplicationQueueSize |Número de operaciones |1024 |Número máximo de operaciones en la cola principal Hola. Una operación se libera después de Replicador de hello principal recibe confirmación de todos los replicadores de hello secundaria. Este valor debe ser mayor que 64 y una potencia de 2. |
| MaxSecondaryReplicationQueueSize |Número de operaciones |2048 |Número máximo de operaciones en la cola secundaria Hola. Una operación se libera después de que su estado pase a ser de alta disponibilidad mediante persistencia. Este valor debe ser mayor que 64 y una potencia de 2. |

## <a name="store-configuration"></a>Configuración de almacén
Configuraciones de almacén son utilizados tooconfigure Hola almacén local que está en estado de hello toopersist utilizado que se está replicando.
configuración predeterminada de Hello generado por la plantilla de Visual Studio de Hola y debe ser suficiente. En esta sección habla de las configuraciones adicionales que son almacén local de hello tootune disponible.

### <a name="section-name"></a>Nombre de sección
&lt;ActorName&gt;ServiceLocalStoreConfig

### <a name="configuration-names"></a>Nombres de configuración
| Nombre | Unidad | Valor predeterminado | Comentarios |
| --- | --- | --- | --- |
| MaxAsyncCommitDelayInMilliseconds |Milisegundos |200 |Establece el máximo Hola intervalo para confirmaciones de almacén local duradero de procesamiento por lotes. |
| MaxVerPages |Número de páginas |16384 |número máximo de Hola de páginas de versión en hello local almacena la base de datos. Determina el número máximo de hello las transacciones pendientes. |

## <a name="sample-configuration-file"></a>Archivo de configuración de ejemplo
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
   </Section>
   <Section Name="MyActorServiceLocalStoreConfig">
      <Parameter Name="MaxVerPages" Value="8192" />
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


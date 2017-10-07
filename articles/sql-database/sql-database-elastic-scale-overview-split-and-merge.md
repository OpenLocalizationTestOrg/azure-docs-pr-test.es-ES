---
title: aaaMoving datos entre bases de datos de escala horizontal en la nube | Documentos de Microsoft
description: "Explica cómo toomanipulate particiones y mover datos a través de un servicio hospedado por sí mismo mediante elástico de base de datos API."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 204fd902-0397-4185-985a-dea3ed7c7d9f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 629dee06e22609e9b61edf93ba5c38d997132d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-between-scaled-out-cloud-databases"></a>Moving data between scaled-out cloud databases (Mover datos entre bases de datos en la nube escaladas horizontalmente)
Si es un Software como un programador del servicio y, de repente la aplicación experimenta una enorme demanda, necesita el crecimiento de hello tooaccommodate. De este modo, agrega más bases de datos (particiones). ¿Cómo se redistribuye Hola datos toohello nuevas bases de datos sin interrumpir la integridad de los datos Hola? Hola de uso **herramienta Dividir-combinar** toomove datos restringida toohello nuevas bases de datos de bases de datos.  

herramienta de combinación de la división de Hola se ejecuta como un servicio web de Azure. Un administrador o desarrollador usa Hola herramienta toomove shardlets (datos de una partición) entre distintas bases de datos (particiones). herramienta de Hello usa particiones mapa toomaintain Hola servicio metadatos base de datos y asegúrese de asignaciones coherente.

![Información general][1]

## <a name="download"></a>Descargar
[Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/)

## <a name="documentation"></a>Documentación
1. [Tutorial de la herramienta de división y combinación de Base de datos elástica](sql-database-elastic-scale-configure-deploy-split-and-merge.md)
2. [Configuración de seguridad de división y combinación](sql-database-elastic-scale-split-merge-security-configuration.md)
3. [Split-merge security considerations](sql-database-elastic-scale-split-merge-security-configuration.md)
4. [Administración de mapas de particiones.](sql-database-elastic-scale-shard-map-management.md)
5. [Migrar tooscale-fuera de las bases de datos existente](sql-database-elastic-convert-to-use-elastic-tools.md)
6. [Elastic database tools](sql-database-elastic-scale-introduction.md)
7. [Glosario de las herramientas de bases de datos elásticas](sql-database-elastic-scale-glossary.md)

## <a name="why-use-hello-split-merge-tool"></a>¿Por qué usar la herramienta de combinación de la división de hello?
**Flexibilidad**

Las aplicaciones necesitan toostretch flexible más allá de los límites de Hola de una sola base de datos de la base de datos de SQL Azure. Usar datos de toomove de herramienta de hello como bases de datos necesarias toonew conservando la integridad.

**División toogrow** 

Necesita tooincrease general toohandle drástico crecimiento de capacidad. toodo crear por lo tanto, una capacidad adicional particionamiento Hola datos y si se distribuye entre las bases de datos de forma incremental más hasta que se cumplen las necesidades de capacidad. Se trata de un buen ejemplo de Hola 'split' característica. 

**Mezcla tooshrink**

Es necesario reducir capacidad debido toohello estacionales naturaleza de la empresa. Hola herramienta permite que reducir toofewer unidades de escalado cuando se reduce el negocio. característica de 'merge' Hola Hola escala elástica dividir-combinar servicio cubre este requisito. 

**Administrar zonas activas moviendo shardlets**

Con varios inquilinos por base de datos, asignación de Hola de tooshards de shardlets puede reducir los cuellos de botella toocapacity en algunas particiones. Esto requiere volver a asignar shardlets o mover shardlets ocupado toonew o menos particiones infrautilizados. 

## <a name="concepts--key-features"></a>Conceptos y características clave
**Servicios hospedados por el cliente**

Hola dividir-combinar se entrega como un servicio hospedado por el cliente. Debe implementar y hospedar el servicio de hello en su suscripción de Microsoft Azure. paquete de Hello que descargar de NuGet contiene un toocomplete de plantilla de configuración con información de Hola para su implementación. Vea hello [dividir-combinar tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md) para obtener más información. Puesto que el servicio de Hola se ejecuta en su suscripción de Azure, puede controlar y configurar la mayoría de aspectos de seguridad de servicio de Hola. plantilla predeterminada de Hello incluye Hola opciones tooconfigure SSL, la autenticación de cliente basada en certificados, cifrado para las credenciales almacenadas, DoS protegiendo y restricciones de IP. Puede encontrar más información sobre Hola aspectos de seguridad en hello siguiente documento [configuración de seguridad de dividir-combinar](sql-database-elastic-scale-split-merge-security-configuration.md).

valor predeterminado de Hello implementado se ejecuta el servicio con un trabajo y un rol web. Cada uno de ellos usa el tamaño de VM A1 de hello en los servicios de nube de Azure. Mientras no se puede modificar esta configuración al implementar el paquete de hello, se puede cambiar después de una implementación correcta en hello ejecutando el servicio en la nube, (a través del portal de Azure Hola). Tenga en cuenta que ese rol de trabajo hello no debe configurarse con más de una sola instancia por razones técnicas. 

**Integración de mapas de particiones**

servicio de dividir-combinar Hola interactúa con mapa de particiones de Hola de aplicación hello. Al utilizar toosplit de servicio de división y combinación de Hola o intervalos de mezcla o toomove shardlets entre las particiones, el servicio de hello mantiene automáticamente mapa de particiones de hello seguridad toodate. toodo por lo tanto, servicio Hola conecta toohello base de datos de administrador de mapa de particiones de aplicación hello y mantiene intervalos y asignaciones de progreso de las solicitudes de división o combinación/mover. Esto garantiza que Hola particiones se asignan siempre presenta una vista actualizada cuando las operaciones de combinación de división va. Dividir, se implementan las operaciones de movimiento de mezcla y shardlet moviendo un lote de shardlets de partición de destino de hello origen particiones toohello. Durante la hello shardlet movimiento operación hello shardlets asunto toohello lote actual se marcan como sin conexión en el mapa de particiones de hello y no están disponibles para conexiones de enrutamiento dependiente de los datos mediante hello **OpenConnectionForKey** API. 

**Conexiones coherentes de shardlets**

Cuando se inicia el movimiento de datos para un nuevo lote de shardlets, cualquier mapa de particiones proporciona dependiente de los datos enrutamiento conexiones toohello particiones almacenar hello shardlet son conexiones eliminadas y posteriores de mapa de particiones de hello toohello API estos shardlets se bloquean mientras movimiento de datos de Hello está en curso en incoherencias de tooavoid de orden. Las conexiones tooother shardlets en hello también obtener eliminará misma partición, pero se realizará correctamente nuevo inmediatamente al volver a intentarlo. Una vez que se mueven por lotes de hello, hello shardlets se marcan en línea nuevo para la partición de destino de Hola y datos de origen de saludo se quitan de la partición de origen de Hola. servicio de Hola quede a través de estos pasos en todos los lotes hasta que todos los shardlets que se han movido. Esto daría lugar las operaciones de eliminación de conexión de tooseveral durante el curso de Hola de completar la operación split, merge, mover Hola.  

**Administración de la disponibilidad de shardlets**

Limitar el lote actual de toohello de shardlets según se explicó anteriormente la terminación de conexión de Hola restringe el ámbito de Hola de lote de tooone de falta de disponibilidad de shardlets a la vez. Esto es preferible a un enfoque donde partición completa Hola se mantendría sin conexión para todos sus shardlets durante el transcurso de Hola de una operación de división o combinación. tamaño de Hola de un lote, definido como número de Hola de toomove shardlets distintos a la vez, es un parámetro de configuración. Se puede definir para cada operación de división y combinación según las necesidades de disponibilidad y el rendimiento de la aplicación hello. Tenga en cuenta que el intervalo de Hola que se está bloqueando en mapa de particiones de hello puede ser mayor que el tamaño de lote de hello especificado. Esto es porque el servicio de Hola toma el tamaño del intervalo de Hola tal que el número real de Hola de valores de clave de particionamiento de datos de hello aproximadamente coincide con el tamaño del lote de Hola. Esto es importante tooremember en particular para las claves de particionamiento apenas lleno. 

**Almacenamiento de metadatos**

servicio de dividir-combinar Hello usa un toomaintain de base de datos su estado e tookeep inicia una sesión durante el procesamiento de la solicitud. usuario de Hello crea esta base de datos en su suscripción y prevea la cadena de conexión de hello en archivo de configuración de hello para la implementación del servicio de Hola. Los administradores de organización del usuario de hello también pueden conectarse toothis progreso de solicitud de base de datos tooreview y tooinvestigate detallan información relativa a posibles errores.

**Reconocimiento de particionamiento**

servicio de dividir-combinar Hola marca la diferencia entre tablas particionadas (1), las tablas de referencia (2) y (3) normales tablas. semántica de Hola de una operación de división/combinación/movimiento depende Hola tipo de tabla de hello utilizada y se define como sigue: 

* **Tablas particionadas**: división y combinación, las operaciones de movimiento mover shardlets de partición de origen tootarget. Tras finalizar correctamente Hola solicitar en general, los shardlets ya no están presentes en el origen de Hola. Tenga en cuenta que las tablas de destino de hello necesitan tooexist en la partición de destino de hello y no deben contener datos en el intervalo de destino Hola anterior tooprocessing de operación de Hola. 
* **Hacer referencia a tablas**: para las tablas de referencia, división de hello, combinar y mover las operaciones de copien los datos de Hola de partición de destino de hello origen toohello. Sin embargo, tenga en cuenta que no se producen cambios en la partición de destino de Hola para una tabla dada si cualquier fila ya está presente en esta tabla de destino de Hola. tabla de Hello tiene toobe vacía para cualquier tooget de operación de copia de tabla de referencia procesado.
* **Otras tablas**: otras tablas pueden estar presentes en el origen de Hola o de destino de Hola de una operación de división y combinación. servicio de dividir-combinar Hello no tiene en cuenta estas tablas para cualquier movimiento de datos o las operaciones de copia. Sin embargo, observe que pueden interferir con estas operaciones en caso de restricciones.

se proporciona información Hola referencia frente a tablas particionadas hello **SchemaInfo** las API en el mapa de particiones de Hola. Hola siguiente ejemplo muestra uso de Hola de estas API en un smm de objeto de partición determinado mapa manager: 

    // Create hello schema annotations 
    SchemaInfo schemaInfo = new SchemaInfo(); 

    // Reference tables 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "region")); 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "nation")); 

    // Sharded tables 
    schemaInfo.Add(new ShardedTableInfo("dbo", "customer", "C_CUSTKEY")); 
    schemaInfo.Add(new ShardedTableInfo("dbo", "orders", "O_CUSTKEY")); 

    // Publish 
    smm.GetSchemaInfoCollection().Add(Configuration.ShardMapName, schemaInfo); 

Hola tablas 'region' y 'nación' se definen como tablas de referencia y se copiará con las operaciones de división/combinación/movimiento. A su vez, las tablas "customer" y "orders" se definen como tablas particionadas. C_claveCliente y O_CUSTKEY actúan como clave de particionamiento de Hola. 

**Integración referencial**

servicio de dividir-combinar Hola analiza las dependencias entre las tablas y utiliza las operaciones de relaciones de clave principal y clave externa toostage Hola para mover las tablas de referencia y shardlets. En general, las tablas de referencia primero se copian en orden de dependencia, luego los shardlets se copia según el orden de sus dependencias dentro de cada lote. Esto es necesario para que se respetan las restricciones de PK-FK en particiones de destino de hello como llegan datos nuevos de Hola. 

**Coherencia de mapa de particiones y eventual finalización**

En presencia de Hola de errores, servicio de dividir-combinar Hola reanuda operaciones después de cualquier interrupción y tiene como objetivo toocomplete cualquiera de las peticiones de progreso. Sin embargo, puede haber situaciones irrecuperables, por ejemplo, cuando se pierde o puesto en peligro no se puede reparar particiones de destino de Hola. En esas circunstancias, algunas shardlets que se debe mover toobe puede continuar tooreside en particiones de origen Hola. servicio Hola garantiza que las asignaciones de shardlet solo se actualizan después de los datos necesarios de hello destino toohello copió correctamente. Shardlets sólo se eliminan en origen Hola una vez copiado todos sus datos de destino toohello y asignaciones correspondientes Hola se han actualizado correctamente. operación de eliminación de Hello sucede en segundo plano de hello mientras intervalo Hola ya está en línea en la partición de destino de Hola. servicio de dividir-combinar Hola siempre garantiza correcto de asignaciones de hello almacenadas en mapa de particiones de Hola.

## <a name="hello-split-merge-user-interface"></a>interfaz de usuario de división y combinación de Hola
paquete de servicio de dividir-combinar Hola incluye un rol de trabajo y un rol web. rol web de Hello es toosubmit usado dividir-combinar solicitudes de forma interactiva. componentes principales de Hola de interfaz de usuario de hello son los siguientes:

* Tipo de operación: el tipo de operación de hello es un botón de opción que controla Hola tipo de operación realizada por el servicio de Hola para esta solicitud. Puede elegir entre la división de hello, combinar y mover escenarios. También puede cancelar una operación anteriormente enviada. Puede usar las solicitudes de división, combinación y movimiento para los mapas de particiones de intervalo. Los mapas de particiones de lista solo admiten operaciones de movimiento.
* Mapa de particiones: Hola siguiente sección de información de portada de parámetros de solicitud sobre el mapa de particiones de Hola y aloja su mapa de particiones de base de datos de Hola. En concreto, necesita tooprovide Hola nombre del servidor de base de datos de SQL Azure de Hola y base de datos de hospedaje hello shardmap, particiones de credenciales tooconnect toohello base de datos se asignan y finalmente Hola nombre del mapa de particiones de Hola. Actualmente, la operación de hello acepta solo un único conjunto de credenciales. Estas credenciales necesitan los permisos necesarios toohave tooperform cambia toohello mapa de particiones, así como datos de usuario de toohello en particiones de Hola.
* Intervalo de origen (División y combinación): una operación de división y combinación procesa un intervalo con su clave superior e inferior. toospecify una operación con un unbounded valor de clave superior, verificación Hola "clave superior es max" casilla de verificación y deje el campo de clave alta de hello vacía. Hola intervalo valores de clave que especifique no necesidad tooprecisely coinciden con una asignación y los límites en el mapa de particiones. Si no especifica los límites de intervalo en absoluto servicio Hola deducirá intervalo más cercano de hello automáticamente. Puede utilizar asignaciones actuales de hello GetMappings.ps1 PowerShell script tooretrieve hello en un mapa de particiones especificado.
* Comportamiento del origen de división (split): para las operaciones de división, definir el intervalo de origen de hello punto toosplit Hola. Para ello, proporcionando la clave de particionamiento de Hola donde desea Hola divide toooccur. Botón de opción Usar Hola especifique si desea que la parte inferior de Hola de hello toomove de intervalo (excepto Hola dividir la clave), o si quiere toomove de la parte superior de hello (incluida la clave de la división de hello).
* Shardlet (movimiento) de origen: mover operaciones son diferentes de dividir o combinar las operaciones que no requieren un origen de intervalo toodescribe Hola. Un origen para mover simplemente se identifica por el valor de clave de particionamiento de Hola que planea toomove.
* Particiones (división) de destino: una vez que ha proporcionado información de hello en origen de saludo de la operación de división, necesita toodefine donde desea Hola datos toobe copia servidor de base de datos de SQL Azure Hola proporcionando tooby y nombre de base de datos de destino de Hola.
* Intervalo de destino (merge): las operaciones de combinación mover particiones de shardlets tooan existente. Identificar particiones existentes de hello proporcionando los límites del intervalo de rango existente de Hola que desee toomerge con Hola.
* Tamaño de lote: controles de tamaño de lote de Hola Hola número de shardlets que irá sin conexión a la vez durante el movimiento de datos Hola. Esto es un valor entero que puede usar valores más pequeños cuando haya toolong confidencial períodos de tiempo de inactividad de shardlets. Los valores mayores aumentará el tiempo de Hola que es un shardlet determinado sin conexión pero puede mejorar el rendimiento.
* Id. de operación (cancelar): Si tiene una operación en curso que ya no es necesario, puede cancelar operación Hola proporcionando su Id. de operación en este campo. Puede recuperar el Id. de operación de Hola de tabla de estado de solicitud de hello (consulte la sección 8.1) o de salida de hello en el Explorador de web de Hola que envía la solicitud de Hola.

## <a name="requirements-and-limitations"></a>Requisitos y limitaciones
Hola la implementación actual del servicio de dividir-combinar hello es asunto toohello siguiendo los requisitos y limitaciones: 

* particiones de Hello necesitan tooexist y estar registrados en el mapa de particiones de Hola para poder realizar una operación de combinación de división en esas particiones. 
* servicio de Hello no crea tablas u otros objetos de base de datos automáticamente como parte de sus operaciones. Esto significa que Hola esquema de tablas particionadas todas las y hacer referencia a tablas necesita tooexist en la operación de división/combinación/movimiento de hello destino particiones tooany anterior. En concreto las tablas particionadas son necesario toobe vacía en el intervalo de Hola donde nuevos shardlets son toobe agregada por una operación de división/combinación/movimiento. En caso contrario, la operación de Hola se producirá un error comprobación de coherencia inicial de hello en particiones de destino de Hola. También tenga en cuenta que los datos de referencia se copian solo si la tabla de referencia de hello está vacía y que no hay ningún coherencia garantiza con operaciones de escritura simultáneas tooother de tener en cuenta en las tablas de referencia de Hola. Se recomienda esto: al ejecutar las operaciones de división/combinación, ninguna otra operación de escritura realizar los cambios de las tablas de referencia toohello.
* servicio de Hola se basa en la identidad de fila establecido por un índice único o la clave que incluye el rendimiento de tooimprove clave de particionamiento de Hola y la confiabilidad de shardlets grandes. Esto permite toomove datos del servicio de hello en una granularidad más fina incluso que simplemente Hola particionamiento valor de clave. Esto ayuda a la cantidad máxima de hello tooreduce de espacio en el registro y los bloqueos que son necesarios durante la operación de Hola. Considere la posibilidad de crear un índice único o una clave principal, incluida la clave de particionamiento de hello en una tabla dada si desea toouse esa tabla con las solicitudes de división o combinación/mover. Por motivos de rendimiento clave de particionamiento de hello debe ser Hola iniciales columna clave Hola Hola índice o.
* Durante el transcurso de Hola de procesamiento de solicitudes, algunos datos de shardlet pueden encontrarse tanto en el origen de Hola y partición de destino de Hola. Esto es necesario tooprotect frente a errores durante el movimiento de los shardlets Hola. Hello integración de dividir-combinar con el mapa de particiones de hello asegura que las conexiones a través de hello datos dependientes enrutamiento API mediante Hola **OpenConnectionForKey** método en el mapa de particiones de hello no ve los estados intermedios incoherentes. Sin embargo, si conecta origen toohello o hello el destino particiones sin usar hello **OpenConnectionForKey** método, pueden verse los estados intermedios incoherentes cuando las solicitudes de división/combinación/movimiento va. Estas conexiones pueden aparecer los resultados parciales o duplicados según tiempo de Hola o conexión de Hola Hola partición subyacente. Esta limitación incluye actualmente las conexiones de hello realizadas por Shard varios escala elástica-consultas.
* base de datos de metadatos de Hola para servicio de dividir-combinar hello no debe compartirse entre distintos roles. Por ejemplo, un rol de servicio de dividir-combinar hello en ejecución en la base de datos de las necesidades toopoint tooa distintos metadatos que la función de la producción de hello provisional.

## <a name="billing"></a>Facturación
servicio de dividir-combinar Hola se ejecuta como un servicio de nube en su suscripción de Microsoft Azure. Por lo tanto, los cargos de servicios en la nube aplicarán tooyour instancia del servicio de Hola. A menos que realice operaciones de división/combinación/desplazamiento de manera frecuente, le recomendamos eliminar el servicio en la nube División y combinación. Esto ahorra costos relacionados con instancias de servicio en la nube en ejecución o implementadas. Puede volver a implementar e iniciar la configuración del ejecutable fácilmente cuando necesite tooperform dividir o combinar las operaciones. 

## <a name="monitoring"></a>Supervisión
### <a name="status-tables"></a>Tablas de estado
Servicio de dividir-combinar Hello proporciona hello **RequestStatus** tabla de base de datos del almacén de metadatos de hello para la supervisión de las solicitudes en curso y completadas. tabla de Hello muestra una fila para cada solicitud de dividir-combinar que se ha enviado toothis instancia del servicio de dividir-combinar Hola. Se da la siguiente información para cada solicitud de Hola:

* **Marca de tiempo**: Hola cuando se inició la solicitud de Hola de fecha y hora.
* **OperationId**: un GUID que identifica de forma única solicitud de saludo. Esta solicitud también puede ser usado toocancel Hola operación mientras está aún en curso.
* **Estado**: Hola estado actual de la solicitud de saludo. Para las solicitudes en curso, también se muestra Hola fase actual en qué hello es solicitud.
* **CancelRequest**: una marca que indica si se ha cancelado la solicitud de saludo.
* **Curso**: una estimación de porcentaje de finalización de la operación de Hola. Un valor de 50 indica que la operación de hello es aproximadamente un 50% completado.
* **Details**: un valor XML que proporciona un informe de progreso más detallado. informe de progreso de Hola se actualiza periódicamente como conjuntos de filas se copian de tootarget de origen. En caso de errores o excepciones, esta columna también incluye información más detallada sobre los errores de Hola.

### <a name="azure-diagnostics"></a>Diagnóstico de Azure
servicio de dividir-combinar Hello usa diagnósticos de Azure basado en Azure SDK 2.5 para la supervisión y diagnóstico. Controlar la configuración de diagnóstico Hola tal como se describe aquí: [habilitar diagnósticos en servicios en la nube y máquinas virtuales](../cloud-services/cloud-services-dotnet-diagnostics.md). paquete de descarga de Hello incluye dos configuraciones de diagnósticos: uno para el rol web de hello y otro para el rol de trabajo de Hola. Estas configuraciones de diagnóstico para el servicio de hello seguir las instrucciones de Hola de [Fundamentos de servicio de nube de Microsoft Azure](https://code.msdn.microsoft.com/windowsazure/Cloud-Service-Fundamentals-4ca72649). Incluye definiciones de hello toolog contadores de rendimiento, registros de IIS, registros de eventos de Windows y registros de eventos de aplicación de mezcla de división. 

## <a name="deploy-diagnostics"></a>Implementar diagnósticos
tooenable la supervisión y diagnóstico mediante programación con la configuración de diagnóstico Hola para los roles de web y de trabajo de hello proporcionados por el paquete de NuGet hello, ejecute hello siga los comandos del uso de PowerShell de Azure: 

    $storage_name = "<YourAzureStorageAccount>" 

    $key = "<YourAzureStorageAccountKey" 

    $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key  


    $config_path = "<YourFilePath>\SplitMergeWebContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWeb" 


    $config_path = "<YourFilePath>\SplitMergeWorkerContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWorker" 

Puede encontrar más información sobre cómo tooconfigure e implementar la configuración de diagnóstico aquí: [habilitar diagnósticos en servicios en la nube y máquinas virtuales](../cloud-services/cloud-services-dotnet-diagnostics.md). 

## <a name="retrieve-diagnostics"></a>Recuperar diagnósticos
Puede acceder fácilmente a los diagnósticos de hello Explorador de servidores de Visual Studio en Azure, parte del árbol del explorador de servidores de Hola Hola. Abra una instancia de Visual Studio y, en la barra de menús de hello, haga clic en vista y el Explorador de servidores. Haga clic en hello icono de Azure tooconnect tooyour suscripción de Azure. A continuación, desplácese tooAzure -> almacenamiento -> <your storage account> -> tablas -> WADLogsTable. Para obtener más información, consulte [Exploración de recursos de almacenamiento con el Explorador de servidores](http://msdn.microsoft.com/library/azure/ff683677.aspx). 

![WADLogsTable][2]

Hola WADLogsTable resaltado en la siguiente figura hello contiene Hola detallada de eventos del registro de aplicación del servicio de hello dividir-combinar. Tenga en cuenta que Hola de forma predeterminada la configuración de hello Descargar paquete es dirigido hacia una implementación de producción. Por lo tanto, intervalo de saludo en el que se extraigan registros y contadores en instancias de servicio de hello es grandes (5 minutos). Para pruebas y desarrollo, intervalo de saludo menor ajustando los valores de diagnóstico de Hola de web de Hola o tooyour de rol de trabajo de hello necesita. Haga doble clic en el rol de Hola Hola Explorador de servidores de Visual Studio (véase más arriba) y, a continuación, ajustar hello período de transferencia en el cuadro de diálogo de Hola para opciones de configuración de diagnósticos de hello: 

![Configuración][3]

## <a name="performance"></a>Rendimiento
En general, un mejor rendimiento es toobe esperado a partir de hello superior, más niveles de servicio de rendimiento en la base de datos de SQL Azure. Asignaciones de memoria, CPU y E/S mayor para los niveles de servicio superiores de Hola Hola de copia masiva benefician y eliminación operaciones que Hola dividir-combinar servicio utiliza. Por esta razón, aumente el nivel de servicio de hello solo para esas bases de datos durante un período definido, limitado de tiempo.

servicio de Hello también realiza consultas de validación como parte de sus operaciones normales. Estas consultas de validación comprobación inesperado presencia de datos en el intervalo de destino de Hola y asegúrese de que cualquier operación de división/combinación/movimiento se inicia desde un estado coherente. Estas consultas todos funcionan sobre intervalos de clave de particionamiento definidos por el ámbito de Hola de operación de Hola y el tamaño de lote de hello proporcionadas como parte de la definición de la solicitud de Hola. Estas consultas demostrar un mejor comportamiento cuando un índice está presente cuya clave de particionamiento de hello como Hola columna inicial. 

Además, una propiedad de unicidad con clave de particionamiento de hello como columna inicial Hola permitirá Hola servicio toouse un enfoque optimizado que limita el consumo de recursos en cuanto a memoria y espacio en el registro. Esta propiedad de unicidad es necesario toomove tamaños de datos de gran tamaño (normalmente por encima de 1GB). 

## <a name="how-tooupgrade"></a>Cómo tooupgrade
1. Siga los pasos de hello en [implementar un servicio de dividir-combinar](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
2. Cambiar el archivo de configuración de servicio de nube para sus implementación de dividir-combinar tooreflect Hola nuevos parámetros de configuración. Un nuevo parámetro requerido es información de hello sobre certificado Hola usado para el cifrado. Una manera fácil toodo trata toocompare Hola nuevo plantilla archivo de configuración de descarga de hello en la configuración existente. Asegúrese de que agregar configuración de Hola de "DataEncryptionPrimaryCertificateThumbprint" y "DataEncryptionPrimary" para web hello y rol de trabajo de Hola.
3. Antes de implementar hello tooAzure de actualización, asegúrese de que han terminado de todas las operaciones de mezcla de división actualmente en ejecución. Puede hacerlo fácilmente consultando las tablas de estado de la solicitud y PendingWorkflows de hello en base de datos de metadatos de mezcla de la división de Hola para las solicitudes en curso.
4. Actualizar la implementación del servicio en la nube existente para dividir-combinar en la suscripción de Azure con el nuevo paquete de Hola y el archivo de configuración de servicio actualizada.

No es necesario tooprovision una nueva base de datos de metadatos para dividir-combinar tooupgrade. nueva versión de Hello actualizará automáticamente la versión nueva de metadatos base de datos toohello existente. 

## <a name="best-practices--troubleshooting"></a>Prácticas recomendadas y solución de problemas
* Definir a un inquilino de prueba y ejecutar las operaciones de división o combinación/mover más importantes con el inquilino de prueba de hello entre varias particiones. Asegúrese de que todos los metadatos se definen correctamente en el mapa de particiones y que las operaciones de hello no infringen las restricciones o las claves externas.
* Tamaño de datos del inquilino de mantener Hola prueba anteriormente Hola tamaño máximo de datos del inquilino más grande de problemas relacionados con el tooensure no se está produciendo tamaño de los datos. Esto ayuda a evaluar un límite superior de Hola que tarda toomove un solo inquilino alrededor. 
* Asegúrese de que el esquema permita las eliminaciones. servicio de dividir-combinar Hola requiere que los datos de tooremove Hola capacidad de partición de origen Hola vez datos Hola destino toohello copió correctamente. Por ejemplo, **eliminar desencadenadores** puede impedir que se eliminen datos de hello en el origen de hello servicio hello y puede provocar toofail de operaciones.
* clave de particionamiento de Hola debe ser la columna inicial de hello en la clave principal o la definición de índice único. Que garantiza un rendimiento óptimo para Hola Hola dividir o combinar consultas de validación y para hello datos reales movimiento y la eliminación de las operaciones que siempre funcionan en intervalos de clave de particionamiento.
* Colocar el servicio de dividir-combinar en el centro de datos y la región de Hola donde residen las bases de datos. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-overview-split-and-merge/split-merge-overview.png
[2]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics.png
[3]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics-config.png


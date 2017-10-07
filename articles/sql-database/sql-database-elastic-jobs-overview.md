---
title: las bases de datos de escala horizontal en la nube de aaaManaging | Documentos de Microsoft
description: "Muestra el servicio de trabajo de base de datos elástica Hola"
metakeywords: azure sql database elastic databases
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 6fa47cf2-1162-4534-a206-6e2d95b78580
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: b6d330cd712421b8cba781e835830772e6e5b77e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-scaled-out-cloud-databases"></a>Administración de bases de datos escaladas horizontalmente en la nube
Hola de bases de datos particionada de toomanage escala horizontal, **trabajos de base de datos elástica** activa (vista previa) se tooreliably ejecutar un script de Transact-SQL (T-SQL) a través de un grupo de bases de datos, incluidos:

* una colección personalizada de bases de datos (se explica más adelante)
* todas las bases de datos de un [grupo elástico](sql-database-elastic-pool.md)
* un conjunto de particiones (creadas con la [biblioteca de cliente de bases de datos elásticas](sql-database-elastic-database-client-library.md)) 

## <a name="documentation"></a>Documentación
* [Instalar componentes de trabajo de base de datos elástica hello](sql-database-elastic-jobs-service-installation.md). 
* [Introducción a Trabajos de base de datos elástica](sql-database-elastic-jobs-getting-started.md)
* [Creación y administración de un grupo de bases de datos SQL elásticas mediante PowerShell](sql-database-elastic-jobs-powershell.md).
* [Creación y administración de Bases de datos SQL de Azure escaladas horizontalmente](sql-database-elastic-jobs-getting-started.md)

**Trabajos de base de datos elásticos** actualmente es un servicio de nube de Azure hospedada por el cliente que permite la ejecución de Hola de ad hoc y tareas administrativas programadas, denominadas **trabajos**. Con trabajos, puede fácilmente y administrar de forma confiable grandes grupos de bases de datos de SQL Azure mediante la ejecución de operaciones administrativas de tooperform de secuencias de comandos de Transact-SQL. 

![Servicio del trabajo de bases de datos elásticas][1]

## <a name="why-use-jobs"></a>¿Por qué usar trabajos?
**Manage**

Realice fácilmente cambios de esquema, administración de credenciales, actualizaciones de datos de referencia, recopilación de datos de rendimiento o recopilación de telemetría de inquilinos (cliente).

**Informes**

Agregue datos de una colección de bases de datos SQL de Azure en una tabla de destino única.

**Reducción de la sobrecarga**

Normalmente, debe conectar tooeach base de datos de forma independiente en instrucciones de Transact-SQL de orden toorun o realizar otras tareas administrativas. Un trabajo controla la tarea hello del inicio de sesión de grupo de destino de hello en la base de datos tooeach. También definir, mantener y conservar toobe de secuencias de comandos de Transact-SQL ejecutado a través de un grupo de bases de datos de SQL Azure.

**Control**

Los trabajos ejecutan hello secuencia de comandos y registro de hello el estado de ejecución para cada base de datos. Obtenga también el reintento automático en caso de errores.

**Flexibilidad**

Defina grupos personalizados de bases de datos SQL de Azure, así como programaciones para ejecutar un trabajo.

> [!NOTE]
> Hola portal de Azure, un conjunto reducido de funciones limitado tooSQL Azure elástico grupos está disponible. Usar hello conjunto completo Hola de PowerShell APIs tooaccess de funcionalidad actual.
> 
> 

## <a name="applications"></a>Aplicaciones
* Realice tareas administrativas como, por ejemplo, la implementación de un nuevo esquema
* Actualice información de producto con datos de referencia comunes en todas las bases de datos. O bien, programe actualizaciones automáticas todos los días laborables, fuera del horario de trabajo.
* Vuelva a generar el rendimiento de las consultas tooimprove índices. Hola, volver a generar puede ser tooexecute configurado a través de una colección de bases de datos de forma periódica, como durante las horas.
* Recopile los resultados de consulta de un conjunto de bases de datos en una tabla central de forma continua. Las consultas de rendimiento se pueden ejecutar continuamente y configurado tootrigger tareas adicionales toobe ejecutado.
* Ejecutar consultas de procesamiento de datos de ejecución más larga a través de un conjunto grande de las bases de datos, por ejemplo Hola colección de telemetría de cliente. Los resultados se recopilan en una sola tabla de destino para su posterior análisis.

## <a name="elastic-database-jobs-end-to-end"></a>Información detallada sobre los trabajos de base de datos elástica
1. Instalar hello **trabajos de base de datos elástica** componentes. Para obtener más información, vea [Instalación de Trabajos de base de datos elástica](sql-database-elastic-jobs-service-installation.md). Si se produce un error en la instalación de hello, consulte [cómo toouninstall](sql-database-elastic-jobs-uninstall.md).
2. Utilizar hello tooaccess PowerShell APIs más funcionalidad, por ejemplo al crear las colecciones de base de datos personalizado, agregar programaciones o conjuntos de resultados de la recopilación. Portal de Hola de uso para la instalación simple y la creación y la supervisión de trabajos de limitado tooexecution contra un **grupo elástico**. 
3. Crear las credenciales cifradas de la ejecución del trabajo y [Agregar base de datos de tooeach de usuario (o el rol) de hello en el grupo de hello](sql-database-security-overview.md).
4. Crear un script de T-SQL que se pueden ejecutar en cada base de datos en el grupo de hello idempotente. 
5. Siga estos trabajos de toocreate pasos con hello portal de Azure: [crear y administrar los trabajos de la base de datos elástica](sql-database-elastic-jobs-create-and-manage.md). 
6. O bien use scripts de PowerShell: [Creación y administración de trabajos de base de datos elástica de Base de datos SQL (vista previa)](sql-database-elastic-jobs-powershell.md).

## <a name="idempotent-scripts"></a>Scripts idempotentes
deben ser scripts Hello [idempotente](https://en.wikipedia.org/wiki/Idempotence). En otras palabras, "idempotente" significa que si el script de Hola se realiza correctamente y vuelva a ejecutar, hello mismo resultado se produce. Una secuencia de comandos puede producir errores debido a problemas de red tootransient. En ese caso, el trabajo de hello reintentará automáticamente script de Hola ejecuta un número de veces antes de desisting preestablecido. Una secuencia de comandos idempotente tiene Hola el mismo resultado incluso si se ha ejecutado correctamente dos veces. 

Una táctica simple es tootest existencia Hola de un objeto antes de crearla.  

    IF NOT EXIST (some_object)
    -- Create hello object 
    -- If it exists, drop hello object before recreating it.

De forma similar, una secuencia de comandos debe ser capaz de tooexecute correctamente comprobando lógicamente y contra las condiciones que encuentra.

## <a name="failures-and-logs"></a>Errores y registros
Si se produce un error en una secuencia de comandos después de varios intentos, el trabajo de Hola registra Hola error y continúa. Después de que finalice un trabajo (es decir, una ejecución en todas las bases de datos en el grupo de hello), puede comprobar su lista de intentos fallidos. registros de Hello proporcionan detalles toodebug defectuoso scripts. 

## <a name="group-types-and-creation"></a>Tipos de grupo y creación
Hay dos tipos de grupos: 

1. Conjuntos de particiones
2. Grupos personalizados

Grupos de conjunto de particiones se crean mediante hello [herramientas de base de datos elástica](sql-database-elastic-scale-introduction.md). Cuando se crea un grupo de conjunto de particiones, las bases de datos se agregan o se quitan del grupo de hello automáticamente. Por ejemplo, una nueva partición será automáticamente en el grupo de hello cuando se agrega toohello mapa de particiones. A continuación, se puede ejecutar un trabajo en grupo de Hola.

Grupos personalizados, en Hola otra parte, se definen de forma rígida. Debe agregar o quitar explícitamente las bases de datos de los grupos personalizados. Si se quita una base de datos en el grupo de hello, el trabajo de hello intentará script de Hola toorun en lo que produce un error eventual de base de datos de Hola. Grupos creados con hello portal de Azure actualmente son grupos personalizados. 

## <a name="components-and-pricing"></a>Componentes y precios
Hello componentes siguientes funcionan conjuntamente toocreate un servicio de nube de Azure que permite la ejecución ad hoc de trabajos administrativos. componentes de Hello están instalados y se configura automáticamente durante la instalación, en su suscripción. Puede identificar Hola servicios como todas ellas han Hola mismo autogenerada nombre. nombre de Hello es único y consta de hello prefijo "edj" seguido de 21 caracteres generadas de forma aleatoria.

* **Servicio de nube de Azure**: trabajos de bases de datos elásticas (vista previa) se entrega como una nube de Azure hospedada por el cliente tooperform ejecución del servicio de hello tareas solicitadas. Desde el portal de hello, servicio de Hola se implementa y hospeda en su suscripción de Microsoft Azure. Hola implementado de forma predeterminada se ejecuta con mínimo de Hola de dos roles de trabajo para lograr alta disponibilidad. tamaño predeterminado de Hola de cada rol de trabajo (ElasticDatabaseJobWorker) se ejecuta en una instancia de A0. Para obtener información sobre los precios, vea [Precios de servicios de nube](https://azure.microsoft.com/pricing/details/cloud-services/). 
* **La base de datos de SQL Azure**: servicio de hello utiliza una base de datos de SQL Azure, conocido como hello **base de datos de control** toostore todos Hola trabajo metadatos. nivel de servicio de Hello predeterminada es un S0. Para obtener información sobre precios, vea [Precios de bases de datos SQL](https://azure.microsoft.com/pricing/details/sql-database/).
* **Service Bus de Azure**: es un Bus de servicio de Azure para coordinar el trabajo de hello en hello servicio de nube de Azure. Vea [Precios del bus de servicio](https://azure.microsoft.com/pricing/details/service-bus/).
* **Almacenamiento de Azure**: se usa la cuenta de un almacenamiento de Azure toostore diagnóstico salida de registro de eventos de Hola que un problema requiere una depuración más exhaustiva (vea [habilitar diagnósticos en servicios en la nube y máquinas virtuales](../cloud-services/cloud-services-dotnet-diagnostics.md)). Para obtener información sobre precios, vea [Precios de almacenamiento de Azure](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-elastic-database-jobs-work"></a>Funcionamiento de Trabajos de base de datos elástica
1. Se designa una Base de datos SQL de Azure como **base de datos de control** que almacena todos los datos de estado y los metadatos.
2. se obtiene acceso a base de datos de control de Hola Hola **trabajo servicio** tooexecute trabajos toolaunch y realizar un seguimiento.
3. Dos roles diferentes se comunican con la base de datos de control de hello: 
   * Controlador: Determina qué trabajos requieren Hola de tooperform tareas solicitado trabajos y trabajos con errores reintentos mediante la creación de nuevas tareas de trabajo.
   * Ejecución de la tarea de trabajo: Lleva a cabo las tareas de trabajo de Hola.

### <a name="job-task-types"></a>Tipos de tareas de trabajo
Hay varios tipos de tareas de trabajo que efectúan la ejecución de trabajos:

* ShardMapRefresh: Consultas Hola toodetermine de mapa de particiones usan todas las bases de datos de hello como particiones
* ScriptSplit: Divide el script de Hola en instrucciones 'GO' en lotes
* ExpandJob: crea trabajos secundarios para cada base de datos en un trabajo destinado a un grupo de bases de datos
* ScriptExecution: ejecuta un script en una base de datos concreta con las credenciales que se definan
* Dacpac: Se aplica un DACPAC tooa base de datos concreta con credenciales determinadas

## <a name="end-to-end-job-execution-work-flow"></a>Flujo de trabajo de ejecución de trabajos completo
1. Usa Hola Portal u Hola API de PowerShell, se inserta un trabajo en hello **base de datos de control**. trabajo de Hello solicita la ejecución de una secuencia de comandos de Transact-SQL para un grupo de bases de datos mediante credenciales específicas.
2. controlador de Hello identifica nuevo trabajo de Hola. Tareas de trabajo se crean y ejecutan la secuencia de comandos de toosplit hello y bases de datos del grupo de toorefresh Hola. Por último, un nuevo trabajo se crea y ejecuta el trabajo de hello tooexpand y crea trabajos, donde cada trabajo secundario es tooexecute especificado Hola script de Transact-SQL en una base de datos individual en el grupo de Hola de nuevo elemento secundario.
3. controlador de Hello identifica Hola creado trabajos secundarios. Para cada trabajo, controlador de hello crea y desencadena una secuencia de comandos de trabajo tarea tooexecute hello en una base de datos. 
4. Después de completar todas las tareas de trabajo, el controlador de hello actualiza el estado de tooa completado de trabajos de Hola. 
   En cualquier momento durante la ejecución del trabajo, Hola PowerShell API puede ser usado tooview Hola estado actual de la ejecución del trabajo. Todas las horas devolviendo Hola PowerShell APIs se representan en formato UTC. Si lo desea, una solicitud de cancelación puede ser toostop iniciado por un trabajo. 

## <a name="next-steps"></a>Pasos siguientes
[Instalar componentes de hello](sql-database-elastic-jobs-service-installation.md), a continuación, [crear y agregar un registro de grupo de Hola de bases de datos en la base de datos tooeach](sql-database-manage-logins.md). toofurther comprender la administración y creación de trabajos, consulte [crear y administrar trabajos de base de datos elástica](sql-database-elastic-jobs-create-and-manage.md). Vea también [Introducción a Trabajos de base de datos elástica](sql-database-elastic-jobs-getting-started.md).

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-overview/elastic-jobs.png
<!--anchors-->



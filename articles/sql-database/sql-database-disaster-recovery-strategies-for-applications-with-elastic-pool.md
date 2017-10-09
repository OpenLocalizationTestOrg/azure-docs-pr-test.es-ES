---
title: "soluciones de recuperación ante desastres de aaaDesign - base de datos de SQL de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodesign la solución de nube para la recuperación ante desastres eligiendo el patrón de hello derecho de conmutación por error."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2db99057-0c79-4fb0-a7f1-d1c057ec787f
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 9d9eca7570c7a01c992d0b33d449721709b471c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-strategies-for-applications-using-sql-database-elastic-pools"></a>Estrategias de recuperación ante desastres para aplicaciones que usan grupos elásticos de SQL Database
Durante años de Hola hemos hemos visto que Servicios de nube no son infalible y producen incidentes catastróficos. Base de datos SQL proporciona varios tooprovide capacidades de continuidad del negocio hello de la aplicación cuando se producen estos incidentes. [Grupos elásticos](sql-database-elastic-pool.md) y bases de datos solo admiten Hola mismo tipo de recuperación de desastres. En este artículo se describen varias estrategias de recuperación ante desastres para grupos elásticos que sacan partido a esas características de continuidad de negocio de Base de datos SQL.

Este artículo usa Hola siguiendo el patrón de aplicación de ISV de SaaS canónico:

<i>Una aplicación web modernos basados en la nube aprovisiona una base de datos SQL para cada usuario final. Hola ISV tiene muchos clientes y, por tanto, utiliza muchas bases de datos, conocidas como bases de datos de inquilino. Ya que las bases de datos del inquilino de hello normalmente tienen patrones de actividad imprevisible, Hola ISV usa un costo de base de datos de grupo elástico toomake Hola muy predecible durante períodos ampliados de tiempo. grupo elástico Hello también simplifica la administración del rendimiento de hello cuando pico de actividad de usuario de hello. Además la aplicación hello de toohello inquilino bases de datos también utiliza varias bases de datos toomanage los perfiles de usuario, seguridad, recopilan etcetera los patrones de uso. Disponibilidad de inquilinos individuales de hello no afecta a la disponibilidad de la aplicación hello como todo. Sin embargo, hello disponibilidad y el rendimiento de las bases de datos de administración es fundamentales para la función de la aplicación hello y si las bases de datos de administración de hello son Hola sin conexión de la aplicación completa está sin conexión.</i>  

En este artículo se describe las estrategias de recuperación ante desastres que abarcan una variedad de escenarios de costo inicio confidencial aplicaciones tooones con requisitos estrictos de disponibilidad.

## <a name="scenario-1-cost-sensitive-startup"></a>Escenario 1. Inicio sensible al costo
<i>Acabo de crear una empresa y me preocupan sobremanera los costos.  Desea toosimplify implementación y administración de la aplicación hello y ¿tengo un SLA limitado para los clientes individuales. Pero desea aplicación hello de tooensure como un todo nunca está sin conexión.</i>

requisito de toosatisfy Hola simplicidad, implementar todas las bases de datos de inquilino en un grupo elástico Hola región de Azure de su elección e implementar bases de datos de administración como la replicación geográfica de las bases de datos únicos. Para la recuperación ante desastres de Hola de inquilinos, use la restauración geográfica, que se incluye sin costo adicional alguno. disponibilidad de hello tooensure de Hola bases de datos de administración, replicar geográficamente ellos región tooanother uso de un grupo de conmutación por error automática (en vista previa) (paso 1). costo actual de Hola de configuración de recuperación ante desastres de hello en este escenario es toohello igual costo total de bases de datos secundarias de Hola. Esta configuración se muestra en el diagrama siguiente Hola.

![En la Ilustración 1](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-1.png)

Si se produce una interrupción en la región principal de hello, Hola toobring de pasos de recuperación se ilustran la aplicación en línea con un diagrama siguiente Hola.

* grupo de conmutación por error de Hello inicia la conmutación automática por error de región de recuperación ante desastres de toohello de hello administración base de datos. aplicación Hello es toohello reconectada automáticamente nuevas principal y todas las nuevas cuentas y las bases de datos de inquilinos se crean en la región de recuperación ante desastres de Hola. los clientes existentes de Hello verán sus datos no está disponibles temporalmente.
* Crear grupo elástico Hola con hello misma configuración que el grupo original de hello (2).
* Utilizar la restauración geográfica toocreate copias de bases de datos de inquilino de hello (3). Puede considerar desencadenar restauraciones individuales hello las conexiones de usuario final de Hola o utilizar algún otro esquema de prioridad específica de la aplicación.


En este momento la aplicación está vuelve a estar conectada en la región de recuperación ante desastres de hello, pero algunos clientes experimentan retraso al tener acceso a sus datos.

![Ilustración 2](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-2.png)

Si la interrupción de hello era temporal, es posible que esa región principal Hola se recuperarán a Azure antes de que todas las restauraciones de base de datos de hello están completadas en la región de hello recuperación ante desastres. En este caso, organizar móvil región principal de hello aplicación toohello atrás. proceso de Hello lleva a cabo los pasos de Hola se muestra en el diagrama siguiente Hola.

* Cancele todas las solicitudes de restauración geográfica pendientes.   
* Conmutar por región principal bases de datos toohello administración de hello (5). Después de la recuperación de la región de hello, los elementos antiguos Hola automáticamente han convertido en secundarias. Ahora vuelven a cambiar los roles. 
* Cambiar la región principal de la aplicación hello conexión cadena toopoint toohello atrás. Ahora todas las cuentas nuevas y las bases de datos de inquilinos se crean en la región principal de Hola. Algunos clientes existentes verán que sus datos no están disponibles temporalmente.   
* Establecer todas las bases de datos en hello DR grupo solo tooread tooensure que no se puede modificar en la región de recuperación ante desastres de hello (6). 
* Para cada base de datos en el grupo de recuperación ante desastres que ha cambiado desde la recuperación de Hola Hola, cambie el nombre o eliminar bases de datos correspondientes de hello en el grupo principal de hello (7). 
* Hola copia actualiza bases de datos de hello conjunto principal de toohello de grupo de recuperación ante desastres (8). 
* Eliminar grupo de recuperación ante desastres de hello (9)

En este momento la aplicación está en línea en la región principal de Hola a todos los inquilinos bases de datos disponibles en el grupo principal de Hola.

![Ilustración 3](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-3.png)

clave de Hello **beneficiarse** de esta estrategia es de bajo coste en curso para la redundancia de nivel de datos. Las copias de seguridad se realizan automáticamente por hello servicio de base de datos de SQL con ninguna aplicación de reescritura y sin costo adicional alguno.  Hola se incurre solo cuando se restauran las bases de datos elástica Hola. Hola **equilibrio** es que la recuperación completa de Hola de todas las bases de datos de inquilino tarda mucho tiempo. Hello período de tiempo depende Hola número total de la restauración iniciar Hola recuperación ante desastres de región y el tamaño total de hello las bases de datos de inquilinos. Incluso si se da prioridad a restauraciones algunos inquilinos sobre otras, debe competir con hello todos los otros restauraciones que se inician en Hola misma región como servicio de hello arbitra y limita toominimize Hola impacto global en las bases de datos de hello los clientes existentes. Además, no se puede iniciar recuperación Hola de bases de datos de inquilino de hello hasta que se cree el nuevo grupo elástico hello en la región de recuperación ante desastres de Hola.

## <a name="scenario-2-mature-application-with-tiered-service"></a>Escenario 2. Aplicación madura con servicio en capas
<i>Tengo una aplicación de SaaS desarrollada con ofertas de servicio en capas y distintos Acuerdos de Nivel de Servicio para clientes de versiones de prueba y de pago. Para los clientes de prueba de hello, tengo tooreduce Hola costo tanto como sea posible. Clientes de prueba pueden tardar un tiempo de inactividad, pero deseo tooreduce su probabilidad. Para los clientes que pagan de hello, los tiempos de inactividad es un riesgo de vuelo. Por lo que deseo toomake Asegúrese de que los clientes que pagan siempre son tooaccess capaz de sus datos.</i> 

toosupport este escenario, independiente Hola inquilinos de prueba de pago, los inquilinos colocándolos en diferentes grupos elásticos. los clientes de prueba de Hello tienen inferior eDTU por inquilino y SLA inferior con un tiempo de recuperación. los clientes que pagan Hola están en un grupo con mayor eDTU por inquilino y un SLA superior. tooguarantee Hola menor tiempo de recuperación de, las bases de datos del inquilino de hello pago los clientes tienen replicación geográfica. Esta configuración se muestra en el diagrama siguiente Hola. 

![Ilustración 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-4.png)

Como en el primer escenario hello, bases de datos de administración de hello están muy activas, por lo que usar una sola base de datos replicadas geográficamente para él (1). Esto garantiza un rendimiento predecible Hola para nuevas suscripciones de cliente, las actualizaciones de perfiles y otras operaciones de administración. Hello en el que residen primarios Hola de bases de datos de administración de Hola Hola principal región está y hello en el que residen secundarias Hola de bases de datos de administración de Hola Hola DR región está.

Hello las bases de datos del inquilino de pago de los clientes tienen bases de datos activas en hello "pago" grupo aprovisionado en la región principal de Hola. Aprovisionar un grupo secundario con hello mismo nombre en la región de hello recuperación ante desastres. Cada inquilino es grupo de replicación geográfica toohello secundaria (2). Esto permite una recuperación rápida de todas las bases de datos de inquilino mediante la conmutación por error. 

Si se produce una interrupción en la región principal de hello, Hola toobring de pasos de recuperación en línea la aplicación se ilustran en el diagrama siguiente hello:

![Ilustración 5.](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-5.png)

* Conmutar inmediatamente por región de recuperación ante desastres de hello administración bases de datos toohello (3).
* Cambiar región de la aplicación hello conexión cadena toopoint toohello recuperación ante desastres. Ahora todas las cuentas nuevas y las bases de datos de inquilinos se crean en el área de recuperación ante desastres de Hola. los clientes de prueba existentes de Hello verán sus datos no está disponibles temporalmente.
* Conmutar por error Hola pago toohello grupo de bases de datos del inquilino en hello DR región tooimmediately restaurar su disponibilidad (4). Puesto que Hola conmutación por error es un cambio del nivel de metadatos rápido, considere la posibilidad de una optimización donde se activan Hola individuales, las conmutaciones por error a petición por las conexiones de usuario final de Hola. 
* Si el tamaño del grupo secundario de eDTU ha sido inferior a Hola principal porque Hola bases de datos secundarias solo Hola requiere capacidad tooprocess Hola cambio registros mientras estaban elementos secundarios, inmediatamente aumentar la capacidad del grupo de hello ahora tooaccommodate Hola completa carga de trabajo de todos los inquilinos (5). 
* Crear nuevo grupo de elástico de hello con hello mismo nombre y Hola misma configuración de región de hello recuperación ante desastres para bases de datos de hello prueba los clientes (6). 
* Una vez que se crea el grupo de hello prueba los clientes, utilizar bases de datos de la restauración geográfica toorestore Hola inquilino de prueba individual en el nuevo grupo de hello (7). Considere la posibilidad de activar restauraciones individuales hello las conexiones de usuario final de Hola o utilizar algún otro esquema de prioridad específica de la aplicación.

En este momento la aplicación está vuelve a estar conectada en la región de recuperación ante desastres de Hola. Todos los clientes que pagan tienen acceso a datos de tootheir mientras los clientes de prueba de hello experimentar retraso al tener acceso a sus datos.

Cuando se recupera la región principal de hello Azure *después* se haya restaurado la aplicación hello en región Hola DR puede continuar ejecutando la aplicación hello en dicha región. también puede optar región principal de toofail toohello atrás. Si se recupera la región principal de hello *antes de* se completa el proceso de conmutación por error de Hola, considere la posibilidad de errores de copia de forma inmediata. conmutación por recuperación de Hello lleva a cabo los pasos de Hola se muestra en el diagrama siguiente hello: 

![Ilustración 6.](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-6.png)

* Cancele todas las solicitudes de restauración geográfica pendientes.   
* Conmutar por error bases de datos de administración de hello (8). Después de la recuperación de la región de hello, hello antiguo principal pone automáticamente Hola secundaria. Ahora se convierte en Hola principal nuevo.  
* Conmutar por error Hola pagada bases de datos de inquilino (9). Del mismo modo, después de la recuperación de la región de hello, primarios antiguo Hola pone automáticamente secundarias Hola. Ahora vuelven a ser primarios Hola. 
* Conjunto Hola restaura bases de datos de prueba que han cambiado en la región de recuperación ante desastres de hello solo tooread (10).
* Para cada base de datos en el grupo de recuperación ante desastres de clientes de prueba de Hola que ha cambiado desde la recuperación de hello, cambie el nombre o eliminar base de datos correspondiente de hello en el conjunto principal de los clientes de prueba hello (11). 
* Hola copia actualiza bases de datos de hello conjunto principal de toohello de grupo de recuperación ante desastres (12). 
* Eliminar grupo de recuperación ante desastres de hello (13) 

> [!NOTE]
> operación de conmutación por error de Hello es asincrónica. tiempo de recuperación de toominimize hello es importante que ejecute el comando de conmutación por error de hello inquilino bases de datos en lotes de al menos 20 bases de datos. 
> 
> 

clave de Hello **beneficiarse** de esta estrategia es que proporciona SLA más alto de Hola para los clientes que pagan de Hola. También garantiza que evaluaciones nueva Hola se desbloquean en cuanto se crea el grupo de recuperación ante desastres de pruebas de Hola. Hola **equilibrio** es que este programa de instalación aumenta el costo total Hola de bases de datos de inquilino de Hola por costo de Hola de grupo de recuperación ante desastres secundario hello para los clientes de pago. Además, si grupo secundario de hello tiene un tamaño diferente, los clientes que pagan Hola experimentan un rendimiento inferior tras la conmutación por error hasta que hello actualización de grupo de región de hello DR se complete. 

## <a name="scenario-3-geographically-distributed-application-with-tiered-service"></a>Escenario 3. Aplicación distribuida geográficamente con servicio en capas
<i>Tengo una aplicación de SaaS desarrollada con ofertas de servicio en capas. Desea toooffer una toomy SLA muy agresiva los clientes de pago y minimizar el riesgo de Hola de impacto cuando se producen interrupciones, ya que incluso breve interrupción puede provocar descontento de los clientes. Es fundamental que los clientes que pagan de hello siempre puede tener acceso a sus datos. las evaluaciones de Hello son gratuitos y no se ofrece un SLA durante el período de prueba de Hola.</i> 

toosupport este escenario, utilice grupos elásticos independiente tres. Las bases de datos del inquilino de los clientes de pago, aprovisionar dos grupos de igual tamaño con alta Edtu por base de datos en dos hello toocontain de diferentes regiones. Hola tercer grupo servidor que contiene a los inquilinos de prueba de hello puede tener inferior Edtu por base de datos y haber aprovisionado en uno de dos regiones de Hola.

tooguarantee Hola menor tiempo de recuperación durante las interrupciones, las bases de datos del inquilino de hello pago los clientes tienen replicación geográfica en el 50% de bases de datos principales de hello en cada una de las regiones de hello dos. Del mismo modo, cada región tiene 50% de bases de datos secundarias de Hola. De esta manera, si una región está sin conexión, solo el 50% de hello las bases de datos de los clientes de pago se ven afectado y toofail sobre. Hello otras bases de datos permanecen intactos. Esta configuración se muestra en hello siguiente diagrama:

![Ilustración 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-7.png)

Como en escenarios anteriores de hello, bases de datos de administración de hello están muy activos por lo que se configuran bases de datos de replicación geográfica como una sola (1). Esto garantiza un rendimiento predecible Hola de nuevas suscripciones de cliente hello, las actualizaciones de perfiles y otras operaciones de administración. Región A es la región principal de Hola para bases de datos de administración de Hola y Hola región B se usará para la recuperación de bases de datos de administración de Hola.

las bases de datos del inquilino de Hello pago los clientes también tienen replicación geográfica pero con colores primarios y secundarios se divide entre región A y la región B (2). De esta manera, bases de datos de hello inquilino principal afectados por la interrupción de hello pueden conmutar por error toohello otra región y estén disponibles. Hola sí la mitad de las bases de datos del inquilino de hello no se afecta en absoluto. 

diagrama siguiente de Hello muestra tootake de pasos de recuperación de hello si se produce una interrupción en la región A.

![Ilustración 5.](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-8.png)

* Conmutar inmediatamente tooregion de bases de datos de administración de hello B (3).
* Cambiar conexión cadena toopoint toohello administración bases de datos la aplicación hello en la región B. modificar Hola administración bases de datos toomake seguro Hola nuevas cuentas y las bases de datos de inquilinos se crean en la región B y bases de datos de inquilino existentes Hola se encuentran allí como bueno. los clientes de prueba existentes de Hello verán sus datos no está disponibles temporalmente.
* Conmutar por error Hola pago toopool de bases de datos del inquilino 2 en la región B tooimmediately restaurar su disponibilidad (4). Puesto que Hola conmutación por error es un cambio del nivel de metadatos rápido, puede considerar una optimización donde se activan Hola individuales, las conmutaciones por error a petición por las conexiones de usuario final de Hola. 
* Desde ahora grupo 2 contiene solo las bases de datos principales, Hola cargas de trabajo total en hello grupo aumenta e inmediatamente puede aumentar su tamaño eDTU (5). 
* Crear nuevo grupo de elástico de hello con hello mismo nombre y Hola misma configuración en la región de hello B para bases de datos de hello prueba los clientes (6). 
* Una vez que se crea al grupo de hello usar base de datos de la restauración geográfica toorestore Hola inquilino de prueba individual en el grupo de hello (7). Puede considerar desencadenar restauraciones individuales hello las conexiones de usuario final de Hola o utilizar algún otro esquema de prioridad específica de la aplicación.

> [!NOTE]
> operación de conmutación por error de Hello es asincrónica. tiempo de recuperación de toominimize hello, es importante que ejecute el comando de conmutación por error de hello inquilino bases de datos en lotes de al menos 20 bases de datos. 
> 

En este momento la aplicación está vuelve a estar conectada en la región B. Todos los clientes que pagan tienen acceso a datos de tootheir mientras los clientes de prueba de hello experimentar retraso al tener acceso a sus datos.

Cuando se recupera la región A necesita toodecide si desea toouse región B para clientes de prueba o un grupo de clientes de prueba de conmutación por recuperación toousing hello en la región A. Un criterio podría ser Hola % de las bases de datos de inquilino de prueba modificado desde la recuperación de Hola. Sin tener en cuenta esa decisión, debe equilibrar toore Hola pago inquilinos entre dos grupos. diagrama de Hello siguiente ilustra el proceso de hello cuando las bases de datos del inquilino de prueba de hello producirá un error A. tooregion back-  

![Ilustración 6.](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-9.png)

* Cancelar todos los bloques de tootrial recuperación ante desastres de las solicitudes de restauración geográfica pendientes.   
* Conmutar por base de datos de administración de hello (8). Después de la recuperación de la región de hello, principal antiguo Hola automáticamente se convirtió en hello secundaria. Ahora se convierte en Hola principal nuevo.  
* Seleccione qué bases de datos de pago inquilino producirá un error toopool back-1 e iniciar conmutación por error tootheir secundarias (9). Después de la recuperación de la región de hello, todas las bases de datos en el grupo 1 automáticamente pasara a ser elementos secundarios. Ahora el 50 % volverán a ser principales. 
* Reducir tamaño de Hola de eDTU del grupo 2 toohello original (10).
* Restaurar de conjunto de todas las bases de datos de prueba en la región de hello B solo tooread (11).
* Para cada base de datos de prueba grupo de recuperación ante desastres de Hola que ha cambiado desde la recuperación de hello, cambiar ni eliminar la base de datos correspondiente de hello en grupo principal prueba de hello (12). 
* Hola copia actualiza bases de datos de hello conjunto principal de toohello de grupo de recuperación ante desastres (13). 
* Eliminar grupo de recuperación ante desastres de hello (14) 

clave de Hello **ventajas** de esta estrategia son:

* Admite SLA más exigente de Hola Hola los clientes que pagan porque garantiza que una interrupción del servicio no puede afectar a más del 50% de las bases de datos del inquilino de Hola. 
* Garantiza que los ensayos nueva Hola sean desbloqueados tan pronto como pista de hello grupo de recuperación ante desastres se crea durante la recuperación de Hola. 
* Permite el uso más eficaz de la capacidad del grupo de hello como 50% de las bases de datos secundarias en el grupo 1 y grupo 2 se garantiza que toobe menos activo de bases de datos principales de Hola.

Hola principal **ventajas e inconvenientes** son:

* las operaciones CRUD de Hello en bases de datos de administración de hello tienen menor latencia para hello los usuarios finales conectados tooregion A que para los usuarios finales conectados de hello tooregion B mientras se ejecutan contra Hola principal de bases de datos de administración de Hola.
* Requiere un diseño más complejo de base de datos de administración de Hola. Por ejemplo, cada registro de inquilino tiene una etiqueta de ubicación que necesita toobe cambiado durante la conmutación por error y conmutación por recuperación.  
* Hola, los clientes que pagan puede experimentar un rendimiento menor de lo habitual hasta que hello actualización de grupo de región B se complete. 

## <a name="summary"></a>Resumen
En este artículo se centra en estrategias de recuperación ante desastres de hello para el nivel de base de datos de hello utilizado por una aplicación de varios inquilinos de ISV de SaaS. Hello estrategia que elija depende de necesidades de hello de la aplicación hello, como modelo de negocio de hello, SLA de Hola desee toooffer tooyour clientes, presupuesto restricción etcetera. Describe cada una estrategia contornos Hola ventajas y compensaciones por lo que puede tomar una decisión informada. Además, la aplicación específica probablemente incluya otros componentes de Azure. Para revisar su orientación de continuidad del negocio y coordinar la recuperación de Hola de nivel de base de datos de hello con ellos. toolearn más información acerca de la administración de recuperación de aplicaciones de base de datos en Azure, consulte demasiado[diseño de soluciones de nube para recuperación ante desastres](sql-database-designing-cloud-solutions-for-disaster-recovery.md).  

## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca de las copias de seguridad automatizada de base de datos SQL Azure, consulte [copias de seguridad automáticas de base de datos SQL](sql-database-automated-backups.md).
* Para obtener una descripción general y los escenarios de la continuidad empresarial, consulte [Información general sobre la continuidad empresarial](sql-database-business-continuity.md).
* toolearn sobre el uso de copias de seguridad automatizadas para la recuperación, consulte [restaurar una base de datos de copias de seguridad de hello iniciadas por el servicio](sql-database-recovery-using-backups.md).
* toolearn acerca de las opciones de recuperación más rápidos, consulte [replicación geográfica activa](sql-database-geo-replication-overview.md).
* toolearn sobre el uso de copias de seguridad automatizadas para el archivado, vea [copiar base de datos](sql-database-copy.md).


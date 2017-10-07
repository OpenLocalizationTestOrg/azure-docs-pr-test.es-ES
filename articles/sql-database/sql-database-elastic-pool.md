---
title: "¿aaaWhat son grupos elásticos? Administración de varias instancias de SQL Database: Azure | Microsoft Docs"
description: "Administración y escalado de muchas instancias de SQL Database, cientos y miles, mediante los grupos elásticos. Un precio para los recursos que se puede distribuir cuando sea necesario."
keywords: varias bases de datos, recursos de base de datos, rendimiento de la base de datos
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: b46e7fdc-2238-4b3b-a944-8ab36c5bdb8e
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 07/31/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 2098d7817ebe1277b5c131421f23c00803ec78f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-pools-help-you-manage-and-scale-multiple-sql-databases"></a>Los grupos elásticos pueden ayudarle a administrar y escalar varias instancias de SQL Database

Los grupos elásticos de SQL Database son una solución simple y rentable para la administración y escalado de varias bases de datos que tienen distintas e imprevisibles demandas de uso. las bases de datos de Hello en un grupo elástico se encuentran en un único servidor de base de datos de SQL Azure y compartir un número de conjunto de recursos ([unidades de transacción de base de datos elástica](sql-database-what-is-a-dtu.md) (Edtu)) a un precio de conjunto. Grupos elásticos en la base de datos de SQL Azure permiten SaaS a los desarrolladores toooptimize Hola precio rendimiento para un grupo de bases de datos dentro de un presupuesto prescrito al tiempo que ofrece la flexibilidad de rendimiento para cada base de datos.   

> [!NOTE]
> Los grupos elásticos están disponibles con carácter general (GA) en todas las regiones de Azure excepto oeste de la India, donde actualmente se encuentran en versión preliminar.  La disponibilidad general de grupos elásticos en esta región se producirá tan pronto como sea posible.
>

## <a name="what-are-sql-elastic-pools"></a>¿Qué son los grupos elásticos de SQL? 

Los desarrolladores de SaaS crean aplicaciones en los niveles superiores de datos de la escala que constan de varias bases de datos. Un patrón de aplicación común es tooprovision una sola base de datos para cada cliente. Pero distintos clientes suelen tienen los patrones de uso de variables y no previstos, y es difícil toopredict requisitos de recursos de Hola de cada usuario de base de datos individuales. Tradicionalmente, había dos opciones: 

- Aprovisionar recursos en exceso basándose en el uso máximo y pagando de más, o
- Toosave de aprovisionar los costos, a expensas de Hola de satisfacción del cliente y de rendimiento durante los picos de actividad. 

Grupos elásticos solucionar este problema asegurándose de que las bases de datos obtengan recursos de rendimiento de Hola que necesitan cuando la necesitan. Proporcionan un mecanismo de asignación de recursos simples dentro de un presupuesto predecible. toolearn más información acerca de los patrones de diseño para aplicaciones de SaaS con grupos elásticos, consulte [patrones de diseño para aplicaciones de SaaS multiempresa con base de datos de SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Elastic-databases-helps-SaaS-developers-tame-explosive-growth/player]
>

Grupos elásticos habilitar Hola developer toopurchase [unidades de transacción de base de datos elástica](sql-database-what-is-a-dtu.md) (Edtu) para un grupo compartido por varios períodos impredecible de tooaccommodate de las bases de datos de uso de las bases de datos individuales. requisito de eDTU de Hola para un grupo se determina según la utilización agregado de Hola de sus bases de datos. número de Hola de grupo de Edtu toohello disponibles se controla mediante asignación de desarrollador de Hola. desarrollador de Hello simplemente agrega el grupo de servidores de bases de datos toohello, Establece el mínimo de Hola y Edtu máximo para las bases de datos de hello y, a continuación, Establece hello eDTU del grupo de hello en función de su presupuesto de. Un desarrollador puede usar grupos de tooseamlessly crecer su servicio de un negocio maduro de tooa inicio eficiente en escala creciente.

En el grupo de hello, bases de datos individuales tienen tooauto escala de hello flexibilidad dentro de los parámetros de conjunto. Con mucha carga, una base de datos puede consumir más Edtu toomeet demanda. Las bases de datos con cargas ligeras consumen menos y las bases de datos sin carga no consumen ninguna eDTU. Aprovisionamiento de recursos para el grupo completo de hello en lugar de para las bases de datos únicos simplifica las tareas de administración. Además de tener un presupuesto de predicción para el grupo de Hola. Edtu adicionales puede agregarse tooan grupo existente sin tiempo de inactividad de la base de datos, salvo que las bases de datos de Hola que necesite toobe movido tooprovide Hola adicional recursos para la nueva reserva de eDTU Hola de proceso. De manera similar, si ya no se necesitan eDTU adicionales, se pueden quitar de un grupo existente en cualquier momento dado. Y puede agregar o restar el grupo de servidores de bases de datos toohello. Si una base de datos infrautiliza recursos de forma predecible, sáquela del grupo.

Puede crear y administrar un grupo elástico con hello [portal de Azure](sql-database-elastic-pool-manage-portal.md), [PowerShell](sql-database-elastic-pool-manage-powershell.md), [Transact-SQL](sql-database-elastic-pool-manage-tsql.md), [C#](sql-database-elastic-pool-manage-csharp.md), y Hola API de REST. 

## <a name="when-should-you-consider-a-sql-database-elastic-pool"></a>¿Cuándo se debe usar un grupo elástico de SQL Database?

Los grupos son apropiados para un amplio número de bases de datos con patrones de utilización específicos. Para una base de datos determinada, este patrón está caracterizado por una utilización media baja con picos de utilización relativamente poco frecuentes.

Hello más bases de datos puede agregar tooa Hola de grupo mayor se convierten en sus ahorros. Dependiendo de su patrón de uso de la aplicación, es posible toosee ahorro con tan sólo dos bases de datos de S3.  

siguiente Hola secciones le servirán cómo tooassess si la colección específica de las bases de datos puede beneficiarse de estar en un grupo. Hello ejemplos utilizan grupos estándares pero hello mismos principios también aplican tooBasic y los grupos de Premium.

### <a name="assessing-database-utilization-patterns"></a>Evaluación de los patrones de utilización de base de datos

Hello en la ilustración siguiente se muestra un ejemplo de una base de datos que emplea mucho tiempo de inactividad, pero tiene un pico periódicamente con la actividad. Se trata de un patrón de uso que es apropiado para un grupo:

   ![una base de datos única adecuada para un grupo](./media/sql-database-elastic-pool/one-database.png)

Para hello muestra el período de cinco minutos, picos DB1 seguridad too90 Dtu, pero su uso medio total es inferior a cinco Dtu. Un nivel de rendimiento es de S3 requiere toorun esta carga de trabajo en una sola base de datos, pero esto deja la mayoría de los recursos de hello sin usar durante los períodos de poca actividad.

Un grupo permite estos toobe Dtu sin usar que se comparte entre varias bases de datos y, por lo que reduce el costo necesaria y global de Dtu de Hola.

Basándose en el ejemplo de Hola a anterior, supongamos que hay bases de datos adicionales con los patrones de uso similares como DB1. En hello a continuación dos ilustraciones siguientes, Hola utilización de cuatro bases de datos y 20 bases de datos están organizadas por niveles en hello del mismo gráfico naturaleza de no superpuestos Hola de tooillustrate de su uso con el tiempo:

   ![cuatro bases de datos con un patrón de uso adecuado para un grupo](./media/sql-database-elastic-pool/four-databases.png)

  ![veinte bases de datos con un patrón de uso adecuado para un grupo](./media/sql-database-elastic-pool/twenty-databases.png)

uso de DTU agregado Hello en 20 todas las bases de datos se muestra en línea hello negro en hello anterior figura. Esto muestra que uso agregado de la DTU de hello nunca supera 100 Dtu e indica que 20 bases de datos de hello puedan compartir 100 Edtu durante este período de tiempo. Esto produce una reducción de 20 x en Dtu y una 13 x precio en comparación con la reducción tooplacing cada de bases de datos de hello en los niveles de rendimiento S3 para bases de datos únicos.

En este ejemplo es ideal para hello siguientes motivos:

* Existen grandes diferencias entre la utilización de picos y la utilización media por base de datos.  
* pico de uso de Hola para cada base de datos se produce en distintos puntos en el tiempo.
* Las eDTU se comparten entre varias bases de datos.

precio de Hola de un grupo es una función de hello Edtu de grupo. Mientras precio por unidad hello eDTU para un grupo es 1,5 x mayor que el precio por unidad hello DTU para una sola base de datos, **Edtu de grupo puede compartirse entre varias bases de datos y se necesita menos Edtu total**. Estas diferencias de precios y compartir eDTU son la base de hello del potencial de ahorro de precio de Hola que pueden proporcionar grupos.  

Hello siguientes reglas generales relacionadas con toodatabase recuento y la base de datos de uso de la Ayuda tooensure que ofrece un grupo de reduce el costo en comparación con los niveles de rendimiento toousing para bases de datos únicos.

### <a name="minimum-number-of-databases"></a>Número mínimo de bases de datos

Si suma de Hola de hello Dtu de niveles de rendimiento para las bases de datos únicos sea más de 1,5 x Edtu Hola necesarios para el grupo de hello, un grupo elástico es más rentable. Para tamaños disponibles, consulte [Límites de almacenamiento y de eDTU para grupos de bases de datos elásticas y bases de datos elásticas](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

***Ejemplo***<br>
Al menos dos bases de datos de S3 o bases de datos de al menos 15 S0 son necesarios para un toobe de grupo de 100 eDTU más rentables que el uso de los niveles de rendimiento para bases de datos únicos.

### <a name="maximum-number-of-concurrently-peaking-databases"></a>Número máximo de bases de datos de picos simultáneamente

Edtu de uso compartido, no todas las bases de datos de un grupo pueden utilizar simultáneamente los Edtu seguridad toohello límite disponible al utilizar los niveles de rendimiento para bases de datos únicos. Hola menos bases de datos al mismo tiempo máximo, eDTU del grupo de hello inferior Hola pueden establecer y hello que más de hello rentable de grupo se vuelve. En general, no más de 2/3 (o 67%) de las bases de datos de hello en el grupo de Hola simultáneamente deben alcanzar fácilmente tootheir eDTU limitan.

***Ejemplo***<br>
los costes de tooreduce para tres bases de datos de S3 en un grupo de eDTU 200, a lo sumo dos de estas bases de datos al mismo tiempo pueden elevarse en su uso. En caso contrario, si más de dos de estas cuatro bases de datos de S3 alcanzar fácilmente al mismo tiempo, grupo de hello tendría toomore toobe tamaño de 200 Edtu. Si el grupo de Hola es toomore cuyo tamaño ha cambiado de 200 Edtu, más bases de datos de S3 necesitaría toobe agrega costos de tookeep de toohello grupo inferiores a los niveles de rendimiento para bases de datos únicos.

Tenga en cuenta que este ejemplo no tiene en cuenta el uso de otras bases de datos en bloque de Hola. Si todas las bases de datos tienen algún uso en un momento dado en el tiempo, a continuación, menor que 2/3 (o 67%) de las bases de datos de hello pueden elevarse al mismo tiempo.

### <a name="dtu-utilization-per-database"></a>Utilización de DTU por base de datos
Una gran diferencia entre las horas punta de Hola y uso promedio de una base de datos indica largos períodos de poca utilización y breves períodos de uso elevado. Este patrón de uso es ideal para compartir recursos entre bases de datos. Debe considerarse utilizar una base de datos para un grupo cuando su uso máximo es aproximadamente 1,5 veces mayor que su uso medio.

***Ejemplo***<br>
Una base de datos de S3 que alcanza el máximo de Dtu de too100 y por término medio usa 67 Dtu o menor es un buen candidato para el uso compartido de Edtu de un grupo. O bien, una base de datos de S1 que alcanza el máximo de Dtu de too20 y por término medio usa 13 Dtu o menor es un buen candidato para un grupo.

## <a name="how-do-i-choose-hello-correct-pool-size"></a>¿Cómo se puede elegir el tamaño del grupo correcto de hello?

tamaño recomendado de Hola para un grupo depende de Edtu agregado de Hola y recursos de almacenamiento necesarios para todas las bases de datos en bloque de Hola. Esto implica determinar Hola mayor de siguiente hello:

* Dtu máximas usadas por todas las bases de datos de grupo de Hola.
* Bytes de almacenamiento máximo utilizados por todas las bases de datos de grupo de Hola.

Para tamaños disponibles, consulte [Límites de almacenamiento y de eDTU para grupos de bases de datos elásticas y bases de datos elásticas](#what-are-the-resource-limits-for-elastic-pools).

Base de datos SQL automáticamente se evalúa como el uso de recursos histórico Hola de bases de datos en un servidor de base de datos SQL existente y se recomienda configuración de grupo adecuado de Hola Hola portal de Azure. En las recomendaciones de toohello de suma, una experiencia integrada calcula el uso de eDTU de Hola para un grupo personalizado de bases de datos servidor hello. Esto permite un análisis "y si" toodo interactivamente agregando el grupo de servidores de bases de datos toohello y eliminándolas de los análisis de uso de recursos de tooget y consejos de ajuste de tamaño antes de confirmar los cambios. Para ver un procedimiento, consulte [Supervisión y administración de un grupo de bases de datos elásticas con el Portal de Azure](sql-database-elastic-pool-manage-portal.md).

En casos donde no se puede usar las herramientas, siguiente Hola paso a paso puede ayudarle a calcular si un grupo es más rentable que las bases de datos únicos:

1. Calcular Edtu Hola necesarios para el grupo de hello como sigue:

   MAX(<*Número total de bases de datos* X *promedio de uso de DTU por base de datos*>,<br>
   <*Número de bases de datos con picos simultáneos* X *Uso de picos de DTU por base de datos*)
2. Estimar el espacio de almacenamiento de hello necesario para el grupo de Hola agregando Hola número de bytes necesarios para todas las bases de datos de hello en el grupo de Hola. A continuación, determine el tamaño del grupo de eDTU Hola que proporciona esta cantidad de almacenamiento. Para conocer los límites de almacenamiento de grupo basados en el tamaño de grupo de eDTU, consulte [Límites de almacenamiento y de eDTU para grupos de bases de datos elásticas y bases de datos elásticas](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).
3. Tomar Hola mayor de hello eDTU estimaciones del paso 1 y el paso 2.
4. Vea hello [página de precios de base de datos de SQL](https://azure.microsoft.com/pricing/details/sql-database/) y buscar el tamaño de grupo de eDTU de hello más pequeño que es mayor que la estimación de hello en el paso 3.
5. Compara Hola grupo del precio del paso 5 toohello precio del uso de los niveles de rendimiento adecuado de Hola para bases de datos únicos.

### <a name="changing-elastic-pool-resources"></a>Cambio de los recursos de un grupo elástico

Puede aumentar o reducir el grupo elástico Hola recursos tooan disponibles en función de las necesidades de recursos.

* Cambiar normalmente Hola min Edtu por base de datos o el número máximo de Edtu por base de datos completa en 5 minutos o menos.
* Cambiar hello Edtu por grupo de depende de la cantidad total de Hola de espacio utilizado por todas las bases de datos de grupo de Hola. Los cambios tienen un duración media de 90 minutos o menos por cada 100 GB. Por ejemplo, si utiliza el espacio total de Hola por todas las bases de datos de grupo de hello es de 200 GB, Hola espera latencia para cambiar hello eDTU del grupo por grupo es de 3 horas o menos.

## <a name="what-are-hello-resource-limits-for-elastic-pools"></a>¿Cuáles son los límites de recursos de Hola para grupos elásticos?

Hola las tablas siguientes describe los límites de recursos de Hola de grupos elásticos.  Tenga en cuenta que los límites de recursos de Hola de bases de datos individuales en grupos elásticos suelen ser Hola mismas que para las bases de datos únicos fuera de grupos en función de Dtu y nivel de servicio de Hola.  Por ejemplo, hello max simultánea los trabajadores de una base de datos de S2 es 120 trabajadores.  Por lo tanto, Hola max simultáneas los trabajadores de una base de datos en un grupo estándar también es 120 trabajadores, si DTU máx. por base de datos en bloque de Hola Hola es 50 Dtu (que es el equivalente tooS2).

[!INCLUDE [SQL DB service tiers table for elastic pools](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Si se usan todas las Dtu de un grupo elástico, cada base de datos en bloque de hello recibe cantidades equivalentes de las consultas de tooprocess de recursos.  Hola servicio de base de datos SQL proporciona recursos compartidos equidad entre bases de datos al garantizar iguales intervalos de tiempo de ejecución. Uso compartido equidad de recursos de grupo elástico es además tooany cantidad de recursos garantizada que en caso contrario, base de datos de tooeach cuando hello DTU mín. por base de datos se establece en valor de tooa distinto de cero.

### <a name="database-properties-for-pooled-databases"></a>Propiedades de base de datos para bases de datos agrupadas

Hello en la tabla siguiente describe las propiedades de Hola para bases de datos agrupados.

| Propiedad | Description |
|:--- |:--- |
| Cantidad máxima de eDTU por base de datos |número máximo de Hola de Edtu que puede utilizar cualquier base de datos en bloque de hello, si basan disponibles en función del uso por otras bases de datos en bloque de Hola.  La cantidad máxima de eDTU por base de datos no garantiza la disponibilidad de recursos.  Esta es una configuración global que se aplica a las bases de datos de tooall en grupo Hola. Establecer max Edtu por base de datos lo suficientemente alto como toohandle picos sobre el uso de la base de datos de. Se espera cierto grado de sobrecarga porque grupo Hola generalmente se da por supuesto patrones de uso activos e inactivos para las bases de datos donde no se picos simultáneamente todas las bases de datos. Por ejemplo, suponga que el pico de uso de Hola por base de datos es 20 Edtu y solo el 20% de las bases de datos de hello 100 en el grupo de hello son máxima de Hola mismo tiempo.  Si hello eDTU máx. por base de datos se establece too20 Edtu, es razonable tooovercommit grupo de hello 5 veces y conjunto hello Edtu por too400 de grupo. |
| Cantidad mínima de eDTU por base de datos |número mínimo de Hola de Edtu que se garantiza que cualquier base de datos en bloque de Hola.  Esta es una configuración global que se aplica a las bases de datos de tooall en grupo Hola. Hola min eDTU por base de datos puede establecerse too0 y también es el valor predeterminado de Hola. Esta propiedad se establece tooanywhere entre el uso de eDTU promedio de hello y 0 por base de datos. producto de Hello del número de Hola de bases de datos de grupo de Hola y Hola min Edtu por base de datos no puede superar hello Edtu por grupo.  Por ejemplo, si un grupo tiene 20 bases de datos y hello eDTU mín. por base de datos establece too10 Edtu, a continuación, hello Edtu por grupo debe ser al menos tan grande como 200 Edtu. |
| Almacenamiento máximo de datos por base de datos |Hola máxima de almacenamiento de una base de datos en un grupo. Las bases de datos agrupados uso compartido del almacenamiento de grupo, por lo que el almacenamiento de base de datos es limitado toohello menor de restantes grupo de almacenamiento y almacenamiento máximo por base de datos. Almacenamiento máximo por base de datos hace referencia toohello tamaño máximo de archivos de datos de hello y no incluye el espacio de hello utilizado por los archivos de registro. |
|||

## <a name="using-other-sql-database-features-with-elastic-pools"></a>Empleo de otras características de SQL Database con grupos elásticos

### <a name="elastic-jobs-and-elastic-pools"></a>Trabajos elásticos y grupos elásticos

Con un grupo, las tareas de administración se simplifican al ejecutarse los scripts en **[trabajos elásticos](sql-database-elastic-jobs-overview.md)**. Un trabajo elástico elimina la mayoría de las tediosas tareas asociadas con un gran número de bases de datos. toobegin, consulte [Introducción a trabajos elásticos](sql-database-elastic-jobs-getting-started.md).

Para más información sobre otras herramientas de bases de datos para trabajar con varias bases de datos, consulte [Escalado horizontal con Azure SQL Database](sql-database-elastic-scale-introduction.md).

### <a name="business-continuity-options-for-databases-in-an-elastic-pool"></a>Opciones de continuidad de negocio para bases de datos de un grupo elástico
Agrupar las bases de datos generalmente compatibilidad Hola mismo [características de continuidad de negocio](sql-database-business-continuity.md) que son bases de datos de toosingle disponible.

- **Punto de restauración a un momento**: punto en el tiempo de restauración utiliza las copias de seguridad de base de datos automática toorecover una base de datos en un momento concreto de tooa de grupo en el tiempo. Consulte [Restauración a un momento dado](sql-database-recovery-using-backups.md#point-in-time-restore)

- **La restauración geográfica**: la restauración geográfica ofrece la opción de recuperación predeterminado de hello cuando una base de datos no está disponible debido a un incidente en la región de Hola donde se hospeda la base de datos de Hola. Vea [restaurar tooa secundario para una base de datos de SQL Azure o conmutación por error](sql-database-disaster-recovery.md)

- **Replicación geográfica activa**: en el caso de aplicaciones con requisitos de recuperación más exigentes que los que puede ofrecer la georestauración, configure la [replicación geográfica activa](sql-database-geo-replication-overview.md).

## <a name="manage-sql-database-elastic-pools-using-hello-azure-portal"></a>Administrar grupos elásticos de base de datos SQL con hello portal de Azure

### <a name="creating-a-new-sql-database-elastic-pool-using-hello-azure-portal"></a>Crear un nuevo grupo elástico de base de datos SQL mediante Hola portal de Azure

Hay dos maneras de que crear un grupo elástico Hola portal de Azure. Puede hacerlo desde el principio si sabe Hola grupo el programa de instalación que desee, o inicia con una recomendación de servicio de Hola. Base de datos de SQL tiene inteligencia incorporada que recomienda el programa de instalación de un grupo elástico si es más rentable en función de hello más allá de telemetría de uso para las bases de datos. 

Crear un grupo elástico de existente **server** hoja en el portal de hello es hello más fáciles manera toomove bases de datos existentes en un grupo elástico. También puede crear un grupo elástico mediante una búsqueda **grupo elástico de SQL** en hello **Marketplace** o haga clic en **+ agregar** en hello **grupos elásticos SQL**examinar hoja. Es capaz de toospecify un servidor nuevo o existente a través de este flujo de trabajo de aprovisionamiento del bloque.

> [!NOTE]
> Puede crear varios grupos en un servidor, pero no se puede agregar las bases de datos de distintos servidores en hello mismo grupo.
>  

Hello tarifa del grupo determina Hola características elastics toohello disponibles en el grupo de Hola y Hola número máximo de Edtu (eDTU máx.) y la base de datos de almacenamiento (GB) tooeach disponibles. Si desea obtener detalles, consulte [Niveles de servicio](#edtu-and-storage-limits-for-elastic-pools).

nivel de precios toochange hello para el grupo de hello, haga clic en **tarifa**, haga clic en hello tarifa que desee y, a continuación, haga clic en **seleccione**.

> [!IMPORTANT]
> Después de elegir el nivel de precios de Hola y confirmar los cambios, haga clic en **Aceptar** en último paso hello, no será hello toochange capaz de tarifa del grupo de Hola. toochange Hola a nivel de precios para un grupo elástico existente, crear un grupo elástico en el nivel de precios deseada de Hola y migrar toothis nuevo grupo de bases de datos de Hola.
>

Si las bases de datos de Hola que trabaja tienen suficiente telemetría históricas de uso, Hola **estimado de eDTU y GB uso** hello y gráfico **uso de eDTU real** toohelp de actualización de gráfico de barras realizar configuración decisiones. Además, servicio de hello puede proporcionarle un toohelp de mensaje de recomendación, ajustar Hola grupo.

Hola servicio de base de datos SQL se evalúa como el historial de uso y recomienda uno o más grupos cuando resulta más rentable que las bases de datos único. Cada recomendación se configura con un subconjunto de las bases de datos del servidor de Hola que mejor se ajustan grupo Hola único.

![grupo recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

recomendación de grupo de Hello consta de:

- Un nivel de precios para el grupo de hello (Basic, Standard, Premium o Premium RS)
- Las **eDTU del grupo** adecuadas (también denominadas eDTU máx. por grupo)
- Hola **eDTU máxima** y **eDTU mín.** por base de datos
- lista de Hola de bases de datos recomendados para el grupo de Hola

> [!IMPORTANT]
> servicio de Hello tiene últimos 30 días de telemetría de hello en cuenta al recomendar grupos. Para toobe de base de datos que se consideran como candidata para un grupo elástico, debe existir para al menos 7 días. Las bases de datos que ya están en un grupo elástico no se consideran candidatas para las recomendaciones de grupos elásticos.
>

servicio de Hello evalúa las necesidades de recursos y rentabilidad de hello móvil único bases de datos en cada nivel de servicio en grupos de hello mismo nivel. Por ejemplo, se evalúan todas las bases de datos Standard en un servidor para que quepan en un bloque de bases de datos elásticas Standard. Esto significa servicio hello no hace recomendaciones de nivel entre como mover una base de datos estándar en un grupo de Premium.

Después de agregar el grupo de servidores de bases de datos toohello, las recomendaciones se generan dinámicamente según el uso históricos Hola de bases de datos de Hola que seleccionó. Estas recomendaciones se muestran en hello eDTU y GB gráfico de uso y de un encabezado de recomendación en parte superior de Hola de hello **Configurar grupo** hoja. Estas recomendaciones son tooassist previsto en la creación de un grupo elástico optimizado para las bases de datos específicos.

![Recomendaciones dinámicas](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

### <a name="manage-and-monitor-an-elastic-pool"></a>Administración y supervisión de un grupo elástico

Hola portal de Azure, puede supervisar el uso de Hola de un grupo elástico y bases de datos de hello dentro de ese grupo. También puede realizar un conjunto de cambios grupo elástico tooyour y enviar todos los cambios realizados en hello mismo tiempo. Estos cambios incluyen agregar o quitar bases de datos, cambiar la configuración del grupo elástico o cambiar la configuración de la base de datos.

Hola siguiente gráfico muestra un grupo elástico de ejemplo. vista de Hello incluye:

*  Gráficos para supervisar el uso de recursos de grupo elástico de Hola y bases de datos de hello contenidas en el grupo de Hola.
*  Hola **configurar** grupo botón toomake cambia toohello de grupo elástico.
*  Hola **crear base de datos** botón que crea una base de datos y lo agrega el grupo elástico de toohello actual.
*  Los trabajos elásticos que le ayudarán a administran un gran número de bases de datos mediante la ejecución de scripts de Transact SQL en todas las bases de datos de una lista.

![Vista Grupo](./media/sql-database-elastic-pool-manage-portal/basic.png)

Puede ir tooa determinado grupo toosee su utilización de recursos. De forma predeterminada, el grupo de hello es uso de eDTU y almacenamiento de tooshow configurado para hello última hora. gráfico de Hello puede ser tooshow configurado diferentes métricas sobre varias ventanas de tiempo. Haga clic en hello **utilización de recursos** del gráfico en **grupo elástico supervisión** tooshow una vista detallada de Hola especificados métricas en el período de tiempo especificado de Hola.

![Supervisión de grupo elástico](./media/sql-database-elastic-pool-manage-portal/basic-2.png)

![Cuadro de métricas](./media/sql-database-elastic-pool-manage-portal/metric.png)

### <a name="toocustomize-hello-chart-display"></a>presentación de gráfico de hello toocustomize

Puede editar gráfico de Hola y Hola hoja métrica toodisplay otras métricas como porcentaje de CPU, porcentaje de E/S de datos y porcentaje de E/S de registro utilizado.

![Haga clic en Editar.](./media/sql-database-elastic-pool-manage-portal/edit-metric.png)

En hello **Editar gráfico** formulario, puede seleccionar un intervalo de tiempo (más allá de la hora, en la actualidad, o más allá de la semana), o haga clic en **personalizado** tooselect cualquier intervalo de fechas en hello dos últimas semanas. Puede elegir entre una barra o un gráfico de líneas y, a continuación, seleccione Hola recursos toomonitor.

> [!Note]
> Solo el gráfico de métricas con hello misma unidad de medida se pueden mostrar en hello en hello mismo tiempo. Por ejemplo, si selecciona "porcentaje de eDTU" solo puede seleccionar otras métricas de porcentaje como unidad de medida de Hola.
>

Haga clic en [Editar](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

### <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Administración y supervisión de bases de datos en un grupo elástico

También se pueden supervisar bases de datos individuales en caso de un problema potencial. En **Supervisión de base de datos elástica**hay un gráfico que muestra las métricas para cinco bases de datos. De forma predeterminada, Hola gráfico muestra hello principales 5 bases de datos en bloque de hello mediante el uso de eDTU promedio en hello última hora. 

![Supervisión de grupo elástico](./media/sql-database-elastic-pool-manage-portal/basic-3.png)

Haga clic en hello **uso de eDTU para bases de datos de última hora de hello** en **supervisión de bases de datos elásticas**. Se abrirá **utilización de recursos de base de datos** y proporciona una vista detallada de uso de la base de datos de hello en bloque de Hola. Con la cuadrícula de hello en parte inferior de Hola de hoja de hello, puede seleccionar las bases de datos en hello grupo toodisplay su uso en el gráfico de hello (seguridad de bases de datos de too5). También puede personalizar la ventana de métricas y la hora de hello muestra en el gráfico de hello haciendo clic en **Editar gráfico**.

![Hoja de utilización de recursos de base de datos](./media/sql-database-elastic-pool-manage-portal/db-utilization.png)

### <a name="toocustomize-hello-view"></a>vista de hello toocustomize

Puede editar Hola gráfico tooselect un intervalo de tiempo (más allá de hora o más allá de 24 horas), o haga clic en **personalizado** tooselect día diferente en hello más allá de toodisplay de 2 semanas.

![Clic en Editar gráfico](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

![Clic en Personalizado](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

También puede hacer clic en hello **comparar las bases de datos** tooselect un toouse métrica diferentes al comparar las bases de datos de lista desplegable.

![Editar gráfico de Hola](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect toomonitor de bases de datos

En la lista de bases de datos de Hola Hola **utilización de recursos de base de datos** hoja, puede encontrar las bases de datos determinadas consultando a través de páginas de hello en lista de Hola o escribiendo en nombre de Hola de una base de datos. Base de datos de uso Hola casilla tooselect Hola.

![Busque toomonitor de bases de datos](./media/sql-database-elastic-pool-manage-portal/select-dbs.png)


### <a name="add-an-alert-tooan-elastic-pool-resource"></a>Agregar un recurso de grupo elástico tooan alerta

Puede agregar el grupo elástico de reglas tooan que envíe correo electrónico de alerta o toopeople cadenas tooURL los puntos de conexión al grupo elástico Hola alcanza un umbral de uso que configuró.

**tooadd un recurso de tooany alerta:**

1. Haga clic en hello **utilización de recursos** Hola de gráfico tooopen **métrica** hoja, haga clic en **Agregar alerta**y, a continuación, rellene la información de Hola Hola **agregar una alerta regla** hoja (**recursos** se configura automáticamente de grupo de hello toobe trabaja con).
2. Escriba un **nombre** y **descripción** que identifica tooyou alerta hello y destinatarios de Hola.
3. Elija un **métrica** que desea tooalert de lista de Hola.

    gráfico de Hello dinámicamente muestra la utilización de recursos para esa métrica toohelp que elija un umbral.

4. Elija una **condición** (mayor que, menor que, etc.) y un **umbral**.
5. Elija un **período** de tiempo que Hola métrica regla debe cumplirse antes de desencadenadores de alerta de Hola.
6. Haga clic en **Aceptar**.

Para más información, consulte cómo [crear alertas de SQL Database en Azure Portal](sql-database-insights-alerts-portal.md).

### <a name="move-a-database-into-an-elastic-pool"></a>Movimiento de una base de datos a un grupo elástico

Puede agregar o quitar las bases de datos de un grupo existente. las bases de datos de Hello pueden estar en otros grupos. Sin embargo, solo puede agregar bases de datos que están en Hola mismo servidor lógico.

 ![Haga clic en Configurar grupo.](./media/sql-database-elastic-pool-manage-portal/configure-pool.png)

![Haga clic en Agregar toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)

![Seleccione las bases de datos tooadd](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

![Adiciones de grupo pendientes.](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

![Haga clic en Guardar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="move-a-database-out-of-an-elastic-pool"></a>Movimiento de una base de datos fuera de un grupo elástico

![lista de bases de datos](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

![lista de bases de datos](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

![Adición de base de datos de vista previa y eliminación](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

![Haga clic en Guardar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="change-performance-settings-of-an-elastic-pool"></a>Cambio de la configuración de rendimiento de un grupo elástico

Al supervisar la utilización de recursos de Hola de un grupo elástico, es posible que descubra que no se necesitan algunos ajustes. Quizá grupo Hola necesita un cambio en los límites de rendimiento o almacenamiento de Hola. Posiblemente desee toochange configuración de base de datos de hello en el grupo de Hola. Puede cambiar el programa de instalación de Hola de grupo de Hola en cualquier momento tooget Hola mejor equilibrio entre rendimiento y costo. Consulte [¿Cuándo se debe utilizar un grupo elástico?](sql-database-elastic-pool.md) para más información.

toochange hello Edtu o almacenamiento limita por grupo y Edtu por base de datos:

![Uso de recursos de grupos elásticos](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

![Actualización de un grupo elástico y nuevo coste mensual](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="manage-sql-database-elastic-pools-using-powershell"></a>Administración de grupos elásticos de SQL Database mediante PowerShell

toocreate y administrar grupos elásticos de base de datos de SQL con Azure PowerShell, use Hola siguientes cmdlets de PowerShell. Si necesita tooinstall o actualice PowerShell, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps). toocreate y administrar las bases de datos, servidores y las reglas de firewall, consulte [crear y administrar servidores de base de datos de SQL Azure y bases de datos mediante PowerShell](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-powershell). 

> [!TIP]
> Para los scripts de ejemplo de PowerShell, consulte [crear grupos elásticos y mover las bases de datos entre grupos y fuera de un grupo con PowerShell](scripts/sql-database-move-database-between-pools-powershell.md) y [toomonitor de usar PowerShell y escala de bloque de un elástico SQL en la base de datos de Azure SQL](scripts/sql-database-monitor-and-scale-pool-powershell.md).
>

| Cmdlet | Descripción |
| --- | --- |
|[New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool)|Crea un grupo de bases de datos elásticas en un servidor SQL Server lógico.|
|[Get-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/get-azurermsqlelasticpool)|Obtiene los grupos elásticos y los valores de sus propiedades de un servidor SQL Server lógico.|
|[Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool)|Modifica las propiedades de un grupo de bases de datos elásticas en un servidor SQL Server lógico.|
|[Remove-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/remove-azurermsqlelasticpool)|Elimina un grupo de bases de datos elásticas en un servidor SQL Server lógico.|
|[Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity)|Obtiene el estado de Hola de operaciones en un grupo elástico en un servidor lógico de SQL.|
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Crea una nueva base de datos en un grupo existente o como una sola base de datos. |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Obtiene una o más bases de datos.|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Establece las propiedades de una base de datos o mueve una base de datos existente a un grupo elástico, fuera de él o entre grupos elásticos.|
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|Quita una base de datos.|

> [!TIP]
> Creación de varias bases de datos en un grupo elástico puede tardar tiempo cuando se realiza mediante el portal de Hola o los cmdlets de PowerShell que crean una sola base de datos a la vez. creación de tooautomate en un grupo elástico, consulte [CreateOrUpdateElasticPoolAndPopulate](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).
>

## <a name="manage-sql-database-elastic-pools-using-hello-azure-cli"></a>Administrar grupos elásticos de base de datos SQL con hello CLI de Azure

toocreate y administrar grupos elásticos de base de datos de SQL con hello [CLI de Azure](/cli/azure/overview), utilice Hola siguiente [base de datos de SQL Azure CLI](/cli/azure/sql/db) comandos. Hola de uso [Shell en la nube](/azure/cloud-shell/overview) toorun Hola CLI en el explorador, o [instalar](/cli/azure/install-azure-cli) en Windows, Linux o Mac OS. 

> [!TIP]
> Para los scripts de ejemplo de CLI de Azure, consulte [toomove de CLI de usar una base de datos de SQL Azure en un grupo elástico de SQL](scripts/sql-database-move-database-between-pools-cli.md) y [tooscale de CLI de Azure Use un grupo elástico de SQL en la base de datos de SQL Azure](scripts/sql-database-scale-pool-cli.md).
>

| Cmdlet | Descripción |
| --- | --- |
|[az sql elastic-pool create](/cli/azure/sql/elastic-pool#create)|Crea un grupo elástico.|
|[az sql elastic-pool list](/cli/azure/sql/elastic-pool#list)|Devuelve una lista de grupos elásticos de un servidor.|
|[az sql elastic-pool list-dbs](/cli/azure/sql/elastic-pool#list-dbs)|Devuelve una lista de bases de datos de un grupo elástico.|
|[az sql elastic-pool list-editions](/cli/azure/sql/elastic-pool#list-editions)|Además incluye los parámetros disponibles de DTU de grupo, los límites de almacenamiento y la configuración por base de datos. En el nivel de detalle de pedido tooreduce, límites de almacenamiento adicional y por base de datos de configuración está ocultos de forma predeterminada.|
|[az sql elastic-pool update](/cli/azure/sql/elastic-pool#update)|Actualiza un grupo elástico.|
|[az sql elastic-pool delete](/cli/azure/sql/elastic-pool#delete)|Elimina el grupo elástico Hola.|

## <a name="manage-sql-database-elastic-pools-using-transact-sql"></a>Administración de grupos elásticos de SQL Database mediante Transact-SQL

toocreate y mover bases de datos de grupos elásticos existentes o tooreturn información acerca de un grupo elástico de base de datos SQL con Transact-SQL, utilice Hola siga los comandos de T-SQL. Puede emitir estos comandos mediante el portal de Azure, Hola [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [código de Visual Studio](https://code.visualstudio.com/docs), o cualquier otro programa que se puede conectar el servidor de base de datos de SQL Azure tooan y pasar Transact-SQL comandos. toocreate y administrar las bases de datos, servidores y las reglas de firewall, consulte [crear y administrar servidores de base de datos de SQL Azure y bases de datos mediante Transact-SQL](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-transact-sql).

> [!IMPORTANT]
> No es posible crear, actualizar ni eliminar un grupo elástico de Azure SQL Database mediante Transact-SQL. Puede agregar o quitar las bases de datos de un grupo elástico, y puede utilizar DMV tooreturn información acerca de los grupos elásticos existentes.
>

| Comando | Descripción |
| --- | --- |
|[CREATE DATABASE (Azure SQL Database)](/sql/t-sql/statements/create-database-azure-sql-database)|Crea una nueva base de datos en un grupo existente o como una sola base de datos. Debe ser toocreate de base de datos maestra toohello conectada una nueva base de datos.|
| [ALTER DATABASE (Base de datos SQL de Azure)](/sql/t-sql/statements/alter-database-azure-sql-database) |Mueve una base de datos a un grupo elástico, fuera de él o entre grupos elásticos.|
|[DROP DATABASE (Transact-SQL)](/sql/t-sql/statements/drop-database-transact-sql)|Permite eliminar una base de datos.|
|[sys.elastic_pool_resource_stats (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-elastic-pool-resource-stats-azure-sql-database)|Devuelve estadísticas de uso de recursos para todos los grupos de bases de datos elásticas de hello en un servidor lógico. Para cada grupo de bases de datos elásticas hay una fila por cada ventana de informe de 15 segundos (cuatro filas por minuto). Esto incluye uso de CPU, E/S, registro, consumo de almacenamiento y solicitud/sesiones simultáneas por todas las bases de datos de grupo de Hola.|
|[sys.database_service_objectives (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Devuelve Hola edition (nivel de servicio), el objetivo de servicio (nivel de precios) y el nombre del grupo elástico, si existe, para una base de datos de SQL Azure o un almacén de datos de SQL Azure. Si una sesión en la base de datos maestra toohello en un servidor de base de datos de SQL Azure, devuelve información sobre todas las bases de datos. Para almacenamiento de datos de SQL Azure, debe ser toohello conectado la base de datos maestra.|

## <a name="manage-sql-database-elastic-pools-using-hello-rest-api"></a>Administrar grupos elásticos de base de datos SQL con hello API de REST

toocreate y administrar grupos elásticos de base de datos SQL con hello API de REST, vea [API de REST de base de datos de SQL Azure](/rest/api/sql/).

## <a name="next-steps"></a>Pasos siguientes

* Para ver un vídeo, vea el [Curso de vídeo de la Academia virtual de Microsoft sobre las funcionalidades de las bases de datos elásticas en Azure SQL Database](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554).
* toolearn más información acerca de los patrones de diseño para aplicaciones de SaaS con grupos elásticos, consulte [patrones de diseño para aplicaciones de SaaS multiempresa con base de datos de SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).
* Para obtener un tutorial de SaaS con grupos elásticos, consulte [Introducción toohello aplicación SaaS Wingtip](sql-database-wtp-overview.md).

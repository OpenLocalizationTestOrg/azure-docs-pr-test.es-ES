---
title: datos de aaaDistribute global con la base de datos de Azure Cosmos | Documentos de Microsoft
description: "Obtenga más información sobre replicación geográfica, conmutación por error y recuperación de datos a escala mundial con bases de datos globales de Azure Cosmos DB, un servicio de base de datos con varios modelos distribuido globalmente."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: ba5ad0cc-aa1f-4f40-aee9-3364af070725
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/14/2017
ms.author: arramac
ms.openlocfilehash: b50e8433dc7e70c54d68c4c2f99954a13f4951f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodistribute-data-globally-with-azure-cosmos-db"></a>¿Cómo toodistribute datos globalmente con la base de datos de Azure Cosmos
Azure es ubicuo, se puede encontrar en más de treinta regiones geográficas y se encuentra en continua expansión. Con su presencia en todo el mundo, una de las capacidades de hello diferenciado que Azure ofrece a los desarrolladores de tooits es Hola toobuild de capacidad, implementar y administrar fácilmente aplicaciones distribuidas globalmente. 

[Azure Cosmos DB](../cosmos-db/introduction.md) es un servicio de base de datos con varios modelos y distribución global de Microsoft para aplicaciones críticas. Base de datos de Cosmos Azure proporciona una distribución global llave en mano, [escalado flexible de rendimiento y almacenamiento](../cosmos-db/partition-data.md) latencias de milisegundo en todo el mundo, solo dígito se escriben en el percentil 99 de hello, [cinco niveles de coherencia bien definido ](consistency-levels.md)y garantiza la alta disponibilidad, todo ello respaldado por [líderes en la industria SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Base de datos de Azure Cosmos [automáticamente los datos de índices](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sin necesidad de toodeal con administración de esquema y de índice. Sigue varios modelos y es compatible con los modelos de datos de documento, de clave-valor, de grafo y de columnas. Como un servicio procedentes de la nube, base de datos de Azure Cosmos está diseñado cuidadosamente con hello masa distribución de multiempresa y global.

**Una sola colección de Azure Cosmos DB particionada y distribuida en varias regiones de Azure**

![Colección de Azure Cosmos DB particionada y distribuida en tres regiones](./media/distribute-data-globally/global-apps.png)

Como hemos aprendido al crear Azure Cosmos DB, la incorporación de distribución global no es algo que se pueda hacer en el último momento, no se puede "atornillar" sobre un sistema de base de datos de "único sitio". capacidades de Hola que ofrece una base de datos distribuido globalmente abarcan más allá que del tradicional ante desastres geográfica recuperación (Geo-DR) que ofrecen las bases de datos de "sitio único". Las bases de datos de sitio único que ofrecen la funcionalidad de Geo-DR son un estricto subconjunto de las bases de datos distribuidas globalmente. 

Con la distribución global de Azure Cosmos base de datos llave en mano, los desarrolladores no tienen toobuild su propios scaffolding de replicación mediante el uso de cualquier patrón de expresión Lambda hello (por ejemplo, [DynamoDB AWS replicación](https://github.com/awslabs/dynamodb-cross-region-library/blob/master/README.md)) a través del registro de base de datos de Hola o mediante Esto "escrituras dobles" en varias regiones. No se recomienda estos enfoques ya que es imposible tooensure corrección de estos enfoques y proporcionar sonidos SLA. 

En este artículo se ofrece información general sobre las funcionalidades de distribución global de Azure Cosmos DB. También se describe tooproviding único enfoque del Cosmos base de datos Azure SLA completa. 

## <a id="EnableGlobalDistribution"></a>Habilitación de una distribución global inmediata
Base de datos de Azure Cosmos proporciona siguiente Hola capacidades tooenable tooeasily escribir aplicaciones de escala de planeta. Estas capacidades están disponibles a través de recursos de DB hello Azure Cosmos basado en proveedor [API de REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/) , así como Hola portal de Azure.

### <a id="RegionalPresence"></a>Presencia regional ubicua 
La presencia geográfica de Azure crece constantemente y aumenta el número de [regiones nuevas](https://azure.microsoft.com/regions/) en línea. Azure Cosmos DB está disponible de manera predeterminada en todas las nuevas regiones de Azure. Esto permite tooassociate una región geográfica con su cuenta de base de datos de la base de datos de Azure Cosmos tan pronto como Azure abre la nueva área de hello para empresas.

**Azure Cosmos DB está disponible de manera predeterminada en todas las regiones de Azure**

![Azure Cosmos DB está disponible en todas las regiones de Azure](./media/distribute-data-globally/azure-regions.png)

### <a id="UnlimitedRegionsPerAccount"></a>Asociación de un número ilimitado de regiones a una cuenta de base de datos de Azure Cosmos DB
Base de datos de Azure Cosmos permite tooassociate cuenta de base de datos de cualquier número de regiones de Azure con la base de datos de Azure Cosmos. Fuera de las restricciones de barrera geográfica (por ejemplo, China, Alemania), no hay ninguna limitación respecto al número de Hola de regiones que se pueden asociar con la cuenta de base de datos de la base de datos de Azure Cosmos. Hola figura siguiente muestra un toospan de cuenta configurada de la base de datos en 25 regiones de Azure.  

**Cuenta de base de datos de Azure Cosmos DB de un inquilino que abarca 25 regiones de Azure**

![Cuenta de base de datos de Azure Cosmos DB que abarca 25 regiones de Azure](./media/distribute-data-globally/spanning-regions.png)

### <a id="PolicyBasedGeoFencing"></a>Geovallado basado en directivas
Base de datos de Azure Cosmos es toohave diseñada capacidades de barrera geográfica basada en directivas. Barrera geográfica es un componente importante tooensure restricciones de gobernanza y cumplimiento de normas de datos y puede impedir la asociación de una región específica con su cuenta. Ejemplos de barrera geográfica incluyen (pero no está obligados a), definir el ámbito de las regiones de toohello de distribución global dentro de una nube soberano (por ejemplo, China y en Alemania) o dentro de un límite de impuestos de gobierno (por ejemplo, Australia). las directivas de Hola se controlan mediante metadatos de Hola de su suscripción de Azure.

### <a id="DynamicallyAddRegions"></a>Incorporación y eliminación dinámicas de regiones
Base de datos de Azure Cosmos permite tooadd (asociado) o quitar (desasociar) cuenta de base de datos de las regiones tooyour en cualquier momento (vea [en la ilustración anterior se](#UnlimitedRegionsPerAccount)). En virtud de replicar datos entre particiones en paralelo, base de datos de Azure Cosmos garantiza que cuando se ponga en línea una nueva área de base de datos de Azure Cosmos esté disponible dentro de 30 minutos en cualquier lugar de Hola a todos para seguridad too100 TBs. 

### <a id="FailoverPriorities"></a>Prioridades de conmutación por error
toocontrol secuencia exacta de conmutaciones por error regional cuando se produce una interrupción en varias regiones, base de datos de Azure Cosmos permite tooassociate Hola prioridad toovarious las regiones de asociado de cuenta de base de datos de hello (vea Hola figura siguiente). Azure DB Cosmos garantiza que la secuencia de hello conmutación automática por error se produce en orden de prioridad de hello especificado. Para obtener más información sobre las conmutaciones por error regionales, vea [Conmutaciones por error regionales automáticas para la continuidad empresarial en Azure Cosmos DB](regional-failover.md).

**Un inquilino de base de datos de Azure Cosmos puede configurar el orden de prioridad de conmutación por error de hello (panel derecho) para las regiones asociadas a una cuenta de base de datos**

![Configuración de prioridades de conmutación por error con Azure Cosmos DB](./media/distribute-data-globally/failover-priorities.png)

### <a id="OfflineRegions"></a>Desconexión dinámica de una región
Base de datos de Azure Cosmos permite tootake cuenta sin conexión en una región específica de la base de datos y ponerlo en línea más adelante. Regiones de marcado como sin conexión no participan activamente en la replicación y no forman parte de la secuencia de conmutación por error de Hola. Esto le permite hello toofreeze última conocida imagen buena de la base de datos en uno de hello leer regiones antes de lanzar potencialmente peligrosos actualiza la aplicación de tooyour.

### <a id="ConsistencyLevels"></a>Varios modelos de coherencia bien definidos para bases de datos replicadas globalmente
Azure Cosmos DB expone [varios niveles de coherencia bien definidos](consistency-levels.md) respaldados por acuerdos de nivel de servicio. Puede elegir un modelo de coherencia específico (en la lista de disponibles de Hola de opciones) según Hola/escenarios de carga de trabajo. 

### <a id="TunableConsistency"></a>Coherencia optimizable para bases de datos replicadas globalmente
Base de datos de Azure Cosmos permite tooprogrammatically invalidación y ser menos exigentes con opción de coherencia predeterminada de hello en función de cada solicitud, en tiempo de ejecución. 

### <a id="DynamicallyConfigurableReadWriteRegions"></a>Regiones de escritura y lectura configurables dinámicamente
Base de datos de Azure Cosmos permite regiones de hello tooconfigure (asociadas a la base de datos de hello) para "lectura", "escritura" o "lectura/escritura" regiones. 

### <a id="ElasticallyScaleThroughput"></a>Rendimiento de escalado elástico en regiones de Azure
Para escalar elásticamente las colecciones de Azure Cosmos DB, es preciso aprovisionar el rendimiento mediante programación. rendimiento de Hello es regiones de hello tooall aplicado colección Hola se distribuye en.

### <a id="GeoLocalReadsAndWrites"></a>Escrituras y lecturas geolocalizadas
Hola principal ventaja de una base de datos distribuido globalmente es toooffer baja latencia acceder a toohello los datos en cualquier parte de Hola a todos. Azure Cosmos DB ofrece garantía de baja latencia en P99 para realizar diversas operaciones de base de datos. Garantiza que todas las lecturas se toohello enrutado región lectura local más cercano. se utiliza tooserve una solicitud de lectura, región de hello quórum toohello local en el que se emite Hola leer; Hello Esto mismo aplica toohello escrituras. Una operación de escritura se confirma después de una mayoría de las réplicas de manera duradera confirmarse escritura Hola localmente pero sin que se está controlada en las réplicas remotas tooacknowledge Hola escrituras. Colocar de forma diferente, protocolo de hello replicación de base de datos de Azure Cosmos funciona con suposición Hola Hola de lectura y escritura quórums siempre son lectura toohello local y escriben regiones, respectivamente, en qué solicitud Hola se emite.

### <a id="ManualFailover"></a>Inicio manual de una conmutación por error regional
Base de datos de Azure Cosmos permite conmutación por error de tootrigger Hola de Hola Hola de toovalidate de cuenta de base de datos *finalizar tooend* propiedades de disponibilidad de toda la aplicación hello (más allá de la base de datos de hello). Dado que ambos Hola seguridad y se garantiza que las propiedades de vida de elección de detección y líder de error de hello, garantiza la base de datos de Azure Cosmos *sin pérdida de datos* para una operación iniciada por el inquilino manual conmutación por error.

### <a id="AutomaticFailover"></a>Conmutación por error automática
Azure Cosmos DB admite la conmutación por error automática en caso de una o varias interrupciones regionales. Durante una conmutación por error regional, Azure Cosmos DB mantiene sus acuerdos de nivel de servicio de latencia de lectura, disponibilidad del tiempo de actividad, coherencia y rendimiento. Base de datos de Azure Cosmos proporciona un límite superior en duración de Hola de un toocomplete de operación de conmutación por error automática. Esta es la ventana de hello potencial de pérdida de datos durante la interrupción regional Hola.

### <a id="GranularFailover"></a>Diseñado para diferentes granularidades de conmutación por error
Actualmente Hola automáticas y capacidades de conmutación por error manual se exponen con una granularidad de Hola de cuenta de base de datos de Hola. Tenga en cuenta que internamente Cosmos base de datos Azure es diseñada toooffer *automática* conmutación por error con una granularidad más fina de una base de datos, colección o incluso una partición (de una colección posee un intervalo de claves). 

### <a id="MultiHomingAPIs"></a>API de hospedaje múltiple en Azure Cosmos DB
Base de datos de Azure Cosmos permite toointeract con base de datos de hello con lógica (independiente de la región) o puntos de conexión físicos (específico de la región). Utilizar puntos de conexión lógicas garantiza que aplicación hello transparente puede ser de host múltiple en caso de conmutación por error. Hola extremos físicos, este últimos, proporcionan un control minucioso toohello aplicación tooredirect las lecturas y escrituras toospecific regiones.

Puede encontrar información sobre cómo tooconfigure lee las preferencias de hello [DocumentDB API](../cosmos-db/tutorial-global-distribution-documentdb.md), [API Graph](../cosmos-db/tutorial-global-distribution-graph.md), [API de tabla](../cosmos-db/tutorial-global-distribution-table.md), y [MongoDB API](../cosmos-db/tutorial-global-distribution-mongodb.md)en sus respectivas vincular artículos.

### <a id="TransparentSchemaMigration"></a>Migración transparente y coherente del índice y esquema de la base de datos 
Azure Cosmos DB es totalmente [independiente del esquema](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf). diseño único Hola de su motor de base de datos permite tooautomatically y sincrónicamente indizar todos los datos de Hola introduce sin necesidad de ningún esquema ni índices secundarios del usuario. Esto permite tooiterate la aplicación distribuida globalmente rápidamente sin preocuparse de migración de esquema y de índice de base de datos o coordinar las implementaciones de aplicaciones de varias fases de cambios de esquema. Base de datos de Azure Cosmos garantiza que las directivas de tooindexing cambios realizadas explícitamente por el usuario no se produce en una degradación del rendimiento o disponibilidad.  

### <a id="ComprehensiveSLAs"></a>Acuerdos de Nivel de Servicio completos (algo más que la alta disponibilidad)
Como un servicio de base de datos distribuidos globalmente, base de datos de Azure Cosmos ofrece SLA bien definido de **pérdida de datos**, **disponibilidad**, **latencia en P99**, **rendimiento**  y **coherencia** de base de datos de Hola como un todo, independientemente del número de Hola de regiones asociado a la base de datos de Hola.  

## <a id="LatencyGuarantees"></a>Garantías de latencia
Hola principal ventaja de un servicio de base de datos distribuidos globalmente como base de datos de Azure Cosmos es toooffer baja latencia acceder a tooyour los datos en cualquier parte de Hola a todos. Azure Cosmos DB ofrece una baja latencia garantizada en P99 para realizar diversas operaciones de base de datos. Protocolo de replicación de Hola que emplea la base de datos de Azure Cosmos asegura que hello las operaciones de base de datos (lo ideal es que, lee y escribe) siempre se realizan en hello región local toothat de cliente de Hola. latencia de Hola para que DB Cosmos SLA de Azure incluye P99 las lecturas, escrituras (sincrónicamente) indizadas y consulta para diversos tamaños de solicitud y respuesta. garantías de latencia de Hola para escrituras incluyen confirmaciones de quórum de mayoría duradero en hello centro de datos local.

### <a id="LatencyAndConsistency"></a>Relación de la latencia con la coherencia 
Para un servicio distribuidos globalmente toooffer homogeneidad en una instalación distribuida globalmente, se necesita toosynchronously Hola replicar escrituras sincrónicas o realizar lecturas entre regiones: velocidad de Hola de luz y Hola dictan de confiabilidad de red de área extensa que homogeneidad genera latencias altas y la baja disponibilidad de las operaciones de base de datos. Por lo tanto, en orden toooffer garantizada latencias bajas en P99 y 99,99 disponibilidad, servicio de hello debe emplear la replicación asincrónica. Esta a su vez requiere que también debe ofrecer servicio hello [elección de coherencia no estricta, bien definido](consistency-levels.md) : más débil que seguro (toooffer baja latencia y disponibilidad garantías) y lo ideal es más fuerte que "la" coherencia ( toooffer un modelo de programación intuitivo).

Base de datos de Azure Cosmos garantiza que una operación de lectura no es necesario toocontact réplicas a través de varias regiones toodeliver Hola específico nivel garantía de coherencia. Del mismo modo, se asegura de que una operación de escritura no se bloquee mientras se está replicando datos hello en todas las regiones de hello (es decir, escrituras se replican asincrónicamente en regiones). Para las cuentas de base de datos de varias regiones hay disponibles varios niveles de coherencia relajada. 

### <a id="LatencyAndAvailability"></a>Relación de la latencia con la disponibilidad 
La latencia y disponibilidad son dos lados de Hola de hello misma moneda. Hablamos de latencia de operación de hello en estado estable y la disponibilidad, en la cara de Hola de errores. Desde la perspectiva de aplicación Hola, una operación de base de datos de ejecución lenta es indistinguible desde una base de datos que no está disponible. 

toodistinguish alta latencia de falta de disponibilidad de base de datos de Azure Cosmos proporciona un límite superior absoluto en la latencia de varias operaciones de base de datos. Si tarda operación de base de datos de hello más toocomplete del límite superior de hello, base de datos de Azure Cosmos devuelve un error de tiempo de espera. Hola SLA de disponibilidad de base de datos de Azure Cosmos garantiza que los tiempos de espera de Hola se cuentan con SLA de disponibilidad de Hola. 

### <a id="LatencyAndThroughput"></a>Relación de la latencia con el rendimiento
Azure Cosmos DB no obliga a elegir entre latencia y rendimiento. Se respeta el SLA de Hola para ambos latencia en P99 y ofrecer rendimiento Hola que ha aprovisionado. 

## <a id="ConsistencyGuarantees"></a>Garantías de coherencia
Mientras hello [modelo homogeneidad](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) es Hola oro estándar de la programación, incide sobre el precio de dificultoso Hola de latencia alta (en estado estable) y la pérdida de disponibilidad (en la cara de Hola de errores). 

Base de datos de Cosmos Azure ofrece una programación tooreason de tooyou modelo bien definido sobre la coherencia de los datos replicados. En orden tooenable se toobuild hosts múltiples aplicaciones, modelos de coherencia de hello expuestos por la base de datos de Azure Cosmos son independientes de región toobe diseñada y no dependen de región de Hola desde donde se atienden Hola lecturas y escrituras. 

SLA de coherencia de Azure DB Cosmos garantiza que el 100% de las solicitudes de lectura se reunirá garantía de coherencia de Hola para nivel de coherencia de hello solicitado por (Hola predeterminado nivel de coherencia en la cuenta de base de datos de hello, o bien valor Hola que se reemplaza en la solicitud de Hola ). Una solicitud de lectura se considera toohave cumplido hello coherencia SLA si se cumplen todas las garantías de coherencia de hello asociadas al nivel de coherencia de Hola. Hello tabla siguiente captura garantías de coherencia de Hola que corresponden a los niveles de coherencia toospecific ofrecidos por base de datos de Azure Cosmos.

**Garantías de coherencia asociadas a un nivel determinado de coherencia en Azure Cosmos DB**

<table>
    <tr>
        <td><strong>Nivel de coherencia</strong></td>
        <td><strong>Características de coherencia</strong></td>
        <td><strong>Acuerdo de Nivel de Servicio</strong></td>
    </tr>
    <tr>
        <td rowspan="3">Sesión</td>
        <td>Leer su propia escritura</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Lectura monotónica</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Prefijo coherente</td>
        <td>100%</td>
    </tr>
    <tr>
        <td rowspan="3">Uso vinculado</td>
        <td>Lectura monotónica (dentro de una región)</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Prefijo coherente</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Límite de obsolescencia &lt; K, T</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Prefijo coherente</td>
        <td>Prefijo coherente</td>
        <td>100%</td>
    </tr>
    <tr>
        <td>Alta</td>
        <td>Linearizable</td>
        <td>100%</td>
    </tr>
</table>

### <a id="ConsistencyAndAvailability"></a>Relación de la coherencia con la disponibilidad
Hola [resultado imposibilidad](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf) de hello [teorema CAP](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf) demuestra que es realmente imposible Hola sistema tooremain disponible y la coherencia de linearizable de oferta en cara Hola de errores. servicio de base de datos de Hello debe elegir toobe CP o AP - sistemas de CP renunciar disponibilidad en favor de coherencia linearizable mientras renunciar a sistemas de hello PA [linearizable coherencia](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) en favor de disponibilidad. Base de datos de Azure Cosmos nunca infringe Hola nivel de coherencia, lo que hace un sistema CP formalmente solicitado. Sin embargo, en la práctica coherencia no es una propuesta de todo o nada: hay varios modelos bien definidos de coherencia a lo largo del espectro de coherencia de hello entre coherencia linearizable y final. En la base de datos de Azure Cosmos, hemos tratado tooidentify varios Hola redujeron los modelos de coherencia con aplicabilidad del mundo real y un modelo de programación intuitivo. Base de datos de Azure Cosmos navega compensaciones de disponibilidad de la coherencia de hello, ya que ofrece 99,99 SLA de disponibilidad junto con [relajan de varios niveles de coherencia aún bien definido](consistency-levels.md). 

### <a id="ConsistencyAndAvailability"></a>Relación de la coherencia con la latencia
Una variación más exhaustiva de CAP la propuso el profesor Daniel Abadi y se llama [PACELC](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf), que también tiene en cuenta las compensaciones de latencia y coherencia en estado estable. Indica que en estado estable, el sistema de bases de datos de hello debe elegir entre coherencia y la latencia. Con varios modelos de coherencia no estricta (respaldados por la replicación asincrónica y lectura local, quórums de escritura), base de datos de Azure Cosmos garantiza que todas las lecturas y escrituras sean local toohello lectura y escriben regiones respectivamente.  Esto permite que garantiza la base de datos de Azure Cosmos toooffer baja latencia dentro de la región de Hola para niveles de coherencia de Hola.  

### <a id="ConsistencyAndThroughput"></a>Relación de la consistencia con el rendimiento
Ya que depende de implementación de Hola de un modelo de coherencia específico de elección de Hola de un [tipo de quórum](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf), rendimiento de hello también varía en función de elección de Hola de coherencia. Por ejemplo, en la base de datos de Azure Cosmos hello rendimiento con lecturas muy coherentes es toothat aproximadamente la mitad de lecturas coherentes. 
 
**Relación de la capacidad de lectura con un nivel de coherencia específico en Azure Cosmos DB**

![Relación entre coherencia y rendimiento](./media/distribute-data-globally/consistency-and-throughput.png)

## <a id="ThroughputGuarantees"></a>Garantías de rendimiento 
Azure Cosmos DB permite tooscale rendimiento (así como, almacenamiento), elásticamente en regiones diferentes según la demanda de Hola. 

**Una sola colección particionada de Azure Cosmos DB (en tres particiones) y luego distribuida en tres regiones de Azure**

![Colecciones particionadas y distribuidas de Azure Cosmos DB](../cosmos-db/media/introduction/azure-cosmos-db-global-distribution.png)

Las colecciones de Azure Cosmos DB se distribuyen en dos dimensiones (dentro de una región y luego entre regiones). Este es el procedimiento: 

* En una sola región, una colección de Azure Cosmos DB se escala horizontalmente en cuanto a particiones de recursos. Cada partición del recurso administra un conjunto de claves y tiene coherencia fuerte y tiene alta disponibilidad en virtud de la replicación del estado de la máquina entre un conjunto de réplicas. Base de datos de Cosmos Azure es un sistema de recurso regulado totalmente donde una partición de recurso es responsable de entregar su cuota de rendimiento para la asignación de Hola de sistema tooit de recursos asignados. Hola escalado de una colección de base de datos de Azure Cosmos es completamente transparente, base de datos de Azure Cosmos administra las particiones de recursos de Hola y divide y combina según sea necesario. 
* Cada una de las particiones de recursos de hello, a continuación, se distribuye en varias regiones. Particiones de recursos propietario Hola mismo conjunto de claves en el conjunto de particiones de formulario de varias regiones (vea [en la ilustración anterior se](#ThroughputGuarantees)).  Particiones de recursos dentro de un conjunto de particiones se coordinan mediante el uso de replicación de máquina de estado a través de hello varias regiones. Según configurarlo el nivel de coherencia de hello, particiones de recursos de hello dentro de un conjunto de particiones se configuran dinámicamente mediante topologías diferentes (por ejemplo, estrella, margarita, árbol etcetera). 

En virtud de una administración de particiones de alta capacidad de respuesta, equilibrio de carga y la regulación de recursos estricta, base de datos de Azure Cosmos permite tooelastically rendimiento de escala en varias regiones de Azure en una colección de base de datos de Azure Cosmos. Variación de rendimiento en una colección es una operación de en tiempo de ejecución en la base de datos de Azure Cosmos: al igual que con otras operaciones de base de datos que base de datos de Azure Cosmos garantiza Hola de límite superior absoluta en la latencia para el rendimiento de hello toochange de solicitud. Por ejemplo, hello figura siguiente muestra la recolección de un cliente con un rendimiento aprovisionado elásticamente (comprendido entre 1M - 10M solicitudes/segundo en dos regiones) según la demanda de Hola.
 
**Colección de un cliente con rendimiento aprovisionado elásticamente (entre un millón y diez millones de solicitudes por segundo)**

![Rendimiento aprovisionado elásticamente de Azure Cosmos DB](./media/distribute-data-globally/elastic-throughput.png)

### <a id="ThroughputAndConsistency"></a>Relación del rendimiento con la coherencia 
Lo mismo que [Relación de la coherencia con el rendimiento](#ConsistencyAndThroughput).

### <a id="ThroughputAndAvailability"></a>Relación del rendimiento con la disponibilidad
Base de datos de Azure Cosmos continúa toomaintain su disponibilidad cuando se realizan cambios de hello toohello rendimiento. Base de datos de Azure Cosmos administra de forma transparente las particiones (por ejemplo, división, combinación, las operaciones de clonación) y se asegura de que las operaciones de hello no degradar el rendimiento o la disponibilidad, mientras la aplicación hello elásticamente aumenta o disminuye el rendimiento. 

## <a id="AvailabilityGuarantees"></a>Garantías de disponibilidad
Base de datos de Azure Cosmos ofrece una disponibilidad de tiempo de actividad del 99,99% SLA para cada uno de hello las operaciones de plano de control y de datos. Como ya se ha descrito, las garantías de disponibilidad de Azure Cosmos DB incluyen un límite superior absoluto de la latencia de todas las operaciones de datos y del plano de control. garantías de disponibilidad de Hello son steadfast y no cambian con el número de Hola de distancia geográfica entre regiones o regiones. Las garantías de disponibilidad se aplican tanto a la conmutación por error manual como a la automática. Base de datos de Azure Cosmos ofrece las API de hospedaje múltiple transparentes que asegúrese de que la aplicación puede funcionar en los puntos de conexión lógicas y puede enrutar de forma transparente región nueva toohello de hello las solicitudes en el caso de conmutación por error. Colocar de forma diferente, la aplicación no es necesario volver a implementar tras la conmutación por error regional de toobe y se mantienen los SLA de disponibilidad de Hola.

### <a id="AvailabilityAndConsistency"></a>Relación de la disponibilidad con la coherencia, la latencia y el rendimiento
La relación de la disponibilidad con la coherencia, la latencia y el rendimiento se describe en [Relación de la coherencia con la disponibilidad](#ConsistencyAndAvailability), [Relación de la latencia con la disponibilidad](#LatencyAndAvailability) y [Relación del rendimiento con la disponibilidad](#ThroughputAndAvailability). 

## <a id="GuaranteesAgainstDataLoss"></a>Garantías y comportamiento del sistema ante la "pérdida de datos"
En Azure Cosmos DB, la alta disponibilidad de cada partición (de una colección) se logra mediante varias réplicas, que se distribuyen entre 10 y 20 dominios de error como mínimo. Todas las escrituras son sincrónicamente y de manera duradera confirmadas por un quórum de mayoría de las réplicas antes de que se confirmen a toohello cliente. La replicación asincrónica se aplica a la coordinación entre las particiones dispersas por varias regiones. Azure Cosmos DB garantiza que no hay pérdida de datos en las conmutaciones por error manuales iniciadas por los inquilinos. Durante la conmutación por error automática, la base de datos de Azure Cosmos garantiza un límite superior de hello configurado limitado intervalo de antigüedad en la ventana de pérdida de datos de hello como parte de su SLA.

## <a id="CustomerFacingSLAMetrics"></a>Métricas de Acuerdo de Nivel de Servicio orientadas al cliente
Base de datos de Azure Cosmos transparente expone las métricas de rendimiento, la latencia, la coherencia y la disponibilidad de Hola. Estas métricas son accesibles mediante programación y a través de hello portal de Azure (vea la siguiente figura). También se pueden configurar alertas en varios umbrales mediante Azure Application Insights.
 
**Métricas de coherencia, la latencia, el rendimiento y disponibilidad están disponibles de forma transparente tooeach inquilino**

![Métricas del Acuerdo de Nivel de Servicio visibles para clientes de Azure Cosmos DB](./media/distribute-data-globally/customer-slas.png)

## <a id="Next Steps"></a>Pasos siguientes
* tooimplement replicación global en su cuenta de base de datos de Azure Cosmos mediante hello Azure portal, vea [la replicación de base de datos global de base de datos de Azure Cosmos de tooperform mediante Hola portal de Azure](tutorial-global-distribution-documentdb.md).
* toolearn acerca de cómo tooimplement arquitecturas de varios maestros con base de datos de Cosmos de Azure, consulte [arquitecturas de varios maestros de la base de datos con la base de datos de Azure Cosmos](multi-region-writers.md).
* toolearn Obtenga más información sobre cómo funcionan los conmutaciones por error automática y manuales en la base de datos de Cosmos de Azure, consulte [Regional las conmutaciones por error en la base de datos de Azure Cosmos](regional-failover.md).

## <a id="References"></a>Referencias
1. Eric Brewer. [Towards Robust Distributed Systems](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf) (Hacia unos sistemas distribuidos sólidos)
2. Eric Brewer. [CAP de doce años posterior: cómo han cambiado las reglas de Hola](http://informatik.unibas.ch/fileadmin/Lectures/HS2012/CS341/workshops/reportsAndSlides/PresentationKevinUrban.pdf)
3. Gilbert, Lynch. - [Brewer&amp;#39;s Conjecture and Feasibility of Consistent, Available, Partition Tolerant Web Services](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf) (Conjetura de Brewer y viabilidad de servicios web coherentes, disponibles y tolerantes a particiones)
4. Daniel Abadi. [Consistency Tradeoffs in Modern Distributed Database Systems Design](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf) (Equilibrios de coherencia en el diseño de los modernos sistemas de bases de datos distribuidas)
5. Martin Kleppmann. [Please stop calling databases CP or AP](https://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html) (Deje de llamar a las bases de datos CP o AP)
6. Peter Bailis et al. [Probabilistic Bounded Staleness (PBS) for Practical Partial Quorums](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf) [Obsolescencia limitada probabilística (PBS) para cuórums parciales prácticos].
7. Naor and Wool. [Load, Capacity and Availability in Quorum Systems](http://www.cs.utexas.edu/~lorenzo/corsi/cs395t/04S/notes/naor98load.pdf) (Carga, capacidad y disponibilidad en sistemas de quórum)
8. Herlihy and Wing. [Lineralizability: A correctness condition for concurrent objects](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) (Linearización: una condición de corrección para objetos concurrentes)
9. [Acuerdo de Nivel de Servicio de Azure Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db/)

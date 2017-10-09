---
title: "Consideraciones de rendimiento y optimización de la búsqueda aaaAzure | Documentos de Microsoft"
description: "Optimización del rendimiento de Búsqueda de Azure y configuración de la escala óptima"
services: search
documentationcenter: 
author: LiamCavanagh
manager: pablocas
editor: 
ms.assetid: 4d3cd864-29d2-4921-be0d-a3f1a819de46
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: 725149ba32773ab6b4c9d4b441424aba78db7c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-performance-and-optimization-considerations"></a>Consideraciones sobre el rendimiento y la optimización de Búsqueda de Azure
Una experiencia de búsqueda excelente es una clave toosuccess para muchos dispositivos móviles y aplicaciones web. Desde la propiedad inmobiliaria, catálogos de tooused automóvil mercados tooonline, búsqueda rápida y los resultados pertinentes afectará a la experiencia del cliente hello. Este documento está previsto toohelp detectar prácticas recomendadas para cómo hello tooget máximo partido de la búsqueda de Azure, especialmente para escenarios avanzados con sofisticadas requisitos de escalabilidad, compatibilidad con varios idioma o clasificación personalizada.  Además, este documento describe los aspectos internos y los enfoques que funcionan de forma eficaz en las aplicaciones de clientes reales.

## <a name="performance-and-scale-tuning-for-search-services"></a>Rendimiento y ajuste de la escala de los servicios de Búsqueda
Estamos todos los motores de toosearch usado como hello y Google y Bing alto rendimiento que ofrecen.  Como resultado, cuando los clientes usan su aplicación móvil o web habilitada para búsqueda, esperan características de rendimiento similares.  Al optimizar el rendimiento de la búsqueda, uno de los mejores métodos de hello es toofocus en la latencia, que es el momento de hello que una consulta toma toocomplete y devuelve los resultados.  Para optimizar la latencia de la búsqueda es importante:

1. Elija una latencia de destino (o la cantidad máxima de tiempo) que una solicitud de búsqueda típicas debe tomar toocomplete.
2. Crear y probar una carga de trabajo real con el servicio de búsqueda con un conjunto de datos realista toomeasure estas tasas de latencia.
3. Comenzar con un número reducido de consultas por segundo (QPS) y continuar número de hello tooincrease ejecutado en pruebas de hello hasta que consulta Hola latencia cae por debajo de hello definido por la latencia de destino.  Se trata de un toohelp de criterio de referencia importante que planee la escala a medida que crece la aplicación en uso.
4. Siempre que sea posible, reutilice las conexiones HTTP.  Si usas Hola SDK de .NET de búsqueda de Azure, esto significa que se debe volver a usar una instancia o [SearchIndexClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchindexclient) de instancia y si utilizas Hola API de REST, debe volver a utilizar un único HttpClient.

Al crear estas cargas de trabajo de prueba, hay algunas características de búsqueda de Azure tookeep en cuenta:

1. Es posible toopush tantos las consultas de búsqueda al mismo tiempo, que se verse desbordados recursos Hola disponibles en el servicio de búsqueda de Azure.  Cuando esto sucede, verá códigos de respuesta HTTP 503.  Por esta razón, es mejor toostart con varios intervalos de búsqueda solicitudes toosee Hola diferencias en las tasas de latencia a medida que agregue más solicitudes de búsqueda.
2. La carga de contenido tooAzure búsqueda afectará Hola el rendimiento general y latencia de Hola servicio de búsqueda de Azure.  Si espera toosend datos mientras los usuarios son realizar búsquedas, es importante tootake esta carga de trabajo en cuenta en las pruebas.
3. No todas las consultas búsqueda llevará a cabo en hello mismo los niveles de rendimiento.  Por ejemplo, una sugerencia de búsqueda o la búsqueda de documentos normalmente se realiza más rápidamente que una consulta, con un número significativo de facetas y filtros.  Es mejor hello tootake varias consultas que espera toosee a tener en cuenta al crear las pruebas.  
4. Variación de las solicitudes de búsqueda es importante porque si se ejecuta continuamente Hola mismo solicitudes de búsqueda, almacenamiento en caché de datos de rendimiento de inicio toomake será mejor que se podría con una consulta más dispares establecido.

> [!NOTE]
> [Pruebas de carga de Visual Studio](https://www.visualstudio.com/docs/test/performance-testing/run-performance-tests-app-before-release) es un tooperform de manera realmente buenos la prueba comparativa prueba ya que permite las solicitudes de tooexecute HTTP como necesite para ejecutar consultas de búsqueda de Azure y habilita la paralelización de solicitudes.
> 
> 

## <a name="scaling-azure-search-for-high-query-rates-and-throttled-requests"></a>Escalado de Búsqueda de Azure para grandes volúmenes de consultas y solicitudes limitadas
Cuando se están recibiendo demasiadas solicitudes limitadas o superan las tarifas de latencia de destino de una carga de consulta, puede consultar las tasas de latencia de toodecrease en uno de dos maneras:

1. **Réplicas de aumento:** una réplica puede considerarse como una copia de los datos que permite a las solicitudes de saldo de búsqueda de Azure tooload contra Hola varias copias.  Todo el equilibrio de carga y administra la replicación de datos entre réplicas de búsqueda de Azure y puede modificar el número de Hola de réplicas asignado para su servicio en cualquier momento.  Puede asignar la too12 réplicas en un servicio de búsqueda estándar y 3 réplicas en un servicio de búsqueda básica. Las réplicas pueden ser ajustado desde hello [portal de Azure](search-create-service-portal.md) o [PowerShell](search-manage-powershell.md).
2. **Aumentar el nivel de búsqueda:** Azure Search se ofrece con [diferentes planes](https://azure.microsoft.com/pricing/details/search/), cada uno de los cuales ofrece diferentes niveles de rendimiento.  En algunos casos, puede tener tantas consultas ese nivel de hello en no puede proporcionar velocidades lo suficientemente baja latencia, incluso cuando se sobrepasa réplicas.  En este caso, puede que desee tooconsider aprovechar uno de niveles superiores de búsqueda hello como nivel de S3 de búsqueda de Azure de Hola que es adecuada para escenarios con un gran número de documentos y las cargas de trabajo de consultas extremadamente alto.

## <a name="scaling-azure-search-for-slow-individual-queries"></a>Escalado de Búsqueda de Azure para consultas individuales lentas
Otro motivo por qué las tasas de latencia pueden ser lentas es de una única consulta toma toocomplete demasiado larga.  En este caso, agregar réplicas no mejorará las tasas de latencia.  En cambio, hay dos opciones disponibles:

1. **Aumentar las particiones**: Una partición es un mecanismo para dividir los datos entre recursos adicionales.  Por este motivo, cuando se agrega una segunda partición, los datos se dividen en dos.  Una tercera partición divide el índice en tres, etc.  Este enfoque también tiene el efecto de Hola que en algunos casos, las consultas lentas llevará a cabo con mayor rapidez debido toohello paralelización de cálculo.  Hemos observado algunos ejemplos en los que esta paralelización funciona muy bien con consultas que tienen consultas de baja selectividad.  Esto consta de las consultas que coinciden con muchos documentos o cuando necesita facetas tooprovide las estadísticas en un gran número de documentos.  Dado que no hay que una gran cantidad de cálculo necesarios pertinencia de hello tooscore de documentos de Hola o números de hello toocount de documentos, agregar particiones adicionales pueden ayudar a cálculo adicionales tooprovide.  
   
   Puede haber un máximo de 12 particiones en el servicio de búsqueda estándar y 1 partición de servicio de búsqueda básica hello.  Las particiones se pueden ajustar desde hello [portal de Azure](search-create-service-portal.md) o [PowerShell](search-manage-powershell.md).
2. **Campos de cardinalidad alta de límite:** un campo de cardinalidad alta consta de un facetable o un campo filtrable que tiene un número significativo de valores únicos y como resultado, tiene una gran cantidad de recursos toocompute resultados sobre.   Por ejemplo, establecer un campo de Id. de producto o la descripción como facetable/filtrables haría para una cardinalidad alta porque la mayoría de los valores de hello de toodocument de documento es única. Siempre que sea posible, limitar número de Hola de campos de cardinalidad alta.
3. **Aumento del nivel de búsqueda:** mover hacia arriba tooa mayor nivel de búsqueda de Azure puede ser otro rendimiento tooimprove de modo de consultas de ejecución lenta.  Cada nivel superior también proporciona CPU más rápidas y más memoria, lo que puede tener un impacto positivo en el rendimiento de las consultas.

## <a name="scaling-for-availability"></a>Escalado para disponibilidad
Las réplicas no solo ayudan a reducir la latencia de las consultas, sino que también permiten una alta disponibilidad.  Con una única réplica debe esperar tiempos de inactividad periódicamente debido tooserver reinicios después de las actualizaciones de software o para otros eventos de mantenimiento que se producirán.  Como resultado, es importante tooconsider si la aplicación requiere alta disponibilidad de las búsquedas (consultas), así como de escritura (eventos indización).  Búsqueda de Azure ofrece opciones de SLA en todos los Hola ofertas de búsqueda de pago con hello siguientes atributos:

* 2 réplicas para alta disponibilidad de cargas de trabajo de solo lectura (consultas)
* 3 o más réplicas para alta disponibilidad de cargas de trabajo de lectura-escritura (consultas e indización)

Para obtener más detalles sobre esto, visite hello [contrato de nivel de servicio de búsqueda de Azure](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

Puesto que las réplicas son copias de los datos, tener varias réplicas permite reinicios de máquina de toodo de búsqueda de Azure y mantenimiento en una réplica a la vez al permitir que las consultas toobe toocontinue ejecutada en Hola otras réplicas.  Por esta razón, también necesitará tooconsider cómo podría afectar a las consultas de Hola que ahora están toobe ejecutada en una copia de datos de hello menos este tiempo de inactividad.

## <a name="scaling-geo-distributed-workloads-and-provide-geo-redundancy"></a>Escalado de cargas de trabajo distribuidas geográficamente y provisión de redundancia geográfica
Para las cargas de trabajo distribuidas geográficamente, encontrará que los usuarios encuentran muy alejado del centro de datos de Hola donde se hospeda el servicio de búsqueda de Azure tendrá mayores tasas de latencia.  Por este motivo, a menudo resulta importante toohave búsqueda varios servicios en las zonas que están en cuanto más se acerque a los usuarios toothese de proximidad.  Búsqueda de Azure no proporciona actualmente un método automatizado de los índices de búsqueda de Azure de replicación geográfica entre regiones, pero hay algunas técnicas que pueden usarse que pueden realizar esta tooimplement simple de proceso y administrar. Se describen en hello siguientes secciones.

objetivo de un conjunto de servicios de búsqueda distribuidos geográficamente Hello es toohave dos o más índices disponibles en dos o más regiones donde un usuario será enrutan toohello servicio de búsqueda de Azure que proporciona la latencia más baja de hello tal como se muestra en este ejemplo:

   ![Tablas de referencias cruzadas de servicios por región][1]

### <a name="keeping-data-in-sync-across-multiple-azure-search-services"></a>Sincronización de los datos entre varios servicios Búsqueda de Azure
Hay dos opciones para mantener los servicios de búsqueda distribuida sincronizados que constan de usando hello [indizador de búsqueda de Azure](search-indexer-overview.md) u Hola API de inserción (también denominada hello tooas [API de REST de búsqueda de Azure](https://docs.microsoft.com/rest/api/searchservice/)).  

### <a name="azure-search-indexers"></a>Indexadores de Búsqueda de Azure
Si usas Hola indizador de búsqueda de Azure, ya va a importar los cambios de datos desde un almacén de datos central como base de datos de SQL Azure o base de datos de Azure Cosmos. Cuando se crea una nueva búsqueda servicio, simplemente crear un nuevo indizador de búsqueda de Azure para ese servicio ese toothis puntos mismo almacén de datos. De este modo, cada vez que proceden de nuevos cambios en el almacén de datos de hello, a continuación, estarán indizado por hello varios indizadores.  

Este es un ejemplo del aspecto que podría tener esa arquitectura.

   ![Origen de datos único con indexador distribuido y combinaciones de servicios][2]

### <a name="push-api"></a>API de inserción
Si utilizas Hola API de inserción de búsqueda de Azure demasiado[actualizar contenido en el índice de búsqueda de Azure](https://docs.microsoft.com/rest/api/searchservice/update-index), puede mantener sincronizados los distintos servicios de búsqueda mediante la aplicación de servicios de búsqueda de tooall de cambios cada vez que se requiere una actualización.  Al hacer esto es importante toomake seguro toohandle casos donde se produce un error en un servicio de búsqueda de tooone de actualización y realice correctamente una o varias actualizaciones.

## <a name="leveraging-azure-traffic-manager"></a>Uso del Administrador de tráfico de Azure
[Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) permite tooroute solicitudes toomultiple ubicados geográficamente sitios Web que, a continuación, está respaldados por varios servicios de búsqueda de Azure.  Una ventaja de hello Traffic Manager es que puede sondear tooensure de búsqueda de Azure que está disponible y enrutar servicios de búsqueda de los usuarios tooalternate en caso de hello de tiempo de inactividad.  Además, si va a enrutar las solicitudes de búsqueda a través de los sitios Web, Azure Traffic Manager permite casos de saldo tooload donde el sitio Web de hello está activo pero no la búsqueda de Azure.  Este es un ejemplo de la arquitectura de Hola que aprovecha el Administrador de tráfico.

   ![Tablas de referencias cruzadas de servicios por región con Administrador de tráfico central][3]

## <a name="monitoring-performance"></a>Supervisión del rendimiento
Búsqueda de Azure ofrece Hola capacidad tooanalyze y supervisar Hola el rendimiento de su servicio a través de [análisis de tráfico de búsqueda (STA)](search-traffic-analytics.md). A través de STA, puede registrar opcionalmente las operaciones de búsqueda individuales de hello, así como la cuenta de almacenamiento de Azure de tooan de métricas agregadas que, a continuación, se procesan para el análisis o visualizar en Power BI.  Con las métricas de STA, puede revisar estadísticas de rendimiento tales como el número promedio de consultas o los tiempos de respuesta de las consultas.  Además, el registro de operaciones de hello permite toodrill en los detalles de las operaciones de búsqueda específico.

STA es una valiosa herramienta toounderstand latencia los índices de esa perspectiva de búsqueda de Azure.  Puesto que registran las métricas de rendimiento de la consulta de Hola se basan en tiempo de hello una consulta toma toobe procesado totalmente en búsqueda de Azure (desde el momento de hello es toowhen solicitado enviarse), es capaz de toouse esta toodetermine si hay problemas de latencia de hello servicio Búsqueda de Azure lado o fuera de Hola service, por ejemplo, de latencia de red.  

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de hello precios niveles y los límites de servicios para cada una de ellas, consulte [límites en la búsqueda de Azure del servicio](search-limits-quotas-capacity.md).

Visite [planeamiento de capacidad](search-capacity-planning.md) toolearn más información acerca de las combinaciones de partición y la réplica.

Para obtener más detalles sobre el rendimiento y toosee algunas demostraciones de cómo tooimplement Hola optimizaciones descritos en este artículo, vea Hola después de vídeo:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<!--Image references-->
[1]: ./media/search-performance-optimization/geo-redundancy.png
[2]: ./media/search-performance-optimization/scale-indexers.png
[3]: ./media/search-performance-optimization/geo-search-traffic-mgr.png

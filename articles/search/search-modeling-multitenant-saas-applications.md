---
title: "aaaModeling multiempresa en búsqueda de Azure | Documentos de Microsoft"
description: "Aprenda sobre patrones de diseño comunes para aplicaciones SaaS multiinquilino mientras usa Azure Search."
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 72e9696a-553b-47dc-9e05-a82db0ebf094
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/26/2016
ms.author: ashmaka
ms.openlocfilehash: dd46cda772d32566b9aaa18d407f12fdf178bd43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multitenant-saas-applications-and-azure-search"></a>Modelos de diseño para aplicaciones SaaS multiinquilino y Azure Search
Una aplicación para varios inquilinos es aquel que proporciona Hola mismo número de tooany de servicios y las capacidades de los inquilinos que no puede ver o compartir datos Hola de otro inquilino. En este documento se describen estrategias de aislamiento de inquilinos para aplicaciones miltiinquilino creadas con Azure Search.

## <a name="azure-search-concepts"></a>Conceptos de Azure Search
Como una solución de búsqueda como servicio, búsqueda de Azure permite la búsqueda a los desarrolladores tooadd experimenta tooapplications sin administrar cualquier infraestructura o pase a ser un experto en la búsqueda. Los datos son cargado toohello servicio y, a continuación, se almacenan en la nube de Hola. Usa solicitudes sencillas toohello API de búsqueda de Azure, datos de hello pueden, a continuación, modificar y buscar. Encontrará información general del servicio de hello en [este artículo](http://aka.ms/whatisazsearch). Antes de hablar sobre los patrones de diseño, es importante toounderstand algunos conceptos en búsqueda de Azure.

### <a name="search-services-indexes-fields-and-documents"></a>Servicios de búsqueda, índices, campos y documentos
Cuando se utiliza la búsqueda de Azure, uno suscribe tooa *servicio de búsqueda*. Como datos están cargado tooAzure búsqueda, se almacena en un *índice* dentro de servicio de búsqueda de Hola. Puede haber varios índices dentro de un único servicio. toouse Hola de conceptos conocidos de las bases de datos, servicio de búsqueda de hello pueden asemejar tooa base de datos mientras los índices de hello dentro de un servicio pueden ser asemejar tootables dentro de una base de datos.

Cada índice dentro de un servicio de búsqueda tiene su propio esquema, que viene definido por in número de *campos*personalizables. Se agregan datos de índice de búsqueda de Azure tooan en forma de Hola de persona *documentos*. Cada documento debe ser el índice determinado de tooa cargados y debe ajustarse el esquema del índice. Al buscar datos mediante la búsqueda de Azure, las consultas de búsqueda de texto completo de Hola se emiten en un índice determinado.  toocompare toothose de estos conceptos de una base de datos, los campos pueden estar asemejar toocolumns en una tabla y los documentos pueden ser asemejar toorows.

### <a name="scalability"></a>Escalabilidad
Cualquier servicio de búsqueda de Azure en hello estándar [tarifa](https://azure.microsoft.com/pricing/details/search/) puede escalar de dos dimensiones: almacenamiento y disponibilidad.

* *Las particiones* se pueden agregar almacenamiento de hello tooincrease de un servicio de búsqueda.
* *Réplicas* puede agregarse el rendimiento de tooa servicio tooincrease Hola de solicitudes que puede administrar un servicio de búsqueda.

Agregar y quitar las particiones y réplicas en permitirá capacidad Hola de hello toogrow de servicio de búsqueda con la cantidad de Hola de datos y el tráfico de demandas de aplicaciones de Hola. En el criterio de un tooachieve de servicio de búsqueda de una lectura [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), requiere dos réplicas. En el criterio de un servicio tooachieve una lectura y escritura [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), requiere tres réplicas.

### <a name="service-and-index-limits-in-azure-search"></a>Límites de servicio e índice en Azure Search
Hay diversos diferentes [los niveles de precios](https://azure.microsoft.com/pricing/details/search/) en búsqueda de Azure, cada uno de los niveles de hello tiene distintos [límites y cuotas de](search-limits-quotas-capacity.md). Algunos de estos límites corren Hola de nivel de servicio, algunas están en el nivel del índice de Hola y algunos son en el nivel de partición Hola.

|  | Básica | Standard1 | Standard2 | Standard3 | Standard3 HD |
| --- | --- | --- | --- | --- | --- |
| Número máximo de réplicas por servicio |3 |12 |12 |12 |12 |
| Número máximo de particiones por servicio |1 |12 |12 |12 |1 |
| Número máximo de unidades de búsqueda (réplicas * particiones) por servicio |3 |36 |36 |36 |36 (3 particiones como máximo) |
| Número máximo de documentos por servicio |1 millón |180 millones |720 millones |1,4 mil millones |600 millones |
| Almacenamiento máximo por servicio |2 GB |< 300 GB |1,2 TB |2,4 TB |600 GB |
| Número máximo de documentos por partición |1 millón |15 millones |60 millones |120 millones |200 millones |
| Almacenamiento máximo por partición |2 GB |25 GB |100 GB |200 GB |200 GB |
| Número máximo de índices por servicio |5 |50 |200 |200 |3000 (1000 índices/partición como máximo) |

#### <a name="s3-high-density"></a>S3 alta densidad'
En el nivel de precios de S3 de búsqueda de Azure, hay una opción para el modo de alta densidad (HD) Hola diseñado específicamente para los escenarios de varios inquilinos. En muchos casos, es necesario toosupport un gran número de inquilinos más pequeños en un ventajas de servicio único tooachieve Hola de simplicidad y la rentabilidad.

S3 HD permite hello toobe de muchos índices pequeños empaquetados en administración de Hola de un servicio de búsqueda sencillo mediante comerciales Hola capacidad tooscale out índices con particiones para hello capacidad toohost varios índices en un único servicio.

En concreto, un servicio de S3 podría tener entre 1 y 200 índices que pudieron hospedar juntos documentos de miles de millones de too1.4. Un HD S3 en hello otra parte permitiría índices individuales tooonly Subir too1 millones de documentos, pero puede administrar los índices de too1000 por partición (arriba too3000 por servicio) con un recuento total del documento de 200 millones por partición (seguridad too600 millones por servicio).

## <a name="considerations-for-multitenant-applications"></a>Consideraciones sobre las aplicaciones multiinquilino
Aplicaciones para varios inquilinos deben distribuir de manera eficaz recursos entre inquilinos Hola conservando cierto nivel de privacidad entre Hola varios inquilinos. Hay algunas consideraciones al diseñar la arquitectura de Hola para este tipo de aplicación:

* *Aislamiento de inquilinos:* los desarrolladores de aplicaciones necesitan tootake tooensure de las medidas adecuadas que ningún inquilino tiene no autorizado o no deseado toohello acceder a los datos de otros inquilinos. Más allá de la perspectiva de Hola de privacidad de los datos, las estrategias de aislamiento de inquilinos requieren administración eficaz de los recursos compartidos y protección frente a los vecinos con ruido.
* *Costo de los recursos de nube:* al igual que sucede con cualquier otra aplicación, las soluciones de software deben tener un costo competitivo en cuanto componente de una aplicación multiinquilino.
* *Facilidad de operaciones:* al desarrollar una arquitectura para varios inquilinos, Hola impacto en las operaciones de la aplicación hello y complejidad es una consideración importante. Azure Search tiene un [Acuerdo de Nivel de Servicio del 99,9 %](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
* *Superficie global:* aplicaciones para varios inquilinos que necesite tooeffectively serve inquilinos que se distribuyen en todo el mundo de Hola.
* *Escalabilidad:* los desarrolladores de aplicaciones necesita tooconsider cómo conciliar entre mantener un nivel de complejidad de las aplicaciones lo suficientemente bajo y diseñar Hola aplicación tooscale con varios inquilinos y tamaño de los datos de los inquilinos de Hola y carga de trabajo.

Búsqueda de Azure ofrece unos límites que pueden ser datos y la carga de trabajo de los inquilinos de tooisolate usado.

## <a name="modeling-multitenancy-with-azure-search"></a>Modelado multiinquilino con Azure Search
En caso de hello de un escenario de varios inquilinos, el desarrollador de aplicaciones de hello consume uno o varios servicios de búsqueda y dividir sus inquilinos entre servicios, los índices o ambos. Azure Search presenta algunos patrones comunes al modelar un escenario multiinquilino:

1. *Índice por inquilino:* cada inquilino tiene su propio índice dentro de un servicio de búsqueda que comparte con otros inquilinos.
2. *Servicio por inquilino:* cada inquilino tiene su propio servicio de Azure Search dedicado, que ofrece el nivel más alto de separación de datos y carga de trabajo.
3. *Mezcla de ambos:* los inquilinos más grandes y activos se asignan a servicios dedicados, mientras que los inquilinos más pequeños se asignan a índices individuales dentro de servicios compartidos.

## <a name="1-index-per-tenant"></a>1. Índice por inquilino
![Una representación del modelo de índice por inquilino Hola](./media/search-modeling-multitenant-saas-applications/azure-search-index-per-tenant.png)

En un modelo de índice por inquilino, varios inquilinos ocupan un único servicio de Azure Search donde cada inquilino tiene su propio índice.

Los inquilinos consiguen el aislamiento de los datos porque todas las solicitudes de búsqueda y las operaciones de documentos se emiten en un nivel de índice en Azure Search. En el nivel de aplicación Hola, hay conocimiento de la necesidad de hello toodirect Hola índices adecuados de varios inquilinos tráfico toohello al administrar también los recursos de nivel de servicio de hello entre todos los inquilinos.

Un atributo clave del modelo de índice por inquilino hello es la capacidad de Hola para hello aplicación developer toooversubscribe Hola la capacidad de un servicio de búsqueda entre los inquilinos de la aplicación hello. Si los inquilinos de hello tienen una distribución desigual de carga de trabajo, la combinación óptima de Hola de los inquilinos pueden distribuirse a través de un servicio de búsqueda de índices tooaccommodate varios inquilinos muy activos, que consumen muchos recursos durante el envío de forma simultánea una cola larga de menos activos, los inquilinos. ventajas y desventajas de Hello son la incapacidad de Hola de situaciones de toohandle de modelo de hello en cada inquilino simultáneamente es muy activo.

modelo de índice por inquilino Hola proporciona la base de Hola para un modelo de costos de variable, donde un servicio de búsqueda de Azure completo se compró inicial y, a continuación, que posteriormente se rellena con los inquilinos. Esto permite toobe de capacidad no usada designado para las evaluaciones y las cuentas gratuitas.

Para las aplicaciones con una superficie global, Hola índice por inquilino puede no ser modelo hello más eficaz. Si los inquilinos de la aplicación se distribuyen en todo el mundo de hello, un servicio independiente puede ser necesario para cada región que se puede duplicar los costos a través de cada uno de ellos.

Búsqueda de Azure permite escalar Hola de índices individuales de Hola y el número total de Hola de toogrow de índices. Si un precio adecuado se elige capa, particiones y réplicas se pueden agregar servicio de búsqueda completa toohello cuando un índice individual dentro de servicio de hello crece demasiado grande en términos de almacenamiento o el tráfico.

Si el número total de Hola de índices aumenta demasiado grande para un único servicio, otro servicio tiene toobe aprovisionado tooaccommodate Hola a nuevos inquilinos. Si los índices tienen toobe movido entre los servicios de búsqueda a medida que se agregan nuevos servicios, los datos de Hola desde el índice de hello son toobe copiado manualmente desde un índice toohello otros como búsqueda de Azure no permite un toobe índice movido.

## <a name="2-service-per-tenant"></a>2. Servicio por inquilino
![Una representación del modelo de servicio por inquilino Hola](./media/search-modeling-multitenant-saas-applications/azure-search-service-per-tenant.png)

En una arquitectura de servicio por inquilino, cada inquilino tiene su propio servicio de búsqueda.

En este modelo, aplicación hello alcanza Hola el grado máximo de aislamiento de sus inquilinos. Cada servicio tiene almacenamiento y capacidad de proceso dedicados para administrar las solicitudes de búsqueda, así como claves de API independientes.

Para las aplicaciones donde cada inquilino tiene una superficie de gran tamaño o carga de trabajo de hello tiene poca variabilidad del inquilino tootenant, modelo de servicio por inquilino hello es una opción eficaz como recursos no se comparten entre las cargas de trabajo de varios inquilinos.

Un servicio por cada modelo de inquilinos también ofrece la ventaja de Hola de un modelo de predicción costo fijo. No hay ninguna inversión inicial en un servicio de búsqueda completa hasta que haya un toofill inquilino, sin embargo es mayor que un modelo de índice por inquilino Hola costo por inquilino.

modelo de servicio por inquilino Hello es una opción eficaz para las aplicaciones con una superficie global. Con inquilinos distribuidos geográficamente, resulta fácil toohave servicio de cada inquilino de región adecuada de Hola.

desafíos de Hello en este patrón de ajuste de escala surgen cuando los inquilinos individuales superan la capacidad de su servicio. Búsqueda de Azure no admite actualmente la actualización Hola tarifa de un servicio de búsqueda, por lo que todos los datos tendría toobe copiado manualmente tooa nuevo servicio.

## <a name="3-mixing-both-models"></a>3. Mezcla de ambos modelos
Otro patrón para modelar la arquitectura multiinquilino es mezclar las estrategias de índice por inquilino y servicio por inquilino.

Mediante la combinación de patrones de hello dos, inquilinos más grandes de una aplicación pueden ocupar servicios dedicados mientras Hola tiempo final del menos inquilinos activos, más pequeños puede ocupar índices en un servicio compartido. Este modelo garantiza que los inquilinos más grandes de hello constantemente alto rendimiento de servicio de Hola y ayudar a tooprotect Hola a inquilinos más pequeños de los vecinos con ruido.

Sin embargo, la implementación de esta estrategia depende de la previsión de qué inquilinos necesitarán un servicio dedicado, por oposición a un índice en un servicio compartido. Complejidad de la aplicación aumenta con hello necesidad toomanage ambos de estos modelos multiempresa.

## <a name="achieving-even-finer-granularity"></a>Obtención incluso de una granularidad más fina
Hola por encima de los escenarios de varios inquilinos toomodel de diseño patrones de búsqueda de Azure supone un ámbito uniforme donde cada inquilino es una instancia completa de una aplicación. Sin embargo, en ocasiones las aplicaciones pueden controlar ámbitos mucho más pequeños.

Si los modelos de servicio por inquilino y de índice por inquilinos no son lo bastante pequeños ámbitos, es posible toomodel un tooachieve un incluso mayor grado de granularidad de índice.

toohave un único índice comportarse de forma diferente para los extremos de cliente diferente, un campo puede ser índice tooan agregada que designa un valor determinado para cada cliente. Cada vez que un cliente llama a tooquery de búsqueda de Azure o modificar un índice, código de hello de aplicación de cliente de Hola especifica el valor adecuado de Hola para ese campo mediante la búsqueda de Azure [filtro](https://msdn.microsoft.com/library/azure/dn798921.aspx) capacidad en el momento de la consulta.

Este método puede ser tooachieve usa la funcionalidad de cuentas de usuario independientes, los niveles de permisos distintos y aplicaciones incluso completamente independientes.

> [!NOTE]
> Con el enfoque de hello había descrita anteriormente tooconfigure un único índice tooserve varios inquilinos afecta a Hola por relevancia de los resultados de la búsqueda. Puntuaciones de importancia de la búsqueda se calculan en un ámbito de nivel del índice, no es un ámbito de nivel del inquilino, por lo que los datos de todos los inquilinos se incorporan en las estadísticas subyacentes de las puntuaciones de importancia de hello como su frecuencia.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Búsqueda de Azure es una opción atractiva para muchas aplicaciones, [leer más acerca de las eficaces capacidades del servicio de hello](http://aka.ms/whatisazsearch). Al evaluar Hola distintos modelos para aplicaciones para varios inquilinos de diseño, considere la posibilidad de hello [distintos niveles de precios](https://azure.microsoft.com/pricing/details/search/) hello respectivo y [límites de servicio](search-limits-quotas-capacity.md) toobest adaptar toofit de búsqueda de Azure arquitecturas de todos los tamaños y las cargas de trabajo de la aplicación.

Se puede dirigir alguna pregunta acerca de la búsqueda de Azure y situaciones de varios inquilinos tooazuresearch_contact@microsoft.com.


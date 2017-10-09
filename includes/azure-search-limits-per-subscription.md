Puede crear varios servicios en una suscripción, cada uno de ellos proporciona en un nivel concreto, limitado solo por el número de hello de servicios permitidos en cada nivel. Por ejemplo, puede crear los servicios de too12 en el nivel básico de Hola y servicios de otro 12 en nivel de hello S1 dentro de hello mismo suscripción. Para más información acerca de los niveles, consulte [Selección de SKU o plan de tarifa de Azure Search](../articles/search/search-sku-tier.md).

El límite máximo de servicios se puede elevar a petición. Póngase en contacto con soporte técnico de Azure si necesita más servicios dentro de hello misma suscripción.

| Recurso | Gratuito | Básica | S1 | S2 | S3 | S3 HD <sup>1</sup> |
| --- | --- | --- | --- | --- | --- | --- |
| Servicios máximos |1 |12 |12 |6 |6 |6 |
| Escala máxima en SU <sup>2</sup> |N/D <sup>3</sup> |3 SU <sup>4</sup> |36 unidades de búsqueda |36 unidades de búsqueda |36 unidades de búsqueda |36 unidades de búsqueda |

<sup>1</sup> HD S3 no admite [indexadores](../articles/search/search-indexer-overview.md) en este momento. 

<sup>2</sup> Las unidades de búsqueda (SU) son unidades facturables, asignadas como *réplica* o como *partición*. Ambos recursos se necesitan para las operaciones de almacenamiento, indexación y consulta. más información acerca de cómo se calculan las unidades de búsqueda, además de un gráfico de combinaciones válidas que permanecen en los límites máximos de hello, consulte toolearn [escalar los niveles de recursos para las cargas de trabajo de consulta e índice](../articles/search/search-capacity-planning.md). 

<sup>3</sup> Gratis se basa en los recursos compartidos que usan varios suscriptores. En este nivel, no hay ningún recurso dedicado para un suscriptor individual. Por este motivo, la escala máxima se marca como no aplicable.

<sup>4</sup> Básico tiene una partición fija. En este nivel, se utilizan SU adicionales para asignar más réplicas a más cargas de trabajo de consulta.


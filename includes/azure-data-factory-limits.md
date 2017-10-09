Factoría de datos es un servicio de varios inquilinos que ha Hola siguiendo los límites predeterminados del lugar toomake seguro de las suscripciones de cliente están protegidas frente a cargas de trabajo entre ellos. Muchos de los límites de hello pueden generar fácilmente para su suscripción de límite máximo de toohello póngase en contacto con soporte técnico.

| **Recurso** | **Límite predeterminado** | **Límite máximo** |
| --- | --- | --- |
| data factories en una suscripción de Azure |50 |[Ponerse en contacto con soporte técnico](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| canalizaciones dentro de una factoría de datos |2.500 |[Ponerse en contacto con soporte técnico](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| conjuntos de datos dentro de una factoría de datos |5000 |[Ponerse en contacto con soporte técnico](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| fragmentos simultáneos por conjunto de datos |10 |10 |
| bytes por objeto para objetos de canalización <sup>1</sup> |200 KB |200 KB |
| bytes por objeto para objetos de conjunto de datos y de servicio vinculados <sup>1</sup> |100 KB |2000 KB |
| Núcleos de clúster a petición de HDInsight con una suscripción <sup>2</sup> |60 |[Ponerse en contacto con soporte técnico](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Unidades de movimiento de datos de nube<sup>3</sup> |32 |[Ponerse en contacto con soporte técnico](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Número de reintentos de ejecuciones de la actividad Canalización |1000 |MaxInt (32 bits) |

<sup>1</sup> Los objetos de canalización, de conjunto de datos y de servicio vinculado representan una agrupación lógica de la carga de trabajo. Límites de estos objetos no se relacionan con tooamount de datos, puede mover y procesar con el servicio de factoría de datos de Azure Hola. Factoría de datos está diseñada tooscale toohandle petabytes de datos.

<sup>2</sup> núcleos de HDInsight a petición se asignan fuera de la suscripción de Hola que contiene la factoría de datos de Hola. Como resultado, Hola por encima del límite es hello factoría de datos aplica el límite de núcleos de núcleos de HDInsight a petición y es diferente de límite de núcleos de hello asociada a su suscripción de Azure.

<sup>3</sup> La unidad de movimiento de datos de nube (DMU) se usa en una operación de copia de la nube a la nube. Es una medida que representa la potencia de hello (una combinación de asignación de recursos de red, CPU y memoria) de una sola unidad de factoría de datos. Poder usar más DMU en algunos escenarios permite lograr una mayor capacidad de procesamiento de copia. Consulte demasiado[unidades de movimiento de datos en la nube](../articles/data-factory/data-factory-copy-activity-performance.md#cloud-data-movement-units) sección de detalles.

| **Recurso** | **Límite inferior predeterminado** | **Límite mínimo** |
| --- | --- | --- |
| Intervalo de programación |15 minutos |15 minutos |
| Intervalo entre reintentos |1 segundo |1 segundo |
| Valor de tiempo de espera de reintento |1 segundo |1 segundo |

### <a name="web-service-call-limits"></a>Límites de llamadas de servicio web
Azure Resource Manager tiene límites para las llamadas de API. Puede realizar llamadas de API a una velocidad de hello [API del Administrador de recursos de Azure limita](../articles/azure-subscription-service-limits.md#resource-group-limits).

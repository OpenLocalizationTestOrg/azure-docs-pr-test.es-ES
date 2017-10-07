---
title: aaaMicrosoft del uso de Azure y RateCard API habilitar Cloudyn tooProvide ITFM para clientes | Documentos de Microsoft
description: "Proporciona una perspectiva exclusiva de facturación de Microsoft Azure asociado Cloudyn, en sus experiencias integrar hello las API de facturación de Azure en su producto.  Esto es especialmente útil para los clientes de Azure y de Cloudyn que están interesados en usar o probar Cloudyn para servicios de Azure."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: f1397397-7e92-4c20-9862-ab6b93afefb7
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: e221ac8b8feebb725a1cc669c8143ab829621a8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-usage-and-ratecard-apis-enable-cloudyn-tooprovide-itfm-for-customers"></a>Uso de Microsoft Azure y RateCard API habilitar Cloudyn tooProvide ITFM para clientes
Cloudyn, un socio de desarrollo de Microsoft y un de los principales proveedores de capacidades de administración de la nube, se ha elegido una vista previa privada de hello nuevo de uso de recursos de Microsoft Azure y RateCard APIs.  Hola API de uso proporciona datos de consumo de Azure de tooestimated de acceso para una suscripción. Hola API RateCard proporciona información sobre los precios completa de todos los servicios de Azure, para los clientes que no sean - contrato Enterprise EA. Integradas juntas, estas API ofrecen una base de información completa para introducirla en herramientas de administración financiera de TI (ITFM) como las proporcionadas por Cloudyn.

## <a name="introduction"></a>Introducción
Hola denominada "multiplicación" de datos de hello API de uso con los datos de hello API RateCard (price de uso [unidades] [$unit] = detallados de uso y el costo) crea hello más granular, preciso y fiable información de facturación disponible para Azure hoy en día.

![Información general de ITFM][1]

Consumir estas API proporciona información clave sobre el uso y los costos, permitiendo que Cloudyn tooanalyze cliente las cuentas de una manera simple y mediante programación y tooperform diversas tareas ITFM para sus clientes de los clientes.

## <a name="integrating-cloudyn-with-hello-ratecard-and-usage-apis"></a>Integración de Cloudyn con hello RateCard y uso de API
Hola API RateCard requiere varios parámetros de entrada, como información de la región, moneda y configuración regional--pero hello más importante uno es OfferDurableID, que especifica el tipo hello Azure Customer Hola oferta está usando (pago por uso, heredado 6 y 12 meses compromiso los planes, MSDN ofertas, MPN ofertas, ofertas promocionales y otros). Hello OfferDurableID puede encontrarse en hello [del uso de Azure y el portal de facturación](https://account.windowsazure.com/Subscriptions), bajo Hola "Ofrecen ID" para hello suscripción concreta.

Al registrarse para [Cloudyn para Azure](https://www.cloudyn.com/microsoft-azure/) services, los clientes pueden agregar su código OfferDurableID, lo que permite Cloudyn toopull su información de precios relevante a través de API RateCard Hola.  Puede encontrar información acerca de diferentes tipos de ofertas de Hola uno Hola [Microsoft Azure ofrecen detalles](https://azure.microsoft.com/support/legal/offer-details/) página.

![Información general del motor ITFM de Cloudyn][2]

Usa Cloudyn que ambos Hola RateCard APIs y uso en suma toohello rendimiento API de Azure, toocreate capas adicionales de visualización, análisis, alertas, informes, costo recomendaciones útiles, proporcionando un confiable los clientes de Azure y administración herramienta ITFM de empresa en la nube.

## <a name="cloudyn-itfm-use-cases-enabled-by-usage-and-ratecard-api-integration"></a>Casos de uso de ITFM de Cloudyn habilitados por la integración de las API de uso y de RateCard
Entre los casos de uso de ITFM de Cloudyn comunes habilitados por la integración de las API de uso y de RateCard se incluyen:

* **Análisis de costos** -permite nube cuesta toobe desglosado tooany nativo de identificación de dimensión (proveedor de servicio, cuenta, región etcetera.). Hola del uso de Azure y RateCard APIs hacen que una tarea fácil, proporcionando más granular desglose de Hola de datos de uso y el costo por cuenta, que es, a continuación, agrupan y filtrado por Cloudyn y presentan toohello usuario, en forma de gráfico o tabular.

![Gráfico circular de análisis de costos][3]

* **Costo asignación 360** -hello de toouncover de administradores de TI real y habilita Finanzas costo desglose, los controladores y las tendencias de su implementación en la nube. Además permite administradores tooeasily los gastos de implementación asociado con las unidades de negocio, departamentos, regiones etc., proporcionando información sin precedentes sobre los costos de la nube y facilitación de enterprise recargos y showbacks. Hola del uso de Azure y RateCard APIs actúan como motor de asignación del entrada tooCloudyn costo, que complementa Hola API mediante la definición de métodos y la lógica de negocios para la asignación de recursos no etiquetados o untaggable.

![Gráfico de asignación de costos 360][4]

* **Ajuste de tamaño rentable** -proporciona recomendaciones de ajuste de tamaño para infrautilizados máquinas virtuales, lo que reduce los gastos del cliente de hello en máquinas provistas en exceso o demasiado grandes. Se hace examinando la CPU de la máquina virtual y las métricas de RAM (con la API de rendimiento), las horas de tiempo de ejecución (con la API de uso) y el costo (con la API de RateCard). Cloudyn, a continuación, se proporcionan recomendaciones de ajuste de tamaño en función de los recursos de CPU o memoria RAM (rendimiento) y calcula el ahorro estimado multiplicando delta de precio hello (RateCard) entre las máquinas virtuales de Hola por hello real tiempo de uso (uso) del programa Hola a máquina infrautilizada.

![Ajuste de tamaño rentable][5]

* **Recomendaciones sobre portabilidad en nube** : proporciona asesoramiento financiero sobre portabilidad en nube. Examina los costos actual de un usuario de recursos de nube que se implementan en los proveedores de nube principales y lo compara el costo de toohello de una implementación equivalente en Azure. A continuación, proporciona granular, por recursos, financieramente basada en trasladar tooAzure de recomendaciones. Después de evaluar una implementación equivalente Hola necesaria en Azure (según las preferencias de usuario y las métricas de rendimiento), Cloudyn usa costo de hello API RateCard tooevaluate Hola de implementación equivalente de hello en Azure.
* **Informes de rendimiento** -habilita el rendimiento de Azure API, estos informes proporcionan una serie de características de uso de CPU y RAM toooptimization recomendaciones. A continuación se muestra un ejemplo de informe de utilización de instancia, que presenta un desglose de instancia por uso medio de CPU.

![Informes de rendimiento][6]

* **Administrador de la categoría** -una característica muy eficaz en Cloudyn que incorpora criterio toounorganized recursos en la nube. Proporciona a los usuarios Hola libertad toocreate sus propias categorías únicos (tags) para medir el efectivo y los informes que está en consonancia con las prácticas empresariales. Además, los usuarios pueden fácilmente regular y clasificar etiquetas incoherentes (por ejemplo, errores tipográficos y otras discrepancias) y detectar automáticamente recursos sin etiquetas para una atribución precisa de los costos.

![Administrador de categoría][7]

## <a name="video"></a>Vídeo
Este es un breve vídeo que muestra cómo un cliente de Azure puede usar Cloudyn en hello API de facturación de Azure, visión toogain de sus datos de consumo de Azure y Azure.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Cloudyn-Provides-Cloud-ITFM-Tools-Via-Microsoft-Azure-APIs/player]
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* Iniciar una segunda [Cloudyn para Azure](https://www.cloudyn.com/microsoft-azure/) toosee prueba cómo obtener costo transparencia con informes personalizados y análisis para la implementación de nube de Microsoft Azure.
* Vea [obtener información sobre el consumo de recursos de Microsoft Azure](billing-usage-rate-card-overview.md) para obtener información general de uso de recursos de Azure de Hola y RateCard APIs.
* Extraer del repositorio hello [referencia de API de REST de facturación de Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) para obtener más información sobre las API, que forman parte del conjunto de Hola de las API proporcionadas por hello Azure Resource Manager.
* Si desea que toodive directamente en el código de ejemplo de Hola, visite nuestros ejemplos código de API de facturación de Azure de Microsoft en [ejemplos de código de Azure](https://azure.microsoft.com/documentation/samples/?term=billing).

## <a name="learn-more"></a>Más información
* toolearn más información acerca de ofertas de Microsoft Azure Enterprise acuerdo (EA), visite [licencias de Azure para hello Enterprise](https://azure.microsoft.com/pricing/enterprise-agreement/)
* Vea hello [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) artículo toolearn más información acerca de hello Azure Resource Manager.
* Para obtener información adicional en el conjunto de Hola de herramientas dedicar toohelp necesario para obtener una descripción de la nube, consulte demasiado Gartner artículo [Guía de mercado para herramientas de administración de financieros TI (ITFM)](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

<!--Image references-->
[1]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Overview.png
[2]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Engine-Overview.png
[3]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Analysis-Pie-Chart.png
[4]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Allocation-360-Chart.png
[5]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Effective-Sizing.png
[6]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Performance-Reports.png
[7]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Category-Manager.png

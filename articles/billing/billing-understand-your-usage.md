---
title: aaaUnderstand Azure detallados de uso | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooread y entender las secciones de Hola de su uso detallada CSV para su suscripción de Azure"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: tonguyen
ms.openlocfilehash: c9284bf94bfa9f36cdd5d39e653a35def7c1aa34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-terms-on-your-microsoft-azure-detailed-usage-charges"></a>Descripción de los términos de los cargos de uso detallados de Microsoft Azure 
Hola detallados de uso archivo CSV de cargos contiene diariamente y cargos por uso de nivel de medidor de hello período de facturación actual. 

tooget el archivo de uso detallada, consulte [cómo tooget la facturación de Azure de factura y datos de uso diario](billing-download-azure-invoice-daily-usage-date.md).
Está disponible en un formato de archivo de valores separados por comas (.csv) que se puede abrir en una aplicación de hoja de cálculo. Si ve dos versiones disponibles, descargue la versión 2. Es el formato de archivo más actual de Hola.

Los cargos de uso son Hola total **mensual** cargos en una suscripción. Los cargos de uso no tienen en cuenta los créditos o descuentos.

## <a name="detailed-terms-and-descriptions-of-your-detailed-usage-file"></a>Términos y descripciones detallados del archivo de uso detallado
Hello siguientes secciones describen los términos importantes Hola que se muestra en la versión 2 del archivo de uso detallada de Hola.

### <a name="statement"></a>Instrucción
la sección superior Hola de hello detallada uso CSV muestra hello servicios de archivo que ha utilizado durante el período de facturación del mes de Hola. Hello tabla siguiente enumeran los términos de Hola y descripciones que se muestra en esta sección.

| Término | Descripción |
| --- | --- |
|Período de facturación |período de facturación de Hello cuando se utilizaron metros Hola |
|Categoría de medidor |Identifica el servicio de nivel superior de hello para el uso de Hola |
|Subcategoría de medidor |Define el tipo de saludo de servicio de Azure que puede afectar a la velocidad de Hola |
|Nombre de medidor |Identifique la unidad de medida para el medidor de hello consumido Hola |
|Medidor de la región |Identifica la ubicación de hello del centro de datos de Hola para determinados servicios que tienen un precio en función de la ubicación de centro de datos |
|SKU |Identifica el identificador de sistema único de Hola para cada contador de Azure |
|Unidad |Identifica Hola unidad que se cobra servicio hello en. Por ejemplo, GB, horas, 10.000 s. |
|Cantidad consumida |cantidad de Hola de métrica de Hola que se usa durante el período de facturación de Hola |
|Cantidad incluida |cantidad de Hola de medidor de Hola que se incluye sin cargo en el período de facturación actual |
|Cantidad de superávit |Muestra hello diferencia entre Hola cantidad consumida y Hola incluyen cantidad. Se factura este importe. Para las ofertas de pago por uso con ninguna cantidad incluidos con la oferta de hello, este total es Hola igual Hola cantidad consumida. |
|Dentro del compromiso |Muestra los cargos de medidor de Hola que se restan a la cantidad del compromiso asociado con su oferta de 6 o 12 meses. Los cargos por medidor se restan en orden cronológico. |
|Moneda |moneda Hello en el período de facturación actual |
|Superávit |Muestra los cargos de medidor de Hola que superan la cantidad del compromiso asociado con su oferta de 6 o 12 meses |
|Tarifa de compromiso |Muestra la velocidad de compromiso de hello en función de la cantidad del compromiso total de hello asociado con su oferta de 6 o 12 meses |
|Tarifa |tasa de Hola que se le cobrará por unidad facturable |
|Valor |Muestra el resultado de hello de multiplicación Hola columna cantidad por encima del límite de columna de la tasa de Hola. Si hello que no supera la cantidad consumida hello cantidad incluye, no hay ningún cargo en esta columna. |

### <a name="daily-usage"></a>Uso diario

la sección uso diario del archivo CSV de Hola Hola muestra los detalles de uso que afectan a las tasas de facturación de Hola. Hello tabla siguiente enumeran los términos de Hola y descripciones que se muestra en esta sección.

| Término | Descripción |
| --- | --- |
|Fecha de uso |fecha de Hello cuando usó medidor Hola |
|Categoría de medidor |Identifica el servicio de nivel superior de hello para la que pertenece este uso |
|Id. de medidor |Hola factura identificador de medidor que ha utilizado el uso de facturación tooprice |
|Subcategoría de medidor |Define el tipo de servicio de Azure de Hola que puede afectar a la velocidad de Hola |
|Nombre de medidor |Identifique la unidad de medida para el medidor de hello consumido Hola |
|Medidor de la región |Identifica la ubicación de hello del centro de datos de Hola para determinados servicios que tienen un precio en función de la ubicación de centro de datos |
|Unidad |Identifica unidad Hola ese medidor Hola se carga en. Por ejemplo, GB, horas, 10.000 s. |
|Cantidad consumida |cantidad de Hola de medidor de Hola que se ha consumido durante ese día |
|Ubicación del recurso |Identifica Hola centro de datos donde se está ejecutando medidor Hola |
|Servicio consumido |servicio de la plataforma Windows Azure que se usaba Hola |
|Grupo de recursos |en qué Hola medidor implementada se ejecuta en el grupo de recursos de Hola. <br/><br/>Para más información, consulte [Información general de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
|Id. de instancia | identificador de Hello para el medidor de Hola. <br/><br/> identificador de Hello contiene nombre de Hola que especifique para el medidor de hello cuando se creó. Puede ser nombre hello del recurso de Hola u Hola completo identificador de recurso. Para más información, consulte [API de Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/resources). |
|Etiquetas | Etiqueta asignar toohello medidor. Usar registros de facturación de toogroup de etiquetas.<br/><br/>Por ejemplo, puede usar etiquetas toodistribute costos por departamento Hola que usa el medidor de Hola. Los servicios que admiten etiquetas emitir son máquinas virtuales, almacenamiento y servicios de red aprovisionados con hello [API de Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/resources). Para más información, consulte [Organize your Azure resources with tags](http://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) (Organización de los recursos de Azure con etiquetas). |
|Información adicional |Metadatos específicos del servicio. Por ejemplo, un tipo de imagen de una máquina virtual. |
|Información de servicio 1 |nombre de proyecto de Hola que Hola servicio pertenece tooon su suscripción |
|Información de servicio 2 |Campo heredado que captura los metadatos específicos del servicio opcional. |

## <a name="how-do-i-make-sure-that-hello-charges-in-my-detailed-usage-file-are-correct"></a>¿Cómo puedo asegurarme de que los cargos de hello en mi archivo detallados de uso son correctos?
Si hay un cargo en el archivo de uso detallado del que quiera tener más detalles, consulte [Descripción de la factura de Microsoft Azure.](./billing-understand-your-bill.md)

## <a name="external"></a>¿Qué son los cargos de servicios externos?
Los servicios externos (también conocidos como pedidos de Marketplace) se proporcionan mediante proveedores de servicios independientes y se facturan por separado. los cargos de Hello no aparecen en hello factura de Azure. más información, consulte toolearn [comprender los cargos de servicio externos Azure](billing-understand-your-azure-marketplace-charges.md).

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Póngase en contacto con el servicio de soporte técnico.
Si sigue necesitando ayuda, [póngase en contacto con el servicio de soporte técnico](https://portal.azure.com/?) para resolver el problema rápidamente.

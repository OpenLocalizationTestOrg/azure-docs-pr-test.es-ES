---
title: aaaUnderstand su factura de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooread y comprender el uso y facturación para la suscripción de Azure"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 32eea268-161c-4b93-8774-bc435d78a8c9
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: tonguyen
ms.openlocfilehash: a3195eb129b1576e8cb665aa6f88a1a2647edd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-bill-for-microsoft-azure"></a>Comprender la factura de Microsoft Azure
toounderstand facturar a Azure, compare la factura con archivos de uso detallada diaria de Hola y Hola costo informes de administración en hello portal de Azure.

tooobtain un PDF de la factura y una copia de su detalladas diaria uso archivo CSV para la descarga, consulte [obtener las datos de uso de factura y diariamente la facturación de Azure](billing-download-azure-invoice-daily-usage-date.md). 

Para términos y descripciones detallados de su factura y el archivo de uso diario detallado, vea [Descripción de los términos en su factura de Microsoft Azure](billing-understand-your-invoice.md) y [Understand terms on your Microsoft Azure detailed usage](billing-understand-your-usage.md) (Descripción de los términos sobre el uso detallado de Microsoft Azure). 

Para obtener detalles sobre los informes de administración de costes de hello, consulte [portal de Azure la administración de costes](https://docs.microsoft.com/en-us/azure/billing/billing-getting-started).


## <a name="charges"></a>¿Cómo puedo asegurarme de que los cargos de hello en mi factura son correctos?
Si hay un cargo en la factura del que quiera tener más detalles, hay un par de opciones.

### <a name="option-1-review-your-invoice-and-compare-hello-usage-and-costs-with-hello-detailed-usage-csv-file"></a>Opción 1: Revisar la factura y comparar el uso de Hola y los costos con hello detallada archivo CSV de uso

Hello archivo CSV de uso detallada muestra los cargos por período de facturación y uso diario. consulte el archivo CSV, detallados de uso de tooget [obtener las datos de uso de factura y diariamente la facturación de Azure](https://docs.microsoft.com/en-us/azure/billing/billing-download-azure-invoice-daily-usage-date).

Los cargos por uso se muestran en el nivel de medidor Hola. Hello siguientes términos significan lo mismo en ambas factura Hola de Hola y Hola archivo detallados de uso. Por ejemplo, hello ciclo en factura Hola de facturación es período de facturación toohello equivalente que se muestra en el archivo de hello detallados de uso.

 | Factura (PDF) | Uso detallado (CSV)|
 | --- | --- |
|Ciclo de facturación | Período de facturación |
 |Nombre |Categoría de medidor |
 |Tipo |Subcategoría de medidor |
 |Recurso |Nombre de medidor |
 |Region |Medidor de la región |
 |Consumida |Cantidad consumida |
 |Se incluye |Cantidad incluida |
 |Facturable |Cantidad de superávit |

Hola **cargos por uso** sección de la factura tiene el valor total de Hola para cada contador que se ha utilizado durante el período de facturación. Por ejemplo, hello captura de pantalla siguiente muestra un cargo de uso para hello servicio Programador de Azure.

![Cargos de uso de la factura](./media/billing-understand-your-bill/1.png)

Hola **instrucción** sección de su uso detallada CSV muestra Hola mismo cargo. Ambos hello *consumido* cantidad y *valor* asociar Hola facturas.

![Cargos de uso del archivo CSV](./media/billing-understand-your-bill/2.png)

toosee un desglose de este cargo a diario, vaya toohello **uso diario** sección de hello CSV. Filtrar por "Programador" en *medidor de la categoría* y puede ver qué medidor de hello días se usó y cuánto consumido. Hola *recursos* y *grupo de recursos* también se incluye información para la comparación. Hola *consumido* valores deben sumar del toowhat se muestra en la factura de Hola.

![Sección uso diaria en hello CSV](./media/billing-understand-your-bill/3.png)

costo de hello tooget por día, multiplique hello *consumido* cantidades con hello *velocidad* valor de hello **instrucción** sección.

toolearn más información acerca de la factura de hello, consulte [entender la factura Azure](billing-understand-your-invoice.md).

toolearn sobre cada una de las columnas de Hola Hola CSV, consulte [entender el uso detallado Azure](billing-understand-your-invoice.md).

### <a name="option-2-review-your-invoice-and-compare-with-hello-usage-and-costs-in-hello-azure-portal"></a>Opción 2: Revise la factura y comparar con el uso de Hola y los costos en hello portal de Azure

Hola portal de Azure también puede ayudarle a comprobar los cargos. Hola portal de Azure proporciona gráficos de administración de costos para una introducción rápida de los cargos de hello y uso en su factura.

toocontinue con ejemplo de Hola desde arriba, visite hello [página suscripciones](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), seleccione la suscripción y, a continuación, elija **análisis de costos**. Desde allí, puede especificar el intervalo de tiempo de Hola y ver cargos de uso para el servicio de programador de Azure Hola.

![Vista de análisis de costos en Azure Portal](./media/billing-understand-your-bill/4.png)

Desglose toosee Hola de costo diario en **costo historial**, haga clic en la fila de Hola.

![Visualización del historial de costos en Azure Portal](./media/billing-understand-your-bill/5.png)

más información, consulte toolearn [evitar costos inesperados con la administración de costos y facturación de Azure](billing-getting-started.md#costs).

## <a name="external"></a>¿Qué son los cargos de servicios externos?
Los servicios externos (también conocidos como pedidos de Azure Marketplace) se proporcionan mediante proveedores de servicios independientes y se facturan por separado. los cargos de Hello no aparecen en la factura de Azure. más información, consulte toolearn [comprender los cargos de servicio externos Azure](billing-understand-your-azure-marketplace-charges.md).

## <a name="payment"></a>¿Cómo puedo realizar un pago?

Si configuras una tarjeta de crédito o una tarjeta de débito como su método de pago, pago Hola se cargará automáticamente en el plazo de 10 días una vez finalizado el período de facturación de Hola. En el extracto de la tarjeta de crédito, elemento de línea de hello diría **MSFT Azure**.

Si se [pagar por facturación](billing-how-to-pay-by-invoice.md), la ubicación de toohello de pago se enumeran en parte inferior de Hola de su factura de envío. Para obtener ayuda, [póngase en contacto con el equipo de soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="how-do-i-check-hello-status-of-a-payment-made-by-credit-card"></a>¿Cómo se puede comprobar el estado de Hola de pago realizado por la tarjeta de crédito?

[Crear una incidencia de soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooask estado de Hola de tu pago. 

## <a name="tips-for-cost-management"></a>Sugerencias de administración de costes
- Estimar los costos mediante el uso de hello [Calculadora de precios](https://azure.microsoft.com/pricing/calculator/) y [costo total de calculadora de propiedad](https://aka.ms/azure-tco-calculator)y obtener hello [obtener información sobre precios de cada servicio](https://azure.microsoft.com/en-us/pricing/).
- [Configure las alertas de facturación](billing-set-up-alerts.md).
- [Revise el uso y los costos con regularidad en hello portal de Azure](billing-getting-started.md#costs).

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Póngase en contacto con el servicio de soporte técnico.

Si aún necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema.

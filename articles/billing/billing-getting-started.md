---
title: "aaaPrevent inesperado de los costos, administrar facturación - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooavoid cargos inesperados en la factura de Azure. Use características de administración y seguimiento del costo de las suscripciones a Microsoft Azure."
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 482191ac-147e-4eb6-9655-c40c13846672
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: tonguyen
experimental_id: a2b2579c-cd2e-41
ms.openlocfilehash: 4827c65a55fe953c329ab26cc4e882266073c60a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prevent-unexpected-costs-with-azure-billing-and-cost-management"></a>Prevención de costes inesperados con la administración de costes y facturación de Azure

Al suscribirse a Azure, hay varias cosas que puede hacer tooget una idea más clara de los gastos. Hola [portal de Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), cuando se selecciona suscripción hello, puede ver el desglose de costo actual y tasa de evolución. También se puede [descargar facturas pasadas y archivos de uso detallados](billing-download-azure-invoice-daily-usage-date.md). Si desea que los costos de toogroup para recursos que usa para los equipos o proyectos diferentes, mire [recursos etiquetado](../azure-resource-manager/resource-group-using-tags.md). Si su organización tiene un sistema de informes que prefiere toouse, desproteger hello [API de facturación](billing-usage-rate-card-overview.md). 

Para más información sobre el uso diario, consulte [Comprender la factura de Microsoft Azure](billing-understand-your-bill.md).

Si la suscripción es a través de un contrato Enterprise (EA), proveedor de soluciones de nube (CSP) o patrocinio de Azure, a continuación, muchas características en este artículo no aplican tooyou. En su lugar, tiene a su disposición un conjunto diferente de herramientas que puede usar para administrar costes. Vea [Recursos adicionales para EA, CSP y Patrocinio](#other-offers).

Si la suscripción es una prueba gratuita, [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), Azure en abierto (AIO) o BizSpark, a continuación, obtenga información acerca de [los límites de gastos](#spending-limit) tooavoid con su suscripción unexpectantly deshabilitado. 

## <a name="day-0-before-you-add-azure-services"></a>Día 0: Antes de agregar servicios de Azure

### <a name="estimate-cost-online-using-hello-pricing-calculator"></a>Costo de la estimación en línea utilizando Calculadora de precios de Hola

Extraer del repositorio hello [Calculadora de precios](https://azure.microsoft.com/pricing/calculator/) y [costo total de calculadora de propiedad](https://aka.ms/azure-tco-calculator) tooget un costo mensual de Hola de estimación del servicio de Hola que le interesa. Por ejemplo, una máquina Virtual (VM) de A1 Windows es estimado toocost $66.96 USD/mes en proceso horas si deja Hola todo tiempo de ejecución:

![Captura de pantalla de la calculadora de precios de hello muestra que una VM de Windows A1 es estimado toocost 66.96 dólares al mes](./media/billing-getting-started/pricing-calcVM.png)

Para más información, consulte las [preguntas más frecuentes sobre precios](https://azure.microsoft.com/pricing/faq/). O bien, si desea que tootalk tooa persona, llame a 1-800-867-1389.

### <a name="check-your-subscription-and-access"></a>Comprobación de la suscripción y el acceso

Los costos de visualización requieren [información de acceso de nivel de suscripciones toobilling](billing-manage-access.md), pero Hola solo el Administrador de la cuenta puede tener acceso a hello [centro de cuentas de](https://account.windowsazure.com/Home/Index), cambiar información de facturación y administrar suscripciones. Hola, Administrador de cuenta es Hola quien se dirigió a través del proceso de registro de hello. Para obtener más información, consulte [agregar o cambiar roles de administrador de Azure que administran la suscripción de Hola o servicios](billing-add-change-azure-subscription-administrator.md).

toosee si está Hola Administrador de la cuenta, vaya toohello [hoja de suscripciones en el portal de Azure hello](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) y fíjese en la lista de Hola de suscripciones tienen acceso a. Busque en **Mi rol**. Si dice *Administrador de cuenta*, entonces, todo correcto. Si dice algo más como *Propietario*, entonces no tiene privilegios completos.

![Vista de suscripciones en la captura de pantalla de su rol en Hola Hola portal de Azure](./media/billing-getting-started/sub-blade-view.PNG)

Si no está Hola Administrador de la cuenta, alguien probablemente le dio acceso parcial a través de [basada en roles de Azure Active Directory Access Control](../active-directory/role-based-access-control-configure.md) (RBAC). toomanage suscripciones y facturación, información de [buscar Administrador de la cuenta de hello](billing-subscription-transfer.md#whoisaa) y pídale que las tareas de hello tooperform o [transferir Hola suscripción tooyou](billing-subscription-transfer.md).

Si el Administrador de la cuenta ya no está en su organización y necesita facturación toomanage, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). 

### <a name="spending-limit"></a> Comprobación para saber si tiene un límite de gasto activado

Si tiene una suscripción que usa créditos, a continuación, Hola límite de gasto está activado para, de forma predeterminada. De esta manera, cuando gasta todos sus créditos, no se le cobra en su tarjeta de crédito. Vea hello [lista completa de ofertas de Azure y la disponibilidad de Hola de límite de gasto](https://azure.microsoft.com/support/legal/offer-details/).

Sin embargo, si se alcanza el límite de gasto, se deshabilitarán sus servicios. Esto significa que se desasignarán sus máquinas virtuales. tiempo de inactividad de servicio tooavoid, debe desactivar Hola límite de gasto. Cualquier uso por encima del límite se cargará en su tarjeta de crédito guardada. 

toosee si se ha obtenido límite de gasto, vaya toohello [vista de suscripciones en el centro de cuentas de hello](https://account.windowsazure.com/Subscriptions). Aparecerá un mensaje emergente si su límite de gasto está activo:

![Captura de pantalla que muestra una advertencia sobre invierte más del límite que se está en hello centro de cuentas](./media/billing-getting-started/spending-limit-banner.PNG)

Haga clic en el banner de Hola y siga las indicaciones tooremove Hola límite de gasto. Si no escribe información de tarjeta de crédito cuando se suscribió, debe escribirla hello tooremove límite de gasto. Para obtener más información, consulte [Azure límite de gasto: cómo funciona y cómo tooenable o lo quite](https://azure.microsoft.com/pricing/spending-limits/).

### <a name="set-up-billing-alerts"></a>Configurar alertas de facturación para las suscripciones de Microsoft Azure

Configurar alertas de facturación tooget mensajes de correo electrónico cuando los costos de uso superan un importe especificado. Si dispone de créditos mensuales, configure alertas para cuando supere una cantidad específica. Para obtener más información, consulte [Configurar alertas de facturación para las suscripciones de Microsoft Azure](billing-set-up-alerts.md).

![Captura de pantalla de un correo electrónico de alerta de facturación](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> Esta característica está todavía en versión preliminar, por lo que debe comprobar periódicamente el uso.

Puede ser conveniente toouse Hola costo estimado de hello Calculadora de precios como guía para la primera alerta.

### <a name="understand-limits-and-quotas-for-your-subscription"></a>Descripción de los límites y cuotas de su suscripción

Hay límites predeterminados tooeach suscripción para elementos como el número de Hola de núcleos de CPU y direcciones IP. Esté atento a estos límites. Para más información, consulte [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md). Puede solicitar un aumento del límite de tooyour o una cuota por [ponerse en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="day-1-as-you-add-services"></a>Día 1: A medida que agrega servicios

### <a name="review-hello-estimated-cost-in-hello-portal"></a>Costo de hello estimado de revisión en el portal de Hola

Normalmente cuando se agrega un servicio en hello portal de Azure, hay una vista que muestra un costo estimado similar al mes. Por ejemplo, al elegir el tamaño de saludo de la máquina virtual de Windows verá Hola estimación de costo mensual para horas de proceso de hello:

![Ejemplo: una VM de Windows A1 es estimado toocost 66.96 dólares al mes](./media/billing-getting-started/vm-size-cost.PNG)

### <a name="tags"></a>Agregue etiquetas tooyour recursos toogroup sus datos de facturación

Puede usar datos de facturación de toogroup de etiquetas para los servicios compatibles. Por ejemplo, si ejecuta varias máquinas virtuales para los distintos equipos, puede usar etiquetas toocategorize costos por centro de costo (recursos humanos, marketing, Finanzas) o entorno (prueba de preproducción, producción,). 

![Captura de pantalla que muestra cómo configurar etiquetas en el portal de Hola](./media/billing-getting-started/tags.PNG)

Hola etiquetas se muestran a lo largo de costo diferentes vistas de informes. Por ejemplo, son visibles directamente en la [vista de análisis de costes](#costs) y en los archivos [.csv de uso detallados](#invoice-and-usage) después del primer período de facturación.

Para obtener más información, consulte [mediante etiquetas tooorganize los recursos de Azure](../azure-resource-manager/resource-group-using-tags.md).

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a>Habilitación de medidas de reducción de costes como el apagado automático de las máquinas virtuales

Según el escenario, puede configurar apagado automático para las máquinas virtuales en hello portal de Azure. Para más información, consulte [Auto-shutdown for VMs using Azure Resource Manager](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/) (Apagado automático de máquinas virtuales mediante Azure Resource Manager)///.

![Captura de pantalla de opción de cierre automático en el portal de Hola](./media/billing-getting-started/auto-shutdown.PNG)

Cierre automático no Hola igual que cuando cerró durante Hola VM con opciones de energía. Apagado automático se detiene y desasigna su toostop de máquinas virtuales en gastos de uso adicionales. Para más información, consulte las preguntas más frecuentes sobre precios de [máquinas virtuales Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) y [máquinas virtuales Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) y sobre los estados de máquinas virtuales.

Para conocer más medidas de reducción de costes de los entornos de desarrollo y pruebas, visite [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).

## <a name="cost-reporting"></a> Día 2+: Después de usar los servicios, vea el uso

### <a name="costs"></a>Visite el portal de hello para el análisis de costos con regularidad y tasa de evolución

Después de ejecutar los servicios, compruebe regularmente el coste de estos. Puede ver Hola actual invierte y tasa de evolución en el portal de Azure. 

1. Visite hello [hoja de suscripciones en el portal de Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).

2. Seleccione la suscripción que desee toosee. Solo tendrá una tooselect.

3. Debe ver desglose de costo de Hola y tasa de evolución en la hoja de la ventana emergente de Hola. No puede admitirse para su oferta (se mostrará una advertencia cerca de la parte superior de hello). Espere 24 horas después de agregar un servicio para hello toopopulate de datos.
    
    ![Captura de pantalla de tasa de avance y desglose en hello portal de Azure](./media/billing-getting-started/burn-rate.PNG)

4. Puede ser conveniente que el panel de tooyour de toopin Hola view.

    ![Captura de pantalla de anclar un panel de vista toohello](./media/billing-getting-started/pin.PNG)

5. Haga clic en **análisis de costos** en hello lista toohello toosee izquierdo Hola costo desglose por recurso.

    ![Captura de pantalla de vista de análisis de costos de hello en el portal de Azure](./media/billing-getting-started/cost-analysis.PNG)

6. Puede filtrar por diferentes propiedades como [etiquetas](#tags), grupo de recursos e intervalo de tiempo. Haga clic en **aplicar** tooconfirm filtros de Hola y **descargar** tooexport Hola ver tooa valores separados por comas (.csv) el archivo.

7. Haga clic en un recurso toosee dedicar el historial y la cantidad se le cuesta cada día.

    ![Captura de pantalla de hello dedican la vista de historial en el portal de Azure](./media/billing-getting-started/costhistory.PNG)

Le recomendamos que compruebe los costos de Hola que se ven con las estimaciones de Hola que vio cuando selecciona servicios de Hola. Si los costos de hello bastante difieren de las estimaciones, compruébela Hola precios plan (A1 vs VM A0, por ejemplo) que ha seleccionado para sus recursos. 

#### <a name="view-costs-for-all-your-subscriptions-in-hello-billing-blade"></a>Ver los costos de todas las suscripciones en la hoja de facturación de Hola

Si administra varias suscripciones como administrador de la cuenta de hello, puede ver desglose y cantidad de hello bill agregado para todas las suscripciones en hello [hoja facturación](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade). 

<!-- Add screenshots of multiple subs each with billed usage -->

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a>Active y compruebe las recomendaciones de Azure Advisor

[Azure Advisor](../advisor/advisor-overview.md) es una característica en versión preliminar que ayuda a reducir los costes, ya que identifica los recursos que se usan poco. Actívelo en hello portal de Azure:

![Captura de pantalla del botón de Azure Advisor en Azure Portal](./media/billing-getting-started/advisor-button.PNG)

A continuación, puede obtener recomendaciones útiles en hello **costo** ficha Panel de Asistente de hello:

![Captura de pantalla de ejemplo de recomendación de coste de Advisor](./media/billing-getting-started/advisor-action.PNG)

Para obtener más información, consulte las [recomendaciones sobre el costo de Advisor](../advisor/advisor-cost-recommendations.md).

### <a name="invoice-and-usage"></a> Obtención de la factura y de los archivos de detalles de uso después del primer período de facturación

Después del primer período de facturación, puede descargar la factura en formato Portable Document Format (.pdf) y los detalles de uso como archivos de valores separados por comas (.csv). También puede participar en toohave la factura por correo electrónico tooyou. Estos archivos de ayuda toounderstand ¿qué es facturación en última instancia tooyou después de impuestos, descuentos y créditos. Si no tiene una suscripción de pago método adjunta tooyour, estos archivos podrían no estar disponibles para usted. Para obtener más información, consulte [cómo tooget la facturación de Azure de factura y datos de uso diario](billing-download-azure-invoice-daily-usage-date.md) y [comprender la facturación de Microsoft Azure](billing-understand-your-bill.md).

![Captura de pantalla de una factura en formato .pdf](./media/billing-getting-started/invoice.png)

etiquetas de Hello establecidas anteriormente se muestran en los archivos .csv de hello detalle uso:

![Captura de pantalla que muestra las etiquetas de hello uso .csv](./media/billing-getting-started/csv.png)

### <a name="billing-api"></a>API de facturación

Utilice los datos de uso de get de facturación API tooprogrammatically. Mediante hello API RateCard y tooget conjuntamente de API de uso de hello el uso de facturación. Para más información, consulte [Obtención de información sobre el consumo de recursos de Microsoft Azure](billing-usage-rate-card-overview.md).

## <a name="other-offers"></a> Recursos adicionales para EA, CSP y Patrocinio

Hable Gestor de cuentas de tooyour o tooget de asociado de Azure iniciado.

| Oferta | Recursos |
|-------------------------------|-----------------------------------------------------------------------------------|
| Contrato Enterprise (EA) | [Portal EA](https://ea.azure.com/), [documentos de ayuda](https://ea.azure.com/helpdocs) e [informe de Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/) |
| Proveedor de soluciones en la nube (CSP) | Hable tooyour proveedor |
| Patrocinio de Azure | [Portal de patrocinio](https://www.microsoftazuresponsorships.com/) |

Si está administrando TI para una organización grande, es recomendable leer [scaffold Azure enterprise](../azure-resource-manager/resource-manager-subscription-governance.md) hello y [enterprise notas del producto IT](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (descarga de PDF, sólo en inglés).

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Ponerse en contacto con soporte técnico

Si necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema.

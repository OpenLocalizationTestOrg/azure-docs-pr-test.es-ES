---
title: aaaUnderstand los cargos de servicio externos Azure | Documentos de Microsoft
description: "Obtenga información sobre la facturación de los servicios externos, anteriormente conocidos como Marketplace, en Azure."
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1d2cb28319e2ab4eff753177220993cbf94c96ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a>Descripción de la facturación de Azure para gastos de servicios externos
Servicios externos utilizan toobe llamado Azure Marketplace. Por lo general, son servicios publicados por parte de terceros que están disponibles para Azure, pero están completamente integrados en Azure. Por ejemplo, ClearDB y SendGrid son servicios externos que puede adquirir en Azure, pero que no están publicados por Microsoft.

Cuando aprovisiona un nuevo servicio externo o un recurso, aparece una advertencia:

![Advertencia de compra de Marketplace](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> Los servicios externos los publican empresas distintas a Microsoft pero, a veces, los productos de Microsoft también se pueden clasificar como servicios externos.
> 
> 

## <a name="how-external-services-are-billed"></a>Cómo se facturan los servicios externos
- Los servicios externos se facturan por separado. Los servicios externos se tratan como pedidos individuales dentro de la suscripción de Azure. período de facturación de Hola para cada servicio se establece al adquirir un servicio de Hola. No toobe confundirse con el período de facturación de Hola de suscripción de hello en el que lo adquirió. Además, recibirá facturas independientes y se le cobrará en su tarjeta de crédito por separado.
- Cada servicio externo tiene un modelo de facturación diferente. Algunos servicios se facturan mediante la modalidad de pago por uso, mientras que otros utilizan un modelo basado en el pago mensual. Necesitará una tarjeta de crédito para los servicios externos de Azure ya que no se pueden comprar servicios externos mediante el pago de factura.
- No puede usar créditos mensuales gratuitos para los servicios externos. Si usa una suscripción de Azure que incluye [libre créditos](https://azure.microsoft.com/pricing/spending-limits/), no pueden ser facturas de servicio tooexternal aplicada. Usar una tarjeta de crédito toopurchase los servicios externos.


## <a name="view-external-service-spending-and-history-in-hello-azure-portal"></a>Gastos de servicio externo de vista y el historial en hello portal de Azure
Puede ver una lista de servicios externos de Hola que se encuentran en cada suscripción hello [portal de Azure](https://portal.azure.com/): 

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) como administrador de la cuenta de hello.
2. En el menú del concentrador hello, seleccione **suscripciones**.
   
    ![Seleccione las suscripciones en el menú del concentrador de Hola](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. Hola **suscripciones** hoja, suscripción de hello select que desee tooview y, a continuación, seleccione **servicios externos**.
   
    ![Seleccione una suscripción en la hoja facturación Hola](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. Debería ver cada uno de los pedidos de servicio externo, el nombre del publicador de hello, que compró el nivel de servicio, nombre que asignó recursos hello y estado actual de la orden de Hola. toosee más allá de las facturas, seleccione un servicio externo.
   
    ![Seleccionar un servicio externo](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. Desde aquí, puede ver más allá de los importes de factura incluidos desglose de impuestos Hola.
   
    ![Ver historial de facturación de los servicios externos](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a>Visualización de los gastos de los servicios externos para los clientes de Contrato Enterprise (EA)
Los clientes EA pueden ver gastos de servicio externo y descargar informes del portal EA Hola. Vea [Azure Marketplace para clientes EA](https://ea.azure.com/helpdocs/azureMarketplace) tooget iniciado.

## <a name="manage-payment-methods-for-external-service-orders"></a>Administración de los métodos de pago para pedidos de servicios externos
Actualizar los métodos de pago para los pedidos de servicio externo de hello [centro de cuentas de](https://account.windowsazure.com/).

> [!NOTE]
> Si adquirió la suscripción con una cuenta de empresa o centro educativo, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake cambia el método de pago tooyour.
> 
> 

1. Inicie sesión en toohello [centro de cuentas de](https://account.windowsazure.com/) y [navegue toohello **marketplace** ficha](https://account.windowsazure.com/Store)
   
    ![Seleccione marketplace en Centro de cuentas de Hola](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. Seleccione servicio externo de Hola que desee toomanage
   
    ![Seleccione servicio externo de Hola que desee toomanage](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. Haga clic en **Cambiar método de pago** en hello derecha de la página de Hola. Este vínculo abre tooa diferentes portal toomanage su método de pago.
   
    ![Resumen del pedido](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. Haga clic en **editar la información** y siga las instrucciones tooupdate su información de pago.
   
    ![Seleccione Editar información](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a>Cancelación de un pedido de servicio externo
Si desea toocancel su pedido de servicio externo, eliminar el recurso de Hola Hola [portal de Azure](https://portal.azure.com).

![Eliminar recurso](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Póngase en contacto con el servicio de soporte técnico.
Si sigue teniendo preguntas, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema.


---
title: "aaaDownload facturación factura y diaria uso datos de Azure | Documentos de Microsoft"
description: "Describe cómo toodownload o ver la facturación de Azure de factura y datos de uso diario."
keywords: "factura, facturación, descarga de factura, factura de Azure, uso de Azure"
services: 
documentationcenter: 
author: genlin
manager: tonguyen
editor: 
tags: billing
ms.assetid: 6d568d1d-3bd6-4348-97d0-1098b5fe0661
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2826df10f39914fcaeb9985271dadde550c68dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="download-or-view-your-azure-billing-invoice-and-daily-usage-data"></a>Procedimiento para descargar las datos de uso diario y de factura de Azure
Puede descargar la factura de hello [portal de Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) o hacer que se envíe por correo electrónico. toodownload su uso diario, vaya toohello [centro de cuentas de Azure](https://account.windowsazure.com). Solo determinados roles tienen tooget permiso factura y uso de datos, como Hola Administrador de la cuenta de facturación. vea toolearn más acerca de cómo obtener acceso a información de toobilling, [tooAzure de acceso de administrar roles de facturación](billing-manage-access.md).

## <a name="get-your-invoice-in-email-pdf"></a>Obtención de la factura por correo electrónico (.pdf)
Puede elegir y configurar tooreceive destinatarios adicionales factura de Azure en un correo electrónico. Esta característica puede no estar disponible para determinadas suscripciones, como ofertas de soporte técnico, contratos Enterprise o Azure bajo licencia Open.

1. Seleccione la suscripción de hello [hoja suscripciones](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade). Tendrá que habilitar la opción en cada suscripción que posea. Haga clic en **Facturas** y luego en **Email my invoice** (Enviar mi factura por correo electrónico). 

    ![Captura de pantalla que muestra hello participar en el flujo](./media/billing-download-azure-invoice-daily-usage-date/InvoicesDeepLink.PNG)
    
2. Haga clic en **participar en** y acepte los términos de Hola.

    ![Captura de pantalla que muestra hello participar en el flujo](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep2.PNG)
 
3. Una vez que ha aceptado el contrato de hello, puede configurar a los destinatarios adicionales.

    ![Captura de pantalla que muestra hello participar en el flujo](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep3.PNG)
    
Si no recibe un correo electrónico después de seguir los pasos de hello, asegúrese de que su dirección de correo electrónico sea correcta en hello [preferencias de comunicación en el perfil de](https://account.windowsazure.com/profile).

## <a name="download-invoice-from-azure-portal-pdf"></a>Descarga de la factura desde Azure Portal (.pdf)

1. Seleccione la suscripción de hello [hoja suscripciones](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) en el portal de Azure como [un usuario con acceso tooinvoices](billing-manage-access.md).

2. Seleccione **Facturas**. 

    ![Captura de pantalla que muestra la opción de facturación y uso de Hola](./media/billing-download-azure-invoice-daily-usage-date/billingandusage.png) 

3. Haga clic en **descargar factura** tooview una copia de la factura PDF. Si dice **no está disponible**, consulte [¿por qué no ve una factura para hello último período de facturación?](#noinvoice)

    ![Captura de pantalla que muestra los períodos de facturación, opción de descarga de Hola y cargos totales para cada período de facturación](./media/billing-download-azure-invoice-daily-usage-date/billing4.png)

4. También puede ver el uso diario haciendo clic en el período de facturación de Hola. 

Para más información sobre la factura, consulte [Comprender la factura de Microsoft Azure](billing-understand-your-bill.md). Para ayudar a administrar los costos, consulte [Prevención de costos inesperados con la administración de costos y facturación de Azure](billing-getting-started.md).

## <a name="download-usage-from-hello-account-center-csv"></a>Descargar el uso de hello centro de cuentas (.csv)

1. Inicio de sesión en hello [centro de cuentas de Azure](https://account.windowsazure.com/subscriptions) como Hola Administrador de la cuenta.

2. Seleccione la suscripción de hello para el que desea información de facturación y uso de Hola.

3. Seleccione **HISTORIAL DE FACTURACIÓN**. 

    ![Captura de pantalla que muestra la opción del historial de facturación](./media/billing-download-azure-invoice-daily-usage-date/Billinghisotry.png)

4. Puede ver las instrucciones para hello últimos seis períodos de facturación y Hola no facturado período actual. 

    ![Captura de pantalla que muestra los períodos de facturación, opciones toodownload factura y uso diario y total de cargos para cada período de facturación](./media/billing-download-azure-invoice-daily-usage-date/billingSum.png)

5. Seleccione **Ver extracto actual** toosee generó una estimación de los cargos de la estimación de hello tiempo Hola. Esta información solo se actualiza diariamente y es posible que no incluya todo el uso. La factura mensual puede ser distinta a esta estimación.

    ![Captura de pantalla que muestra la opción de ver extracto actual Hola](./media/billing-download-azure-invoice-daily-usage-date/billingSum2.png)

    ![Captura de pantalla que muestra la estimación de Hola de cargos actuales](./media/billing-download-azure-invoice-daily-usage-date/billingSum3.png)

6. Seleccione **descargar uso** datos toodownload Hola de uso diario como un archivo CSV. Si ve dos versiones disponibles, descargue la versión 2.

    ![Captura de pantalla que muestra la opción de descargar uso Hola](./media/billing-download-azure-invoice-daily-usage-date/DLusage.png)

Hola sólo administrador de la cuenta puede tener acceso a hello Azure Account Center. Otros administradores de facturación, por ejemplo, un propietario, pueden obtener información de uso con hello [API facturación](billing-usage-rate-card-overview.md).

Para más información sobre el uso diario, consulte [Comprender la factura de Microsoft Azure](billing-understand-your-bill.md). Para ayudar a administrar los costos, consulte [Prevención de costos inesperados con la administración de costos y facturación de Azure](billing-getting-started.md).

## <a name="noinvoice"></a>¿Por qué no ve una factura para hello último período de facturación?

Pueden existir varias razones por las que no ve una factura:

- Tiene un importe de crédito mensual con la suscripción que no ha superado o tiene una evaluación gratuita. Solo se genera una factura cuando debe dinero.

- Es menor que 30 días desde el día de hello que suscrito tooAzure.

- factura Hola aún no se genera. Espere hasta final de hello del período de facturación de Hola.

- Si no estás Hola Administrador de la cuenta, facturas anteriores pueden no ser tooyou disponible.

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Póngase en contacto con el servicio de soporte técnico.
Si tienes más preguntas, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema.


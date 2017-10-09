---
title: "aaaSet las alertas de crédito o de facturación para las suscripciones de Azure | Documentos de Microsoft"
description: "Describe cómo puede configurar alertas en su factura de Azure para que pueda evitar sorpresas de facturación."
keywords: "alerta de crédito, alerta de facturación"
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a>Configuración de alertas de crédito o facturación para las suscripciones de Microsoft Azure
Si le hello Administrador de cuenta para una suscripción de Azure, puede usar hello Azure facturación servicio de alertas de facturación toocreate personalizado las alertas que le ayudan a supervisar y administrar la actividad de facturación para las cuentas de Azure.

Este servicio está en vista previa, por lo que necesita tooenable, en la página de características de vista previa de hello en primer lugar.

## <a name="set-hello-alert-threshold-and-email-recipients"></a>Configurar destinatarios de umbral y el correo electrónico de alerta Hola
1. Visite [página de características de vista previa de hello](https://account.windowsazure.com/PreviewFeatures) y habilitar **servicio de alertas de facturación**.

1. Después de recibir la confirmación por correo electrónico de Hola que está activado el servicio de facturación de Hola para su suscripción, visite [página de suscripciones de hello](https://account.windowsazure.com/Subscriptions) en portal de cuentas de Hola. Haga clic en hello suscripción que desee toomonitor y, a continuación, haga clic en **alertas**.

    ![Captura de pantalla de vista de suscripciones de hello del centro de cuentas de Azure, con las alertas destacadas][Image1]

2. A continuación, haga clic en **Agregar alerta** toocreate primera vez. Puede establecer un total de cinco alertas de facturación por suscripción, con un umbral diferente e instalación tootwo destinatarios de correo electrónico para cada alerta.

    ![Vista de alertas de captura de pantalla de hello, donde puede agregar alerta][Image2]

3. Cuando se agrega una alerta, asígnele un nombre único, elija un umbral de gasto y elija Hola direcciones de correo electrónico donde se envían las alertas. Al configurar el umbral de hello, puede elegir un **Total de facturación** o un **un crédito monetario** de hello **alerta para** lista. Para obtener un total de facturación, se envía una alerta cuando el gasto de la suscripción supera el umbral de Hola. Para un crédito monetario, se envía una alerta cuando los créditos monetarios caen por debajo del límite de Hola. Créditos monetarios normalmente son aplicables a las suscripciones de prueba y Visual Studio tooFree.

    ![Captura de pantalla de la vista de alerta suma hello, donde puede configurar los destinatarios][Image3]

Azure admite cualquier dirección de correo electrónico pero no comprobar que la dirección de correo electrónico de hello funcione, así que revise si hay errores ortográficos.

## <a name="check-on-your-alerts"></a>Comprobación de las alertas
Después de configurar las alertas, Hola centro de cuentas enumera y muestra cuántas más puede configurar. Para cada alerta, verá Hola límite de fecha y hora de envío, si se trata de una alerta para el Total de facturación o un crédito monetario y Hola que configurar. formato de fecha y hora de Hello es 24 horas horario Universal coordinado (UTC) y fecha de hello es el formato aaaa-mm-dd. Haga clic en hello más firmarlo de una alerta en hello lista tooedit o haga clic en hello-Papelera toodelete lo.

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a>Alertas de facturación para los clientes del Contrato Enterprise (EA)
Los clientes EA pueden obtener alertas para cada departamento con una inscripción estableciendo cuotas de gastos. Vea [las cuotas de gastos de departamento](https://ea.azure.com/helpdocs/departmentSpendingQuotas) en hello EA portal tooget iniciado.

## <a name="learn-more-about-azure-cost-management"></a>Más información sobre la administración de costos de Azure
- Estimar los costos mediante hello [Calculadora de precios](https://azure.microsoft.com/pricing/calculator/), [costo total de calculadora de propiedad](https://aka.ms/azure-tco-calculator), y cuando se agrega un servicio.
- [Revise el uso y los costos con regularidad en Azure Portal](billing-getting-started.md#costs).
- Active las [recomendaciones sobre el costo de Azure Advisor](../advisor/advisor-cost-recommendations.md).

más información, consulte toolearn [instrucciones para la administración de Azure costo](billing-getting-started.md).

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 

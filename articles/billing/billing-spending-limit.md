---
title: limitar aaaUnderstand gastos de Azure | Documentos de Microsoft
description: "Describe cómo funciona de límite de gasto de Azure y cómo tooremove,"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: genli
ms.openlocfilehash: ed01401a07c3d0e7edebe42fb1482b7b60b1df51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-spending-limit-and-how-tooremove-it"></a>Comprender el límite de gasto de Azure y cómo tooremove,

El límite de gasto de Azure es un límite de cuánto puede gastar su suscripción de Azure. Todos los clientes nuevos que registran para la oferta de evaluación de Hola u ofertas que incluye créditos durante varios meses tienen Hola activado de forma predeterminada el límite de gasto. límite de gasto de Hello es $0. No se puede cambiar. Hola límite de gasto no está disponible para los tipos de suscripción como las suscripciones de pago por uso y planes de compromiso. Vea hello [lista completa de ofertas de Azure y la disponibilidad de Hola de límite de gasto de hello](https://azure.microsoft.com/support/legal/offer-details/).

## <a name="what-happens-when-i-reach-hello-spending-limit"></a>¿Qué ocurre cuando alcance el límite de gasto de hello?

Cuando el uso de da como resultado los cargos que agotar Hola cantidades mensuales incluidas en su oferta, servicios de Hola que ha implementado están deshabilitados para el resto de Hola de ese mes de facturación. Por ejemplo, los servicios Cloud Services que desarrolló se quitan de la producción y las máquinas virtuales de Azure se detienen y se desasignan. tooprevent los servicios de estar habilitada, puede elegir tooremove el límite de gasto. Cuando los servicios están deshabilitados, datos de hello en sus cuentas de almacenamiento y bases de datos están disponibles en modo de solo lectura para los administradores. Hola principio de hello siguiente mes de facturación, si su oferta incluye créditos durante varios meses, su suscripción, se vuelve a habilitar. A continuación, puede volver a implementar servicios en la nube y tener bases de datos y las cuentas de almacenamiento de tooyour de acceso completo.

Después de suscripción de prueba gratuita de hello alcanza el límite de gasto de hello, puede volver a habilitar la suscripción de Hola y para que automáticamente [oferta de pago por uso estándar de actualización tooour](billing-upgrade-azure-subscription.md) dentro de 90 días.

Recibir notificaciones cuando se alcanza el límite de gasto para su oferta de Hola. Inicie sesión en toohello [centro de cuentas de Azure](https://account.windowsazure.com), seleccione **cuenta**y, a continuación, seleccione **suscripciones**. Ver notificaciones acerca de las suscripciones que han alcanzado el límite de gasto de Hola.

## <a name="things-you-are-charged-for-even-if-you-have-a-spending-limit-enabled"></a>Cosas por las que se le cobra incluso si tiene un límite de gasto habilitado

Algunos servicios de Azure y [realizar compras en Marketplace](https://azure.microsoft.com/marketplace/) puede incurrir en cargos en forma de pago de hello (CC) incluso si se establece un límite de gasto. Algunos ejemplos son licencias de Visual studio, Azure Active Directory premium, planes de soporte técnico y la mayoría de otros fabricantes vendidos a través de hello Marketplace de servicios de la marca.


## <a name="when-not-toouse-hello-spending-limit"></a>Cuando no toouse Hola límite de gasto

límite de gasto de Hello podría impedir que implementar o con ciertas marketplace y los servicios de Microsoft. Presentamos escenarios de hello en el que debe quitar Hola límite de gasto en su suscripción.

- Planee toodeploy primeras imágenes de entidad como servicios, como Visual Studio Team Services y Oracle. Este escenario hace tooexceed los gastos limitar casi de inmediato y hace que su toobe de suscripción deshabilitada.

- Tiene servicios que no se pueden interrumpir.

- Tiene servicios y recursos con la configuración, como direcciones IP virtual que no desea toolose. Estos valores se pierden cuando se cancela la asignación de recursos y servicios de Hola.


## <a name="remove-hello-spending-limit"></a>Quitar límite de gasto de Hola

Puede quitar Hola invierte más del límite en cualquier momento mientras hay un método de pago válida asociado a su suscripción. Para las ofertas que tienen crédito durante varios meses, también puede volver a habilitar el límite de gasto en principio de Hola de su próximo ciclo de facturación de Hola.

los gastos limitar tooremove, siga estos pasos:

1. Inicie sesión en toohello [centro de cuentas de Azure](https://account.windowsazure.com).

2. Seleccione una suscripción.

3. Si se deshabilita la suscripción de Hola due toohello que se ha alcanzado el límite de gastos, haga clic en esta notificación: "La suscripción alcanzó el límite de gasto de Hola y ha sido deshabilitado tooprevent cargos." En caso contrario, haga clic en **quitar límite de gasto** en hello **estado de la suscripción** área.

4. Seleccione una opción que sea apropiada para usted.

|Opción|Efecto|
|-------|-----|
|Quitar el límite de gasto indefinidamente|Quita el límite de gasto sin activarlo automáticamente al principio de Hola de hello siguiente período de facturación de Hola.|
|Quitar límite de gasto para hello período de facturación actual|Quita el límite de gasto para que se active volver automáticamente al principio de Hola de hello siguiente período de facturación de Hola.|

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Póngase en contacto con el servicio de soporte técnico.
Si aún necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema.

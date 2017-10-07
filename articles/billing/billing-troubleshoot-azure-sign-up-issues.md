---
title: aaaTroubleshoot Azure problemas en el registro | Documentos de Microsoft
description: "Describe cómo tootroubleshoot algunos Azure comunes se suscriben problemas."
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: a0907da1-cb2d-41d1-a97f-43841fabe355
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee649bfc3be7ba1fe2dd863fac09e1c2311d835b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a>Solucionar problemas de inicio de suscripción para Azure
Si no puede suscribirse a Azure, use sugerencias de hello en este problemas comunes de tootroubleshoot los artículos. Si tiene algún problema con la tarjeta de crédito durante el inicio de sesión, vea [La tarjeta de débito o crédito se rechazó al suscribirse a Azure](billing-credit-card-fails-during-azure-sign-up.md). Si tiene una cuenta de Azure, pero no puede iniciar sesión, consulte [no se puede iniciar sesión en toomanage mi suscripción a Azure](billing-cannot-login-subscription.md).

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a>La barra de progreso se bloquea en la sección "Comprobación de identidad por tarjeta"

verificación de identidad de hello toocomplete con tarjeta, se deben permitir las cookies de terceros para su explorador.

![Captura de pantalla de hello verificación de identidad por la sección tarjeta queda bloqueada durante la suscripción a](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

Usar hello siguiendo los pasos tooupdate configuración de cookies de su explorador.

1. Si usas Chrome, vaya demasiado**configuración** > **Mostrar configuración avanzada** > **privacidad** > **contenido configuración de**. Desactive la opción **Bloquear los datos de sitios y las cookies de terceros**.
2. Si usas borde, vaya demasiado**configuración** > **ver la configuración avanzada** > **Cookies**. Seleccione **No bloquear cookies**.
3. Actualizar hello Azure página de inicio de sesión y comprobar si se ha resuelto el problema de Hola.
4. Si la actualización de hello no resuelve el problema de hello, salga y reinicie el explorador e inténtelo de nuevo.

## <a name="credit-card-form-doesnt-support-my-billing-address"></a>Incompatibilidad del formulario de tarjeta de crédito con la dirección de facturación
La dirección de facturación debe toobe en país Hola que seleccionó en hello **acerca de usted** sección. Asegúrese de que seleccionar país correcto Hola.

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a>No hay mensajes de texto o llamadas durante la comprobación de la cuenta de suscripción
Aunque es normalmente mucho más rápido, puede tardar minutos toofour toobe de código de comprobación de la entrega. número de teléfono de Hello que escriba para la comprobación no se guardan como un número de contacto para la cuenta de hello.

Estas son algunas sugerencias adicionales:
* No se puede usar un número de teléfono VOIP para el proceso de comprobación de teléfono de Hola.
* Número de teléfono de doble comprobación Hola escriba, incluido el código de país de Hola que seleccionó en el menú desplegable de Hola.
* Si el teléfono no recibe mensajes de texto (SMS), intente hello **Llamarme** opción.
* Asegúrese de que su teléfono puede recibir llamadas o mensajes SMS desde un número de Estados Unidos.

Cuando recibe mensajes de bienvenida del texto o llamada de teléfono, escriba el código que reciba en el cuadro de texto de Hola.

## <a name="credit-card-declined-or-not-accepted"></a>Tarjeta de crédito rechazada o no aceptada
Las tarjetas de crédito o débito virtuales o de prepago no se aceptan como opciones de pago para suscripciones de Azure. toosee ¿qué más puede provocar la toobe tarjeta rechazado, consulte [se rechaza la tarjeta de débito o tarjeta de crédito en Azure suscripción](billing-credit-card-fails-during-azure-sign-up.md).

## <a name="free-trial-is-not-available"></a>"La prueba gratuita no está disponible."
¿Ha utilizado una suscripción de Azure en hello anterior? Hola acuerdo de términos de uso de Azure limita la activación de prueba disponible solo para un usuario que sea tooAzure nueva. Si tiene cualquier otro tipo de suscripción de Azure, no puede activar una evaluación gratuita. Considere la posibilidad de suscribirse a una [suscripción de pago por uso](https://azure.microsoft.com/offers/ms-azr-0003p/).

## <a name="i-saw-a-charge-on-my-free-trial-account"></a>Hay un cargo reflejado en la cuenta de evaluación gratuita
Es posible que vea una pequeña comprobación se mantenga en su cuenta de tarjeta de crédito después de registrarse, que se quita en 3 días de too5. Si le preocupan los costos de administración, lea más información en la página sobre [prevención de costos inesperados](https://docs.microsoft.com/azure/billing/billing-getting-started).

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a>No se puede activar un plan de prestaciones de Azure como MSDN, BizSpark, BizSparkPlus o MPN
Asegúrese de que está usando el inicio de sesión correcto hello las credenciales. A continuación, compruebe Hola beneficio programa toomake seguro de que está elegibles. 

* MSDN
  * Compruebe su estado de elegibilidad en la [página de la cuenta de MSDN](https://msdn.microsoft.com/subscriptions/manage/default.aspx).
  * Si no se puede comprobar su estado, póngase en contacto con hello [centros de atención de cliente de las suscripciones de MSDN](https://msdn.microsoft.com/subscriptions/contactus.aspx)
* BizSpark
  * Inicie sesión en toohello [BizSpark portal](https://www.microsoft.com/bizspark/default.aspx#start-two) y comprobar su estado de elegibilidad para BizSpark y BizSpark Plus.
  * Si no se puede comprobar su estado, puede [obtener ayuda en los foros de hello BizSpark](http://aka.ms/bzforums).
* MPN
  * Inicie sesión en toohello [portal MPN](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) y verificar el estado de elegibilidad. Si tienes Hola adecuado [competencias de plataforma de nube](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx), puede ser elegible para ventajas adicionales.
  * Si no puede verificar el estado, póngase en contacto con el [soporte técnico de MPN](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx).

## <a name="cant-activate-new-azure-in-open-subscription"></a>No se puede activar una nueva suscripción de Azure bajo licencia Open
toocreate una suscripción de Azure en abierto, debe tener una clave de activación de servicio en línea (OSA) válida con al menos un tooit asociado de Azure en Abrir símbolo (token). Si no tiene una clave OSA, póngase en contacto con alguno de los asociados de Microsoft que aparecen en [Microsoft Pinpoint](http://pinpoint.microsoft.com/).

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Póngase en contacto con el servicio de soporte técnico.
Si aún necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema.

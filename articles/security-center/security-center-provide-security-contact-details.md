---
title: detalles de contacto de seguridad aaaProvide en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo seguridad tooprovide en contacto con los detalles en el centro de seguridad de Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 6c378c9c84c6e4fce70b2541e4cc121018700269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a>Proporcionar detalles de contacto de seguridad en Azure Security Center
Azure Security Center recomendará que proporcione los detalles de contacto de seguridad para su suscripción de Azure si no lo ha hecho ya. Toocontact Microsoft usará esta información si Hola Microsoft Security Response Center (MSRC) detecta que una entidad ilegal o no autorizada ha obtenido acceso a los datos de clientes. MSRC realiza una supervisión de infraestructura y de red de Azure Hola seleccione seguridad y recibe las quejas de inteligencia y controlar el abuso de amenaza de terceros.

Se envía una notificación de correo electrónico en hello primera diaria aparición de una alerta y solo las alertas de gravedad alta. Las preferencias de correo electrónico solo pueden configurarse para las directivas de suscripción. Los grupos de recursos de una suscripción heredan esta configuración.

> [!NOTE]
> Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.  No se trata de una guía paso a paso.
>
>

## <a name="implement-hello-recommendation"></a>Implementar la recomendación de Hola
1. Hola **recomendaciones** hoja, seleccione **proporcionar detalles de contacto de seguridad**.
   ![Proporcionar contacto de seguridad][1]
2. Esto abre una hoja de hello **proporcionar detalles de contacto de seguridad**. Seleccione esta opción información de contacto tooprovide Hola suscripción de Azure.
   ![Proporcionar datos de los contactos de seguridad][2]
3. Se abre una segunda hoja **Proporcionar datos de los contactos de seguridad** .

   * Escriba la dirección de correo electrónico de contacto de seguridad de Hola o direcciones separadas por comas. No es un toohello limitar el número de direcciones de correo electrónico que se pueden escribir.
   * Escriba un número de teléfono internacional de seguridad.
   * mensajes de correo electrónico tooreceive sobre alertas de gravedad alta, activar la opción hello **Enviarme correos electrónicos sobre alertas**.
   * Hola futura, tendrá propietarios de toosubscription de notificaciones de correo electrónico de hello opción toosend. De momento, esta opción aparece atenuada.
   * Seleccione **Aceptar** seguridad de hello tooapply póngase en contacto con suscripción de tooyour de información.

## <a name="see-also"></a>Otras referencias
toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.
* [Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
* [Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : obtener información y noticias de seguridad de Azure más recientes de Hola.

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png

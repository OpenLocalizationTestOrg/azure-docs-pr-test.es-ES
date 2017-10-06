---
title: "aaaThe elementos de correo electrónico de invitación de colaboración B2B de Azure Active Directory Hola | Documentos de Microsoft"
description: "Plantilla de correo electrónico de invitación de colaboración B2B de Azure Active Directory"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: f4908014d71a63442bbdca2182f54c7a79675a82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="hello-elements-of-hello-b2b-collaboration-invitation-email"></a>elementos de saludo de correo electrónico de invitación de colaboración B2B de hello

Mensajes de correo electrónico de invitación son un asociados de toobring de componente esencial a bordo como usuarios de colaboración B2B de Azure AD. Puede utilizarlos confianza del destinatario de tooincrease Hola. Puede agregar legitimidad y el correo electrónico de toohello prueba sociales, destinatario de hello seguro toomake se sienta cómodo con la selección Hola al **Introducción** botón invitación de hello tooaccept. Esta relación de confianza es que una clave significa tooreduce fricción de uso compartido. Y también desea toomake Hola correo electrónico aspecto excelente!

![Correo electrónico de invitación de B2B de Azure AD](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-hello-email"></a>Correo electrónico que se explican de Hola
Echemos un vistazo a unos cuantos elementos de correo electrónico de Hola para conocer la mejor manera de toouse sus capacidades.

### <a name="subject"></a>Asunto
asunto del mensaje de correo electrónico de Hola Hola sigue Hola siguiente patrón: le invito toohello &lt;nombreinquilino&gt; organización

### <a name="from-address"></a>Dirección De
Utilizamos un patrón similar LinkedIn para saludo de la dirección.  Se debe quedar claro que es el autor de la invitación hello y desde la que la empresa y también aclarar que correo electrónico Hola procede de una dirección de correo electrónico de Microsoft. formato de Hello es: &lt;nombre para mostrar del autor de la invitación&gt; de &lt;nombreinquilino&gt; (a través de Microsoft) <invites@microsoft.com&gt;

### <a name="reply-to"></a>Responder a
Hola respuesta-tooemail se establece correo electrónico cuando esté disponible, del toohello autor de la invitación poder responder a correo electrónico toohello envía una invitador toohello atrás de correo electrónico.

### <a name="branding"></a>Personalización de marca
invitación Hola correos electrónicos de su inquilino utilizar empresa Hola personalización de marca que puede configurar para su inquilino. Si desea que tootake aprovechar esta capacidad, [aquí](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) son Hola detalles acerca de cómo tooconfigure lo. logotipo del banner Hola aparece en el correo electrónico de Hola. Siga el tamaño de la imagen de Hola y las instrucciones de calidad [aquí](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) para obtener los mejores resultados. Además, nombre de la compañía de hello también se presenta en hello llamada tooaction.

### <a name="call-tooaction"></a>Llamar a tooaction
Hola llamada tooaction consta de dos partes: que explique por qué destinatario Hola ha recibido correo electrónico de Hola y qué destinatario Hola se pide toodo sobre él.
- Hola la sección "¿por qué" se puede cubrir con hello siguiente patrón: ha estado aplicaciones tooaccess invitados en hello &lt;nombreinquilino&gt; organización

- Hello sección "¿qué le piden toodo" se indica por la presencia de Hola de Hola y **Introducción** botón. Cuando se ha agregado el destinatario Hola sin necesidad de Hola de invitaciones, este botón no se muestre.

### <a name="inviters-information"></a>Información sobre el invitador
nombre para mostrar del invitador Hola se incluye en el mensaje de Hola. Y además, si ha configurado una imagen de perfil para la cuenta de Azure AD, Hola invitar a correo electrónico incluirá también esa imagen. Ambos es tooincrease previsto confiabilidad de la de los destinatarios de correo electrónico de Hola.

Si aún no ha configurado la imagen del perfil, se muestra un icono con iniciales del invitador hello en lugar de la imagen de hello:

  ![mostrar las iniciales del invitador Hola](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a>Cuerpo
cuerpo de Hello contiene mensajes de bienvenida que invitador Hola crea o se pasa a través de la invitación de hello API. Al ser un área de texto, por motivos de seguridad no se procesan las etiquetas HTML.

### <a name="footer-section"></a>Sección de pie de página
pie de página de Hello contiene la marca de empresa de Microsoft de Hola y permite destinatario Hola saber si el correo electrónico de hello fue enviada desde un alias no supervisado. Casos especiales:

- invitador Hello no tiene una dirección de correo electrónico en hello invitar a los inquilinos

  ![imagen del autor de la invitación no tiene una dirección de correo electrónico en hello invitar a los inquilinos](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- destinatario de Hello no necesita la invitación de hello tooredeem

  ![Cuando los destinatarios no necesitan tooredeem invitación](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a>Pasos siguientes

Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:

* [¿Qué es la colaboración B2B de Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?](active-directory-b2b-admin-add-users.md)
* [¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?](active-directory-b2b-iw-add-users.md)
* [Canje de invitación de colaboración B2B](active-directory-b2b-redemption-experience.md)
* [Concesión de licencias de colaboración B2B de Azure AD](active-directory-b2b-licensing.md)
* [Solución de problemas de colaboración B2B de Azure Active Directory](active-directory-b2b-troubleshooting.md)
* [Preguntas frecuentes sobre la colaboración B2B de Azure Active Directory (P+F)](active-directory-b2b-faq.md)
* [Personalización y API de colaboración B2B de Azure Active Directory](active-directory-b2b-api.md)
* [Autenticación multifactor para usuarios de colaboración B2B](active-directory-b2b-mfa-instructions.md)
* [Incorporación de usuarios de colaboración B2B sin invitación](active-directory-b2b-add-user-without-invite.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)

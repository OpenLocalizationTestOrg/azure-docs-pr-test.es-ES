---
title: "aaaHow Azure suscripciones están asociadas con Azure Active Directory | Documentos de Microsoft"
description: "Iniciar sesión en Azure tooMicrosoft y relacionados con problemas, como la relación de hello entre una suscripción de Azure y Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bc4773c2-bc4a-4d21-9264-2267065f0aea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4f831cfb972efec57083fcaa63adb43fde7b2faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a>Asociación de las suscripciones de Azure con Azure Active Directory
Este artículo contiene información acerca de la relación de hello entre una suscripción de Azure y Azure Active Directory (Azure AD) y cómo tooadd un directorio de Azure AD tooyour suscripción existente.

## <a name="your-azure-subscriptions-relationship-tooazure-ad"></a>TooAzure de relación de su suscripción a Azure AD
Su suscripción de Azure tiene una relación de confianza con Azure AD, lo que significa que confía en los dispositivos, servicios y usuarios de hello directory tooauthenticate. Varias suscripciones pueden confiar Hola mismo directorio, pero cada suscripción confía en un único directorio. 

relación de confianza de Hola que tiene una suscripción con un directorio es distinto de la relación de Hola que tiene con otros recursos de Azure (sitios Web, bases de datos y así sucesivamente). Si caduca una suscripción, tener acceso a toohello otros recursos asociados a la suscripción de hello también se detiene. Pero sigue siendo un directorio de Azure AD en Azure, y puede asociar otra suscripción a ese directorio y administrar el directorio Hola usando Hola nueva suscripción.

![Diagrama de asociación de suscripciones](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

Todos los usuarios tienen un único directorio de inicio que los autentica, pero también pueden ser invitados en otros directorios. En Azure AD, puede ver los directorios de Hola de que su cuenta de usuario es un miembro o invitado.

## <a name="azure-ad-and-cloud-service-subscriptions"></a>Azure AD y suscripciones de servicios en la nube
Azure AD proporciona identidad y directorio principal de hello capacidades de administración detrás de la mayoría de servicios de nube de Microsoft, incluidos:

* Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

Obtener Hola libre de servicio de Azure AD al suscribirse para cualquiera de estos servicios de nube de Microsoft. Si desea tooadd un directorio de suscripción de Azure adicionales tooan Azure AD, debe iniciar sesión con una cuenta de Microsoft. Si iniciar sesión en tooAzure con un trabajo o escuela cuenta, no se puede agregar un directorio existente de suscripción de Azure tooan porque no se puede autenticar su cuenta profesional o educativa directamente en Azure. 

## <a name="tooadd-an-existing-subscription-tooyour-azure-ad-directory"></a>tooadd un directorio de Azure AD tooyour suscripción existente
Debe iniciar sesión con una cuenta que existe en ambas directorio actual Hola con qué hello suscripción está asociada y en el directorio de hello desea tooadd a. 

1. Inicie sesión en toohello [centro de cuentas de Azure](https://account.windowsazure.com/Home/Index) con una cuenta que es Hola el Administrador de la cuenta de suscripción de hello cuya propiedad desea tootransfer.
2. Asegúrese de ese usuario Hola que quieran toobe propietario de la suscripción de Hola se encuentra en el directorio de Hola de destino.
3. Haga clic en **Transferir suscripción**.
4. Especifica al destinatario de Hola. destinatario de Hello recibe automáticamente un correo electrónico con un vínculo de aceptación.
5. destinatario de Hello hace clic en el vínculo de Hola y sigue las instrucciones de hello, incluidos introducir su información de pago. Cuando el destinatario de Hola se realiza correctamente, se transfiere suscripción Hola. 
6. se cambia el directorio predeterminado de Hola de suscripción de hello toohello el directorio tiene ese usuario Hola.


## <a name="suggestions-toomanage-both-a-subscription-and-a-directory"></a>Sugerencias toomanage ninguna suscripción y un directorio
roles administrativos de Hola para una suscripción de Azure administran recursos vinculados toohello suscripción de Azure. En esta sección se explica las diferencias de hello entre administradores de suscripción de Azure y directorio de Azure AD. Funciones administrativas y otras sugerencias para su uso toomanage su suscripción están cubiertos en [asignar roles de administrador en Azure Active Directory](active-directory-assign-admin-roles.md).

De forma predeterminada, se asignan roles de administrador de servicios de hello al registrarse. Si otros usuarios necesita toosign en y acceder a los servicios mediante Hola misma suscripción, puede agregarlas como coadministradores. 

Azure AD tiene un conjunto diferente de directorio de hello toomanage funciones administrativas y las características relacionadas con la identidad. Por ejemplo, administrador global de Hola de un directorio puede agregar usuarios y directorios de toohello de grupos o requerir una autenticación multifactor para los usuarios. Un usuario que crea un directorio se asigna el rol de administrador global de toohello y puede asignar roles administrativos tooother a los usuarios. Otros servicios, como Office 365 y Microsoft Intune, también usan los roles administrativos de Azure AD. 

Los administradores de suscripciones de Azure y los administradores de directorios de Azure AD son dos roles diferentes. 
* Los administradores de suscripciones de Azure pueden administrar recursos en Azure y pueden usar Azure AD en hello portal de Azure (porque Hola propio portal de Azure es un recurso de Azure). 
* Administradores de directorios pueden administrar las propiedades solo en el directorio de Azure AD Hola.

Una persona puede tener ambos roles, pero no es obligatorio. El administrador global de directorios puede no estar asignado como administrador de servicios o coadministrador de una suscripción de Azure, o viceversa. No es un administrador de suscripción de hello, usuario de Hola puede iniciar sesión en toohello portal de Azure, pero no puede administrar los directorios de Hola para esa suscripción en el portal de Hola. Sin embargo, este usuario puede administrar los directorios con otras herramientas como PowerShell de Azure AD o hello centro de administración de Office 365.

## <a name="next-steps"></a>Pasos siguientes
* toolearn Obtenga más información sobre cómo los administradores de toochange para una suscripción de Azure, consulte [transferir la propiedad de una cuenta de tooanother de suscripción de Azure](../billing/billing-subscription-transfer.md)
* toolearn más información acerca de cómo se controla el acceso a los recursos en Microsoft Azure, consulte [descripción de acceso a los recursos de Azure](active-directory-understanding-resource-access.md)
* Para obtener más información acerca de cómo las funciones de tooassign en Azure AD, consulte [asignar roles de administrador en Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG

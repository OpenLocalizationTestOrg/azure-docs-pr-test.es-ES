---
title: "aaaCompare B2B de colaboración y B2C en Azure Active Directory | Documentos de Microsoft"
description: "¿Cuál es la diferencia de hello entre la colaboración B2B de Azure Active Directory y Azure AD B2C?"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 34d88b9a7d023e077568e8df3d5e1610ae05b361
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="compare-b2b-collaboration-and-b2c-in-azure-active-directory"></a>Comparación de la colaboración B2B y B2C de Azure Active Directory

La colaboración B2B de Azure Active Directory (Azure AD) y Azure AD B2C le permiten toowork con usuarios externos en Azure AD. Pero, ¿cómo se comparan?


Funcionalidades de la colaboración B2B |     Oferta independiente de Azure AD B2C
-------- | --------
Destinado: las organizaciones que desean toobe tooauthenticate capaz de usuarios de una organización asociada, independientemente del proveedor de identidades. | Destinado a: invitar a los clientes de su móvil y aplicaciones web, ya sean personas, instituciones u organizaciones, en Azure AD.
Identidades compatibles: empleados con cuentas profesionales o educativas, asociados con cuentas profesionales o educativas o cualquier dirección de correo electrónico. Toosupport pronto federación directa.  | Identidades compatibles: usuarios consumidores con cuentas de aplicación local (cualquier dirección de correo electrónico o nombre de usuario) o cualquier identidad social compatible con federación directa.
Que son usuarios de directorio Hola asociados en: asociado a los usuarios de la organización externa Hola se administran en Hola el mismo directorio que los empleados, pero anotado especialmente. Se pueden administrar hello igual forma que los empleados, puede ser agregado toohello mismo grupos y así sucesivamente  | Que son entidades de usuario de cliente de directorio hello en: en el directorio de la aplicación hello. Administrados con independencia de hello empleados y socios directorio de la organización (si lo hay.
Single sign-on (SSO) tooall Azure se admite aplicaciones conectadas de AD. Por ejemplo, puede proporcionar acceso tooOffice 365 o aplicaciones locales y tooother aplicaciones de SaaS como Salesforce, Workday.  |  SSO toocustomer propiedad aplicaciones dentro de los inquilinos de Azure AD B2C hello es compatible. SSO tooOffice 365 o tooother aplicaciones de SaaS que no sean de Microsoft y Microsoft no es compatible.
Ciclo de vida de socio comercial: Hola host/invitar a organización administra.  | Ciclo de vida de cliente: administrada por la aplicación hello o de autoservicio.
Directiva de seguridad y cumplimiento de normas: Hola host/invitar a organización administra.  | Directiva de seguridad y cumplimiento de normas: administrados por la aplicación hello.
Personalización de marca: se utiliza la marca de la organización anfitriona o invitadora.  |    Personalización de marca: administrada por la aplicación. Por lo general suele producto toobe marca con atenuación de la organización de hello en segundo plano de Hola.
Más información: [entrada de blog](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [documentación](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)  | Más información: [página de producto](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [documentación](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)


### <a name="next-steps"></a>Pasos siguientes

Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:

* [¿Qué es la colaboración B2B de Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propiedades de usuario de la colaboración B2B](active-directory-b2b-user-properties.md)
* [Agregar un rol de tooa de usuario de la colaboración B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegación de las invitaciones de colaboración B2B](active-directory-b2b-delegate-invitations.md)
* [Grupos dinámicos y colaboración B2B](active-directory-b2b-dynamic-groups.md)
* [Configuración de aplicaciones de SaaS para la colaboración B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokens de usuario de colaboración B2B](active-directory-b2b-user-token.md)
* [Asignación de notificaciones de usuario de colaboración B2B](active-directory-b2b-claims-mapping.md)
* [Uso compartido externo de Office 365](active-directory-b2b-o365-external-user.md)
* [Limitaciones actuales de la colaboración B2B](active-directory-b2b-current-limitations.md)
* [Obtención de soporte técnico para colaboración B2B](active-directory-b2b-support.md)

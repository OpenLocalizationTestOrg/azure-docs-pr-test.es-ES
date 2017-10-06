---
title: "aaaSelf-service portal de suscripción para la colaboración B2B de Azure Active Directory | Documentos de Microsoft"
description: "Colaboración B2B de Active Directory de Azure es compatible con las relaciones entre empresas habilitando tooselectively los socios comerciales acceso aplicaciones corporativas"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a>Portal de autoservicio para el registro en la colaboración B2B de Azure AD

Los clientes pueden hacer muchas cosas con características integradas de Hola que se exponen a través de nuestro administrador de TI [portal de Azure](https://portal.azure.com) y nuestro [Panel de acceso de la aplicación](https://myapps.microsoft.com) para los usuarios finales. Pero también somos conscientes de que las empresas necesitan el flujo de trabajo de toocustomize Hola incorporación de B2B usuarios toofit las necesidades de su organización. Puede hacerlo con [nuestra API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).

En las conversaciones con nuestros clientes, se observa una necesidad común que sobresale por encima de todas las demás. Hola invitar a la organización no puede saber antelación que Hola colaboradores externos individuales son que necesita tener acceso a recursos de tootheir. Deseaban una manera para los usuarios de las empresas asociadas demasiado registran a sí mismos con un conjunto de directivas ese Hola invitar a los controles de la organización. Como este escenario es posible gracias a nuestras API, publicamos un proyecto en Github que lo lleva a cabo: [proyecto de ejemplo de Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).

Nuestro proyecto de Github muestra cómo pueden usar nuestras API organizaciones y proporcionar una funcionalidad de inicio de sesión basada en directivas, autoservicio para sus asociados de confianza, con las reglas que determinan Hola puede tener acceso a las aplicaciones. Los usuarios de socios comerciales pueden obtener acceso tooresources cuando los necesitan, de forma segura, sin necesidad de hello invitar a incorporar toomanually de organización ellos. Puede implementar fácilmente el proyecto de hello en una suscripción de Azure de su elección.

## <a name="as-is-code"></a>Código “tal cual”

Recuerde que este código debe ponerse a disposición como un ejemplo de uso de toodemonstrate de invitación de hello Azure Active Directory B2B API. Su equipo de desarrollo o el asociado deben realizar la personalización y revisión antes de implementarlo en un escenario de producción.

## <a name="next-steps"></a>Pasos siguientes

Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:
* [¿Qué es la colaboración B2B de Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?](active-directory-b2b-admin-add-users.md)
* [¿Cómo agregan los trabajadores de la información usuarios de colaboración B2B?](active-directory-b2b-iw-add-users.md)
* [elementos de saludo de correo electrónico de invitación de colaboración B2B de hello](active-directory-b2b-invitation-email.md)
* [Canje de invitación de colaboración B2B](active-directory-b2b-redemption-experience.md)
* [Concesión de licencias de colaboración B2B de Azure AD](active-directory-b2b-licensing.md)
* [Solución de problemas de colaboración B2B de Azure Active Directory](active-directory-b2b-troubleshooting.md)
* [Preguntas frecuentes sobre la colaboración B2B de Azure Active Directory (P+F)](active-directory-b2b-faq.md)
* [Autenticación multifactor para usuarios de colaboración B2B](active-directory-b2b-mfa-instructions.md)
* [Incorporación de usuarios de colaboración B2B sin invitación](active-directory-b2b-add-user-without-invite.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
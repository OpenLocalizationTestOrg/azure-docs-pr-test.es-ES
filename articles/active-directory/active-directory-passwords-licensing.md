---
title: 'Licensing: Azure AD SSPR (Licencias: SSPR de Azure AD) | Microsoft Docs'
description: "Requisitos de concesión de licencias del autoservicio de restablecimiento de contraseña de Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a>Licensing requirements for Azure AD self-service password reset (Requisitos de concesión de licencias del autoservicio de restablecimiento de contraseña de Azure AD)

En orden de restablecimiento de contraseña de Azure AD toofunction, le **debe tener al menos una licencia asignada en su organización**. No se aplican licencias en la experiencia de restablecimiento de contraseña de Hola por usuario. toomaintain el cumplimiento con el contrato de licencia de Microsoft, necesita que tooassign licencias tooany usuarios que usen las características premium.

* **Solo usuarios en la nube**: Office 365 (O365), cualquier SKU de pago o Azure AD Basic
* **Usuarios en la nube** o **locales**: Azure AD Premium P1 o P2, Mobility + Security (EMS) o Secure Productive Enterprise (SPE)

## <a name="licenses-required-for-password-writeback"></a>Licencias necesarias para la escritura diferida de contraseñas

escritura diferida de contraseñas toouse, debe tener uno de hello después licencias asignadas en el inquilino.

* Azure AD Premium P1
* Azure AD Premium P2
* Enterprise Mobility + Security E3
* Enterprise Mobility + Security E5
* Secure Productive Enterprise E3
* Secure Productive Enterprise E5

> [!NOTE]
> Planes de licencias por independiente Office 365 **no admiten la escritura diferida de contraseñas** y necesitan una de hello anterior planes para este toowork de funcionalidad.

Información de licencia adicional incluidos los costos puede encontrarse en hello después de páginas

* [Sitio sobre precios de Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a>Habilitar licencias basadas en grupos o usuarios

Ahora, Azure AD admite basado en el grupo licencias permitiendo administradores tooassign licencias en grupo de tooa de forma masiva de usuarios en lugar de asignar uno a la vez. [Asignar, comprobar y resolver los problemas con licencias](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

Algunos servicios de Microsoft no están disponibles en todas las ubicaciones. Antes de poder asignar una licencia de usuario de tooa, Administrador de hello debe especificar la propiedad de "Ubicación de uso" de hello en usuario Hola. Es posible la asignación de licencias de usuario > perfil > sección de configuración en hello portal de Azure. **Cuando se utiliza la asignación de licencias del grupo, los usuarios sin especificar una ubicación de uso heredan ubicación hello del directorio de Hola.**

## <a name="next-steps"></a>Pasos siguientes

Hola siguientes vínculos proporciona más información sobre el uso de Azure AD de restablecimiento de contraseña

* [**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD 
* [**Datos** ](active-directory-passwords-data.md) : comprender los datos de Hola que es necesarios y cómo se utiliza para la administración de contraseñas
* [**Implementación** ](active-directory-passwords-best-practices.md) -planear e implementar a los usuarios de Autoservicio tooyour usando la orientación de hello encontrar aquí
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Hola apariencia y funcionamiento del programa Hola a la experiencia de Autoservicio de su empresa.
* [**Informes**](active-directory-passwords-reporting.md): detectan si los usuarios acceden a la funcionalidad de SSPR, cuándo lo hacen y dónde.
* [**Profundización técnica** ](active-directory-passwords-how-it-works.md) -ir detrás de hello cortina toounderstand cómo funciona
* [**Preguntas más frecuentes**](active-directory-passwords-faq.md): ¿Cómo? ¿Por qué? ¿Qué? ¿Dónde? ¿Quién? ¿Cuándo? -Responde tooquestions siempre deseara tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Obtenga información acerca de cómo problemas comunes de tooresolve que vemos con SSPR


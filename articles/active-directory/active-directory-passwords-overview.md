---
title: "información general de restablecimiento de contraseña de autoservicio de aaaAzure AD | Documentos de Microsoft"
description: "¿Para qué puede servir el autoservicio de restablecimiento de contraseña de Azure AD en una organización?"
services: active-directory
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
ms.openlocfilehash: 0efc291b1eeec0b7ae33ff5a7d9ed38e70c8be6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-self-service-password-reset-for-hello-it-professional"></a>Restablecimiento de contraseña de autoservicio de Azure AD para hello profesional de TI

"Autoservicio" es una palabra de moda producida alrededor dentro de muchos de los departamentos de TI a través de hello world con distintos significados. mercado Hola se congestiona con productos que le permiten grupos locales de toomanage, contraseñas o perfiles de usuario de nube de Hola o de forma local.

El autoservicio de restablecimiento de contraseña (SSPR) de Azure Active Directory (Azure AD) se diferencia de otros servicios por la facilidad de uso e implementación. El autoservicio de restablecimiento de contraseña de Azure AD combina un conjunto de funcionalidades que:

* Permitir la toomanage a los usuarios su contraseña
  * Desde cualquier dispositivo
  * En cualquier ubicación
  * En cualquier momento
* Mantienen el cumplimiento con directivas que defina como administrador

Si está listo, puede comenzar a utilizar SSPR de Azure AD con la [guía de inicio rápido](active-directory-passwords-getting-started.md) y permitir que los usuarios restablezcan las contraseñas con rapidez.

## <a name="what-is-possible"></a>Lo que es posible

* **Cambio de contraseña de autoservicio** permite a los usuarios finales o los administradores toochange sus contraseñas sin ayuda del administrador
* **Desbloqueo de cuentas de autoservicio** permite toounlock de los usuarios finales de su propia cuenta sin ayuda del administrador
* **Restablecimiento de contraseña de autoservicio** permite a los usuarios finales o los administradores tooreset sus contraseñas automáticamente sin ayuda del administrador. El Autoservicio de restablecimiento de contraseña requiere Azure AD Premium o Básico; véase [Ediciones de Azure Active Directory](active-directory-editions.md).
* **Restablecer la contraseña de administrador inició** permite que un administrador tooreset contraseña de un usuario final o de otro administrador de hello [portal de Azure](https://docs.microsoft.com/azure/azure-portal-overview)
* Los **informes de actividad de administración de contraseñas** proporcionan a los administradores perspectivas sobre una actividad de registro y restablecimiento de contraseña en su organización; véase [informes de administración](active-directory-passwords-reporting.md).
* **Escritura diferida de contraseñas** permite la administración de contraseñas locales desde la nube de Hola para federado precedente de hello todos los escenarios pueden realizarse por, o en nombre de hello, o los usuarios sincronizados con contraseña. La escritura diferida de contraseñas requiere [Azure AD Premium](active-directory-get-started-premium.md).

## <a name="why-choose-azure-ad-self-service-password-reset"></a>Por qué elegir el autoservicio de restablecimiento de contraseñas de Azure AD

* **Reducir los costos**: el restablecimiento de contraseñas con asistencia de un servicio y departamento de soporte técnico normalmente supone el 20 % del gasto en TI de una organización.
* **Mejorar la experiencia del usuario final** y **reducir el volumen del departamento de soporte técnico** proporcionando final usuarios Hola power tooresolve sus propios problemas de contraseña a la vez sin llamar a un departamento de soporte técnico o abrir una solicitud de soporte técnico.
* **Impulsar la movilidad**: los usuarios pueden restablecer sus contraseñas desde cualquier lugar en que se encuentren.

## <a name="azure-ad-self-service-password-reset-availability"></a>Disponibilidad de autoservicio de restablecimiento de contraseña de Azure AD

El autoservicio de restablecimiento de contraseña de Azure AD está disponible en tres niveles, en función de la suscripción de que se trate.

* **Azure AD Gratis**: los administradores que están solo en la nube pueden restablecer sus propias contraseñas.
* **Azure AD Básico** o cualquier **suscripción de pago de Office 365**: los usuarios y administradores que están solo en la nube pueden restablecer sus propias contraseñas.
* **Azure AD Premium**: cualquier usuario o administrador, incluidos los que están solo en la nube, los federados o los usuarios sincronizados con contraseña, pueden restablecer sus propias contraseñas. Contraseñas locales requieren toobe de reescritura de contraseña habilitada.

## <a name="azure-ad-self-service-password-reset-a-sum-of-hello-parts"></a>Restablecimiento de contraseña de autoservicio de Azure AD, una suma de las partes de Hola

Contraseña de autoservicio de restablecimiento en Azure AD se compone de Hola de los componentes siguientes:

* **Portal de configuración de administración de contraseñas** donde puede controlar opciones para la administración de contraseñas en el inquilino a través de hello portal de Azure
* **Portal de registro de restablecimiento de contraseñas**: aquí los usuarios pueden registrarse automáticamente para el restablecimiento de contraseñas.
* **Portal de restablecimiento de contraseña** ha proporcionado donde los usuarios pueden restablecer su contraseña con desafíos de hello definidos por el Administrador de Hola y Hola responde a los usuarios
* **Portal de cambio de contraseñas de usuario**: aquí los usuarios pueden cambiar sus propias contraseñas si escriben su contraseña anterior y proporcionan una contraseña nueva.
* **Informes de administración de contraseñas** informa de que los administradores pueden ver y analizar la actividad de la contraseña de sus inquilinos Hola portal de Azure
* **Contraseña reescritura tooon locales mediante Azure AD Connect** permite la administración del tooenable, de, federado local, o los usuarios de la nube de hello sincronizados con contraseña

## <a name="azure-ad-pricing-sla-updates-and-roadmap"></a>Precios, SLA, actualizaciones y hoja de ruta de Azure AD

Más detalles acerca de estos temas pueden encontrarse en hello después de páginas

* [**Detalles de precios de Azure AD**](https://azure.microsoft.com/pricing/details/active-directory/)
* [**Precios de Office 365**](https://products.office.com/compare-all-microsoft-office-products?tab=2)
* [**Acuerdos de Nivel de Servicio**](https://azure.microsoft.com/support/legal/sla/)
* [**Acuerdo de Nivel de Servicio de Microsoft Online Services**](http://go.microsoft.com/fwlink/?LinkID=272026&clcid=0x409)
* [**Actualizaciones de Azure**](https://azure.microsoft.com/updates/)
* [**Hoja de ruta de Azure**](https://www.microsoft.com/cloud-platform/roadmap-recently-available)

## <a name="next-steps"></a>Pasos siguientes

Hola siguientes vínculos proporciona más información sobre el uso de Azure AD de restablecimiento de contraseña

* [**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD 
* [**Licencias**](active-directory-passwords-licensing.md): configuración de licencias de Azure AD
* [**Datos** ](active-directory-passwords-data.md) : comprender los datos de Hola que es necesarios y cómo se utiliza para la administración de contraseñas
* [**Implementación** ](active-directory-passwords-best-practices.md) -planear e implementar a los usuarios de Autoservicio tooyour usando la orientación de hello encontrar aquí
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Hola apariencia y funcionamiento del programa Hola a la experiencia de Autoservicio de su empresa.
* [**Informes**](active-directory-passwords-reporting.md): detectan si los usuarios acceden a la funcionalidad de SSPR, cuándo lo hacen y dónde.
* [**Profundización técnica** ](active-directory-passwords-how-it-works.md) -ir detrás de hello cortina toounderstand cómo funciona
* [**Preguntas más frecuentes**](active-directory-passwords-faq.md): ¿Cómo? ¿Por qué? ¿Qué? ¿Dónde? ¿Quién? ¿Cuándo? -Responde tooquestions siempre deseara tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Obtenga información acerca de cómo problemas comunes de tooresolve que vemos con SSPR


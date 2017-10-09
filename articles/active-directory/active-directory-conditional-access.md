---
title: "acceso aaaConditional Hola portal de Azure clásico | Documentos de Microsoft"
description: "Usar el control de acceso condicional en hello Azure toocheck portal clásico para condiciones específicas al autenticar para tooapplications de acceso."
services: active-directory
keywords: tooapps de acceso condicional, el acceso condicional con Azure AD, proteger el acceso toocompany recursos, las directivas de acceso condicional
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: da3f0a44-1399-4e0b-aefb-03a826ae4ead
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.custom: oldportal
ms.openlocfilehash: 049bd3f6ec9e35479319ee7608b007b9a1e16647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-hello-azure-classic-portal"></a>Acceso condicional en hello portal de Azure clásico

Este tema trata sobre el acceso condicional en hello portal de Azure clásico. Para información más reciente de hello sobre el acceso condicional en hello Azure Active Directory, consulte [acceso condicional en Azure Active Directory](active-directory-conditional-access-azure-portal.md).


capacidades de Hola de control de acceso condicional de Azure Active Directory (Azure AD) ofrecen varias maneras sencillas toohelp recursos seguros en la nube de Hola y local. Directivas de acceso condicional, como la autenticación multifactor puede ayudar a proteger contra Hola riesgos de robo y phished credenciales. Otras directivas de acceso condicional pueden ayudar a mantener seguros los datos de su organización. Por ejemplo, además toorequiring credenciales, puede que tenga una directiva que solo los dispositivos que están inscritos en un sistema de administración de dispositivos móviles como Microsoft Intune puede tener acceso a servicios confidenciales de su organización.

## <a name="prerequisites"></a>Requisitos previos
El acceso condicional de Azure AD es una característica de [Azure Active Directory Premium](http://www.microsoft.com/identity). Cada usuario que acceda a una aplicación a la que se hayan aplicado directivas de acceso condicional debe tener una licencia de Azure AD Premium. Puede obtener más información sobre los requisitos de licencia en [Informe de uso sin licencia](https://aka.ms/utc5ix).

## <a name="how-is-conditional-access-control-enforced"></a>¿Cómo se aplica el control de acceso condicional?
Con control de acceso condicional en su lugar, Azure AD comprueba las condiciones específicas de hello establecido para un usuario tooaccess una aplicación. Después de que se cumplen los requisitos de acceso, el usuario de hello está autenticado y puede tener acceso a la aplicación hello.  

![Introducción al acceso condicional](./media/active-directory-conditional-access/conditionalaccess-overview.png)

## <a name="conditions"></a>Condiciones
Puede incluir las siguientes condiciones en una directiva de acceso condicional:

* **Pertenencia a grupos**. Controle el acceso de un usuario en función de su pertenencia a un grupo.
* **Ubicación**. Utilice la ubicación de Hola Hola tootrigger varios factores de autenticación de usuarios y controles de bloque de cuando un usuario no está en una red de confianza.
* **Plataforma de dispositivo**. Utilice plataforma de dispositivo de hello, como iOS, Android, Windows Mobile o Windows, como una condición para aplicar la directiva.
* **Dispositivo habilitado**. El estado del dispositivo, habilitado o deshabilitado, se valida durante la evaluación de la directiva de dispositivo. Si deshabilita un dispositivo perdido o robado en directorio de hello, ya no pueda satisfacer los requisitos de directiva.
* **Inicio de sesión y riesgo de usuario**. Puede usar [Azure AD Identity Protection](active-directory-identityprotection.md) para directivas de riesgo de acceso condicional. Las directivas de riesgo de acceso condicional proporcionan a su organización una protección anticipada en función de eventos de riesgo y actividades de inicio de sesión no habituales.

## <a name="controls"></a>Controles
Se trata de controles que puede usar tooenforce una directiva de acceso condicional:

* **Autenticación multifactor**. Puede requerir una autenticación sólida por medio de la autenticación multifactor. Puede usar la autenticación multifactor con Azure Multi-Factor Authentication o mediante un proveedor de autenticación multifactor local, en combinación con Servicios de federación de Active Directory (AD FS). Utilizar la autenticación multifactor le ayuda a proteger los recursos de que se obtiene acceso por un usuario no autorizado que podría haber obtenido acceso toohello credenciales de un usuario válido.
* **Bloqueo**. Se pueden aplicar condiciones como acceso de usuario de tooblock de ubicación de usuario. Por ejemplo, puede bloquear el acceso cuando el usuario no esté en una red de confianza.
* **Dispositivos compatibles**. Puede establecer directivas de acceso condicional en el nivel de dispositivo de Hola. Podría configurar una directiva para que solo puedan acceder a los recursos de su organización aquellos equipos que estén unidos a un dominio o aquellos dispositivos móviles que estén inscritos en una aplicación de administración de dispositivos móviles. Por ejemplo, puede usar Intune toocheck el cumplimiento de dispositivos y, a continuación, notificarlo tooAzure AD para la aplicación cuando el usuario de hello intenta tooaccess una aplicación. Para obtener instrucciones detalladas sobre cómo toouse Intune tooprotect aplicaciones y datos, vea [proteger aplicaciones y datos con Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/protect-apps-and-data-with-microsoft-intune). También puede usar la protección de datos de tooenforce de Intune para dispositivos perdidos o robados. Para obtener más información, consulte [Ayudar a proteger los datos con el borrado selectivo o completo mediante Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

## <a name="applications"></a>Aplicaciones
Puede aplicar una directiva de acceso condicional en el nivel de aplicación Hola. Establecer niveles de acceso para aplicaciones y servicios en la nube de Hola o de forma local. Directiva de Hello es aplicar directamente toohello sitio Web o servicio. se aplica la directiva de Hola para acceso toohello explorador e tooapplications que tienen acceso a servicio de Hola.

## <a name="device-based-conditional-access"></a>Acceso condicional basado en dispositivos
Puede restringir el acceso tooapplications desde dispositivos que están registrados con Azure AD, y que cumplen determinadas condiciones. Acceso condicional basado en dispositivo protege los recursos de una organización de los usuarios que intentan recursos de hello tooaccess desde:

* Dispositivos desconocidos o no administrados.
* Dispositivos que no cumplen las directivas de seguridad de hello su organización ha implantado.

Puede establecer directivas basadas en estos requisitos:

* **Dispositivos unidos a un dominio**. Establecer un toodevices de acceso de toorestrict directiva que son tooan Unidos a un dominio de Active Directory de local y que están registrados con Azure AD. Esta directiva aplica tooWindows escritorios, equipos portátiles y tabletas de empresa.
  Para obtener más información acerca de cómo tooset el registro automático de dispositivos Unidos a un dominio con Azure AD, consulte [configurar el registro automático de dispositivos Unidos a un dominio de Windows con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).
* **Dispositivos compatibles**. Establecer un toodevices de acceso de toorestrict de directiva que se marcan **conforme** en el directorio del sistema de administración de Hola. Esta directiva garantiza que solo se permite el acceso a los dispositivos que cumplen las directivas de seguridad, como exigir el cifrado de archivos en un dispositivo. Puede usar esta directiva de acceso de toorestrict de hello siguientes dispositivos:
  
  * **Dispositivos unidos a un dominio de Windows**. Administrado por System Center Configuration Manager (en la rama actual de hello) implementados en una configuración híbrida.
  * **Dispositivos Windows 10 Mobile para uso personal o profesional**. Administrados con Intune o un sistema de administración de dispositivos móviles de terceros compatible.
  * **Dispositivos iOS y Android**. Administrados con Intune.

Los usuarios que tengan acceso a aplicaciones que están protegidas por basado en un dispositivo, directiva de entidad de certificación debe tener acceso a aplicación hello desde un dispositivo que cumpla los requisitos de la directiva. Se deniega el acceso si intentan acceder en un dispositivo que no cumpla los requisitos de la directiva.

Para obtener información acerca de cómo tooconfigure un dispositivo basada en directiva de entidad de certificación en Azure AD, consulte [establecer una directiva de acceso condicional basado en el dispositivo para aplicaciones conectadas con Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).

## <a name="resources"></a>Recursos
Vea Hola después toolearn de categorías y los artículos de recursos más sobre la configuración de acceso condicional para su organización.

### <a name="multi-factor-authentication-and-location-policies"></a>Directivas de ubicación y autenticación multifactor
* [Introducción a acceso condicional tooAzure conectado AD aplicaciones basadas en grupo, la ubicación y las directivas de autenticación multifactor](active-directory-conditional-access-azuread-connected-apps.md)
* [Aplicaciones y navegadores compatibles](active-directory-conditional-access-supported-apps.md)

### <a name="device-based-conditional-access"></a>Acceso condicional basado en dispositivos
* [Establecer una directiva de acceso condicional basado en el dispositivo para el acceso a aplicaciones de control tooAzure conectado a Active Directory](active-directory-conditional-access-policy-connected-applications.md)
* [Configuración del registro automático de dispositivos unidos a un dominio de Windows con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)
* [Solución de problemas de acceso de Azure Active Directory](active-directory-conditional-access-device-remediation.md)
* [Ayudar a proteger los datos con el borrado selectivo o completo mediante Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)

### <a name="protect-resources-based-on-sign-in-risk"></a>Protección de recursos basada en el riesgo de inicio de sesión
* [Azure AD Identity Protection](active-directory-identityprotection.md)

### <a name="next-steps"></a>Pasos siguientes
* [Preguntas más frecuentes acerca del acceso condicional](active-directory-conditional-faqs.md)
* [Referencia técnica](active-directory-conditional-access-technical-reference.md)


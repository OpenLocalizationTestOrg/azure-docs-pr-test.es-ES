---
title: "aaaFundamentals de administración de identidades de Azure | Documentos de Microsoft"
description: 
keywords: 
author: jeffgilb
manager: femila
ms.reviewr: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: a9710b8e543cdbb2f78ea9e3f83b183e1983b31d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="fundamentals-of-azure-identity-management"></a>Aspectos básicos de la administración de identidades de Azure
Cada vez más recursos digitales de empresa en vivo fuera de la red corporativa de hello, en la nube de Hola y en los dispositivos, una excelente en la nube identidad y acceso de solución de administración se está convirtiendo en una necesidad. Identidades basadas en la nube son ahora control de hello mejor manera toomaintain over y visibilidad, cómo y cuándo los usuarios acceder a aplicaciones y datos corporativos.

Microsoft se ha protección de identidades en la nube para más de una década y ahora, con [Azure Active Directory (AD)](https://docs.microsoft.com/azure/active-directory/active-directory-editions), estos mismos sistemas de protección están disponible tooyou. Con Azure AD, los administradores de las empresas pueden garantizar fácilmente la responsabilidad de los usuarios y administradores con mayor seguridad y gobernanza que nunca.

Azure AD Premium está una basada en la nube identidad y acceso de solución de administración con capacidades de protección avanzada que permite una identidad segura para todas las aplicaciones, protección de identidad (mejorados con hello [gráfico de seguridad de Microsoft intelligence](https://www.microsoft.com/en-us/security/intelligence)) y la administración de identidad con privilegios. No sólo otra supervisión o informes de herramienta, Azure AD Premium puede proteger las identidades del usuario en tiempo real y habilitar toocreate acceso en función del riesgo, adaptable directivas tooprotect datos de su organización.

En este breve vídeo verá una introducción rápida a la protección y administración de identidades de Azure AD:
<iframe width="560" height="315" src="https://www.youtube.com/embed/9LGIJ2-FKIM" frameborder="0" allowfullscreen></iframe>

Microsoft no sólo proporciona una identidad que le guíe en todas partes, pero también un conjunto de herramientas tooautomate, ayudar a proteger y administrar TI dentro de su organización. Incluso después de la llegada de Hola de informática en nube, hay todavía exigen toomanage y controlar las tareas de TI como departamento de soporte técnico llama tooreset las contraseñas de usuario, grupo de usuarios administración y las solicitudes de aplicación. Lo que complica aún más cosas, los empleados ahora traerán su toowork dispositivos personales y usar aplicaciones SaaS estén disponibles. Todo ello hace que no sea nada fácil mantener el control sobre sus aplicaciones en los centros de datos corporativos y en las plataformas en la nube pública.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="connect-on-premises-active-directory-with-azure-ad-and-office-365"></a>Conexión de una instancia local de Active Directory a Azure AD y Office 365
Las organizaciones que han hecho grandes inversiones en local de Active Directory pueden ampliar esos nube toohello de las inversiones mediante la integración de sus directorios locales con Azure AD en [administración de identidades híbridas](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview). Dicho cambio aumenta la productividad de los usuarios, ya que proporciona una identidad común para acceder a los recursos, independientemente de su ubicación. Los usuarios y las organizaciones pueden usar inicio de sesión único (SSO) tooaccess ambos recursos locales y servicios como Office 365 en la nube.

[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) es Hola única herramienta que requieren la integración de hello tooget realiza. Azure AD Connect proporciona capacidades toosupport la sincronización de identidades necesita y reemplaza las versiones anteriores de herramientas de integración de identidad como DirSync y Azure AD Sync. Con Azure AD Connect, la administración y sincronización de identidades entre un entorno local y Azure AD se habilitan a través de:

- Sincronización: este componente es responsable de la creación de usuarios, grupos y otros objetos. También es responsable de asegurarse de que la información de identidad para los usuarios locales y grupos coincidentes en la nube Hola. Reescritura de contraseña también se pueden tookeep habilitado en directorios locales sincronizados cuando un usuario actualiza su contraseña en Azure AD.
- La federación de AD FS - es una capacidad opcional proporcionada por Azure AD Connect que puede ser tooconfigure usa un entorno híbrido con una implementación local infraestructura de AD FS. Federación puede utilizarse por las organizaciones tooaddress las implementaciones complejas, como inicio de sesión único, cumplimiento de directiva de inicio de sesión AD y tarjeta inteligente u otros fabricantes MFA.
- Supervisión de estado - [Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health) puede proporcionar supervisión sólida y proporcionar una ubicación central en hello tooview portal Azure esta actividad.

## <a name="increase-productivity-and-reduce-helpdesk-costs-with-self-service-and-single-sign-on-experiences"></a>Aumento de la productividad y reducción de los costos del departamento de soporte técnico gracias al autoservicio y al inicio de sesión único

Los empleados son más productivos cuando tienen una sola tooremember de nombre de usuario y una contraseña y una experiencia coherente en todos los dispositivos. También hacen ahorrar tiempo al que pueden realizar tareas de autoservicio como [restablecer una contraseña olvidada](https://docs.microsoft.com/azure/active-directory/active-directory-passwords) o la solicitud de acceso tooan aplicación sin tener que esperar para obtener ayuda del departamento de soporte técnico de Hola.

Azure AD [en local de Active Directory se extiende](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) en nube de hello, habilitar usuarios toouse su cuenta profesional principal para sus dispositivos Unidos a un dominio, recursos de la empresa y todas las aplicaciones de SaaS y web de Hola necesita toouse tooget su trabajo. Además toonot tener tooremember varios conjuntos de nombres de usuario y contraseñas, acceso a la aplicación de los usuarios también pueden ser automáticamente aprovisionados (o anular aprovisionados) basado en su pertenencia a grupos de organización y su estado como un empleado. Y puede controlar el acceso para las aplicaciones de la galería o para sus propias aplicaciones locales que haya desarrolladas y publicadas a través de hello [el Proxy de aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="manage-and-control-access-toocorporate-resources"></a>Administrar y controlar el acceso a los recursos toocorporate
Extensión identity and access management soluciones ayuda de Microsoft TI proteger acceso tooapplications y recursos a través del centro de datos corporativo hello y en la nube de hello, permite niveles adicionales de validación como [la autenticación multifactor](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) y [directivas de acceso condicional](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). La supervisión de actividades sospechosas mediante auditorías, alertas e informes de seguridad avanzados contribuye a minimizar los posibles problemas de seguridad.

Directivas de acceso condicional en Azure AD Premium ofrece ninguna, Hola administrador empresarial, Hola reglas de acceso basada en directivas de toocreate de capacidad para cualquier aplicación conectada a AD Azure (aplicaciones de SaaS, aplicaciones personalizadas que se ejecutan en aplicaciones de web de hello en la nube o local). Azure AD se evalúa como estas directivas en tiempo real y desea que aplique cada vez que un usuario intente tooaccess una aplicación. Las directivas de protección de identidad de Azure permiten tooautomatically realice las acciones si se detecta actividad sospechosa. Estas acciones pueden incluir bloqueo toousers de acceso de alto riesgo, exigir la autenticación multifactor, y restablecer las contraseñas de usuario si parece que las credenciales se han visto comprometidas.


## <a name="azure-active-directory-privileged-identity-management"></a>Azure Active Directory Privileged Identity Management

[La administración de identidad con privilegios](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-getting-started), incluido con hello Azure Active Directory Premium P2 oferta, le permite toodiscover, restringir y supervisar las cuentas administrativas y sus tooresources de acceso en su Azure Active Directory y otros Servicios en línea de Microsoft. También le ayuda administrar período exacto de Hola de tiempo que necesita acceso administrativo a petición.

Privileged Identity Management de puede aplicar derechos de administrador a petición para que los administradores puedan solicitar elevación autenticado y temporal de varios factor de sus privilegios para preconfigurado períodos de tiempo antes de que sus cuentas devuelven tooa normal estado de usuario.

## <a name="benefits-of-azure-identity"></a>Ventajas de la identidad de Azure

Con la administración de identidades de Azure se puede:

-   Crear y administrar una identidad única para cada usuario en toda la empresa, lo que mantiene a los usuarios, grupos y dispositivos sincronizados con [Azure Active Directory Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

-   Proporcionar acceso de inicio de sesión único aplicaciones tooyour incluidos miles de aplicaciones SaaS integradas previamente o proporcionar acceso remoto seguro a aplicaciones de SaaS de tooon locales mediante hello [el Proxy de aplicación de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

-   Habilitar la seguridad del acceso de las aplicaciones mediante la aplicación de [Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) basado en reglas para las aplicaciones locales y en la nube.

-   Mejorar la productividad del usuario con [de restablecimiento de contraseña de autoservicio](https://docs.microsoft.com/azure/active-directory/active-directory-passwords)y de grupo y de aplicación tener acceso a las solicitudes con hello [portal mis aplicaciones](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-user-help).

-   Aprovechar las ventajas de hello [alta disponibilidad y confiabilidad](https://docs.microsoft.com/azure/architecture/resiliency/high-availability-azure-applications) de un nivel empresarial en todo el mundo, solución de administración de identidades y acceso basado en la nube.

## <a name="next-steps"></a>Pasos siguientes
[Obtener más información sobre soluciones de identidad de Azure](https://docs.microsoft.com/azure/active-directory/understand-azure-identity-solutions)
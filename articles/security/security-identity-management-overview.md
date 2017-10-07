---
title: "seguridad de aaaAzure características que ayudan a con la administración de identidad | Documentos de Microsoft"
description: " Este artículo proporciona información general sobre las características de seguridad de Azure de núcleo de Hola que simplifican la administración de identidades. Extensión identity and access management soluciones ayuda de Microsoft TI proteger tooapplications de acceso y recursos a través del centro de datos corporativo hello y en la nube de Hola, habilitación de niveles adicionales de validación, como la autenticación multifactor y condicional directivas de acceso. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 5aa0a7ac-8f18-4ede-92a1-ae0dfe585e28
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: terrylan
ms.openlocfilehash: f08e4f6cf2e48e455a16858b7fee08b53d5aa585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-security-overview"></a>Información general sobre seguridad de administración de identidades de Azure
Extensión identity and access management soluciones ayuda de Microsoft TI proteger tooapplications de acceso y recursos a través del centro de datos corporativo hello y en la nube de Hola, habilitación de niveles adicionales de validación, como la autenticación multifactor y condicional directivas de acceso. La supervisión de actividades sospechosas mediante auditorías, alertas e informes de seguridad avanzados contribuye a minimizar los posibles problemas de seguridad. [Azure Active Directory Premium](../active-directory/active-directory-editions.md) proporciona toothousands de inicio de sesión único de acceso tooweb aplicaciones se ejecutan de forma local y en la nube (SaaS).

Ventajas de seguridad de Azure Active Directory (AD) incluyen la capacidad de hello:

* Crear y administrar una identidad única para cada usuario en toda la empresa híbrida, lo que mantiene los usuarios, grupos y dispositivos sincronizados
* Proporcionar acceso de inicio de sesión único aplicaciones tooyour incluidos miles de aplicaciones SaaS integradas previamente
* Habilitar la seguridad del acceso a las aplicaciones mediante la aplicación de la autenticación multifactor basada en reglas para las aplicaciones locales o en la nube
* Aprovisionamiento de acceso remoto seguro tooon local web aplicaciones a través de Proxy de aplicación de Azure AD

objetivo de Hola de este artículo es tooprovide una visión general de las características de seguridad de Azure de núcleo de Hola que simplifican la administración de identidades. También se proporcionan los vínculos tooarticles que proporcionan detalles de cada característica, por lo que puede obtener más información.  

Hola artículo se centra en hello después de capacidades de administración de identidades de Azure:

* Inicio de sesión único
* Proxy inverso
* Multi-Factor Authentication
* Supervisión de seguridad, alertas e informes basados en aprendizaje automático
* Administración de identidades y acceso de consumidores
* Registro de dispositivos
* Privileged Identity Management
* Protección de identidad
* Administración de identidades híbridas

## <a name="single-sign-on"></a>Inicio de sesión único
Inicio de sesión único (SSO) significa que se va a tooaccess capaz de todas las aplicaciones de Hola y recursos que necesita toodo business, debe iniciar sesión en una sola vez usando una cuenta de usuario único. Una vez iniciado sesión, puede tener acceso a todas las aplicaciones de hello necesaria sin que se va a tooauthenticate necesaria de (por ejemplo, escriba una contraseña) una segunda vez.

Muchas organizaciones confían en el modelo de software como servicio (SaaS), como Office 365, Box y Salesforce para la productividad del usuario final. Históricamente, tooindividually necesita el personal de TI crear y actualizar cuentas de usuario en cada aplicación SaaS, y los usuarios tenían tooremember una contraseña para cada aplicación SaaS.

Azure AD amplía los entornos de Active Directory local en la nube de hello, lo que permite a los usuarios toouse su cuenta organizativa principal toonot solo inicio de sesión tootheir dispositivos Unidos a dominio y recursos de la empresa, pero también todos hello web y aplicaciones de SaaS se necesita para realizar su trabajo.

No solo a los usuarios no tiene toomanage varios conjuntos de nombres de usuario y contraseñas, acceso a la aplicación puede ser desaprovisionados por completo o aprovisionamiento automáticamente en función de grupos de la organización y su estado como un empleado. Introduce la seguridad de Azure AD y los controles de regulación de acceso que permiten toocentrally administran el acceso de los usuarios en todas las aplicaciones de SaaS.

Más información:

* [Información general de inicio de sesión único](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../active-directory/active-directory-appssoaccess-whatis.md)
* [Integración del inicio de sesión único de Azure Active Directory con aplicaciones SaaS](../active-directory/active-directory-sso-integrate-saas-apps.md)

## <a name="reverse-proxy"></a>Proxy inverso
El Proxy de aplicación de Azure AD permite publicar aplicaciones locales, como [SharePoint](https://support.office.com/article/What-is-SharePoint-97b915e6-651b-43b2-827d-fb25777f446f?ui=en-US&rs=en-US&ad=US) sitios, [Outlook Web App](https://technet.microsoft.com/library/jj657718.aspx), y [IIS](http://www.iis.net/)-aplicaciones dentro de su red privada basadas en y proporciona un acceso seguro toousers fuera de la red. El Proxy de aplicación proporciona acceso remoto y el inicio de sesión único (SSO) para muchos tipos de en aplicaciones web locales con hello miles de aplicaciones de SaaS que admite Azure AD. Los empleados pueden iniciar sesión en tooyour las aplicaciones de inicio en sus propios dispositivos y autenticarse a través de este proxy basado en la nube.

Más información:

* [Habilitación del proxy de la aplicación de Azure AD](../active-directory/active-directory-application-proxy-enable.md)
* [Publicación de aplicaciones mediante el proxy de aplicación de Azure AD](../active-directory/active-directory-application-proxy-publish.md)
* [Inicio de sesión único con el Proxy de aplicación](../active-directory/active-directory-application-proxy-sso-using-kcd.md)
* [Uso de acceso condicional](../active-directory/active-directory-application-proxy-conditional-access.md)

## <a name="multi-factor-authentication"></a>Multi-Factor Authentication
Azure la autenticación multifactor (MFA) es un método de autenticación que requiere el uso de Hola de más de un método de comprobación y agrega una segunda capa crítica de inicios de sesión de seguridad toouser y las transacciones. MFA ayuda a proteger acceso toodata y las aplicaciones al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple. Proporciona autenticación sólida mediante una gran variedad de opciones de verificación, como llamadas telefónicas, mensajes de texto, notificaciones de aplicaciones móviles, códigos de verificación y tokens OAuth de terceros.

Más información:

* [Multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [¿Qué es Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)
* [Cómo funciona Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>Supervisión de seguridad, alertas e informes basados en aprendizaje automático
La supervisión y las alertas de seguridad, así como los informes basados en el aprendizaje automático que identifican patrones de acceso incoherentes, puede ayudarle a proteger su negocio. Puede usar el acceso de Active Directory de Azure y visibilidad de toogain de informes de uso de integridad de Hola y seguridad del directorio de su organización. Con esta información, administradores de directorios pueden determinar mejor dónde puede haber posibles riesgos de seguridad para que se pueden planificar adecuadamente toomitigate esos riesgos.

Hola portal de Azure clásico, los informes se clasifican de hello siguientes maneras:

* Informes de anomalías: contienen eventos que encontramos toobe anómalos de inicio de sesión. Nuestro objetivo es toomake, tanto de dicha actividad y le permiten toobe capaz toomake una decisión sobre si un evento es sospechoso.
* Informes de aplicaciones integradas: proporcionan información sobre cómo se usan en su organización aplicaciones en la nube. Azure Active Directory ofrece integración con miles de aplicaciones en la nube.
* Informes de errores: indican errores que pueden surgir al aprovisionar las aplicaciones de tooexternal de cuentas.
* Informes específicos del usuario: muestran los datos de actividad de dispositivo o de inicio de sesión de un usuario concreto.
* Registros de actividad: contienen un registro de todos los eventos auditados en hello últimas 24 horas, los últimos 7 días, o últimos 30 días y cambios de la actividad de grupo y la actividad de registro y restablecimiento de contraseña.

Más información:

* [Visualización de los informes de acceso y uso](../active-directory/active-directory-view-access-usage-reports.md)
* [Introducción a los informes de Azure Active Directory](../active-directory/active-directory-reporting-getting-started.md)
* [Guía de informes de Azure Active Directory](../active-directory/active-directory-reporting-guide.md)

## <a name="consumer-identity-and-access-management"></a>Administración de identidades y acceso de consumidores
Azure B2C directorio activo es un servicio de administración de identidades globales, y alta disponibilidad para las aplicaciones orientadas al consumidor que escala toohundreds de millones de identidades. Se puede integrar en plataformas móviles y web. Los consumidores pueden iniciar sesión tooall sus aplicaciones a través de experiencias personalizables mediante sus cuentas sociales existentes o crear nuevas credenciales.

Hola anteriores, los desarrolladores de aplicaciones que deseaban toosign seguridad e iniciar sesión en los consumidores en sus aplicaciones habría escribe su propio código. Y ha utilizado las contraseñas y nombres de usuario de toostore de bases de datos o sistemas de local. Azure B2C de directorio Active ofrece una administración de identidades consumidor de mejor manera toointegrate en las aplicaciones con ayuda de Hola de una plataforma segura y basada en estándares y un conjunto grande de directivas extensibles de su organización.

El uso de Azure Active Directory B2C permite a los consumidores registrarse en las aplicaciones con sus cuentas de redes sociales existentes (Facebook, Google, Amazon, LinkedIn) o creando nuevas credenciales (dirección de correo electrónico y contraseña o nombre de usuario y contraseña).

Más información:

* [¿Qué es Azure Active Directory B2C?](https://azure.microsoft.com/services/active-directory-b2c/)
* [Versión preliminar de Azure Active Directory B2C: registro e inicio de sesión de consumidores en las aplicaciones](../active-directory-b2c/active-directory-b2c-overview.md)
* [Versión preliminar de Azure Active Directory B2C: tipos de aplicaciones](../active-directory-b2c/active-directory-b2c-apps.md)

## <a name="device-registration"></a>Registro de dispositivos
Registro de dispositivos de Azure AD es la base de hello basado en dispositivos [acceso condicional](../active-directory/active-directory-conditional-access-device-registration-overview.md) escenarios. Cuando se registra un dispositivo, registro de dispositivo de Azure Active Directory proporciona dispositivo Hola con una identidad que sea el dispositivo de hello tooauthenticate usado cuando Hola usuario inicia sesión. dispositivo de Hello autenticado y los atributos de hello de dispositivo de hello, se pueden tooenforce usa directivas de acceso condicional para las aplicaciones que se hospedan en la nube de Hola y local.

Cuando se combina con una solución de administración (MDM) de dispositivos móviles como Intune, los atributos de dispositivo de hello en Azure Active Directory se actualizan con información adicional sobre el dispositivo de Hola. Esto permite que las reglas de acceso condicional de toocreate que exijan el acceso desde dispositivos toomeet los estándares de seguridad y cumplimiento de normas.

Más información:

* [Introducción al Registro de dispositivos de Azure Active Directory](../active-directory/active-directory-conditional-access-device-registration-overview.md)
* [Registro automático de dispositivos en Azure Active Directory para dispositivos Windows unidos a un dominio](../active-directory/active-directory-conditional-access-automatic-device-registration.md)
* [Configuración del registro automático de dispositivos unidos a un dominio de Windows con Azure Active Directory](../active-directory/active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="privileged-identity-management"></a>Privileged Identity Management
Active Directory (AD) Privileged Identity Management de Azure le permite administrar, controlar y supervisar las identidades con privilegios y acceso tooresources en Azure AD, así como otros servicios en línea de Microsoft como Office 365 o Microsoft Intune.

En ocasiones, los usuarios necesitan toocarry operaciones con privilegios en recursos de Azure u Office 365 u otras aplicaciones de SaaS. Esto suele significar que las organizaciones tienen toogive tener acceso ellas con privilegios permanentes en Azure AD. Esto representa un riesgo de seguridad creciente para los recursos hospedados en la nube porque las organizaciones no pueden supervisar suficientemente qué hacen esos usuarios con sus privilegios administrativos. Además, si se pone en peligro una cuenta de usuario que tiene acceso con privilegios, esta situación podría afectar a su seguridad en la nube global. Identity Management de Azure AD privilegios ayuda a tooresolve este riesgo.

Azure AD Privileged Identity Management le permite:

* Ver qué usuarios son administradores de Azure AD
* Habilitar a petición "justo a tiempo" acceso administrativo tooMicrosoft Online Services, como Office 365 e Intune
* Obtener informes sobre el historial de acceso de administrador y sobre los cambios en las asignaciones de administrador
* Obtener alertas sobre los roles con privilegios de acceso tooa

Más información:

* [Administración de identidades con privilegios de Azure AD](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Roles en Privileged Identity Management de Azure AD](../active-directory/active-directory-privileged-identity-management-roles.md)
* [AD Privileged Identity Management de Azure: ¿Cómo tooadd o quitar un rol de usuario](../active-directory/active-directory-privileged-identity-management-how-to-add-role-to-user.md)

## <a name="identity-protection"></a>Protección de identidad
Azure AD Identity Protection es un servicio de seguridad que proporciona una vista consolidada de eventos de riesgo y puntos vulnerables que afectan a las identidades de su organización. Identity Protection aprovecha las funciones de detección de anomalías existentes de Azure Active Directory (disponibles mediante informes de actividad anómala de Azure AD) e introduce nuevos tipos de eventos de riesgo que pueden detectar anomalías en tiempo real.

Más información:

* [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md)
* [Channel 9: Azure AD and Identity Show: Identity Protection Preview (Channel 9: Presentación de Azure AD e Identity: versión preliminar de Identity Protection)](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="hybrid-identity-management"></a>Administración de identidades híbridas
Enfoque tooidentity intervalos locales de Microsoft y en la nube hello, crear una identidad de usuario único para la autenticación y autorización de recursos de tooall, independientemente de su ubicación.

Más información:

* [Notas del producto sobre identidad híbrida](http://download.microsoft.com/download/D/B/A/DBA9E313-B833-48EE-998A-240AA799A8AB/Hybrid_Identity_White_Paper.pdf)
* [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)
* [Blog del equipo de Active Directory](https://blogs.technet.microsoft.com/ad/)

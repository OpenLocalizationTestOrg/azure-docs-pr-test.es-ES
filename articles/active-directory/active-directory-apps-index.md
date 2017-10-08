---
title: "aaaArticle índice para la administración de la aplicación en Azure Active Directory | Microsoft Azure"
description: "Obtenga información acerca de la fecha de expiración de hello toocustomize para los certificados de federación y cómo toorenew certificados que caducará pronto."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 5321b8e4-2afa-4dfe-8d53-4add7abb5ec8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: f8a584baa94dc50e279899074f50160978256559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="article-index-for-application-management-in-azure-active-directory"></a>Índice de artículos sobre la administración de aplicaciones en Azure Active Directory
Esta página proporciona una lista completa de cada documento escrito Hola varias características relacionadas con la aplicación en Azure Active Directory (Azure AD).

Hay un área de características más importantes de tooeach breve introducción, así como instrucciones sobre qué tooread artículos dependiendo de qué información está buscando.

## <a name="overview-articles"></a>Artículos de información general
artículos de Hello siguientes son buenos puntos de partida para aquellos que simplemente desean una breve explicación de las características de administración de aplicaciones de Azure AD.

| Guía de artículos |  |
|:---:| --- |
| Un problemas de administración de aplicaciones de toohello de introducción que resuelve Azure AD |[Administración de aplicaciones con Azure Active Directory (AD)](active-directory-enable-sso-scenario.md) |
| Información general de hello relacionados con distintas características de Azure AD tooenabling inicio de sesión único, definir quién tiene acceso a tooapps y cómo los usuarios inicien aplicaciones |[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md) |
| Un vistazo a Hola diferentes pasos al integrar aplicaciones en Azure AD |[Integración de Azure Active Directory con las aplicaciones](active-directory-integrating-applications-getting-started.md)<br /><br />[Habilitar inicio de sesión único tooSaaS aplicaciones](active-directory-sso-integrate-saas-apps.md)<br /><br />[Administrar acceso tooApps](active-directory-managing-access-to-apps.md) |
| Una explicación técnica de cómo se representan las aplicaciones de Azure AD |[Cómo y por qué aplicaciones se agregan tooAzure AD](active-directory-how-applications-are-added.md) |

## <a name="troubleshooting-articles"></a>Artículos de solución de problemas
Esta sección proporciona acceso rápido guías de solución de problemas de toorelevant. Para obtener más información acerca de cada área de característica puede encontrarse en el resto de Hola de esta página.

| Área de características |  |
|:---:| --- |
| Inicio de sesión único federado |[Cómo depurar el inicio de sesión único basado en SAML en aplicaciones de Azure Active Directory](active-directory-saml-debugging.md) |
| Inicio de sesión único con contraseña |[Solución de problemas de hello extensión del Panel de acceso de Internet Explorer](active-directory-saas-ie-troubleshooting.md) |
| Proxy de aplicación |[Solucionar problemas del proxy de aplicación](active-directory-application-proxy-troubleshoot.md) |
| Inicio de sesión único entre un AD local y Azure AD |[Solución de problemas de sincronización de contraseñas](connect/active-directory-aadconnectsync-implement-password-synchronization.md#troubleshoot-password-synchronization)<br /><br />[Solución de problemas de escritura diferida de contraseñas](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Pertenencia a grupos dinámicos. |[Solución de problemas de pertenencias a grupos dinámicos](active-directory-accessmanagement-troubleshooting.md) |

## <a name="single-sign-on-sso"></a>Inicio de sesión único (SSO)
### <a name="federated-single-sign-on-sign-into-many-apps-using-one-identity"></a>Inicio de sesión único federado: inicio de sesión en muchas aplicaciones con una sola identidad
Inicio de sesión único permite a los usuarios tooaccess una variedad de aplicaciones y servicios mediante un único conjunto de credenciales. La federación es un método a través del cual se puede habilitar el inicio de sesión único. Cuando los usuarios intentan toosign en aplicaciones federadas, obtendrán tootheir redirigida oficial de inicio de sesión página de la organización que se representa mediante Azure Active Directory y pasan a ser redirigido toohello atrás aplicación tras una autenticación correcta.

| Guía de artículos |  |
|:---:| --- |
| Un toofederation de introducción y otros tipos de inicio de sesión |[Inicio de sesión único con Azure AD](active-directory-appssoaccess-whatis.md) |
| Miles de aplicaciones SaaS integradas previamente con Azure AD con pasos de configuración de inicio de sesión único simplificados |[Introducción a la Galería de aplicaciones de Azure AD de Hola](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)<br /><br />[Lista completa de las aplicaciones integradas previamente que admiten federación](http://aka.ms/aadfederatedapps)<br /><br />[Cómo tooAdd toohello de la aplicación de la Galería de aplicaciones de Azure AD](active-directory-app-gallery-listing.md) |
| Más de 150 tutoriales de aplicación en modo tooconfigure inicio de sesión único para aplicaciones como [Salesforce](active-directory-saas-salesforce-tutorial.md), [ServiceNow](active-directory-saas-servicenow-tutorial.md), [Google Apps](active-directory-saas-google-apps-tutorial.md), [Workday](active-directory-saas-workday-tutorial.md)y mucho más |[Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md) |
| ¿Cómo toomanually configurar y personalizar la configuración del inicio de sesión única |[¿Cómo tooConfigure federado Single Sign-On tooApps que no están en hello Galería de aplicaciones de Azure Active Directory](active-directory-saas-custom-apps.md)<br /><br />[Cómo se emiten las notificaciones tooCustomize en hello Token de SAML para aplicaciones Pre-Integrated](active-directory-saml-claims-customization.md) |
| Guía para las aplicaciones federadas que utilizan el protocolo SAML de Hola para solucionar problemas |[Cómo depurar el inicio de sesión único basado en SAML en aplicaciones de Azure Active Directory](active-directory-saml-debugging.md) |
| ¿Cómo tooconfigure fecha de expiración del certificado de la aplicación y cómo toorenew los certificados |[Administración de certificados para inicio de sesión único federado en Azure Active Directory](active-directory-sso-certs.md) |

Un inicio de sesión único federado está disponible para todas las ediciones de Azure AD para la seguridad de aplicaciones de tooten por usuario. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) admite un número ilimitado de aplicaciones. Si su organización tiene [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) o [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), puede [use grupos de aplicaciones de toofederated de tooassign acceso](#managing-access-to-applications).

### <a name="password-based-single-sign-on-account-sharing-and-sso-for-non-federated-apps"></a>Inicio de sesión único con contraseña: uso compartido de cuentas y SSO para aplicaciones no federadas
tooenable único inicio de sesión tooapplications que no son compatibles con la federación, características de administración de contraseñas de ofertas de Azure AD que pueden almacenar de forma segura contraseñas tooSaaS aplicaciones y firmar automáticamente a los usuarios en esas aplicaciones. Puede distribuir las credenciales de las cuentas recién creadas y compartir las cuentas del equipo con varias personas fácilmente. Los usuarios no tienen necesariamente tooknow Hola credenciales toohello las cuentas que ha otorgado acceso a.

| Guía de artículos |  |
|:---:| --- |
| Un funciona SSO basada en contraseña de introducción toohow y una breve descripción general técnica |[Inicio de sesión único con contraseña](active-directory-appssoaccess-whatis.md#password-based-single-sign-on) |
| Relacionados con un resumen de los escenarios de hello tooaccount de uso compartido y cómo se resuelven estos problemas mediante Azure AD |[Uso compartido de cuentas con Azure AD](active-directory-sharing-accounts.md) |
| Cambiar automáticamente contraseña Hola para ciertas aplicaciones a intervalos periódicos |[Sustitución automática de contraseña (vista previa)](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| Implementación y guías para la versión de Internet Explorer Hola de hello extensión de administración de contraseñas de Azure AD de solución de problemas |[¿Cómo tooDeploy Hola extensión del Panel de acceso para Internet Explorer utilizando la directiva de grupo](active-directory-saas-ie-group-policy.md)<br /><br />[Solución de problemas de hello extensión del Panel de acceso de Internet Explorer](active-directory-saas-ie-troubleshooting.md) |

Basado en contraseña de inicio de sesión único está disponible para todas las ediciones de Azure AD para la seguridad de aplicaciones de tooten por usuario. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) admite un número ilimitado de aplicaciones. Si su organización tiene [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) o [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), puede [use grupos tooassign acceso tooapplications](#managing-access-to-applications). La sustitución automática de contraseña es una característica de [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

### <a name="app-proxy-single-sign-on-and-remote-access-tooon-premises-applications"></a>Proxy de aplicación: Aplicaciones de tooon locales del único inicio de sesión y acceso remoto
Si tiene aplicaciones en su red privada que necesita toobe acceso a los usuarios y dispositivos que están fuera de la red de hello, puede usar el Proxy de aplicación de Azure AD tooenable acceso remoto seguro toothose aplicaciones.

| Guía de artículos |  |
|:---:| --- |
| Información general sobre el proxy de aplicación de Azure AD y su funcionamiento |[Proporcionar acceso remoto seguro a aplicaciones locales de tooon](active-directory-application-proxy-get-started.md) |
| Tutoriales sobre cómo tooconfigure Proxy de aplicación y cómo toopublish su primera aplicación |[¿Cómo tooSet los Proxy de aplicación de Azure AD](active-directory-application-proxy-enable.md)<br /><br />[Cómo instalar tooSilently Hola conector del Proxy de aplicación](active-directory-application-proxy-silent-installation.md)<br /><br />[¿Cómo tooPublish aplicaciones mediante el Proxy de aplicación](active-directory-application-proxy-publish.md)<br /><br />[Cómo tooUse su propio nombre de dominio](active-directory-application-proxy-custom-domains.md) |
| Cómo tooenable único acceso de inicio de sesión y condicional para aplicaciones publicadas con Proxy de aplicación |[Inicio de sesión único con el proxy de aplicación](active-directory-application-proxy-sso-using-kcd.md)<br /><br />[Uso de acceso condicional](active-directory-application-proxy-conditional-access.md) |
| Obtener información sobre cómo toouse Proxy de aplicación para los escenarios siguientes de hello |[¿Cómo tooSupport las aplicaciones cliente nativas](active-directory-application-proxy-native-client.md)<br /><br />[¿Cómo tooSupport aplicaciones para notificaciones](active-directory-application-proxy-claims-aware-apps.md)<br /><br />[Cómo publican aplicaciones tooSupport en redes independientes y ubicaciones](active-directory-application-proxy-connectors.md) |
| Guía de solución de problemas del proxy de aplicación |[Solucionar problemas del proxy de aplicación](active-directory-application-proxy-troubleshoot.md) |

Proxy de aplicación está disponible para todas las ediciones de Azure AD para la seguridad de aplicaciones de tooten por usuario. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) admite un número ilimitado de aplicaciones. Si su organización tiene [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) o [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), puede [use grupos tooassign acceso tooapplications](#managing-access-to-applications).

Es podrán que le interese [servicios de dominio de AD de Azure](../active-directory-domain-services/active-directory-ds-overview.md), lo cual permite hacer toomigrate necesidades de su tooAzure de aplicaciones local mientras todavía satisface identidad Hola de esas aplicaciones.

### <a name="enabling-single-sign-on-between-azure-ad-and-on-premises-ad"></a>Habilitación del inicio de sesión único entre Azure AD y AD local
Si su organización mantiene un servidor de Windows Active Directory local junto con Azure Active Directory en la nube de hello, a continuación, probablemente le interesará tooenable inicio de sesión único entre estos dos sistemas. Azure AD Connect (herramienta de Hola que integra estos dos sistemas juntos) proporciona varias opciones para configurar el inicio de sesión único: establecer la federación con AD FS u otro proveedor de federación o habilitar la sincronización de contraseña.

| Guía de artículos |  |
|:---:| --- |
| Ofrece información general sobre las opciones de inicio de sesión único de hello en Azure AD Connect, así como información acerca de cómo administrar entornos híbridos |[Opciones para el inicio de sesión de los usuarios en Azure AD Connect](active-directory-aadconnect-user-signin.md) |
| Guía general para la administración de entornos con la versión local de Active Directory y Azure Active Directory |[Consideraciones de diseño de identidad híbrida de Azure Active Directory](active-directory-hybrid-identity-design-considerations-overview.md)<br /><br />[Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md) |
| Instrucciones sobre el uso de la sincronización de contraseñas tooenable SSO |[Implementación de la sincronización de contraseña mediante la sincronización de Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md)<br /><br />[Solución de problemas de sincronización de contraseñas](https://support.microsoft.com/en-us/kb/2855271) |
| Instrucciones sobre el uso de la escritura diferida de contraseñas tooenable SSO |[Introducción a la administración de contraseñas en Azure AD](active-directory-passwords-getting-started.md)<br /><br />[Solución de problemas de escritura diferida de contraseñas](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Instrucciones sobre el uso de tooenable de proveedores de identidad de terceros SSO |[Lista de compatibles terceros identidad que se pueden utilizar proveedores tooEnable Single Sign-On](https://aka.ms/ssoproviders) |
| Cómo los usuarios de Windows 10 pueden disfrutar de las ventajas de Hola de inicio de sesión único a través de Azure AD Join |[Extender capacidades de la nube tooWindows 10 dispositivos a través de Azure Active Directory Join](active-directory-azureadjoin-overview.md) |

Azure AD Connect está disponible para [todas las ediciones de Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/). Restablecimiento de contraseña de autoservicio de Azure AD está disponible para [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) y [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/). Contraseña de reescritura tooon local AD es un [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) característica.

### <a name="conditional-access-enforce-additional-security-requirements-for-high-risk-apps"></a>Acceso condicional: aplicación de requisitos de seguridad adicionales en aplicaciones de alto riesgo
Una vez configurado recursos y las aplicaciones de tooyour de inicio de sesión único, a continuación, puede proteger aún más aplicaciones confidenciales mediante la aplicación de los requisitos de seguridad específicos en todas las aplicaciones de inicio de sesión toothat. Por ejemplo, puede utilizar toodemand de Azure AD que todos los acceso tooa determinada aplicación siempre requieren la autenticación multifactor, independientemente de si admite o no que la aplicación naturaleza esa funcionalidad. Otro ejemplo común de acceso condicional es toorequire que los usuarios estén conectados toohello organización de confianza de red en orden tooaccess una aplicación especialmente sensible.

| Guía de artículos |  |
|:---:| --- |
| Un capacidades de acceso condicional de introducción toohello ofrecen a través de AD de Azure, Office 365 e Intune |[Administración de riesgos con el acceso condicional](active-directory-conditional-access.md) |
| Cómo obtener acceso tooenable condicional de hello siguientes tipos de recursos |[Introducción al acceso condicional de Azure Active Directory](active-directory-conditional-access-azuread-connected-apps.md)<br /><br />[Directivas de dispositivo de acceso condicional para servicios de Office 365](active-directory-conditional-access-device-policies.md)<br /><br />[Configuración del acceso condicional local mediante el registro de dispositivos de Azure Active Directory](active-directory-conditional-access.md)<br /><br />[Acceso condicional para aplicaciones locales publicadas mediante el proxy de aplicación de Azure AD](active-directory-application-proxy-conditional-access.md) |

| ¿Cómo tooregister dispositivos con Azure Active Directory en el pedido tooenable directivas de acceso condicional basado en dispositivos | [Información general sobre el registro de dispositivos de Azure Active Directory](active-directory-conditional-access-device-registration-overview.md)<br /><br />[¿Cómo tooEnable registro automático de dispositivos para dispositivos de Windows Unidos a un dominio](active-directory-conditional-access-automatic-device-registration.md)<br />: [Pasos para dispositivos Windows 8.1](active-directory-conditional-access-automatic-device-registration-setup.md)<br />: [Pasos para dispositivos Windows 7](active-directory-conditional-access-automatic-device-registration-setup.md) |

| ¿Cómo toouse Hola aplicación Authenticator de Microsoft para la verificación en dos pasos | [Authenticator de Microsoft](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

Acceso condicional es una característica de [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

## <a name="apps--azure-ad"></a>Aplicaciones y Azure AD
### <a name="cloud-app-discovery-find-which-saas-apps-are-being-used-in-your-organization"></a>Cloud App Discovery: búsqueda de las aplicaciones SaaS que se usan en la organización
Cloud App Discovery ayuda a los departamentos de TI a obtener información sobre qué aplicaciones de SaaS se usan en toda la organización de Hola. Puede medir el uso de la aplicación y popularidad, para que TI pueda determinar qué aplicaciones beneficiarán hello más ante sometidos al control de TI y se integra con Azure AD.

| Guía de artículos |  |
|:---:| --- |
| Información general de su funcionamiento |[Búsqueda de aplicaciones de nube no sancionadas con Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md) |
| Un análisis más profundo sobre su funcionamiento, con tooquestions respuestas sobre privacidad |[Consideraciones de seguridad y privacidad de Cloud App Discovery](active-directory-cloudappdiscovery-security-and-privacy-considerations.md) |
| Preguntas frecuentes |[Cloud App Discovery - Frequently Asked Questions (Preguntas frecuentes sobre Cloud App Discovery)](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx) |
| Tutoriales para la implementación de Cloud App Discovery |[Guía de implementación de directivas de grupo](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)<br /><br />[Guía de implementación de System Center](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)<br /><br />[Instalación en servidores proxy con puertos personalizados](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md) |
| Hola cambiar el registro para el agente de Cloud App Discovery toohello de actualizaciones |[Registro de cambios](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx) |

Cloud App Discovery es una característica de [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

### <a name="automatically-provision-and-deprovision-user-accounts-in-saas-apps"></a>Aprovisionamiento y desaprovisionamiento automáticos de cuentas de usuario en aplicaciones SaaS
Automatizar la creación de hello, mantenimiento y eliminación de identidades de usuario en aplicaciones de SaaS como Dropbox, Salesforce, ServiceNow y mucho más. Coincide con y sincronización de identidades existentes entre Azure AD, sus aplicaciones SaaS y controlar el acceso al deshabilitar automáticamente las cuentas cuando los usuarios dejan la organización de Hola.

| Guía de artículos |  |
|:---:| --- |
| Obtenga información acerca de cómo funciona y encuentre respuestas toocommon preguntas |[Automatizar el aprovisionamiento de usuarios & desaprovisionamiento tooSaaS aplicaciones](active-directory-saas-app-provisioning.md) |
| Configuración de cómo se asigna información entre Azure AD y una aplicación SaaS |[Personalización de asignaciones de atributos](active-directory-saas-customizing-attribute-mappings.md)<br><br>[Escritura de expresiones para la asignación de atributos](active-directory-saas-writing-expressions-for-attribute-mappings.md) |
| Cómo tooenable automatizar aprovisionamiento aplicación tooany que admita el protocolo de hello SCIM |[Configurar automatizada de aprovisionamiento de usuarios tooany SCIM-Enabled aplicación](active-directory-scim-provisioning.md) |
| ¿Cómo tooreport en y solucionar problemas de aprovisionamiento de usuarios |[Notificación del aprovisionamiento automático de usuarios](active-directory-saas-provisioning-reporting.md)<br><br>[Aprovisionamiento de notificaciones](active-directory-saas-account-provisioning-notifications.md)<br><br>[Solución de problemas con aprovisionamiento de usuarios](active-directory-application-provisioning-content-map.md) |
| Limitar quién obtiene aplicación tooan aprovisionado según sus valores de atributo |[Aprovisionamiento de aplicaciones basado en atributos con filtros de ámbito](active-directory-saas-scoping-filters.md) |

Aprovisionamiento automático de usuarios está disponible para todas las ediciones de Azure AD para la seguridad de aplicaciones de tooten por usuario. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) admite un número ilimitado de aplicaciones. Si su organización tiene [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) o [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), puede [usar toomanage grupos obtengan aprovisionar los usuarios que](#managing-access-to-applications).

### <a name="building-applications-that-integrate-with-azure-ad"></a>Compilación de aplicaciones que se integran con Azure AD
Si su organización está desarrollando o mantener las aplicaciones de línea de negocio (LoB), o si es un desarrollador de aplicaciones con los clientes que usen Azure Active Directory, Hola tutoriales le ayudará a integrar las aplicaciones con Azure AD.

| Guía de artículos |  |
|:---:| --- |
| Guía para profesionales de TI y desarrolladores de aplicaciones para la integración de aplicaciones en Azure AD |[Guía de Hola profesionales de TI para desarrollar aplicaciones para Azure AD](active-directory-applications-guiding-developers-for-lob-applications.md)<br /><br />[Guía del desarrollador de Hola para Azure Active Directory](active-directory-developers-guide.md) |
| Cómo los proveedores de tooapplication pueden agregar su toohello de aplicaciones de la Galería de aplicaciones de Azure AD |[Enumerar la aplicación Hola Galería de aplicaciones de Azure Active Directory](active-directory-app-gallery-listing.md) |
| Cómo toomanage tener acceso a las aplicaciones de toodeveloped con Azure Active Directory |[La asignación de usuario para aplicaciones desarrolladas tooEnable](active-directory-applications-guiding-developers-requiring-user-assignment.md)<br /><br />[Asignar usuarios tooyour aplicación](active-directory-applications-guiding-developers-assigning-users.md)<br /><br />[Grupo de asignación tooyour aplicación](active-directory-applications-guiding-developers-assigning-groups.md) |

Si va a desarrollar aplicaciones de consumo, puede estar interesado en usar [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) para que no tengan toodevelop su propio toomanage de sistema de identidad a los usuarios. [Más información](../active-directory-b2c/active-directory-b2c-overview.md).

## <a name="managing-access-tooapplications"></a>Administrar acceso tooApplications
### <a name="using-groups-and-self-service-toomanage-who-has-access-toowhich-apps"></a>Uso de grupos y toomanage de autoservicio que tenga acceso toowhich aplicaciones
toohelp administrar que deben tener acceso a los recursos toowhich, Azure Active Directory permite asignaciones tooset y permisos a escala mediante grupos. TI puede elegir tooenable características de autoservicio para que los usuarios simplemente pueden solicitar permiso cuando lo necesiten.

| Guía de artículos |  |
|:---:| --- |
| Introducción a las características de administración de acceso de Azure AD |[Introducción tooManaging tooApps de acceso](active-directory-managing-access-to-apps.md)<br /><br />[Administración del acceso a los recursos con grupos de Azure Active Directory](active-directory-manage-groups.md)<br /><br />[¿Cómo tooUse grupos tooManage tooSaaS acceso a las aplicaciones](active-directory-accessmanagement-group-saasapps.md) |
| Habilitación de la administración autoservicio de aplicaciones y grupos |[Configuración de Azure Active Directory para la administración de grupos de autoservicio](active-directory-self-service-application-access.md)<br /><br />[Administración de grupos de autoservicio](active-directory-accessmanagement-self-service-group-management.md) |
| Instrucciones para configurar los grupos en Azure AD |[¿Cómo tooCreate grupos de seguridad](active-directory-accessmanagement-manage-groups.md)<br /><br />[¿Cómo tooDesignate propietarios de un grupo](active-directory-accessmanagement-managing-group-owners.md)<br /><br />[¿Cómo tooUse Hola "todos" grupo de usuarios](active-directory-accessmanagement-dedicated-groups.md) |
| Use grupos dinámicos tooautomatically rellenar los miembros del grupo mediante las reglas de pertenencia basada en atributos |[Uso de atributos para crear reglas avanzadas](active-directory-accessmanagement-groups-with-advanced-rules.md)<br /><br />[Solución de problemas de pertenencias a grupos dinámicos](active-directory-accessmanagement-troubleshooting.md) |

La administración de acceso a aplicaciones basado en grupos está disponible para [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) y [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/). La administración de grupos de autoservicio, la administración de aplicaciones de autoservicio y los grupos dinámicos son características de [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

### <a name="b2b-collaboration-enable-partner-access-tooapplications"></a>Colaboración B2B: Habilitar la tooapplications de acceso de socios comerciales
Si su empresa se ha asociado a otras compañías, es probable que necesite toomanage asociado acceso tooyour las aplicaciones corporativas. Colaboración Azure de Active Directory B2B proporciona un tooshare de forma fácil y segura las aplicaciones con socios comerciales.

| Guía de artículos |  |
|:---:| --- |
| Información general sobre las diferentes características de Azure AD que pueden ayudarle a administrar usuarios externos como asociados, clientes, etc. |[Comparación de funcionalidades para administrar identidades externas con Azure Active Directory](active-directory-b2b-compare-external-identities.md) |
| Una introducción tooB2B colaboración y cómo se inicia tooget |[Vista previa de la colaboración B2B de Azure AD: integración sencilla y segura de los asociados de la nube](active-directory-b2b-what-is-azure-ad-b2b.md)<br /><br />[Colaboración B2B de Azure Active Directory](active-directory-b2b-collaboration-overview.md) |
| Un análisis más profundo en colaboración B2B de Azure AD y cómo toouse, |[Vista previa de la colaboración B2B de Azure AD: funcionamiento](active-directory-b2b-how-it-works.md)<br /><br />[Limitaciones actuales de la colaboración B2B de Azure AD](active-directory-b2b-current-limitations.md)<br /><br />[Tutorial detallado del uso de la colaboración B2B de Azure AD](active-directory-b2b-detailed-walkthrough.md) |
| Artículos de referencia con detalles técnicos acerca del funcionamiento de la colaboración B2B de Azure AD |[Vista previa de la colaboración B2B de Azure AD: formato de archivo CSV](active-directory-b2b-references-csv-file-format.md)<br /><br />[Vista previa de la colaboración B2B de Azure AD: cambios en los atributos de objeto de usuario externo](active-directory-b2b-references-external-user-object-attribute-changes.md)<br /><br />[Formato de token de usuario externo para usuarios asociados](active-directory-b2b-references-external-user-token-format.md) |

La colaboración B2B está disponible actualmente para [todas las ediciones de Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="access-panel-a-portal-for-accessing-apps-and-self-service-features"></a>Panel de acceso: portal para acceder a las aplicaciones y características de autoservicio
Hola Panel de acceso de Azure AD es donde los usuarios finales pueden iniciar sus aplicaciones y acceso Hola características de autoservicio que les permitan toomanage sus aplicaciones y las pertenencias a grupos. Además toohello Panel de acceso, otras opciones para tener acceso a aplicaciones habilitadas para SSO se incluyen en la siguiente lista de Hola.

| Guía de artículos |  |
|:---:| --- |
| Una comparación de hello diferentes opciones disponibles para la implementación de aplicaciones de inicio de sesión único toousers |[Implementación de aplicaciones integradas de Azure AD tooUsers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) |
| Información general de hello Panel de acceso y su equivalente Mis de aplicaciones móviles |[Introducción tooAccess Panel y mis aplicaciones](active-directory-saas-access-panel-introduction.md)<br />— [iOS](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.myapps) |
| Cómo las aplicaciones de Azure AD tooaccess de Hola sitio Web de Office 365 |[Uso de hello iniciador de aplicaciones de Office 365](https://support.office.com/en-us/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a) |
| Cómo las aplicaciones de Azure AD tooaccess de Hola aplicaciones móviles de Intune Managed Browser |[Administrar el acceso a Internet mediante directivas de explorador administrado con Microsoft Intune](https://technet.microsoft.com/en-us/library/dn878029.aspx)<br />— [iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser) |
| Cómo aplicaciones de Azure AD tooaccess con vínculos profundos tooinitiate inicio de sesión único |[Obtención de vínculos de inicio de sesión directos tooYour aplicaciones](active-directory-appssoaccess-whatis.md#direct-sign-on-links-for-federated-password-based-or-existing-apps) |

El panel de acceso está disponible para [todas las ediciones de Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="reports-easily-audit-app-access-changes-and-monitor-sign-ins-tooapps"></a>Informes: Fácilmente auditar los cambios de acceso de aplicación y supervisar los inicios de sesión tooapps
Azure Active Directory proporciona varios informes y alertas toohelp supervisar tooapplications de acceso de su organización. Puede recibir alertas para las aplicaciones de tooyour de inicios de sesión anómalos, y puede realizar un seguimiento de cuándo y por qué ha cambiado la aplicación de tooan de acceso de un usuario.

| Guía de artículos |  |
|:---:| --- |
| Información general de hello características de informes de Azure Active Directory |[Introducción a los informes de Azure Active Directory](active-directory-reporting-getting-started.md) |
| ¿Cómo toomonitor Hola inicios de sesión y el uso de aplicaciones de los usuarios |[Visualización de los informes de acceso y uso](active-directory-view-access-usage-reports.md) |
| Seguimiento de cambios realizado toowho puede tener acceso a una aplicación concreta |[Eventos del Informe de auditoría de Azure Active Directory](active-directory-reporting-audit-events.md) |
| Exportar datos de Hola de estas herramientas de tooyour preferido de informes mediante Hola API de informes |[Introducción a Hola API Reporting de Azure AD](active-directory-reporting-api-getting-started.md) |

toosee qué informes se incluyen con las diferentes ediciones de Azure Active Directory, [haga clic aquí](active-directory-view-access-usage-reports.md).

## <a name="see-also"></a>Otras referencias
[¿Qué es Azure Active Directory?](active-directory-whatis.md)

[Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/)

[Servicios de dominio de Azure Active Directory](https://azure.microsoft.com/services/active-directory-ds/)

[Azure Multi-Factor Authentication](https://azure.microsoft.com/services/multi-factor-authentication/)

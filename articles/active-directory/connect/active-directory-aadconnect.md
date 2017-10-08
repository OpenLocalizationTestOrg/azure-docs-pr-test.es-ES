---
title: "Conexión de Active Directory con Azure Active Directory | Microsoft Docs"
description: "Azure AD Connect integrará sus directorios locales con Azure Active Directory. Esto le permite tooprovide una identidad común para las aplicaciones de Office 365, Azure y SaaS integrada con Azure AD."
keywords: "Introducción tooAzure AD Connect, información general de Azure AD Connect, ¿qué es Azure AD Connect, instalar active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 59bd209e-30d7-4a89-ae7a-e415969825ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e49f2af4b67e9ed3ad093888541da7c82af0e052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-on-premises-directories-with-azure-active-directory"></a>Integración de los directorios locales con Azure Active Directory
Azure AD Connect integrará sus directorios locales con Azure Active Directory. Esto le permite tooprovide una identidad común para los usuarios para las aplicaciones de Office 365, Azure y SaaS integrada con Azure AD. Este tema le guiará a través de hello planeación, implementación y pasos de la operación. Es una colección de vínculos toohello temas relacionados toothis área.

> [!IMPORTANT]
> [Azure AD Connect se Hola tooconnect de mejor manera su directorio local con Azure AD y Office 365. Se trata de un tooAzure de tooupgrade mucho tiempo AD Connect de Windows Azure Active Directory Sync (DirSync) o sincronización de Azure AD como estas herramientas están ahora en desuso y alcanzará el final del soporte técnico de 13 de abril de 2017.](active-directory-aadconnect-dirsync-deprecated.md)
> 
> 

![Qué es Azure AD Connect](media/active-directory-aadconnect/arch.png)

## <a name="why-use-azure-ad-connect"></a>¿Por qué usar Azure AD Connect?
La integración de directorios locales con Azure AD hace que los usuarios sean más productivos al proporcionar una identidad común para acceder tanto a los recursos en la nube como a los locales. Los usuarios y las organizaciones pueden sacar provecho de siguientes hello:

* Los usuarios pueden utilizar una sola identidad tooaccess local las aplicaciones y servicios, como Office 365 en la nube.
* Única herramienta tooprovide una experiencia de facilitar la implementación de sincronización e inicio de sesión.
* Proporciona capacidades más recientes de Hola para los escenarios. Azure AD Connect sustituye a las versiones anteriores de las herramientas de integración de identidades, como DirSync y Sincronización de Azure AD. Para más información, consulte [Identidades híbridas: comparación de las herramientas para la integración de directorios de identidades híbridas](../active-directory-hybrid-identity-design-considerations-tools-comparison.md).

### <a name="how-azure-ad-connect-works"></a>Cómo funciona Azure AD Connect
Azure Active Directory Connect se compone de tres componentes principales: servicios de sincronización de hello, componente opcional de los servicios de federación de Active Directory de Hola y componente de supervisión de hello denominado [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md) .

<center>![Pila de Azure AD Connect](./media/active-directory-aadconnect-how-it-works/AADConnectStack2.png)
</center>

* Sincronización: este componente es responsable de la creación de usuarios, grupos y otros objetos. También es responsable de asegurarse de que la información de identidad para los usuarios locales y grupos coincidentes en la nube Hola.
* AD FS - Federation es una parte opcional de Azure AD Connect y puede ser un entorno híbrido con una implementación local de tooconfigure usado infraestructura de AD FS. Esto puede utilizarse por las organizaciones tooaddress las implementaciones complejas, como la unión a un dominio SSO, cumplimiento de directiva de inicio de sesión AD y tarjeta inteligente o entidad 3rd MFA.
* Supervisión de estado - Azure AD Connect Health puede proporcionar supervisión sólida y proporcionar una ubicación central en hello tooview portal Azure esta actividad. Para más información, consulte [Supervisión de la infraestructura de identidad local y los servicios de sincronización en la nube](../connect-health/active-directory-aadconnect-health.md).

## <a name="install-azure-ad-connect"></a>Instalación de Azure AD Connect
Encontrará la descarga de Hola para Azure AD Connect en [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=615771).

| Solución | Escenario |
| --- | --- |
| Antes de empezar: [Requisitos previos de Azure AD Connect](active-directory-aadconnect-prerequisites.md) |<li>Pasos toocomplete antes de empezar tooinstall Azure AD Connect.</li> |
| [Configuración rápida](active-directory-aadconnect-get-started-express.md) |<li>Si tiene un único bosque de AD, a continuación, esto se recomienda opción toouse Hola.</li> <li>Usuario iniciar sesión con hello misma contraseña mediante la sincronización de contraseña.</li> |
| [Configuración personalizada](active-directory-aadconnect-get-started-custom.md) |<li>Se usa cuando se tienen varios bosques. Admite muchas [topologías](active-directory-aadconnect-topologies.md) locales.</li> <li>Personalice la opción de inicio de sesión, como ADFS para la federación, o bien use un proveedor de identidades de terceros.</li> <li>Personalice las características de sincronización, como el filtrado y la escritura diferida.</li> |
| [Actualización desde DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Se usa cuando se tiene un servidor de DirSync existente que ya se está ejecutando.</li> |
| [Actualización desde Azure AD Sync o Azure AD Connect](active-directory-aadconnect-upgrade-previous-version.md) |<li>Hay varios métodos diferentes entre los que puede elegir en función de sus preferencias.</li> |

[Después de la instalación](active-directory-aadconnect-whats-next.md) debe comprobar es funciona según lo previsto y asignar licencias a los usuarios de toohello.

### <a name="next-steps-tooinstall-azure-ad-connect"></a>Pasos siguientes tooInstall Azure AD Connect
|Tema. |Vínculo|  
| --- | --- |
|Descarga de Azure AD Connect | [Descarga de Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Instalación mediante configuración rápida | [Instalación rápida de Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|Instalación mediante configuración personalizada | [Instalación personalizada de Azure AD Connect](./active-directory-aadconnect-get-started-custom.md)|
|Actualización desde DirSync | [Actualización desde la herramienta de sincronización de Azure AD (DirSync)](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Después de la instalación | [Comprobar la instalación de Hola y asignar licencias](active-directory-aadconnect-whats-next.md)|

### <a name="learn-more-about-install-azure-ad-connect"></a>Más información sobre la instalación de Azure AD Connect
También puede tooprepare para [operativa](active-directory-aadconnectsync-operations.md) preocupaciones. Conviene toohave un servidor de modo de espera, por lo que fácilmente puede descender si hay un [ante desastres](active-directory-aadconnectsync-operations.md#disaster-recovery). Si tiene previsto cambios frecuentes en la configuración de toomake, debe planear un [modo de almacenamiento provisional](active-directory-aadconnectsync-operations.md#staging-mode) server.

|Tema. |Vínculo|  
| --- | --- |
|Topologías admitidas | [Topologías de Azure AD Connect](active-directory-aadconnect-topologies.md)|
|Conceptos de diseño | [Conceptos de diseño de Azure AD Connect](active-directory-aadconnect-design-concepts.md)|
|Cuentas usadas para la instalación | [Más información sobre las credenciales y los permisos de Azure AD Connect](./active-directory-aadconnect-accounts-permissions.md)|
|Planeación operativa | [Sincronización de Azure AD Connect: tareas y consideraciones operativas](active-directory-aadconnectsync-operations.md)|
|Opciones de inicio de sesión de usuario | [Opciones para el inicio de sesión de los usuarios en Azure AD Connect](active-directory-aadconnect-user-signin.md)|

## <a name="configure-sync-features"></a>Configuración de características de sincronización
Azure AD Connect incluye varias características que puede activar de manera opcional o que están habilitadas de forma predeterminada. En algunas ocasiones, ciertas características pueden requerir configuración adicional en determinados escenarios y topologías.

[Filtrado](active-directory-aadconnectsync-configure-filtering.md) se utiliza cuando desea toolimit qué objetos están sincronizados tooAzure AD. De forma predeterminada todos los usuarios, contactos, grupos y equipos de Windows 10 están sincronizados. Puede cambiar Hola filtrado basado en atributos, las unidades organizativas o dominios.

[Sincronización de contraseña](active-directory-aadconnectsync-implement-password-synchronization.md) sincroniza los hash de contraseña de hello en Active Directory tooAzure AD. por el usuario final de Hello sirve Hola misma contraseña local y en la nube de hello pero solo administrarlo en una ubicación. Ya que usa su Active Directory local como entidad de hello, también puede utilizar su propia directiva de contraseña.

[Escritura diferida de contraseñas](../active-directory-passwords-getting-started.md) permitir su toochange a los usuarios y restablecer sus contraseñas en la nube de Hola y aplicar su directiva de contraseña local.

[Reescritura de dispositivos](active-directory-aadconnect-feature-device-writeback.md) permitirá un dispositivo registrado en toobe de Azure AD reescrito tooon local de Active Directory para que se pueda usar para el acceso condicional.

Hola [evitar eliminaciones accidentales](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) característica está activada de forma predeterminada y protege el directorio en la nube de muchas eliminaciones en hello mismo tiempo. De forma predeterminada permite 500 eliminaciones por cada ejecución. Puede cambiar esta configuración según el tamaño de la organización.

[La actualización automática](active-directory-aadconnect-feature-automatic-upgrade.md) está habilitada de forma predeterminada para las instalaciones de la configuración rápida y garantiza su Azure AD Connect siempre está en funcionamiento toodate con la versión más reciente de Hola.

### <a name="next-steps-tooconfigure-sync-features"></a>Características de sincronización de tooconfigure de pasos siguientes
|Tema. |Vínculo|  
| --- | --- |
|Configuración del filtrado | [Azure AD Connect Sync: configuración del filtrado](active-directory-aadconnectsync-configure-filtering.md)|
|sincronización de contraseñas | [Sincronización de Azure AD Connect: implementación de la sincronización de contraseñas](active-directory-aadconnectsync-implement-password-synchronization.md)|
|escritura diferida de contraseñas | [Introducción a la administración de contraseñas](../active-directory-passwords-getting-started.md)|
|reescritura de dispositivos | [Habilitación de escritura diferida de dispositivos en Azure AD Connect](active-directory-aadconnect-feature-device-writeback.md)|
|evitar eliminaciones accidentales | [Sincronización de Azure AD Connect: cómo evitar eliminaciones accidentales](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)|
|actualización automática | [Azure AD Connect: Actualización automática](active-directory-aadconnect-feature-automatic-upgrade.md)|

## <a name="customize-azure-ad-connect-sync"></a>Personalización de Azure AD Connect Sync
Azure AD Connect sync viene con una configuración predeterminada que es toowork previsto para la mayoría de los clientes y topologías. Pero siempre existen situaciones donde la configuración predeterminada de hello no funciona y se deban ajustar. Es cambios toomake compatibles como documentados en esta sección y los temas vinculados.

Si no ha trabajado con una topología de sincronización antes de que desee conceptos básicos de toostart toounderstand Hola y Hola términos que se usan como se describe en hello [conceptos técnicos](active-directory-aadconnectsync-technical-concepts.md). Azure AD Connect es la evolución de Hola de MIIS2003, ILM2007 y FIM2010. Aunque algunas cosas son idénticas, muchas también han cambiado.

Hola [configuración predeterminada](active-directory-aadconnectsync-understanding-default-configuration.md) se da por supuesto puede haber más de un bosque en la configuración de Hola. En esas topologías un objeto de usuario se puede representar como un contacto de otro bosque. usuario de Hello también podría tener un buzón vinculado en otro bosque de recursos. comportamiento de Hola de configuración predeterminada de Hola se describe en [usuarios y contactos](active-directory-aadconnectsync-understanding-users-and-contacts.md).

modelo de configuración de Hello sincronizada se denomina [aprovisionamiento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md). Hello flujos de atributos avanzados usa [funciones](active-directory-aadconnectsync-functions-reference.md) tooexpress atributo transformaciones. Puede ver y examinar Hola toda configuración mediante herramientas que se incluye con Azure AD Connect. Si necesita toomake cambios de configuración, asegúrese de que siga hello [prácticas recomendadas](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) por lo que es más fácil tooadopt nuevas versiones.

### <a name="next-steps-toocustomize-azure-ad-connect-sync"></a>Pasos siguientes toocustomize Azure AD Connect sync
|Tema. |Vínculo|  
| --- | --- |
|Todos los artículos de sincronización de Azure AD Connect | [Sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md)|
|conceptos técnicos | [Azure AD Connect Sync: conceptos técnicos](active-directory-aadconnectsync-technical-concepts.md)|
|Configuración predeterminada de Hola de descripción | [Azure AD Connect sync: configuración predeterminada de Hola de descripción](active-directory-aadconnectsync-understanding-default-configuration.md)|
|Descripción de usuarios y contactos | [Azure AD Connect Sync: descripción de usuarios y contactos](active-directory-aadconnectsync-understanding-users-and-contacts.md)|
|aprovisionamiento declarativo | [Sincronización de Azure AD Connect: conocimiento de expresiones de aprovisionamiento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)|
|Cambiar la configuración predeterminada de Hola | [Procedimientos recomendados para cambiar la configuración predeterminada de Hola](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)|

## <a name="configure-federation-features"></a>Configuración de características de federación
AD FS pueden ser configurado toosupport [varios dominios](active-directory-aadconnect-multiple-domains.md). Por ejemplo podría tener varios dominios superiores debe toouse para la federación.

Si el servidor de ADFS no ha sido configurado tooautomatically actualizar certificados de Azure AD o si usa una solución de ADFS no, a continuación, se le notificará cuando haya demasiado[actualizar certificados](active-directory-aadconnect-o365-certs.md).

### <a name="next-steps-tooconfigure-federation-features"></a>Características de federación de tooconfigure de pasos siguientes
|Tema. |Vínculo|  
| --- | --- |
|Todos los artículos de AD FS | [Azure AD Connect y la federación](active-directory-aadconnectfed-whatis.md)|
|Configuración de AD FS con subdominios | [Compatibilidad con varios dominios para la federación con Azure AD](active-directory-aadconnect-multiple-domains.md)|
|Administrar una granja de servidores de AD FS | [Administración y personalización de AD FS con Azure AD Connect](active-directory-aadconnect-federation-management.md)|
|Actualización manual de certificados de federación | [Renovación de certificados de federación para Office 365 y Azure AD](active-directory-aadconnect-o365-certs.md)|

## <a name="more-information-and-references"></a>Más información y referencias
|Tema. |Vínculo|  
| --- | --- |
|Historial de versiones | [Historial de versiones](active-directory-aadconnect-version-history.md)|
|Comparación de DirSync, Sincronización de Azure AD y Azure AD Connect | [Comparación de las herramientas para la integración de directorios](../active-directory-hybrid-identity-design-considerations-tools-comparison.md)|
|Lista de compatibilidad no de AD FS para Azure AD | [Lista de compatibilidad de federación de AD Azure](active-directory-aadconnect-federation-compatibility.md)|
|Configuración de un IdP de SAML 2.0|[Uso de un proveedor de identidades (IdP) de SAML 2.0 para el inicio de sesión único](active-directory-aadconnect-federation-saml-idp.md)|
|Atributos sincronizados | [Atributos sincronizados](active-directory-aadconnectsync-attributes-synchronized.md)|
|Supervisión del uso de Azure AD Connect Health | [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md)|
|Preguntas frecuentes | [Preguntas más frecuentes sobre Azure AD Connect](active-directory-aadconnect-faq.md)|

**Recursos adicionales**

Encender 2015 presentación sobre cómo extender la nube de toohello de directorios locales.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3862/player]
> 
> 


---
title: "aaaAzure identidad y acceso prácticas recomendadas de seguridad | Documentos de Microsoft"
description: "Este artículo proporciona un conjunto de procedimientos recomendados para la administración de identidades y la seguridad del control de acceso mediante las funcionalidades integradas de Azure."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 07d8e8a8-47e8-447c-9c06-3a88d2713bc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/30/2017
ms.author: yurid
ms.openlocfilehash: af07dfda84758b9124641078ac8f696f725f2bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-and-access-control-security-best-practices"></a>Procedimientos recomendados para la administración de identidades y la seguridad del control de acceso en Azure
Muchos consideran toobe Hola nuevo límite de la capa de identidad para la seguridad, asumir ese rol desde la perspectiva centrada en la red tradicional de Hola. Esta evolución de pivot principal de Hola para atención de seguridad y sus inversiones proceden de hecho de Hola que se han vuelto cada vez más porosos los perímetros de red y esa defensa perimetral no sea lo más eficaz que tenían una vez toohello anterior explosión de [BYOD](http://aka.ms/byodcg) dispositivos y aplicaciones en la nube.

En este artículo, veremos un conjunto de procedimientos recomendados para la seguridad del control de acceso y la administración de identidades en Azure. Estas prácticas recomendadas se derivan de nuestra experiencia con [Azure AD](../active-directory/active-directory-whatis.md) y experiencias de Hola de clientes como usted mismo.

Para cada procedimiento recomendado, explicaremos:

* ¿Qué recomienda Hola
* ¿Por qué desea tooenable este procedimiento recomendado
* ¿Qué podría ser resultado de hello si no se recomienda tooenable Hola
* Procedimiento recomendado de las alternativas posibles toohello
* ¿Cómo puede obtener información práctica recomendada de hello tooenable

Esta administración de identidades de Azure y control de acceso seguridad artículo de procedimientos recomendados se basa en una opinión de consenso y capacidades de la plataforma Windows Azure y conjuntos de características, tal como aparecen en tiempo de Hola que se escribió este artículo. Las opiniones y las tecnologías que cambian con el tiempo y este artículo será esos cambios se actualizaron en un tooreflect de forma periódica.

Los procedimientos recomendados para la seguridad del control de acceso y la administración de identidades en Azure que se describen en este artículo son:

* Centralización de la administración de identidades
* Habilitación del inicio de sesión único (SSO)
* Implementación de la administración de contraseñas
* Aplicación de Multi-Factor Authentication (MFA) para los usuarios
* Uso del control de acceso basado en rol (RBAC)
* Control de las ubicaciones donde se crean los recursos mediante Resource Manager
* Funciones de identidad de tooleverage de guía a los desarrolladores de aplicaciones SaaS
* Supervisión activa de actividades sospechosas

## <a name="centralize-your-identity-management"></a>Centralización de la administración de identidades
Un paso importante para proteger su identidad es tooensure que TI puede administrar cuentas en una sola ubicación con respecto a donde se creó esta cuenta. Mientras mayoría Hola de empresas de hello las organizaciones de TI tendrán su cuenta principal directorio local, las implementaciones de nube híbrida están en aumento de Hola y es importante comprender cómo toointegrate locales y directorios en la nube y proporcione un experiencia sin problemas toohello al usuario final.

tooaccomplish esto [identidad híbrida](../active-directory/active-directory-hybrid-identity-design-considerations-overview.md) escenario recomendamos dos opciones:

* Sincronizar el directorio local con el directorio en la nube mediante Azure AD Connect
* Federar la identidad local con su directorio en la nube con [Servicios de federación de Active Directory](https://msdn.microsoft.com/library/bb897402.aspx) (AD FS)

Las organizaciones que no cumplan toointegrate que su identidad local con su identidad de nube experimentarán aumentaron administrativas sobrecarga en la administración de cuentas, lo que aumenta la probabilidad de Hola de errores y las infracciones de seguridad.

Para obtener más información acerca de la sincronización de Azure AD, lea el artículo de hello [integrar las identidades locales con Azure Active Directory](../active-directory/active-directory-aadconnect.md).

## <a name="enable-single-sign-on-sso"></a>Habilitación del inicio de sesión único (SSO)
Cuando haya varios toomanage de directorios, esta se convierte en un problema administrativo no solo de TI, sino también para los usuarios finales que tendrán tooremember varias contraseñas. Mediante el uso de [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) proporcionará a los usuarios capacidad Hola de uso hello mismo conjunto de credenciales en toosign y acceder a recursos de Hola que necesitan, sin importar donde este recurso es ubicarse localmente o en la nube de Hola.

Usar SSO tooenable usuarios tooaccess sus [aplicaciones SaaS](../active-directory/active-directory-appssoaccess-whatis.md) basándose en sus cuentas profesionales en Azure AD. Esto no solo es aplicable a las aplicaciones para SaaS de Microsoft, sino también a otras aplicaciones, como [Google Apps](../active-directory/active-directory-saas-google-apps-tutorial.md) y [Salesforce](../active-directory/active-directory-saas-salesforce-tutorial.md). La aplicación puede ser toouse configurado Azure AD como un [identidad basado en SAML](../active-directory/fundamentals-identity.md) proveedor. Como un control de seguridad, Azure AD no emita un token permitiéndoles toosign en aplicación Hola a menos que se les ha concedido acceso mediante Azure AD. Puede concederles acceso directamente o a través de un grupo del que sean miembros.

> [!NOTE]
> Hola decisión toouse SSO afectará a cómo integrar su directorio local con su directorio en la nube. Si desea que el SSO, deberá toouse federación, porque solo proporcionará la sincronización de directorios [misma experiencia de inicio de sesión](../active-directory/active-directory-aadconnect.md).
>
>

Las organizaciones que no aplican SSO para sus usuarios y las aplicaciones son más expuesto tooscenarios donde los usuarios tendrán varias contraseñas que directamente aumenta la probabilidad de Hola de los usuarios volver a usar contraseñas o utilizar contraseñas poco seguras.

Se puede obtener más información acerca de SSO de AD de Azure, lea el artículo de hello [personalización con Azure AD Connect y administración de AD FS](../active-directory/active-directory-aadconnect-federation-management.md).

## <a name="deploy-password-management"></a>Implementación de la administración de contraseñas
En escenarios donde tiene varios inquilinos o desea tooenable demasiado[restablecer su propia contraseña](../active-directory/active-directory-passwords-update-your-own-password.md), es importante que utilice un abuso tooprevent de directivas de seguridad adecuadas. En Azure puede aprovechar la capacidad de restablecimiento de contraseña de autoservicio de Hola y personalizar toomeet de opciones de seguridad de hello sus requisitos empresariales.

Es especialmente importante tooobtain comentarios con respecto a estos usuarios y aprender de sus experiencias tal y como lo intentan tooperform estos pasos. Según estas experiencias, elaborar un plan toomitigate posibles problemas que pueden producirse durante la implementación de Hola para un grupo más amplio. También se recomienda que utilice hello [informe actividad del registro de restablecimiento de contraseña](../active-directory/active-directory-passwords-get-insights.md) toomonitor a los usuarios de Hola que se va a registrar.

Las organizaciones que desean tooavoid contraseña cambiar las llamadas de soporte técnico, pero permiten a los usuarios tooreset sus propias contraseñas son más susceptibles de sufrir tooa superior llamada volumen toohello departamento de servicios debido a problemas de toopassword. En las organizaciones que tienen varios inquilinos, es imperativo que implementa este tipo de capacidad y habilitar los usuarios tooperform el restablecimiento de contraseña dentro de los límites de seguridad que se han establecido en la directiva de seguridad de Hola.

Puede aprender más acerca de cómo leer el artículo de hello restablecimiento de contraseña [implementar la administración de contraseñas y formación a los usuarios toouse](../active-directory/active-directory-passwords-best-practices.md).

## <a name="enforce-multi-factor-authentication-mfa-for-users"></a>Aplicación de Multi-Factor Authentication (MFA) para los usuarios
Para las organizaciones que necesitan toobe conformes con los estándares del sector, como [PCI DSS versión 3.2](http://blog.pcisecuritystandards.org/preparing-for-pci-dss-32), la autenticación multifactor es imprescindible tener capacidad para autenticar a los usuarios. Más allá de ser compatible con los estándares del sector, exigir a los usuarios MFA tooauthenticate también puede ayudar a tipo de robo de credenciales de las organizaciones toomitigate de ataque, como [Pass-the-Hash (PtH)](http://aka.ms/PtHPaper).

Al habilitar Azure MFA para los usuarios, agrega una segunda capa de inicios de sesión de seguridad toouser y las transacciones. En este caso, es posible que durante una transacción se acceda a un documento que se encuentra en un servidor de archivos o en SharePoint Online. MFA de Azure también ayuda a la probabilidad de hello tooreduce de TI que una credencial en peligro tenga los datos del acceso tooorganization.

Por ejemplo: aplicar MFA de Azure para los usuarios y configurar toouse una llamada de teléfono o un mensaje de texto como comprobación. Si se pone en peligro las credenciales del usuario de hello, el atacante hello no ser capaz de tooaccess cualquier recurso ya que no tendrá teléfono del acceso toouser. Las organizaciones que no agregan capas adicionales de protección de identidad sean más susceptibles de ataque de robo de credenciales, lo cual podría provocar el compromiso de toodata.

Una alternativa para las organizaciones que desean control de autenticación en su totalidad de hello tookeep local no se toouse [servidor Azure Multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), también denominado MFA local. Con este método, se seguirá tooenforce capaz de la autenticación multifactor, manteniendo hello MFA server local.

Para obtener más información sobre Azure MFA, lea el artículo de hello [Introducción a la autenticación multifactor Azure en la nube de hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

## <a name="use-role-based-access-control-rbac"></a>Uso del control de acceso basado en rol (RBAC)
Restringir el acceso en función de hello [necesita tooknow](https://en.wikipedia.org/wiki/Need_to_know) y [privilegios mínimos](https://en.wikipedia.org/wiki/Principle_of_least_privilege) principios de seguridad es fundamental para las organizaciones que desean tooenforce las directivas de seguridad de acceso a datos. Azure Control de acceso basado en roles (RBAC) puede ser usado tooassign permisos toousers, grupos y aplicaciones en un ámbito determinado. ámbito de Hola de una asignación de roles puede ser una suscripción, un grupo de recursos o un único recurso.

Puede aprovechar [integrada RBAC](../active-directory/role-based-access-built-in-roles.md) roles en Azure tooassign privilegios toousers. Considere el uso de *colaborador de la cuenta de almacenamiento* para operadores de la nube que necesitan cuentas de almacenamiento de toomanage y *clásico colaborador de cuenta de almacenamiento* cuentas de almacenamiento clásicas toomanage de rol. Para los operadores de nube que necesita toomanage las máquinas virtuales y la cuenta de almacenamiento, considere la posibilidad de agregarlos demasiado*colaborador de la máquina Virtual* rol.

Pueden que las organizaciones que no usan el control de acceso de datos mediante el aprovechamiento de las capacidades como RBAC se da más privilegios que los usuarios tootheir necesarios. Esto puede provocar toodata riesgo por permitir el acceso de los usuarios toocertain tipos de tipos de datos (p. ej., repercusión empresarial alta) que no tienen en primer lugar en Hola.

Se puede obtener más información sobre la RBAC de Azure, lea el artículo de hello [Azure Role-Based el Control de acceso](../active-directory/role-based-access-control-configure.md).

## <a name="control-locations-where-resources-are-created-using-resource-manager"></a>Control de las ubicaciones donde se crean los recursos mediante Resource Manager
Activación de nube operadores tooperform tareas mientras impide que interrumpir las convenciones que son necesarios toomanage recursos de su organización es muy importante. Las organizaciones que desean ubicaciones de hello toocontrol donde se crean recursos deben codificar de forma rígida estas ubicaciones.

tooachieve esto, las organizaciones pueden crear directivas de seguridad que tienen definiciones que describen las acciones de Hola o recursos que se haya denegado específicamente. Asignar esas definiciones de directiva en el ámbito de hello deseado, como suscripción de hello, grupo de recursos o un recurso individual.

> [!NOTE]
> Esto no es Hola igual como RBAC, realmente aprovecha RBAC tooauthenticate Hola los usuarios con privilegios toocreate esos recursos.
>
>

Aproveche [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) directivas personalizadas de toocreate también para escenarios donde hello organización desea tooallow operaciones sólo cuando Hola centro de costo adecuado está asociado; en caso contrario, denegará solicitud Hola.

Las organizaciones que no se controlan cómo se crean recursos son más susceptibles de sufrir toousers que puede abusar servicio hello mediante la creación de más recursos que necesitan. Protección de proceso de creación de recursos de hello es un toosecure paso importante un escenario de varios inquilinos.

Puede aprender más acerca de cómo crear directivas con el Administrador de recursos de Azure, lea el artículo de hello [recursos toomanage de directiva de uso y controlar el acceso](../azure-resource-manager/resource-manager-policy.md).

## <a name="guide-developers-tooleverage-identity-capabilities-for-saas-apps"></a>Funciones de identidad de tooleverage de guía a los desarrolladores de aplicaciones SaaS
La identidad de los usuarios se aprovechará en muchos escenarios cuando los usuarios accedan a [aplicaciones para SaaS](https://azure.microsoft.com/marketplace/active-directory/all/) que se puedan integrar con directorios locales o en la nube. En primer lugar y ante todo, se recomienda que los desarrolladores usar una metodología segura toodevelop estas aplicaciones, como [del ciclo de vida de desarrollo de seguridad (SDL) de Microsoft](https://www.microsoft.com/sdl/default.aspx). Azure AD simplifica la autenticación para los desarrolladores, ya que ofrece identificación como servicio, con compatibilidad con protocolos genéricos estándar del sector como [OAuth 2.0](http://oauth.net/2/) y [OpenID Connect](http://openid.net/connect/), además de bibliotecas de código abierto para distintas plataformas.

Conseguir tooregister seguro de que una aplicación que externalice la autenticación tooAzure AD, se trata de un procedimiento obligatorio. Hola razón es porque Azure AD necesita comunicación de hello toocoordinate con la aplicación hello al control sign-on (SSO) o intercambiar los tokens. sesión del usuario de Hello expira cuando expira el período de duración de Hola de hello símbolo (token) emitido por Azure AD. Evalúe siempre si la aplicación debe usar este tiempo o si puede reducirlo. Duración de hello reducir puede actuar como una medida de seguridad que se forzará usuarios toosign out basándose en un período de inactividad.

Las organizaciones que no garantizan la identidad control tooaccess aplicaciones y no guiar a los programadores en cómo toosecurely integrar aplicaciones con su sistema de administración de identidad pueden ser de tipo de robo de toocredential más susceptible de ataque, como [débil administración de sesiones y de autenticación descrita en la parte superior del proyecto de seguridad de aplicaciones de Web abierto (OWASP) 10](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet).

Puede aprender más sobre los escenarios de autenticación para aplicaciones SaaS en [Escenarios de autenticación para Azure AD](../active-directory/active-directory-authentication-scenarios.md).

## <a name="actively-monitor-for-suspicious-activities"></a>Supervisión activa de actividades sospechosas
Según demasiado[informe de fuga de datos de 2016 de Verizon](http://www.verizonenterprise.com/verizon-insights-lab/dbir/2016/), credenciales en peligro aún está en aumento de Hola y convertirse en una de las empresas más rentables de Hola para delincuentes intrusos. Por esta razón, es importante toohave un sistema de monitor de identidad activa en el lugar al que puede detectar la actividad de un comportamiento sospechoso y desencadenar una alerta para una investigación más rápidamente. Azure AD presenta dos funcionalidades principales que pueden ayudar a las organizaciones a supervisar sus identidades: los [informes de anomalías](../active-directory/active-directory-view-access-usage-reports.md) de Azure AD Premium y funcionalidad de [protección de identidades](../active-directory/active-directory-identityprotection.md) de Azure AD.

Asegúrese de toouse seguro Hola anomalías informes tooidentify intentos toosign en [sin seguimiento](../active-directory/active-directory-reporting-sign-ins-from-unknown-sources.md), [por fuerza bruta](../active-directory/active-directory-reporting-sign-ins-after-multiple-failures.md) los ataques contra una cuenta determinada, los intentos de toosign en desde varias ubicaciones, inicie sesión en de [infectado dispositivos](../active-directory/active-directory-reporting-sign-ins-from-possibly-infected-devices.md) y direcciones IP sospechosas. Tenga en cuenta que se trata de informes. En otras palabras, debe tener los procesos y procedimientos de colocar para toorun de administradores de TI estos informes diario de Hola o a petición (normalmente en un escenario de respuesta a incidentes).

En cambio, Azure Active Directory identity protection es un sistema de supervisión active y marcará los riesgos actuales de hello en su propio panel. Además de eso, también recibirá notificaciones de resumen diarias por correo electrónico. Se recomienda que ajuste el nivel de riesgo de hello según tooyour requisitos empresariales. nivel de riesgo de Hola para un evento de riesgo es una indicación (alto, medio o bajo) de gravedad de Hola de evento de riesgo de Hola. nivel de riesgo de Hello ayuda a los usuarios de la protección de identidad a dar prioridad a acciones de Hola que deben tomar organización tootheir de tooreduce Hola riesgo.

Las organizaciones que no supervisen activamente sus sistemas de identidad corren el riesgo de comprometer las credenciales de los usuarios. Sin el conocimiento que tardan las actividades sospechosas colocar mediante estas credenciales, las organizaciones no será capaz de toomitigate este tipo de amenaza.
Puede aprender más sobre Azure Identity Protection en [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md).

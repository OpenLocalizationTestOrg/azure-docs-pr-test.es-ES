---
title: 'Servicios de dominio de Azure AD: Controladores de dominio los servicios de dominio de AD de Azure comparar tooDIY | Documentos de Microsoft'
description: "Comparación de controladores de dominio de servicios de dominio de Active Directory de Azure tooDIY"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 165249d5-e0e7-4ed1-aa26-91a05a87bdc9
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: maheshu
ms.openlocfilehash: 5e384f6a676e76e4f22ff62d4aeb578bc8481ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodecide-if-azure-ad-domain-services-is-right-for-your-use-case"></a>¿Cómo toodecide si Servicios de dominio de AD de Azure es adecuada para el caso de uso
Con los servicios de dominio de Active Directory de Azure puede implementar las cargas de trabajo en los servicios de infraestructura de Azure, sin necesidad de tooworry acerca del mantenimiento de la infraestructura de identidades de Azure. Este servicio administrado no es lo mismo que una implementación típica de Windows Server Active Directory donde los usuarios son los encargados de llevarla a cabo y administrarla. servicio de Hello es fácil toodeploy y ofrece supervisión de estado automatizado y corrección. Le estamos evolucionando constantemente Hola servicio tooadd compatibilidad con escenarios de implementación comunes.

toodecide si toouse de servicios de dominio de AD de Azure se recomienda Hola siguiendo el material de lectura:

* Ver lista de Hola de [características que ofrecen los servicios de dominio de Azure AD](active-directory-ds-features.md).
* Consulte los [escenarios de implementación comunes de Azure AD Domain Services](active-directory-ds-scenarios.md).
* Por último, [comparar la opción de servicios de dominio de AD de Azure AD personal tooa](active-directory-ds-comparison.md#compare-azure-ad-domain-services-to-diy-ad-domain-in-azure).

## <a name="compare-azure-ad-domain-services-toodiy-ad-domain-in-azure"></a>Comparar el dominio de servicios de dominio de AD de Azure AD tooDIY en Azure
Hello tabla siguiente le ayuda a decidir entre usar servicios de dominio de AD de Azure y administrar su propia infraestructura de AD en Azure.

| **Característica** | **Azure AD Domain Services** | **AD de implementación personal en máquinas virtuales de Azure** |
| --- |:---:|:---:|
| [**Servicio administrado**](active-directory-ds-comparison.md#managed-service) |**&amp;#x2713;** |**&amp;#x2715;** |
| [**Implementaciones seguras**](active-directory-ds-comparison.md#secure-deployments) |**&amp;#x2713;** |Administrador necesita la implementación de hello toosecure. |
| [**Servidor DNS**](active-directory-ds-comparison.md#dns-server) |**&amp;#x2713;** (servicio administrado) |**&amp;#x2713;** |
| [**Domain or Enterprise administrator privileges**](active-directory-ds-comparison.md#domain-or-enterprise-administrator-privileges) |**&amp;#x2715;** |**&amp;#x2713;** |
| [**Unión a un dominio**](active-directory-ds-comparison.md#domain-join) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**Autenticación de dominios mediante NTLM y Kerberos**](active-directory-ds-comparison.md#domain-authentication-using-ntlm-and-kerberos) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**Delegación limitada de Kerberos**](active-directory-ds-comparison.md#kerberos-constrained-delegation)|basada en recursos|basada en recursos y basada en cuentas|
| [**Estructura de unidad organizativa personalizada**](active-directory-ds-comparison.md#custom-ou-structure) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**Extensiones de esquema**](active-directory-ds-comparison.md#schema-extensions) |**&amp;#x2715;** |**&amp;#x2713;** |
| [**Confianzas de bosques o dominios de AD**](active-directory-ds-comparison.md#ad-domain-or-forest-trusts) |**&amp;#x2715;** |**&amp;#x2713;** |
| [**LDAP read**](active-directory-ds-comparison.md#ldap-read) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**LDAP seguro (LDAPS)**](active-directory-ds-comparison.md#secure-ldap) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**LDAP write**](active-directory-ds-comparison.md#ldap-write) |**&amp;#x2715;** |**&amp;#x2713;** |
| [**Group Policy**](active-directory-ds-comparison.md#group-policy) |**&amp;#x2713;** |**&amp;#x2713;** |
| [**Implementación distribuida geográficamente**](active-directory-ds-comparison.md#geo-dispersed-deployments) |**&amp;#x2715;** |**&amp;#x2713;** |

#### <a name="managed-service"></a>Servicio administrado
Los dominios de Azure AD Domain Services los administra Microsoft. No es necesario tooworry sobre la aplicación de revisiones, actualizaciones, supervisión, copias de seguridad y garantizar la disponibilidad de su dominio. Estas tareas de administración se ofrecen como un servicio de Microsoft Azure en los dominios administrados.

#### <a name="secure-deployments"></a>Implementaciones seguras
dominio administrado Hello es bloquear de forma segura según las recomendaciones de seguridad de Microsoft para las implementaciones de AD. Estas recomendaciones derivan de décadas del equipo de producto de hello AD de experiencia en ingeniería y compatibilidad con las implementaciones de AD. Para las implementaciones de personal, necesita implementación específica de tootake toolock pasos hacia abajo y proteger la implementación.

#### <a name="dns-server"></a>Servidor DNS
Un dominio de Azure AD Domain Services incluye servicios DNS administrados. Los miembros del grupo de 'Administradores de controlador de dominio de AAD' hello pueden administrar DNS en el dominio de hello administrado. Miembros de este grupo tienen privilegios completos de administración de DNS para el dominio administrado Hola. Administración de DNS puede realizarse mediante hello 'consola de administración de DNS"incluido en el paquete de herramientas de administración remota del servidor (RSAT) Hola.
[Más información](active-directory-ds-admin-guide-administer-dns.md)

#### <a name="domain-or-enterprise-administrator-privileges"></a>Privilegios de administrador de dominio o empresa
Estos privilegios administrados no se ofrecen en dominios administrados de AAD-DS. Las aplicaciones que requieran estos privilegios elevados no se pueden implementar en los dominios administrados de AAD-DS. Un subconjunto más pequeño de privilegios administrativos es toomembers disponible del grupo de administración delegada de hello llamado 'Administradores de controlador de dominio de AAD'. Estos privilegios incluyen privilegios tooconfigure DNS, configurar la directiva de grupo, obtienen privilegios de administrador en los equipos unidos a un dominio etcetera.

#### <a name="domain-join"></a>Unión a un dominio
Puede combinar máquinas virtuales toohello administrada toohow similar de dominio se une a equipos tooan AD dominio.

#### <a name="domain-authentication-using-ntlm-and-kerberos"></a>Autenticación de dominios mediante NTLM y Kerberos
Con los servicios de dominio de Active Directory de Azure, puede usar su tooauthenticate credenciales corporativas con dominio administrados Hola. Las credenciales se mantienen sincronizadas con el inquilino de Azure AD. Para inquilinos sincronizados, Azure AD Connect garantiza que toocredentials realizado cambios en local está sincronizado tooAzure AD. Con una configuración de dominio personal, puede que necesite tooset un dominio de AD confianza con sus instalaciones en AD para tooauthenticate a los usuarios con sus credenciales corporativas. Como alternativa, puede que necesite tooset seguridad tooensure de replicación de AD que las contraseñas de usuario sincronizan tooyour máquinas de virtuales de controlador de dominio de Azure.

#### <a name="kerberos-constrained-delegation"></a>Delegación limitada de Kerberos
No tiene privilegios de administrador de dominios en un dominio administrado de Active Directory Domain Services. Por lo tanto, no puede configurar la delegación limitada de Kerberos (tradicional) basada en cuentas. Sin embargo, puede configurar hello más segura basada en recursos de la delegación restringida.
[Más información](active-directory-ds-enable-kcd.md)

#### <a name="custom-ou-structure"></a>Estructura de unidad organizativa personalizada
Miembros del grupo de 'Administradores de controlador de dominio de AAD' hello pueden crear unidades organizativas personalizadas dominio Hola administrado. Los usuarios que creen unidades organizativas personalizadas reciben privilegios administrativos completos sobre Hola OU.
[Más información](active-directory-ds-admin-guide-create-ou.md)

#### <a name="schema-extensions"></a>Extensiones de esquema
No se puede extender el esquema de base de Hola de un dominio administrado de los servicios de dominio de AD de Azure. Por lo tanto, las aplicaciones que se basan en el esquema de tooAD extensiones (por ejemplo, nuevos atributos en el objeto de usuario de hello) no se eliminará y se hubiera desplazado dominios tooAAD DS.

#### <a name="ad-domain-or-forest-trusts"></a>Confianzas de bosques o dominios de AD
Dominios administrados no pueden ser configurado tooset las relaciones de confianza (entrada/salida) con otros dominios. Por lo tanto, los escenarios de implementación de bosque de recursos no pueden usar Azure AD Domain Services. De forma similar, las implementaciones donde prefiera no toosynchronize contraseñas tooAzure AD no pueden usar servicios de dominio de AD de Azure.

#### <a name="ldap-read"></a>Lectura LDAP
Hola administra cargas de trabajo lectura de dominio es compatible con LDAP. Por lo tanto, puede implementar las aplicaciones que realizan operaciones con dominio administrados Hola de lectura de LDAP.

#### <a name="secure-ldap"></a>LDAP seguro
Puede configurar servicios de dominio de AD de Azure tooprovide segura LDAP acceso tooyour administrado Hola de dominio, incluidas en internet.
[Más información](active-directory-ds-admin-guide-configure-secure-ldap.md)

#### <a name="ldap-write"></a>Escritura LDAP
dominio administrado Hello es de sólo lectura para los objetos de usuario. Por lo tanto, las aplicaciones que realizan operaciones de escritura LDAP en atributos de objeto de usuario de hello no funcionan en un dominio administrado. Además, las contraseñas de usuario no se pueden cambiar en el dominio administrado Hola. Otro ejemplo sería la modificación de las pertenencias a grupos o atributos de grupo de dominio administrado hello, que no se permite. Sin embargo, los cambios toouser atributos o las contraseñas que se realizan en Azure AD (a través del portal de PowerShell o SQL Azure) o de forma local se sincronizan AD toohello AAD DS administrados dominio.

#### <a name="group-policy"></a>Directiva de grupo
Hay un GPO integrado cada para los contenedores de "Equipos de AADDC" y "AADDC Users" Hola. Puede personalizar estas directivas de grupo de tooconfigure GPO integrados. Miembros del grupo de 'Administradores de controlador de dominio de AAD' hello también pueden crear GPO personalizados y vincularlas tooexisting las unidades organizativas (incluidas unidades organizativas personalizadas).
[Más información](active-directory-ds-admin-guide-administer-group-policy.md)

#### <a name="geo-dispersed-deployments"></a>Implementaciones dispersas geográficamente
Los dominios administrativos de Azure AD Domain Services están disponibles en una sola red virtual en Azure. Para escenarios que requieren dominio controladores toobe disponible en varias regiones de Azure a través de Hola a todos, configurar controladores de dominio en máquinas virtuales de IaaS de Azure podría ser una alternativa mejor Hola.


## <a name="do-it-yourself-diy-ad-deployment-options"></a>Opciones de implementación de AD personal
Puede que tenga casos de uso de la implementación en los que tenga algunas de las capacidades de Hola que ofrece una instalación de Windows Server AD. En estos casos, considere una de las siguientes opciones de personal (DIY) de Hola:

* **Dominio en la nube independiente** : puede configurar un dominio en la nube independiente con máquinas virtuales configuradas como controladores de dominio. Esta infraestructura no se integra con su entorno de AD local. Esta opción requiere un conjunto diferente de 'credenciales en la nube' toologin/administrar máquinas virtuales en la nube de Hola.
* **Implementación de bosques de recursos:** puede configurar un dominio en la topología de bosque de recursos de hello, con máquinas virtuales de Azure configuradas como controladores de dominio. Después, podrá configurar una relación de confianza de AD con su entorno de AD local. Puede que el bosque de recursos de toothis de unión al dominio equipos (máquinas virtuales de Azure) en la nube de Hola. Autenticación de usuario realiza a través en un directorio local VPN/ExpressRoute conexión tooyour.
* **Ampliar su tooAzure de dominio local:** puede conectar una red de red virtual de Azure tooyour local mediante una conexión VPN/ExpressRoute. Esta configuración permite la máquinas virtuales de Azure toobe tooyour combinadas AD local. Otra alternativa es toopromote controladores de dominio de réplica del dominio local en Azure como una máquina virtual. A continuación, puede establecer una tooreplicate en un directorio local VPN/ExpressRoute conexión tooyour. Este modo de implementación eficazmente amplía su tooAzure de dominio local.

> [!NOTE]
> Puede determinar que una opción de implementación personal es más adecuada para sus casos de uso de implementación. Considere la posibilidad de [compartir comentarios](active-directory-ds-contact-us.md) toohelp nos entender lo que sería útil características eligió servicios de dominio de AD de Azure en hello futuras. Estos comentarios nos ayudan a desarrollar Hola servicio toobetter que se adapte a que necesidades de su implementación y casos de uso.
>
>

Nos hemos publicado [directrices para implementar Windows Server Active Directory en máquinas virtuales Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx) toohelp facilitar las instalaciones de la guía.

## <a name="related-content"></a>Contenido relacionado
* [Características de Azure AD Domain Services](active-directory-ds-features.md)
* [Escenarios de implementación de Azure AD Domain Services](active-directory-ds-scenarios.md)
* [Directrices para implementar Windows Server Active Directory en máquinas virtuales de Microsoft Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)

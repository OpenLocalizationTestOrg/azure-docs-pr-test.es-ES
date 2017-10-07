---
title: "Azure Active Directory Domain Services: sincronización en dominios administrados | Microsoft Docs"
description: "Información sobre la sincronización en dominios administrados de Azure Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 57cbf436-fc1d-4bab-b991-7d25b6e987ef
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9be25b61823a6b031906f3576395782e73831fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="synchronization-in-an-azure-ad-domain-services-managed-domain"></a>Sincronización en dominios administrados de Azure AD Domain Services
Hello siguiente diagrama ilustra cómo funciona la sincronización en servicios de dominio de AD de Azure dominios administrados.

![Tipología de sincronización de Azure AD Domain Services](./media/active-directory-domain-services-design-guide/sync-topology.png)

## <a name="synchronization-from-your-on-premises-directory-tooyour-azure-ad-tenant"></a>Sincronización de su inquilino de tooyour Azure AD de directorio local
Azure AD Connect sync es toosynchronize usa cuentas de usuario, las pertenencias a grupos e inquilino de tooyour Azure AD de hashes de credenciales. Atributos de usuario de cuentas como Hola UPN y local se sincronizan SID (identificador de seguridad). Si usa servicios de dominio de AD de Azure, los valores de hash de credencial heredado necesarios para la autenticación NTLM y Kerberos son también inquilino de Azure AD tooyour sincronizados.

Si configura la escritura diferida, cambios que se producen en su directorio Azure AD se sincronizan tooyour atrás Active Directory local. Por ejemplo, si cambia la contraseña con características de cambio de contraseña de autoservicio de Azure AD, contraseña cambiada de Hola se actualiza en sus instalaciones de dominio de Active Directory.

> [!NOTE]
> Utilice siempre la versión más reciente de Hola de Azure AD Connect tooensure tiene correcciones para todos los errores conocidos.
>
>

## <a name="synchronization-from-your-azure-ad-tenant-tooyour-managed-domain"></a>Sincronización de la tooyour del inquilino de Azure AD administrados dominio
Las cuentas de usuario, las pertenencias a grupos y códigos hash de credenciales se sincronizan desde su tooyour de inquilino de Azure AD dominio administrado de los servicios de dominio de AD de Azure. Este proceso de sincronización es automático; No es necesario tooconfigure, supervisar y administrar este proceso de sincronización. Una vez completada la sincronización inicial única Hola de su directorio, se tarda aproximadamente 20 minutos para que los cambios realizados en Azure AD toobe refleja normalmente en el dominio administrado. Este intervalo de sincronización aplica los cambios de toopassword o cambia tooattributes realizadas en Azure AD.

proceso de sincronización de Hola es también un-bidireccional o unidireccional por naturaleza. El dominio administrado es, en gran medida, de solo lectura, excepto para las unidades organizativas personalizadas que cree. Por lo tanto, no se puede realizar cambios toouser atributos, las contraseñas de usuario o las pertenencias a grupos en dominio administrado Hola. Como resultado, no hay ninguna sincronización inversa de los cambios de su tooyour de espera de dominio administrados inquilino de Azure AD.

## <a name="synchronization-from-a-multi-forest-on-premises-environment"></a>Sincronización en un entorno local de varios bosques
Muchas organizaciones tienen una infraestructura de identidad local bastante compleja que consta de varios bosques de cuentas. Azure AD Connect es compatible con la sincronización de los usuarios, grupos y hashes de credenciales de inquilino de Azure AD tooyour de entornos de varios bosques.

En cambio, el inquilino de Azure AD es un espacio de nombres plano y mucho más sencillo. tooenable usuarios tooreliably acceso a las aplicaciones protegidas mediante Azure AD, resuelva los conflictos UPN entre cuentas de usuario en diferentes bosques. Los dominio administrado los servicios de dominio de AD de Azure osos cierre inquilino de Azure AD parecerse tooyour. Por lo tanto, observará una estructura plana de unidades organizativas en el dominio administrado. Todos los usuarios y grupos se almacenan dentro de hello ' AADDC' contenedor, independientemente del dominio local de Hola o desde el que se sincronizan en el bosque. Puede que haya configurado una estructura jerárquica de unidades organizativas en un dominio local. Sin embargo, el dominio administrado sigue teniendo una estructura plana de unidades organizativas.

## <a name="exclusions---what-isnt-synchronized-tooyour-managed-domain"></a>Exclusiones - lo que no está sincronizan el dominio administrado tooyour
Hello siguientes objetos o atributos no son inquilino de Azure AD tooyour sincronizada o dominio administrado tooyour:

* **Excluir atributos:** puede elegir tooexclude determinados atributos de la sincronización de Azure AD tooyour inquilino de su dominio local mediante Azure AD Connect. Estos atributos excluidos no estarán disponibles en el dominio administrado.
* **Las directivas de grupo:** las directivas de grupo configuradas en el dominio local no están sincronizados tooyour de dominio administrados.
* **Recurso compartido SYSVOL:** del mismo modo, contenido de Hola de hello recurso compartido SYSVOL en el dominio local no está sincronizada tooyour de dominio administrados.
* **Objetos de equipo:** objetos de equipo para el dominio de equipos unidos a un tooyour local no están sincronizados tooyour de dominio administrados. Estos equipos no tienen una relación de confianza con el dominio administrado y pertenecen únicamente a dominio local tooyour. En el dominio administrado, buscar objetos de equipo solo para equipos que tenga toohello explícitamente unido a un dominio administran dominio.
* **Atributos de SidHistory para usuarios y grupos:** usuario principal de Hola y los SID de su dominio local del grupo principal son dominio administrado tooyour sincronizados. Sin embargo, los atributos SidHistory existentes para usuarios y grupos no se sincronizan desde el dominio local tooyour dominio administrado.
* **Estructuras de unidades (OU) de organización:** unidades organizativas definidas en el dominio local no se sincronizan dominio administrado tooyour. Hay dos unidades organizativas integradas en el dominio administrado. De forma predeterminada, el dominio administrado tiene una estructura plana de unidades organizativas. Sin embargo puede elegir demasiado[crear una OU personalizada en el dominio administrado](active-directory-ds-admin-guide-create-ou.md).

## <a name="how-specific-attributes-are-synchronized-tooyour-managed-domain"></a>Atributos específicos están sincronizados tooyour de dominio administrados
Hello en la tabla siguiente enumera algunos atributos comunes y describe cómo están sincronizados tooyour administrado dominio.

| Atributo del dominio administrado | Origen | Notas |
|:--- |:--- |:--- |
| UPN |Atributo UPN del usuario del inquilino de Azure AD |atributo UPN de Hola de inquilino de Azure AD se sincroniza mientras es dominio tooyour administrado. Por lo tanto, hello toosign de manera más confiable en el dominio administrado tooyour usa el UPN. |
| SAMAccountName |El atributo MailNickname del usuario del inquilino de Azure AD o uno generado automáticamente |atributo de SAMAccountName de Hello es proceden de un atributo de mailNickname hello en el inquilino de Azure AD. Si dispone de varias cuentas de usuario Hola mismo atributo mailNickname, Hola SAMAccountName es autogenerado. Si hello mailNickname o el prefijo del UPN del usuario tiene más de 20 caracteres, Hola SAMAccountName es autogenerada toosatisfy Hola 20 caracteres límite atributos SAMAccountName. |
| Contraseñas |Contraseña del usuario del inquilino de Azure AD |Los hashes de credenciales necesarios para la autenticación NTLM o Kerberos (también denominados "credenciales complementarias") se sincronizan desde el inquilino de Azure AD. Si el inquilino de Azure AD es un inquilino sincronizado, estas credenciales se obtienen del dominio local. |
| SID de los grupos y usuarios primarios |Generado automáticamente |Hola SID principal para las cuentas de usuario o grupo es generado automáticamente en el dominio administrado. Este atributo no coincide con hello usuario/SID de grupo principal del objeto de hello en el entorno local de dominio de Active Directory. Esta falta de coincidencia es porque el dominio administrado hello tiene un espacio de nombres de SID diferente que su dominio local. |
| Historial de SID de usuarios y grupos |SID de usuarios y grupos primarios locales |Hola SidHistory para usuarios y grupos en el dominio administrado está establecido usuario principal de toomatch Hola correspondiente o SID de grupo en el dominio local. Esta característica ayuda a hacer elevación y-desplazamiento de local de aplicaciones toohello dominio administrado sea más fácil, ya que no es preciso recursos toore ACL. |

> [!NOTE]
> **Inicie sesión en el dominio administrado toohello con formato UPN de hello:** atributo SAMAccountName de hello puede ser generado automáticamente para algunas cuentas de usuario en el dominio administrado. Si varios usuarios han Hola mismo atributo mailNickname o los usuarios tienen demasiado larga los prefijos UPN, Hola SAMAccountName para estos usuarios puede ser generado automáticamente. Por lo tanto, Hola SAMAccountName formato (por ejemplo, ' CONTOSO100\joeuser') no es siempre un toosign de manera confiable en el dominio toohello. Los atributos SAMAccountName generados automáticamente de los usuarios pueden ser distintos de sus prefijos de UPN. Usar el formato de UPN hello (por ejemplo, 'joeuser@contoso100.com') toosign en toohello administra el dominio de forma confiable.
>
>

### <a name="attribute-mapping-for-user-accounts"></a>Asignación de atributos para cuentas de usuario
Hello en la tabla siguiente muestra cómo determinados atributos para objetos de usuario en su inquilino de Azure AD son atributos toocorresponding sincronizada en el dominio administrado.

| Atributo de usuario del inquilino de Azure AD | Atributo de usuario del dominio administrado |
|:--- |:--- |
| accountEnabled |userAccountControl (establece o borra Hola ACCOUNT_DISABLED bits) |
| city |l |
| country |co |
| department |department |
| DisplayName |DisplayName |
| facsimileTelephoneNumber |facsimileTelephoneNumber |
| givenName |givenName |
| jobTitle |título |
| mail |mail |
| mailNickname |msDS-AzureADMailNickname |
| mailNickname |SAMAccountName (a veces, puede generarse automáticamente) |
| mobile |mobile |
| objectid |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |sidHistory |
| passwordPolicies |userAccountControl (establece o borra Hola DONT_EXPIRE_PASSWORD bits) |
| physicalDeliveryOfficeName |physicalDeliveryOfficeName |
| postalCode |postalCode |
| preferredLanguage |preferredLanguage |
| state |st |
| streetAddress |streetAddress |
| surname |sn |
| telephoneNumber |telephoneNumber |
| userPrincipalName |userPrincipalName |

### <a name="attribute-mapping-for-groups"></a>Asignación de atributos de grupos
Hello en la tabla siguiente muestra atributos específicos de objetos de grupo en su inquilino de Azure AD son atributos toocorresponding sincronizada en el dominio administrado.

| Atributo de grupo del inquilino de Azure AD | Atributo de grupo del dominio administrado |
|:--- |:--- |
| DisplayName |DisplayName |
| DisplayName |SAMAccountName (a veces, puede generarse automáticamente) |
| mail |mail |
| mailNickname |msDS-AzureADMailNickname |
| objectid |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |sidHistory |
| securityEnabled |groupType |

## <a name="objects-that-are-not-synchronized-tooyour-azure-ad-tenant-from-your-managed-domain"></a>Objetos que no están sincronizados a tooyour inquilino de Azure AD desde el dominio administrado
Tal y como se describe en la sección anterior de este artículo, no hay ninguna sincronización desde su tooyour de espera de dominio administrados inquilino de Azure AD. Puede elegir demasiado[crear una unidad organizativa (UO) personalizado](active-directory-ds-admin-guide-create-ou.md) en el dominio administrado. Además, puede crear otros usuarios, grupos, cuentas de servicio o unidades organizativas en estas unidades organizativas personalizadas. Ninguno de los objetos de hello creados dentro de unidades organizativas personalizadas se sincronizan a inquilino de Azure AD tooyour atrás. Estos objetos solo están disponibles para utilizarse en el dominio administrado. Por lo tanto, estos objetos no son visibles mediante cmdlets de PowerShell de Azure AD, Azure AD Graph API o con la interfaz de usuario de administración de hello Azure AD.

## <a name="related-content"></a>Contenido relacionado
* [Características de Azure AD Domain Services](active-directory-ds-features.md)
* [Escenarios de implementación de Azure AD Domain Services](active-directory-ds-scenarios.md)
* [Consideraciones de red de Azure AD Domain Services](active-directory-ds-networking.md)
* [Introducción a Azure AD Domain Services](active-directory-ds-getting-started.md)

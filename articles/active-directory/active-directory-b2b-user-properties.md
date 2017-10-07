---
title: "aaaProperties de un usuario de la colaboración B2B de Azure Active Directory | Documentos de Microsoft"
description: "Las propiedades de un usuario de colaboración B2B de Azure Active Directory son configurables."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 78709f64430ed4c14eadf4dc257f175c24698c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="properties-of-an-azure-active-directory-b2b-collaboration-user"></a>Propiedades de un usuario de colaboración B2B de Azure Active Directory

Un usuario de colaboración de negocio a negocio (B2B) de Azure Active Directory (Azure AD) es un usuario con UserType = Guest. Este usuario invitado normalmente proviene de una organización del asociado y tiene limitado privilegios Hola invitar a directorio, de forma predeterminada.

Función hello invitar a las necesidades de organización, un usuario de la colaboración B2B de Azure AD puede estar en uno de hello siguiendo los Estados de cuenta:

- Estado 1: Alojada en una instancia externa de Azure AD y se representa como un usuario invitado en hello invitar a la organización. En este caso, usuario de B2B de hello inicia sesión con una cuenta de Azure AD que pertenece el inquilino toohello invitado. Si la organización del asociado de hello no usa Azure AD, todavía se crea el usuario guest de hello en Azure AD. requisitos de Hello son que canjear su invitación y Azure AD comprueba su dirección de correo electrónico. Esta solución también se denomina inquilino Just-In-Time (JIT) o inquilino "viral".

- Estado 2: Alojada en una cuenta de Microsoft y se representa como un usuario invitado en la organización del host Hola. En este caso, usuario guest de hello inicia sesión con una cuenta de Microsoft. Hola invitó identidades sociales del usuario (google.com o similar), que no es una cuenta de Microsoft, se crea como una cuenta de Microsoft durante la oferta canje.

- Estado 3: Alojada en Active Directory de la organización del host de hello en local y se sincronizan con Azure la organización del host de hello AD. Durante esta versión, debe usar PowerShell toomanually cambio Hola UserType de dichos usuarios en la nube de Hola.

- Estado 4: Alojada en Azure la organización de host AD con UserType = invitado y las credenciales que administra la organización del host Hola.

  ![mostrar las iniciales del invitador Hola](media/active-directory-b2b-user-properties/redemption-diagram.png)


Ahora, veamos cómo es un usuario de colaboración de B2B de Azure AD en estado 1 en Azure AD.

### <a name="before-invitation-redemption"></a>Antes del canje de la invitación

![Antes del canje de la oferta](media/active-directory-b2b-user-properties/before-redemption.png)

### <a name="after-invitation-redemption"></a>Después del canje de la invitación

![Después del canje de la oferta](media/active-directory-b2b-user-properties/after-redemption.png)

## <a name="key-properties-of-hello-azure-ad-b2b-collaboration-user"></a>Propiedades de clave de usuario de la colaboración B2B de Azure AD de Hola
### <a name="usertype"></a>UserType
Esta propiedad indica la relación de Hola de inquilinos de hello usuario toohello host. Esta propiedad puede tener dos valores:
- Miembros: Este valor indica un empleado de la organización del host de Hola y un usuario de nóminas de la organización de Hola. Por ejemplo, este usuario espera sitios que sólo toointernal acceso toohave. Este usuario no se consideraría un colaborador externo.

- Invitado: Este valor indica que un usuario que no sea considerado como empresa toohello interno, como un colaborador externo, un socio, un cliente o un usuario similar. Dicho usuario no ser tooreceive esperado memorando interno del CEO o recibir los beneficios de la empresa, por ejemplo.

  > [!NOTE]
  > Hola UserType no tiene ninguna relación toohow Hola usuario inicia sesión, el rol del directorio Hola de usuario de Hola y así sucesivamente. Esta propiedad simplemente indica la organización del host del usuario de hello relación toohello y permite la organización de hello tooenforce directivas que dependen de esta propiedad.

### <a name="source"></a>Origen
Esta propiedad indica cómo usuario Hola inicia sesión.

- Invited User: este usuario ha recibido la invitación, pero aún no la ha canjeado.

- Active Directory externo: Este usuario está alojado en una organización externa y se autentica con una cuenta de Azure AD que pertenece toohello otra organización. Este tipo de inicio de sesión corresponde tooState 1.

- Microsoft account: el usuario está alojado en una cuenta Microsoft y se autentica mediante una cuenta Microsoft. Este tipo de inicio de sesión corresponde tooState 2.

- Windows Server Active Directory: Este usuario ha iniciado sesión desde local Active Directory que pertenece toothis organización. Este tipo de inicio de sesión corresponde tooState 3.

- Azure Active Directory: Este usuario se autentica con una cuenta de Azure AD que pertenece toothis organización. Este tipo de inicio de sesión corresponde tooState 4.
  > [!NOTE]
  > Source y UserType son propiedades independientes. Un valor de Source no implica un valor concreto de UserType.

## <a name="can-azure-ad-b2b-users-be-added-as-members-instead-of-guests"></a>¿Se pueden agregar usuarios de B2B de Azure AD como miembros, en lugar de como invitados?
Normalmente, un usuario invitado y uno de B2B de Azure AD son sinónimos. Por tanto, de manera predeterminada los usuarios de colaboración de B2B de Azure AD se agregan como usuario con UserType = Guest. Sin embargo, en algunos casos, organización del asociado de hello es que un miembro de una organización de host más grande de organización toowhich Hola también pertenece. Si es así, la organización de host de hello puede querer tootreat a los usuarios en la organización del asociado de hello como miembros en lugar de los invitados. Usar hello las API de Azure AD B2B invitación Manager tooadd o invitar a un usuario de organización Hola asociada organización toohello host como un miembro.

## <a name="filter-for-guest-users-in-hello-directory"></a>Filtro para usuarios invitados en el directorio de Hola

![Filtrar usuarios invitados](media/active-directory-b2b-user-properties/filter-guest-users.png)

## <a name="convert-usertype"></a>Conversión de UserType
Actualmente, es posible que los usuarios tooconvert UserType del miembro tooGuest y viceversa mediante PowerShell. Sin embargo, Hola propiedad UserType debe organización de toohello de relación del usuario de toorepresent Hola. Por lo tanto, debe cambiar valor Hola de esta propiedad si relación Hola de organización de hello usuario toohello cambia. ¿Si se cambia la relación de saludo del usuario de hello, deben ser atendidos problemas, como si debe cambiar el nombre de entidad de seguridad de usuario (UPN) de hello? ¿Debe continuar usuario hello toohave acceso toohello mismos recursos? ¿Debe asignarse un buzón de correo? Por lo tanto, se recomienda no cambiar Hola UserType mediante PowerShell como una actividad atómica. Además, en caso de que esta propiedad se vuelva inmutable mediante PowerShell, no se recomienda depender de este valor.

## <a name="remove-guest-user-limitations"></a>Eliminación de limitaciones de usuarios invitados
Puede haber casos donde probablemente prefiera toogive los privilegios más altos de los usuarios de invitado. Puede agregar un rol de tooany de usuario de invitado e incluso eliminar restricciones de usuario de invitado de hello predeterminadas en hello directory toogive un Hola usuario mismo privilegios como miembros.

Es posible tooturn desactivar limitaciones de usuario de invitado de hello predeterminadas para que se proporciona un usuario invitado en el directorio de la empresa de Hola Hola los mismos permisos que un usuario de miembro.

![Eliminación de limitaciones de usuarios invitados](media/active-directory-b2b-user-properties/remove-guest-limitations.png)

## <a name="next-steps"></a>Pasos siguientes

Examine nuestros otros artículos sobre la colaboración B2B de Azure AD:

* [¿Qué es la colaboración B2B de Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Agregar un rol de tooa de usuario de la colaboración B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegación de las invitaciones de colaboración B2B](active-directory-b2b-delegate-invitations.md)
* [Auditoría y generación de informes de usuarios de colaboración B2B](active-directory-b2b-auditing-and-reporting.md)
* [Grupos dinámicos y colaboración B2B](active-directory-b2b-dynamic-groups.md)
* [Código de colaboración B2B y ejemplos de PowerShell](active-directory-b2b-code-samples.md)
* [Configuración de aplicaciones de SaaS para la colaboración B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokens de usuario de colaboración B2B](active-directory-b2b-user-token.md)
* [Asignación de notificaciones de usuario de colaboración B2B](active-directory-b2b-claims-mapping.md)
* [Uso compartido externo de Office 365](active-directory-b2b-o365-external-user.md)
* [Limitaciones actuales de la colaboración B2B](active-directory-b2b-current-limitations.md)

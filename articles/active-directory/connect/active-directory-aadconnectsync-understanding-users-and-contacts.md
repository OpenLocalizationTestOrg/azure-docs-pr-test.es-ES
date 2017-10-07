---
title: "Sincronización de Azure AD Connect: descripción de usuarios y contactos | Microsoft Docs"
description: Explica los usuarios y los contactos en Azure AD Connect Sync.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d204647-213a-4519-bd62-49563c421602
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: 4d80648c53a2981eb2626338913ed2282423f183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-users-and-contacts"></a>Azure AD Connect Sync: descripción de usuarios y contactos
Hay diversas razones por las que podría interesarle tener varios bosques de Active Directory y hay diversas topologías de implementación. Los modelos comunes incluyen una implementación cuenta-recurso y bosques sincronizados de lista global de direcciones tras una fusión y adquisición. Sin embargo, aunque existan modelos puros, los modelos híbridos también son comunes. configuración predeterminada de Hello en la sincronización de Azure AD Connect no supone ningún modelo concreto, pero dependiendo de cómo se ha seleccionado la coincidencia de usuario en la Guía de instalación de hello, pueden observarse comportamientos diferentes.

En este tema, veremos cómo se comporta la configuración predeterminada de hello en algunas topologías. Se pasará a través de la configuración de Hola y Hola Editor de reglas de sincronización puede ser toolook usado en la configuración de Hola.

Existen varias reglas generales Hola configuración da por supuesto:

* Independientemente de qué orden se importar desde el origen de hello directorios de Active Directory, obteniéndose Hola debe siempre se Hola mismo.
* Una cuenta activa siempre aporta información de inicio de sesión, **userPrincipalName** y **sourceAnchor** incluidos.
* Una cuenta deshabilitada aportará userPrincipalName y sourceAnchor, a menos que sea un buzón vinculado, si no hay ningún toobe cuenta activa que se encuentra.
* Una cuenta con un buzón vinculado nunca se utilizará para userPrincipalName y sourceAnchor. Se da por supuesto que más adelante se encontrará una cuenta activa.
* Un objeto de contacto puede ser aprovisionado tooAzure AD como contacto o como un usuario. No se sabe con seguridad hasta que se han procesado todos los bosques de Active Directory de origen.

## <a name="contacts"></a>Contactos
Tras una fusión o una adquisición donde la solución GALSync actúa como puente entre dos o más bosques de Exchange, es habitual que los contactos representen a un usuario en un bosque diferente. objeto de contacto de Hello siempre se une desde Hola conector espacio toohello metaverso con el atributo de correo de Hola. Si ya existe un objeto de contacto o un objeto de usuario con hello misma dirección de correo, Hola objetos se unen. Esto se configura en la regla de hello **en desde AD – Contact Join**. También hay una regla denominada **en desde AD – Contact Common** con un atributo de metaverso de flujo toohello **sourceObjectType** con constante hello **póngase en contacto con**. Esta regla tiene una precedencia muy baja por lo que si un objeto de usuario es toohello Unidos a un mismo objeto de metaverso, a continuación, regla de hello **en desde AD – User Common** aportará Hola usuario toothis propiedad Value. Con esta regla, este atributo tendrá el valor de Hola póngase en contacto con si no se ha unido ningún usuario y Hola valor del usuario si se ha encontrado al menos un usuario.

Para aprovisionar un tooAzure de objeto AD, Hola regla saliente **Out tooAAD – Contact Join** creará un objeto de contacto si hello atributo metaverso **sourceObjectType** se establece demasiado**póngase en contacto con **. Si este atributo está establecido demasiado**usuario**, a continuación, la regla de hello **Out tooAAD – User Join** creará un objeto de usuario en su lugar.
Es posible que se promueve un objeto de contacto tooUser cuando se importan y se sincronizan más directorios de origen activo.

Por ejemplo, en una topología GALSync encontraremos objetos de contacto para todos los usuarios en el segundo bosque de hello cuando Importemos el primer bosque de Hola. Esto llevará a cabo nuevos objetos de contacto en hello conector AAD. Cuando más adelante Importemos y sincronizar el segundo bosque de hello, se encontrará Hola usuarios reales y combinarlos toohello objetos de metaverso existentes. Se eliminará, a continuación, objeto de contacto de hello en AAD y creará un nuevo objeto de usuario en su lugar.

Si tiene una topología donde los usuarios se representan como contactos, asegúrese de que seleccionar toomatch a los usuarios en el atributo de correo de hello en la Guía de instalación de Hola. Si selecciona otra opción, tendrá una configuración que dependerá del orden. Los objetos de contacto siempre se unirán en el atributo de correo de hello, pero solo se unirán objetos de usuario en el atributo de correo de hello si se selecciona esta opción en la Guía de instalación de Hola. Puede, a continuación, terminará con dos objetos diferentes en el metaverso Hola con hello mismo atributo de correo electrónico si se importó el objeto de contacto de hello antes de objeto de usuario de Hola. Durante la exportación tooAzure AD, se producirá un error. Este comportamiento es así por diseño e indicaría datos incorrectos o esa topología hello no se identificó correctamente durante la instalación de Hola.

## <a name="disabled-accounts"></a>Cuentas deshabilitadas
Cuentas deshabilitadas se sincronizan también tooAzure AD. Cuentas deshabilitadas son recursos toorepresent comunes en Exchange, por ejemplo salas de conferencias. excepción de Hello son los usuarios con un buzón vinculado; como se mencionó anteriormente, nunca aprovisionarán una tooAzure cuenta AD.

Hola supone si se encuentra una cuenta de usuario deshabilitada, a continuación, no se encontrará otra cuenta activa más adelante Hola objeto y aprovisionado tooAzure AD con hello userPrincipalName y sourceAnchor que se encuentra. En caso de otra cuenta activa unirá toohello se usará el mismo objeto de metaverso, a continuación, su userPrincipalName y sourceAnchor.

## <a name="changing-sourceanchor"></a>Cambiar sourceAnchor
Cuando se ha exportado un objeto tooAzure AD, a continuación, que ya no está permitido toochange hello sourceAnchor. Cuando el objeto Hola haya estado atributo de metaverso Hola exportado **cloudSourceAnchor** se establece con hello **sourceAnchor** valor aceptado por Azure AD. Si **sourceAnchor** ha cambiado y no coincide con **cloudSourceAnchor**, regla de hello **Out tooAAD – User Join** producirá error hello **atributo sourceAnchor ha cambiado**. En este caso, se deben corregir los datos o configuración de Hola Hola así mismo sourceAnchor está presente en hello metaverso nuevo para el objeto de Hola puede volver a sincronizar.

## <a name="additional-resources"></a>Recursos adicionales
* [Sincronización de Azure AD Connect: personalización de las opciones de sincronización](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)


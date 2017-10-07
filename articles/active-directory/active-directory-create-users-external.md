---
title: aaaAdd a los usuarios de otros directorios o las empresas asociadas en Azure Active Directory | Documentos de Microsoft
description: "Explica cómo los usuarios de tooadd o cambiar la información de usuario en Azure Active Directory, incluidos los usuarios externos e invitados."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 564a04ec-53c1-470b-9ab9-f3db57da0a89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 92099e5792365c307b0f3d4f2dff5dd8424aeab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-users-from-other-directories-or-partner-companies-in-azure-active-directory"></a>Incorporación de usuarios de otros directorios o compañías asociadas en Azure Active Directory

Este artículo se explica cómo los usuarios de tooadd desde otros directorios en Azure Active Directory o agregar usuarios de empresas asociadas. Para obtener información sobre cómo agregar nuevos usuarios de su organización y agregar los usuarios que tienen cuentas de Microsoft, consulte [agregar nuevos usuarios tooAzure Active Directory](active-directory-create-users.md). 

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo. Para cómo del centro de usuarios de invitados de colaboración tooadd B2B en Azure AD Hola, administrador, consulte [¿qué es la colaboración B2B de Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)

Usuarios agregados no tienen permisos de administrador de forma predeterminada, pero puede asignar roles toothem en cualquier momento.

## <a name="add-a-user"></a>Adición de un usuario
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **Active Directory**y después abra el directorio.
3. Seleccione hello **usuarios** ficha y, a continuación, en la barra de comandos de hello, seleccione **Agregar usuario**.
4. En hello **envíenos comentarios acerca de este usuario** página, en **tipo de usuario**, seleccione:

   * **Usuario de otro directorio de Azure AD** : agrega un directorio de tooyour de cuenta de usuario que se puede generar desde otro directorio de Azure AD. Puede seleccionar un usuario de otro directorio solo si también es un miembro de ese directorio.
   * **Los usuarios en compañías asociadas** -tooinvite y autorizar el directorio de tooyour de los usuarios de empresa de socios (vea [colaboración B2B de Azure Active Directory](active-directory-b2b-what-is-azure-ad-b2b.md)). Necesitará demasiado[cargar un archivo CSV especificar direcciones de correo electrónico](active-directory-b2b-references-csv-file-format.md).
5. En el usuario de hello **perfil** , proporcione un nombre y apellido, un nombre descriptivo y un rol de usuario de hello **Roles** lista. Para obtener más información acerca de los roles del usuario y el administrador, consulte [Asignación de roles de administrador en Azure AD](active-directory-assign-admin-roles.md). Especifique si demasiado**habilitar la autenticación multifactor** para el usuario de Hola.
6. En hello **obtener contraseña temporal** página, seleccione **crear**.

> [!IMPORTANT]
> Si su organización usa más de un dominio, debe conocer Hola problemas siguientes cuando se agrega una cuenta de usuario:
>
> * cuentas de usuario de tooadd con Hola mismo nombre principal de usuario (UPN) entre dominios, **primer** agregar, por ejemplo, geoffgrisso@contoso.onmicrosoft.com, **seguido** geoffgrisso@contoso.com.
> * **No** agregue geoffgrisso@contoso.com antes de geoffgrisso@contoso.onmicrosoft.com.
>

Si cambia la información para un usuario cuya identidad se sincroniza con los servicios de Active Directory local, no se puede cambiar la información de usuario de Hola Hola portal de Azure clásico. toochange Hola información del usuario, utilice las herramientas de administración de Active Directory local.

## <a name="add-external-users"></a>Adición de usuarios externos
También puede agregar usuarios desde otro toowhich de directorio de Azure AD que pertenece o desde las empresas asociadas mediante la carga de un archivo CSV. un usuario externo, tooadd para **tipo de usuario**, especifique **usuario en otro directorio de Microsoft Azure AD** o **usuarios en compañías asociadas**.

Los usuarios de ambos tipos proceden de otro directorio y se agregan como **usuarios externos**. Los usuarios externos pueden colaborar con otros usuarios en un directorio sin ningún tooadd nuevas cuentas de requisito y las credenciales. Los usuarios externos se autentican con su directorio particular cuando inician sesión en, y que la autenticación funciona para cualquier otro toowhich de directorios que se hayan agregado.

## <a name="external-user-management-and-limitations"></a>Limitaciones y administración de usuarios externos
Cuando se agrega un usuario desde otro directorio de tooyour, ese usuario es un usuario externo en el directorio. nombre para mostrar Hello y nombre de usuario se copian desde su directorio particular y utilizados para el usuario externo de hello en el directorio. Desde ese momento, las propiedades de cuenta de usuario externo Hola son totalmente independientes. Si se realizan cambios de propiedad toohello usuario en su directorio particular, estos cambios no se propagarán toohello cuenta de usuario externo en el directorio.

Hola única vinculación entre dos cuentas de hello es que el usuario Hola siempre se autentica con su directorio particular o con su cuenta de Microsoft. Por eso no ve una contraseña de opción tooreset Hola o habilitar la autenticación multifactor para un usuario externo. Actualmente, directiva de autenticación de hello del directorio particular de Hola o cuenta de Microsoft es hello solo uno que se evalúa cuando Hola usuario inicia sesión.

> [!NOTE]
> Puede deshabilitar a usuario externo de hello en directorio de hello, que se bloquea tooyour de obtener acceso al directorio.
>
>

Si se elimina un usuario en su directorio particular o se cancela su cuenta de Microsoft, los usuarios externos de hello sigue existiendo en el directorio. Sin embargo, usuario de hello en el directorio no puede tener acceso a los recursos ya que no pueden autenticarse con una cuenta de Microsoft o un directorio particular.

### <a name="services-that-currently-support-access-by-azure-ad-external-users"></a>Servicios que actualmente permiten el acceso a los usuarios externos de Azure AD
* **Portal de Azure clásico**: permite a un usuario externo que sea un administrador de varios toomanage de directorios por cada de esos directorios.
* **SharePoint Online**: si está habilitado el uso compartido externo, permite que un usuario externo tooaccess recursos de SharePoint Online autorizado.
* **Dynamics CRM**: si la licencia de usuario de Hola se registra mediante PowerShell, permite que un usuario externo tooaccess autorizado recursos de Dynamics CRM.
* **Dynamics AX**: si la licencia de usuario de Hola se registra mediante PowerShell, permite que un usuario externo tooaccess autorizado recursos de Dynamics AX. Hola limitaciones de [usuarios externos de Azure AD](#known-limitations-of-azure-ad-external-users) tooexternal a los usuarios de Dynamics AX también se aplican.

## <a name="next-steps"></a>Pasos siguientes
* [Agregar nuevos usuarios tooAzure Active Directory](active-directory-create-users.md)
* [Administración de Azure AD](active-directory-administer.md)
* [Administración de contraseñas en Azure AD](active-directory-manage-passwords.md)
* [Administración de grupos en Azure AD](active-directory-manage-groups.md)

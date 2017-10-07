---
title: aaaAdd nuevos usuarios tooAzure Active Directory | Documentos de Microsoft
description: "Explica cómo tooadd nuevos usuarios o cambiar la información de usuario en Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a>Agregar nuevos usuarios o los usuarios con tooAzure de cuentas de Microsoft Active Directory
Agregue los usuarios toopopulate en el directorio. Este artículo se explica cómo tooadd nuevos usuarios de su organización y cómo los usuarios de tooadd que tienen cuentas de Microsoft. Para más información sobre cómo agregar usuarios de otros directorios en Azure Active Directory o cómo agregar usuarios de empresas asociadas, consulte [Incorporación de usuarios de otros directorios o compañías asociadas en Azure Active Directory](active-directory-create-users-external.md). Usuarios agregados no tienen permisos de administrador de forma predeterminada, pero puede asignar roles toothem en cualquier momento.

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo. Para tooadd un usuario en el centro de administración de hello Azure AD, vea [agregar nuevos usuarios tooAzure Active Directory](active-directory-users-create-azure-portal.md).

## <a name="add-a-user"></a>Adición de un usuario
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com) con una cuenta que sea un administrador global para el directorio de Hola.
2. Seleccione **Active Directory**y, a continuación, seleccione nombre de hello del directorio de su organización.
3. Seleccione hello **usuarios** ficha y, a continuación, en la barra de comandos de hello, seleccione **Agregar usuario**.
4. En hello **envíenos comentarios acerca de este usuario** página, en **tipo de usuario**, seleccione:

   * **Nuevo usuario de la organización** : agrega una nueva cuenta de usuario al directorio.
   * **Usuario con una cuenta Microsoft existente** : agrega un directorio de tooyour de cuenta de consumidor de Microsoft existente (por ejemplo, una cuenta de Outlook)
5. En función del **tipo de usuario**, escriba un nombre de usuario (para un nuevo usuario) o una dirección de correo electrónico (para un usuario con una cuenta de Microsoft).
6. En el usuario de hello **perfil** , proporcione un nombre y apellido, un nombre descriptivo y un rol de usuario de hello **Roles** lista. Para obtener más información acerca de los roles del usuario y el administrador, consulte [Asignación de roles de administrador en Azure AD](active-directory-assign-admin-roles.md). Especifique si demasiado**habilitar la autenticación multifactor** para el usuario de Hola.
7. En hello **obtener contraseña temporal** página, seleccione **crear**.

> [!IMPORTANT]
> Si su organización usa más de un dominio, debe conocer Hola problemas siguientes cuando se agrega una cuenta de usuario:
>
> * cuentas de usuario de tooadd con Hola mismo nombre principal de usuario (UPN) entre dominios, **primer** agregar, por ejemplo, geoffgrisso@contoso.onmicrosoft.com, **seguido** geoffgrisso@contoso.com.
> * **No** agregue geoffgrisso@contoso.com antes de geoffgrisso@contoso.onmicrosoft.com. Este orden es importante y puede ser tooundo complicada.
>
>

## <a name="change-user-information"></a>Cambiar la información de usuario
Puede cambiar cualquier atributo de usuario excepto Hola Id. de objeto.

1. Abra el directorio.
2. Seleccione hello **usuarios** ficha y nombre para mostrar, a continuación, seleccione Hola de Hola usuario desea toochange.
3. Termine los cambios y, a continuación, haga clic en **Guardar**.

Si el usuario de Hola que va a cambiar está sincronizado con los servicios de Active Directory local, no se puede cambiar la información de usuario de hello mediante este procedimiento. usuario de hello toochange, usar las herramientas de administración de Active Directory local.

## <a name="guest-user-management-and-limitations"></a>Limitaciones y administración de usuarios invitados
Las cuentas de invitado son usuarios de otros directorios que eran tooyour invitados directorio tooaccess los documentos de SharePoint, aplicaciones u otros recursos de Azure. Una cuenta de invitado en el directorio tiene el atributo de UserType subyacente establecido demasiado "Invitado". Los usuarios normales (específicamente, los miembros del directorio) tienen el atributo de UserType de Hola "Member".

Los invitados tienen un conjunto limitado de derechos en el directorio de Hola. Estos derechos limitan la capacidad de Hola para obtener información de toodiscover invitados acerca de otros usuarios en el directorio de Hola. Sin embargo, los usuarios invitados todavía pueden interactuar con hello usuarios y grupos asociados con los recursos de hello trabajan en. Los usuarios invitados pueden:

* Ver otros usuarios y grupos asociados con un toowhich de suscripción de Azure que están asignados
* Ver a miembros de Hola de toowhich de grupos que pertenecen
* Buscar otros usuarios en el directorio de hello, si saben dirección de correo electrónico completa de hello del usuario de Hola
* Ver solo un conjunto limitado de atributos de usuarios de Hola que buscan--toodisplay limitado nombre, dirección de correo electrónico, nombre principal de usuario (UPN) y foto en miniatura
* Obtener una lista de dominios comprobados en directorio Hola
* Tooapplications de consentimiento, concediéndoles Hola mismo acceso que tienen miembros en el directorio

## <a name="set-guest-user-access-policies"></a>Establecimiento de las directivas de acceso del usuario invitado
Hola **configurar** ficha de un directorio incluye opciones toocontrol acceso para usuarios invitados. Un administrador global de directorios solo puede cambiar estas opciones en el Portal de Azure clásico. Actualmente no hay ningún método de PowerShell o de API.

Hola tooopen **configurar** ficha hello Azure seleccione portal, clásico **Active Directory**y, a continuación, seleccione nombre de hello del directorio de Hola.

![Configuración de Azure Active Directory][1]

A continuación, puede editar el acceso de toocontrol de opciones de Hola para usuarios invitados.

![opciones de control de acceso para usuarios invitados][2]

## <a name="whats-next"></a>Pasos siguientes
* [Incorporación de usuarios de otros directorios o compañías asociadas en Azure Active Directory](active-directory-create-users-external.md)
* [Administración de Azure AD](active-directory-administer.md)
* [Administración de contraseñas en Azure AD](active-directory-manage-passwords.md)
* [Administración de grupos en Azure AD](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png

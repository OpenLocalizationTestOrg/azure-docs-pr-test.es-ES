---
title: "Incorporación de nuevos usuarios en Azure Active Directory | Microsoft Docs"
description: "Explica cómo agregar nuevos usuarios o cambiar la información del usuario en Azure Active Directory."
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
ms.openlocfilehash: ff4b742e772a6062885313e9bb49e55907fe125a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-to-azure-active-directory"></a>Incorporación de nuevos usuarios o de usuarios con cuentas de Microsoft en Azure Active Directory
Agregue usuarios para rellenar su directorio. Este artículo explica cómo agregar nuevos usuarios a su organización y cómo agregar a aquellos usuarios que tienen cuentas de Microsoft. Para más información sobre cómo agregar usuarios de otros directorios en Azure Active Directory o cómo agregar usuarios de empresas asociadas, consulte [Incorporación de usuarios de otros directorios o compañías asociadas en Azure Active Directory](active-directory-create-users-external.md). De forma predeterminada, los usuarios agregados no tienen permisos de administrador, pero puede asignárselos en cualquier momento.

> [!IMPORTANT]
> Microsoft recomienda administrar Azure AD con el [Centro de administración de Azure AD](https://aad.portal.azure.com) en Azure Portal en lugar de usar el portal de Azure clásico al que se hace referencia en este artículo. Para agregar un usuario en el centro de administración de Azure AD, consulte [Adición de nuevos usuarios a Azure Active Directory](active-directory-users-create-azure-portal.md).

## <a name="add-a-user"></a>Adición de un usuario
1. Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com) con una cuenta que sea administrador global para el directorio.
2. Haga clic en **Active Directory**y seleccione el nombre del directorio de su organización.
3. Seleccione la pestaña **Usuarios** y, después, en la barra de comandos, seleccione **Agregar usuario**.
4. En la página **Proporcione información sobre este usuario**, elija una de estas opciones en **Tipo de usuario**:

   * **Nuevo usuario de la organización** : agrega una nueva cuenta de usuario al directorio.
   * **Usuario con una cuenta de Microsoft existente** : agrega una cuenta de consumidor de Microsoft existente a su directorio (por ejemplo, una cuenta de Outlook).
5. En función del **tipo de usuario**, escriba un nombre de usuario (para un nuevo usuario) o una dirección de correo electrónico (para un usuario con una cuenta de Microsoft).
6. En la página **Perfiles** del usuario, especifique el nombre, los apellidos y un nombre descriptivo, así como un rol de usuario en la lista **Roles**. Para obtener más información acerca de los roles del usuario y el administrador, consulte [Asignación de roles de administrador en Azure AD](active-directory-assign-admin-roles.md). Especifique si se debe **habilitar Multi-Factor Authentication** para el usuario.
7. En la página **Obtener contraseña temporal**, seleccione **Crear**.

> [!IMPORTANT]
> Si su organización usa más de un dominio, debe tener en cuenta los siguientes problemas al agregar una cuenta de usuario:
>
> * Para agregar cuentas de usuario con el mismo nombre principal de usuario (UPN) en todos los dominios, agregue **primero**, por ejemplo, geoffgrisso@contoso.onmicrosoft.com, **seguido de** geoffgrisso@contoso.com.
> * **No** agregue geoffgrisso@contoso.com antes de geoffgrisso@contoso.onmicrosoft.com. Este orden es importante y puede ser complicado de deshacer.
>
>

## <a name="change-user-information"></a>Cambiar la información de usuario
Puede cambiar los atributos de usuario, excepto el id. objeto.

1. Abra el directorio.
2. Seleccione la pestaña **Usuarios** y, después, el nombre para mostrar del usuario que quiere cambiar.
3. Termine los cambios y, a continuación, haga clic en **Guardar**.

Si el usuario que está intentando cambiar está sincronizado con el servicio de Active Directory local, no puede cambiar la información del usuario mediante este procedimiento. Para cambiar el usuario, utilice las herramientas de administración locales de Active Directory.

## <a name="guest-user-management-and-limitations"></a>Limitaciones y administración de usuarios invitados
Las cuentas de invitado son usuarios de otros directorios que se invitaron a su directorio para que tuvieran acceso a documentos de SharePoint, aplicaciones u otros recursos de Azure. Una cuenta de invitado en su directorio tiene el atributo UserType establecido en "Guest" (Invitado). Los usuarios normales (específicamente, los miembros del directorio) tienen el valor de UserType "Miembro".

Los invitados tienen un conjunto limitado de derechos en el directorio. Estos derechos limitan la capacidad de los invitados para obtener información acerca de otros usuarios en el directorio. Sin embargo, los usuarios invitados todavía pueden interactuar con los usuarios y los grupos asociados a los recursos en los que trabajan. Los usuarios invitados pueden:

* Ver otros usuarios y grupos asociados a una suscripción de Azure a la que están asignados
* Ver los miembros de grupos a los que pertenecen
* Buscar otros usuarios en el directorio, si conocen su dirección de correo electrónico completa
* Ver solo un conjunto limitado de atributos de los usuarios que buscan: el nombre para mostrar, la dirección de correo electrónico, el nombre principal de usuario (UPN) y la foto en miniatura.
* Obtención de una lista de los dominios verificados del directorio.
* Dar su consentimiento a aplicaciones, concediéndoles el mismo acceso que tienen los miembros en su directorio.

## <a name="set-guest-user-access-policies"></a>Establecimiento de las directivas de acceso del usuario invitado
La pestaña **Configurar** de un directorio incluye opciones para controlar el acceso de los usuarios invitados. Un administrador global de directorios solo puede cambiar estas opciones en el Portal de Azure clásico. Actualmente no hay ningún método de PowerShell o de API.

Para abrir la pestaña **Configurar** del Portal de Azure clásico, seleccione **Active Directory** y luego el nombre del directorio.

![Configuración de Azure Active Directory][1]

A continuación, puede editar las opciones para controlar el acceso de usuarios invitados.

![opciones de control de acceso para usuarios invitados][2]

## <a name="whats-next"></a>Pasos siguientes
* [Incorporación de usuarios de otros directorios o compañías asociadas en Azure Active Directory](active-directory-create-users-external.md)
* [Administración de Azure AD](active-directory-administer.md)
* [Administración de contraseñas en Azure AD](active-directory-manage-passwords.md)
* [Administración de grupos en Azure AD](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png

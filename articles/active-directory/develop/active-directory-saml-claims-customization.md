---
title: notificaciones de aaaCustomizing emitidas en el token SAML de Hola para las aplicaciones previamente integradas en Active Directory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocustomize Hola emiten las notificaciones en hello token SAML para aplicaciones previamente integradas en Azure Active Directory"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f1daad62-ac8a-44cd-ac76-e97455e47803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.custom: aaddev
ms.openlocfilehash: a376318929472403e799f02fdd3fbddc91d0a70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-claims-issued-in-hello-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a>Personalizar las notificaciones emitido en hello token SAML para aplicaciones previamente integradas en Azure Active Directory
Hoy en día Azure Active Directory es compatible con miles de aplicaciones previamente integradas en hello Galería de aplicaciones de Azure AD, incluidos los superiores a 360 que admiten el inicio de sesión único mediante el protocolo de hello SAML 2.0. Cuando un usuario autentica tooan aplicación a través de Azure AD con SAML, Azure AD envía una aplicación de símbolo (token) toohello (a través de una solicitud HTTP POST). Y, a continuación, aplicación hello valida y utiliza hello toolog token Hola usuario en lugar de pedir un nombre de usuario y una contraseña. Estos tokens SAML contienen fragmentos de información sobre el usuario de hello conocido como "notificaciones".

En terminología de identidad, una notificación de"" es la información que indica el proveedor de identidades de un usuario dentro de símbolo (token) de Hola que emiten para ese usuario. En [token SAML](http://en.wikipedia.org/wiki/SAML_2.0), estos datos se encuentran normalmente en hello instrucción del atributo SAML. Hello identificador único del usuario se representa normalmente en hello que sujeto SAML también se llama como identificador de nombre.

De forma predeterminada, una aplicación de tooyour token de SAML que contenga una notificación de NameIdentifier, con un valor de nombre de usuario del usuario de hello (nombre principal de usuario AKA) en Azure AD emite Azure Active Directory. Este valor puede identificar usuario Hola. token SAML de Hello también contiene notificaciones adicionales que contiene la dirección de correo electrónico del usuario de hello, nombre y apellidos.

notificaciones de hello tooview o editar emiten en hello aplicación toohello token de SAML, aplicación Hola abierto en el portal de Azure. A continuación, seleccione hello **ver y editar todos los demás atributos de usuario** checkbox en hello **atributos de usuario** sección de la aplicación hello.

![Sección Atributos de usuario][1]

Hay dos razones posibles por las que puede necesitar notificaciones de hello tooedit emitidas en el token SAML de hello:
* aplicación Hello se ha escrito toorequire otro conjunto de notificaciones URI o valores de notificación.
* se ha implementado la aplicación Hello de forma que requiere un valor distinto de hello username (nombre principal de usuario AKA) almacenados en Azure Active Directory toobe de notificación de NameIdentifier Hola.

Puede modificar cualquiera de los valores de notificación predeterminado Hola. Seleccione la fila de la notificación de hello en la tabla de atributos de token de SAML de Hola. Se abrirá hello **Editar atributo** sección y, a continuación, se pueden editar nombre de la notificación, el valor y el espacio de nombres asociado con la notificación de Hola.

![Editar atributo de usuario][2]

También puede quitar notificaciones (que no sean NameIdentifier) mediante el menú contextual de hello, que se abre haciendo clic en hello **...**  icono.  También puede agregar nuevas notificaciones mediante hello **Agregar atributo** botón.

![Editar atributo de usuario][3]

## <a name="editing-hello-nameidentifier-claim"></a>Editar notificación de NameIdentifier Hola
problema de hello toosolve donde se haya implementado la aplicación hello con otro nombre de usuario, haga clic en hello **identificador de usuario** de lista desplegable en hello **atributos de usuario** sección. Con esta acción se mostrará un cuadro de diálogo con varias opciones:

![Editar atributo de usuario][4]

En la lista desplegable de hello, seleccione **user.mail** tooset Hola NameIdentifier notificación de dirección de correo electrónico del usuario de toobe hello en el directorio de Hola. O bien, seleccione **user.onpremisessamaccountname** nombre de cuenta SAM del usuario de tooset toohello que se sincronizó desde Azure AD local.

También puede usar Hola especial **ExtractMailPrefix()** sufijo de dominio de función tooremove Hola de dirección de correo electrónico de hello, nombre de cuenta SAM o nombre principal de usuario de Hola. Esto extrae solo la primera parte del usuario de Hola de hello el nombre que se pasa a través de (por ejemplo, "joe_smith" en lugar de joe_smith@contoso.com).

![Editar atributo de usuario][5]

También ahora hemos agregado hello **join()** Hola de función toojoin comprobado el dominio con el valor de identificador de usuario de Hola. al seleccionar función join() de hello en hello **identificador de usuario** primera instrucción select Hola identificador de usuario como nombre principal de usuario o la dirección de correo electrónico y, a continuación, en hello segunda lista desplegable, seleccione su dominio comprobado. Si selecciona Hola dirección de correo electrónico con el dominio comprobado de hello, Azure AD extrae el nombre de usuario de Hola Hola primer valor joe_smith de joe_smith@contoso.com y se anexa con contoso.onmicrosoft.com. Vea el siguiente ejemplo de Hola:

![Editar atributo de usuario][6]

## <a name="adding-claims"></a>Incorporación de notificaciones
Al agregar una notificación, puede especificar el nombre del atributo hello (que no es estrictamente necesario toofollow un modelo del identificador URI según la especificación SAML de hello). Establezca el atributo de usuario de tooany de valor de Hola que se almacena en el directorio de Hola.

![Agregar atributo de usuario][7]

Por ejemplo, necesita toosend departamento Hola Hola usuario pertenece tooin su organización como una notificación (por ejemplo, ventas). Escriba el nombre de la notificación de hello según lo esperado por la aplicación hello y, a continuación, seleccione **user.department** como valor de Hola.

> [!NOTE]
> Si no hay ningún valor almacenado para un atributo seleccionado para un usuario determinado, a continuación, esa notificación no es se emiten en token Hola.

> [!TIP]
> Hola **user.onpremisesecurityidentifier** y **user.onpremisesamaccountname** solo se admiten al sincronizar los datos de usuario de locales Active Directory con hello [Azure Herramienta de conexión de AD](../active-directory-aadconnect.md).

## <a name="restricted-claims"></a>Notificaciones restringidas

Hay algunas notificaciones restringidas en SAML. Si agrega estas notificaciones, Azure AD no enviará estas notificaciones. Estos son Hola SAML restringe el conjunto de notificaciones:

    | Tipo de notificación (URI) |
    | ------------------- |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/expired |
    | http://schemas.microsoft.com/identity/claims/accesstoken |
    | http://schemas.microsoft.com/identity/claims/openid2_id |
    | http://schemas.microsoft.com/identity/claims/identityprovider |
    | http://schemas.microsoft.com/identity/claims/objectidentifier |
    | http://schemas.microsoft.com/identity/claims/puid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1] |
    | http://schemas.microsoft.com/identity/claims/tenantid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod |
    | http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/groups |
    | http://schemas.microsoft.com/claims/groups.link |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/role |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/wids |
    | http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant |
    | http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown |
    | http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged |
    | http://schemas.microsoft.com/2014/03/psso |
    | http://schemas.microsoft.com/claims/authnmethodsreferences |
    | http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier |
    | http://schemas.microsoft.com/identity/claims/scope |

## <a name="next-steps"></a>Pasos siguientes
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](../active-directory-apps-index.md)
* [Configurar tooapplications de inicio de sesión único que no están en la Galería de aplicaciones de Azure Active Directory Hola](../active-directory-saas-custom-apps.md)
* [Cómo depurar el inicio de sesión único basado en SAML en aplicaciones de Azure Active Directory](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saml-claims-customization/user-attribute-section.png
[2]: ./media/active-directory-saml-claims-customization/edit-claim-name-value.png
[3]: ./media/active-directory-saml-claims-customization/delete-claim.png
[4]: ./media/active-directory-saml-claims-customization/user-identifier.png
[5]: ./media/active-directory-saml-claims-customization/extractemailprefix-function.png
[6]: ./media/active-directory-saml-claims-customization/join-function.png
[7]: ./media/active-directory-saml-claims-customization/add-attribute.png
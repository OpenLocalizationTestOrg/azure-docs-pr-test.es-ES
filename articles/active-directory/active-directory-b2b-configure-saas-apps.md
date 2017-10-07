---
title: "aplicaciones de SaaS aaaConfigure para la colaboración B2B de Azure Active Directory | Documentos de Microsoft"
description: "Ejemplos de código y PowerShell para la colaboración B2B de Azure Active Directory"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a>Configuración de aplicaciones de SaaS para la colaboración B2B

La colaboración de B2B de Azure Active Directory (Azure AD) funciona con la mayoría de las aplicaciones que se integran con Azure AD. En esta sección, se proporcionan las instrucciones necesarias para configurar varias aplicaciones populares de SAS para usarlas con B2B de Azure AD.

Antes de examinar las instrucciones específicas de la aplicación, estas son algunas reglas generales:

* Para la mayoría de las aplicaciones de hello, el programa de instalación de usuario debe toohappen manualmente. Es decir, los usuarios deben crearse manualmente en la aplicación hello así.

* Para las aplicaciones que admiten la instalación automática, por ejemplo, Dropbox, invitaciones independientes se crean desde las aplicaciones de Hola. Los usuarios debe ser seguro tooaccept cada invitación.

* En atributos de usuario de hello, toomitigate los problemas con el disco de perfil de usuario con sufijo (UPD) de usuarios invitados, establezca siempre **identificador de usuario** demasiado**user.mail**.


## <a name="dropbox-business"></a>Dropbox Business

tooenable toosign de los usuarios con su cuenta de organización, debe configurar manualmente Business Dropbox toouse Azure AD como proveedor de identidades de lenguaje de marcado de aserción de seguridad (SAML). Por lo tanto, si Dropbox empresariales no ha sido configurado toodo no se puede solicitar o toosign de usuarios en el uso de Azure AD de otra manera.

1. aplicación de negocio de Dropbox tooadd hello en Azure AD, seleccione **aplicaciones empresariales** en Hola panel izquierdo y, a continuación, haga clic en **agregar**.

  ![botón de "Agregar" Hello en la página de aplicaciones de empresa de Hola](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. Hola **agregar una aplicación** ventana, escriba **dropbox** en Hola cuadro de búsqueda y, a continuación, seleccione **Dropbox para empresas** en la lista de resultados de Hola.

  ![Busque "dropbox" en hello agregar una página de aplicación](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. En hello **inicio de sesión único** página, seleccione **inicio de sesión único** en Hola panel izquierdo y, a continuación, escriba **user.mail** en hello **identificador de usuario** cuadro. (de manera predeterminada se establece como UPN).

  ![Configurar inicio de sesión único para la aplicación hello](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. toodownload Hola certificado toouse para la configuración de la lista desplegable, seleccione **configurar DropBox**y, a continuación, seleccione **SAML único inicio de sesión en dirección URL del servicio** en la lista de Hola.

  ![Descargando certificado de hello para la configuración de Dropbox](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. Inicio de sesión tooDropbox con hello sesión dirección URL de hello **inicio de sesión único** página.

  ![página de Hello en el inicio de sesión de Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. En el menú de hello, seleccione **consola de administración de**.

  ![vínculo de "Consola de administración" de Hello en el menú de Dropbox de Hola](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. Hola **autenticación** cuadro de diálogo, seleccione **más**, cargar el certificado de hello y, a continuación, en hello **iniciar sesión en la dirección URL** cuadro, escriba la dirección URL de hello el inicio de sesión único SAML.

  ![Hola vínculo "Más" en el cuadro de diálogo de autenticación de hello contraído](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Hola "Inicio de sesión en URL" Hola expande el cuadro de diálogo de autenticación](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. el programa de instalación automática de usuarios tooconfigure Hola portal de Azure, seleccione **Provisioning** en hello panel izquierdo, seleccione **automática** en hello **modo de aprovisionamiento** cuadro y, a continuación, seleccione **Autorizar**.

  ![Configurar el aprovisionamiento automático de usuarios en hello portal de Azure](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

Después de que los usuarios invitados o miembro se han configurado en la aplicación de Dropbox hello, que reciben una invitación de independiente de Dropbox. toouse inicio de sesión único en Dropbox, los invitados deben Aceptar invitación Hola haciendo clic en un vínculo en ella.

## <a name="box"></a>Box
Puede permitir a los usuarios tooauthenticate cuadro invitado a los usuarios con su cuenta de Azure AD utilizando federación basada en hello protocolo SAML. En este procedimiento, se carga tooBox.com de metadatos.

1. Agregar aplicación de cuadro de hello de aplicaciones empresariales de Hola.

2. Configurar inicio de sesión único de hello siguiente orden:

  ![Configuración del inicio de sesión único de Box](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 a. Hola **dirección URL de inicio de sesión** cuadro, asegúrese que dirección URL de inicio de sesión de Hola está establecida correctamente para cuadro Hola portal de Azure. Esta dirección URL es Hola de su inquilino de Box.com. Debe seguir la convención de nomenclatura de hello *https://.box.com*.  
 Hola **identificador** no se aplica toothis aplicación, pero sigue apareciendo como un campo obligatorio.

 b. Hola **identificador de usuario** cuadro, escriba **user.mail** (para SSO para las cuentas de invitado).

 c. En **Certificado de firma de SAML**, haga clic en **Crear nuevo certificado**.

 d. toobegin configurar su toouse de inquilino de Box.com Azure AD como proveedor de identidades, Descargar archivo de metadatos de hello y, a continuación, guárdelo tooyour la unidad local.

 e. Reenviar Hola metadatos archivo toohello cuadro equipo de soporte técnico, que configura el inicio de sesión único automáticamente.

3. Para la instalación de usuario automático de Azure AD, en el panel izquierdo de hello, seleccione **Provisioning**y, a continuación, seleccione **Authorize**.

  ![Autorizar el cuadro de herramientas de Azure AD tooconnect](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

Al igual que los invitados de Dropbox, los invitados cuadro deben canjear su invitación de aplicación del cuadro de hello.

## <a name="next-steps"></a>Pasos siguientes

Vea Hola siguientes artículos en la colaboración B2B de Azure AD:

* [¿Qué es la colaboración B2B de Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propiedades de usuario de la colaboración B2B](active-directory-b2b-user-properties.md)
* [Agregar un rol de tooa de usuario de la colaboración B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegación de las invitaciones de colaboración B2B](active-directory-b2b-delegate-invitations.md)
* [Grupos dinámicos y colaboración B2B](active-directory-b2b-dynamic-groups.md)
* [Código de colaboración B2B y ejemplos de PowerShell](active-directory-b2b-code-samples.md)
* [Tokens de usuario de colaboración B2B](active-directory-b2b-user-token.md)
* [Asignación de notificaciones de usuario de colaboración B2B](active-directory-b2b-claims-mapping.md)
* [Uso compartido externo de Office 365](active-directory-b2b-o365-external-user.md)
* [Limitaciones actuales de la colaboración B2B](active-directory-b2b-current-limitations.md)

---
title: "aaaSingle inicio de sesión de administración para aplicaciones empresariales en hello Azure Active Directory | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage inicio de sesión único para aplicaciones empresariales mediante hello Azure Active Directory"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: bcc954d3-ddbe-4ec2-96cc-3df996cbc899
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.openlocfilehash: b0a8e622ab10517b7b69f786406b6e9b9f2e7eaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-single-sign-on-for-enterprise-apps"></a>Administración de inicio de sesión único para aplicaciones empresariales
> [!div class="op_single_selector"]
> * [Portal de Azure](active-directory-enterprise-apps-manage-sso.md)
> * [Portal de Azure clásico](active-directory-sso-integrate-saas-apps.md)
> 

Este artículo se describe cómo hello toouse [portal de Azure](https://portal.azure.com) toomanage inicio de sesión en configuración de inicio único para aplicaciones empresariales. Las aplicaciones empresariales son aplicaciones que se implementan y se usan dentro de su organización. En este artículo se aplica especialmente tooapps que se han agregado desde hello [Galería de aplicaciones de Azure Active Directory](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). 

## <a name="finding-your-apps-in-hello-portal"></a>Buscar las aplicaciones de portal de Hola
Todas las aplicaciones de empresa que se han configurado para el inicio de sesión único pueden ver y administrar en hello portal de Azure. las aplicaciones de Hello pueden encontrarse en hello **más servicios** &gt; **aplicaciones empresariales** sección del portal de Hola de. 

![Hoja Aplicaciones empresariales][1]

Seleccione **todas las aplicaciones** tooview una lista de todas las aplicaciones que se han configurado. Al seleccionar una aplicación carga la hoja de recursos de Hola para esa aplicación, donde se pueden ver informes para que la aplicación y se pueden administrar diversas opciones de configuración.

toomanage único inicio de sesión en configuración, seleccione **inicio de sesión único**.

![Hoja Recursos de aplicación][2]

## <a name="single-sign-on-modes"></a>Modos de inicio de sesión único
Hola **inicio de sesión único** hoja comienza con un **modo** menú, lo que permite toobe de modo de inicio de sesión único de hello configurado. Hola las opciones disponibles incluyen:

* **Inicio de sesión basado en SAML en** -esta opción está disponible si admite la aplicación hello completa federado inicio de sesión único con Azure Active Directory con protocolo de hello SAML 2.0.
* **Password-based sign on** (Inicio de sesión basado en contraseña): esta opción está disponible si Azure AD admite el rellenado de formularios de contraseña para esta aplicación.
* **Vincula el inicio de sesión en** -anteriormente conocido como "Existing single sign-on", esta opción permite a los administradores tooplace una aplicación de toothis de vínculo en el iniciador de aplicaciones de Panel de acceso de Azure AD u Office 365 de los usuarios.

Para más información acerca de estos modos, consulte la sección [¿Cómo funciona el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="saml-based-sign-on"></a>Inicio de sesión basado en SAML
Hola **inicio de sesión basado en SAML en** opción muestra una tarjeta que se divide en cuatro secciones:

### <a name="domains-and-urls"></a>Dominios y direcciones URL
Esto es que todos los detalles acerca de la aplicación hello dominio y las direcciones URL se agregan tooyour directorio de Azure AD. Todas las entradas necesarias toomake aplicación de trabajo de inicio de sesión único se muestran directamente en la pantalla de bienvenida, mientras que todas las entradas opcionales se pueden ver seleccionando hello **mostrar avanzadas de configuración de direcciones URL** casilla de verificación. Hola lista completa de entradas admitidos se incluyen:

* **Dirección URL de inicio de sesión** : cuando el usuario de hello siga toothis toosign de aplicación. Si aplicación hello es servicio de tooperform configurado único iniciado por el proveedor de inicio de sesión, a continuación, cuando un usuario navega toothis URL, el proveedor de servicios de Hola Hola necesarios inicio de sesión y redirección tooAzure AD tooauthenticate Hola usuario en. Si este campo se rellena, Azure AD usará esta aplicación de hello toolaunch de dirección URL de hello Panel de acceso de Azure AD y Office 365. Si se omite este campo, Azure AD en su lugar, realiza el proveedor de identidades-sesión cuando aplicación hello se inicia desde Office 365, Hola el Panel de acceso de Azure AD, o de hello Azure AD único inicio de sesión iniciado por dirección URL.
* **Identificador** -este URI debería identificar únicamente la aplicación hello para que solo inicio de sesión se está configurando. Se trata de valor de Hola que Azure AD envía tooapplication atrás como Hola parámetro audiencia del token SAML de Hola y aplicación hello toovalidate esperado lo. Este valor también aparece como Hola Id. de entidad en los metadatos SAML proporcionado por la aplicación hello.
* **Dirección URL de respuesta** -URL de respuesta de hello es donde la aplicación hello espera token SAML de hello tooreceive. Esto también es una dirección URL de servicio de consumidor de aserción (ACS) de hello tooas que se hace referencia. Después de que se han introducido, haga clic en siguiente tooproceed toohello siguiente pantalla. Esta pantalla proporciona información sobre qué toobe necesidades configurarlo en hello aplicación lado tooenable tooaccept un token de SAML de Azure AD.
* **Estado de la transmisión** -estado de la transmisión de hello es un parámetro opcional que puede ayudarle a indicar la aplicación hello donde tooredirect Hola usuario una vez completada la autenticación. Valor de hello suele ser una dirección URL válida en la aplicación hello, sin embargo, algunas aplicaciones utilizan este campo de forma diferente (vea el inicio de sesión único de la aplicación hello en la documentación para obtener más información). estado de la transmisión de Hello capacidad tooset hello es una característica nueva que sea único toohello nuevo portal de Azure.

### <a name="user-attributes"></a>Atributos de usuario
Aquí es donde pueden ver los administradores y los atributos de Hola de edición que se envían en el token SAML de Hola que emite Azure AD toohello aplicación cada vez que los usuarios iniciar sesión en.

Hola solo admitido el atributo editable es hello **identificador de usuario** atributo. valor de Hola de este atributo es el campo de hello en Azure AD que identifica de forma única cada usuario dentro de la aplicación hello. Por ejemplo, si la aplicación hello se implementó usando "dirección de correo electrónico" hello como nombre de usuario de Hola y el identificador único, a continuación, el valor de Hola se establecería toohello "user.mail" campo en Azure AD.

### <a name="saml-signing-certificate"></a>Certificado de firma SAML
En esta sección muestra los detalles de Hola de certificado de Hola que Azure AD usa tokens SAML de hello toosign que se emiten aplicación toohello que cada vez que lo utiliza Hola autentica. Permite que las propiedades de Hola de hello actual certificado toobe inspeccionado, incluyendo la fecha de expiración de Hola.

### <a name="application-configuration"></a>Configuración de aplicaciones
Hola final sección proporciona documentación de Hola o controles necesarios tooconfigure Hola propia aplicación toouse Azure Active Directory como proveedor de identidades.

Hola **Configurar aplicación** menú emergente proporciona nuevas instrucciones concisas, incrustadas para configurar la aplicación hello. Se trata de otra nueva característica toohello único nuevo portal de Azure.

> [!NOTE]
> Para obtener un ejemplo completo de documentación de embedded, consulte aplicación de Salesforce.com hello. Continuamente se agrega documentación de otras aplicaciones.
> 
> 

![Documentos insertados][3]

## <a name="password-based-sign-on"></a>Password-based sign on
Si se admite la aplicación hello, seleccionar Hola modo SSO basada en contraseña y seleccione **guardar** al instante lo configura toodo SSO basado en contraseña. Para más información sobre la implementación del inicio de sesión único basado en contraseña, consulte la sección [¿Cómo funciona el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Password-based sign on][4]

## <a name="linked-sign-on"></a>Linked sign on
Si se admite la aplicación hello, seleccionar modo de SSO de hello vinculado permite tooenter Hola URL que desea Hola Panel de acceso de Azure AD u Office 365 tooredirect toowhen los usuarios hacer clic en esta aplicación. Para más información sobre el inicio de sesión único vinculado, consulte la sección [¿Cómo funciona el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Inicio de sesión vinculado][5]

##<a name="feedback"></a>Comentarios

Esperamos que le gustaría usar Hola mejoras de la experiencia de Azure AD. Tenga procedentes de comentarios de Hola! Publique sus comentarios y sugerencias para la mejora en hello **Portal de administración de** sección de nuestro [foro de comentarios](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  Esté emocionados acerca de cómo crear nuevos y estupendos todos los días y usar su tooshape de instrucciones y definir qué compilar después.

[1]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade.PNG
[2]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-sso-blade.PNG
[3]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-embedded-docs.PNG
[4]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-password-sso.PNG
[5]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-linked-sso.PNG

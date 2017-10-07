---
title: "aaaProblem configuración federada inicio de sesión único para una aplicación de la Galería de Azure AD | Documentos de Microsoft"
description: "Resolver algunos problemas comunes de Hola que pueden producirse al configurar federado única sesión con SAML para las aplicaciones que se enumeran en hello Galería de aplicaciones de Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Problemas en la configuración del inicio de sesión único federado para una aplicación de la galería de Azure AD

Si se produce un problema al configurar una aplicación. Compruebe que ha seguido todos los pasos de hello en el tutorial de hello para la aplicación hello. En configuración de la aplicación hello, dispone de documentación en línea en cómo tooconfigure Hola aplicación. Además, puede tener acceso a hello [lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para obtener instrucciones paso a paso detallados.

## <a name="cant-add-another-instance-of-hello-application"></a>No se puede agregar otra instancia de la aplicación hello

tooadd una segunda instancia de una aplicación, necesita toobe capaz de:

-   Configurar un identificador único para la segunda instancia de Hola. No será hello tooconfigure pueda mismo identificador utilizado para primera instancia de Hola.

-   Configurar un certificado diferente Hola uno utilizado para la primera instancia de Hola.

Si hello aplicación no admite cualquiera de hello anterior. A continuación, no será capaz de tooconfigure una segunda instancia.

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a>No se puede agregar Hola identificador u Hola dirección URL de respuesta

Si no es capaz de tooconfigure Hola identificador u Hola dirección URL de respuesta, confirme Hola identificador y los valores de dirección URL de respuesta coincidan con modelos de hello configurados previamente para la aplicación hello.

patrones de hello tooknow configurados previamente para la aplicación hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.** Vaya toostep 7. Si ya está en la hoja de configuración de aplicaciones de hello en Azure AD.

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

   * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado** Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooconfigure inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Seleccione **sesión basado en SAML** de hello **modo** lista desplegable.

9.  Vaya toohello **identificador** o **dirección URL de respuesta** cuadro de texto, en hello **sección de dominio y las direcciones URL.**

10. Hay tres formas de patrones de hello admitida tooknow para la aplicación hello:

   * En el cuadro de texto hello, vea Hola admiten patrones como un marcador de posición *ejemplo:* <https://contoso.com>.

   * Si no se admite el patrón de hello, verá una marca de exclamación roja cuando intente tooenter valor de hello en el cuadro de texto de Hola. Si se mantenga el mouse sobre la marca de exclamación rojo hello, verá patrones Hola compatible.

   * En el tutorial de hello para la aplicación hello, también puede obtener información sobre los patrones de hello admite. En hello **inicio de sesión único en configurar Azure AD** sección. Vaya toohello paso para los valores de hello configurado en hello **dominio y las direcciones URL** sección.

Si los valores de hello no coinciden con los patrones de hello configurados previamente en Azure AD. Puede:

-   Trabajar con valores de tooget de proveedor de aplicación de Hola que coinciden con el patrón de hello configurado previamente en Azure AD

-   O bien, puede ponerse en contacto con el equipo de Azure AD en < aadapprequest@microsoft.com > o deje un comentario en la actualización de Hola Hola toorequest tutorial de patrones de hello compatible para la aplicación hello

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>Donde se puede establecer formato de hello EntityID (identificador de usuario)

No será formato de tooselect capaz de hello EntityID (identificador de usuario) que Azure AD envía toohello aplicación en respuesta Hola después de la autenticación de usuario.

Azure formato AD seleccione Hola Hola NameID atributo (identificador de usuario) en función de valor de hello seleccionado u Hola formato solicitado por la aplicación hello en hello AuthRequest de SAML. Para obtener más información, visite el artículo de hello [protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) en la sección de hello NameIDPolicy,

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a>No se puede encontrar la configuración hello Azure AD metadatos toocomplete Hola con la aplicación hello

metadatos de la aplicación hello toodownload o certificado de Azure AD, siga los pasos de hello siguientes:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

   * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado** Todas las aplicaciones.**

6.  Seleccionar aplicación hello ha configurado el inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Vaya demasiado**el certificado de firma de SAML** sección, a continuación, haga clic en **descargar** valor de la columna. Dependiendo de qué aplicación hello es necesario configurar el inicio de sesión único, vea cualquier toodownload de opción Hola Hola Metadata XML u Hola certificado.

Azure AD no proporciona la dirección URL tooget Hola metadatos. solo se pueden recuperar metadatos de Hola como un archivo XML.

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a>No sabe cómo envían notificaciones SAML toocustomize los tooan aplicación

toolearn cómo toocustomize Hola SAML atributo notificaciones envían tooyour aplicación, consulte [notificaciones de asignación en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obtener más información.

## <a name="next-steps"></a>Pasos siguientes
[Administración de aplicaciones con Azure Active Directory](active-directory-enable-sso-scenario.md)

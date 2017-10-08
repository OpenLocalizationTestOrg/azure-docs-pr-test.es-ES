---
title: "configuración del inicio de sesión único en contraseña para una aplicación de la Galería de Azure AD de aaaProblem | Documentos de Microsoft"
description: "Comprender la cara de personas de problemas comunes de hello al configurar un inicio de sesión único de contraseña para las aplicaciones que ya se muestran en hello Galería de aplicaciones de Azure AD"
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
ms.openlocfilehash: 78c37c52453c375bf7ccbca6df5c9008be4ce642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Problemas en la configuración del inicio de sesión único con contraseña para una aplicación de la galería de Azure AD

En este artículo le ayudará toounderstand Hola comunes problemas se enfrentan los usuarios al configurar **contraseña Single Sign-on** con una aplicación de la Galería de Azure AD.

## <a name="credentials-are-filled-in-but-hello-extension-does-not-submit-them"></a>Las credenciales se rellenan pero extensión hello no enviarlos

Esto suele suceder si el proveedor de la aplicación hello ha cambiado su inicio de sesión recientemente página tooadd un campo, cambiar un identificador subyacente se utilizan campos de nombre de usuario y contraseña de hello toodetect o modificar cómo inicio de sesión de hello en experiencia funciona para su aplicación. Afortunadamente, en muchos casos, Microsoft puede trabajar con aplicaciones proveedores toorapidly resolver estos problemas.

Mientras que Microsoft tiene tecnologías tooautomatically detectar cuándo interrumpir estas integraciones, pero a veces no es capaz de toofind estos problemas derecho ausente o llevar a cabo algunas temporal toofix. En caso de hello cuando una de estas integraciones no funcione correctamente, le agradeceríamos si abre un caso de soporte técnico para que podamos solucionar lo más rápido posible.

En suma toothis, **si estás en contacto con el proveedor de la aplicación,** **enviarlas nuestro modo** por lo que podemos trabajar con ellos toonatively integrar su aplicación con Azure Active Directory. Puede enviar Hola proveedor toohello [enumerar la aplicación en la Galería de aplicaciones de Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget ellos iniciados.

## <a name="credentials-are-filled-in-and-submitted-but-hello-page-indicates-hello-credentials-are-incorrect"></a>Se rellena y se envían las credenciales, pero página Hola indica Hola credenciales son incorrectas

tooresolve este problema, primer siguiente Hola de comprobación:

-   Tener usuario hello en primer lugar intente demasiado**iniciar sesión en el sitio Web de aplicación toohello directamente** con credenciales de hello almacenadas para ellos.

  * Si eso funciona, a continuación, tener Hola usuario haga clic en hello **Actualizar credenciales** botón en hello **ventana de aplicación** en hello **aplicaciones** sección de hello [aplicación Obtener acceso al Panel](https://myapps.microsoft.com/) tooupdate les toohello más reciente conocida trabajar username y password.

   * Si encuentra u otro credenciales de hello administrador asignado para este usuario, desplazándose toohello usuario Hola o asignación de aplicación del grupo **usuarios y grupos** pestaña de aplicación hello, seleccione asignación de Hola y al hacer clic en hello **las credenciales de actualización** botón.

-   Si el usuario de hello asigna sus propias credenciales, tienen usuario hello **comprobar toobe seguro de que no ha expirado su contraseña en la aplicación hello** y si es así, **actualice su contraseña expirada** debe iniciar sesión en toohello aplicación directamente.

   * Después de que se ha actualizado la contraseña de hello en aplicación hello, solicitar Hola de hello usuario tooclick **Actualizar credenciales** botón en hello **ventana de aplicación** Hola **aplicaciones** sección de hello [Panel de acceso de la aplicación](https://myapps.microsoft.com/) tooupdate les toohello más reciente conocida trabajar username y password.

   * Si encuentra u otro credenciales de hello administrador asignado para este usuario, desplazándose toohello usuario Hola o asignación de aplicación del grupo **usuarios y grupos** pestaña de aplicación hello, seleccione asignación de Hola y al hacer clic en hello **las credenciales de actualización** botón.

-   Tiene la extensión de explorador del panel de acceso de hello usuario actualización Hola siguiendo los pasos de hello debajo de hello [cómo tooinstall Hola extensión de explorador del Panel de acceso](#how-to-install-the-access-panel-browser-extension) sección.

-   Asegúrese de que la extensión de explorador del panel de acceso de hello está ejecutando y habilitado en el explorador del usuario.

-   Asegúrese de que los usuarios no están tratando de toosign en toohello aplicación desde el panel de acceso de hello en **incognito, inPrivate o Private modo**. no se admite la extensión del panel de acceso de Hello en estos modos.

En caso de que esto no funciona, podría deberse a los casos de Hola que se ha producido un cambio en el lado de la aplicación hello que temporalmente dañó la integración de la aplicación hello con Azure AD. Por ejemplo, esto puede ocurrir cuando el proveedor de la aplicación hello presenta una secuencia de comandos en su página que se comporta de forma diferente para el recálculo manual y automatizada de entrada, lo que hace que habían automatizada integración, como nuestro propio, toobreak. Afortunadamente, en muchos casos, Microsoft puede trabajar con aplicaciones proveedores toorapidly resolver estos problemas.

Mientras que Microsoft tiene tecnologías tooautomatically detectar cuándo interrumpir estas integraciones, pero a veces no es capaz de toofind estos problemas derecho ausente o llevar a cabo algunas temporal toofix. En caso de hello cuando una de estas integraciones no funcione correctamente, le agradeceríamos si abre un caso de soporte técnico para que podamos solucionar lo más rápido posible.

En suma toothis, **si estás en contacto con el proveedor de la aplicación,** **enviarlas nuestro modo** por lo que podemos trabajar con ellos toonatively integrar su aplicación con Azure Active Directory. Puede enviar Hola proveedor toohello [enumerar la aplicación en la Galería de aplicaciones de Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget ellos iniciados.

## <a name="hello-extension-works-in-chrome-and-firefox-but-not-in-internet-explorer"></a>extensión de Hello funciona en Chrome y Firefox, pero no en Internet Explorer

Hay dos causas probables toothis problema:

-   Dependiendo de configuración de seguridad de hello habilitada en Internet Explorer, si el sitio Web de hello no es parte de un **zona de confianza**, a veces nuestro script se impide la ejecución de la aplicación hello.

  *  tooresolve, indicar al usuario Hola demasiado**agregar sitio Web de la aplicación hello** toohello **sitios de confianza** lista dentro de su **configuración de seguridad de Internet Explorer**. Puede enviar su toohello usuarios [cómo tooadd un toomy de sitio de confianza sitios lista](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5) artículo para obtener instrucciones detalladas.

-   En circunstancias excepcionales, validación de seguridad de Internet Explorer en ocasiones puede causar tooload de página de hello más lenta que la ejecución de nuestro script de Hola.

   * Por desgracia, esta situación puede variar dependiendo de la versión del explorador hello, velocidad del equipo o sitio visitado. En este caso, se recomienda ponerse en contacto con soporte técnico para que podamos solucionar la integración de Hola para esta aplicación específica.

En suma toothis, **si estás en contacto con el proveedor de la aplicación,** **enviarlas nuestro modo** por lo que podemos trabajar con ellos toonatively integrar su aplicación con Azure Active Directory. Puede enviar Hola proveedor toohello [enumerar la aplicación en la Galería de aplicaciones de Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget ellos iniciados.

## <a name="check-if-hello-applications-login-page-has-changed-recently-or-requires-an-additional-field"></a>Compruebe si hello página de inicio de sesión de la aplicación ha cambiado recientemente, o requiere un campo adicional

Si la página de inicio de sesión de la aplicación hello ha cambiado considerablemente, a veces, esto hace que nuestro toobreak integraciones. Un ejemplo de esto es cuando un proveedor de la aplicación agrega un inicio de sesión en el campo, un captcha, o la autenticación multifactor tootheir experiencias. Afortunadamente, en muchos casos, Microsoft puede trabajar con aplicaciones proveedores toorapidly resolver estos problemas.

Mientras que Microsoft tiene tecnologías tooautomatically detectar cuándo interrumpir estas integraciones, pero a veces no es capaz de toofind estos problemas inmediatamente. En caso contrario, toman algunos toofix de tiempo. En caso de hello cuando una de estas integraciones no funcione correctamente, le agradeceríamos abrir un caso de soporte técnico para que podamos solucionar lo más rápido posible.

En suma toothis, **si estás en contacto con el proveedor de la aplicación,** **enviarlas nuestro modo** por lo que podemos trabajar con ellos toonatively integrar su aplicación con Azure Active Directory. Puede enviar Hola proveedor toohello [enumerar la aplicación en la Galería de aplicaciones de Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget ellos iniciados.

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>¿Cómo tooinstall Hola extensión de explorador del Panel de acceso

Hola tooinstall extensión de explorador del Panel de acceso, siga Hola pasos:

1.  Abra hello [Panel de acceso](https://myapps.microsoft.com) en uno de los exploradores compatibles de Hola y de inicio de sesión como un **usuario** en Azure AD.

2.  Haga clic en un **aplicación SSO de contraseña** Hola Panel de acceso.

3.  En hello símbolo del sistema que se pregunta tooinstall Hola software, seleccione **instalar ahora**.

4.  Basado en el explorador es que el vínculo de descarga de toohello dirigida. **Agregar** tooyour Explorador de hello extensión.

5.  Si el explorador solicita, seleccione tooeither **habilitar** o **permitir** Hola extensión.

6.  Una vez instalada, **reinicie** la sesión del explorador.

7.  Inicie sesión en el Panel de acceso de Hola y vea si puede **iniciar** las aplicaciones de SSO de contraseña

También puede descargar extensión Hola para Chrome y Firefox de vínculos directos de Hola a continuación:

-   [Extensión del Panel de acceso para Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extensión del Panel de acceso para Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="next-steps"></a>Pasos siguientes
[Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación](active-directory-application-proxy-sso-using-kcd.md)


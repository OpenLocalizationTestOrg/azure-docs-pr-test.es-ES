---
title: "aaaProblem configuración del inicio de sesión único en contraseña para una aplicación no Galería | Documentos de Microsoft"
description: "Comprender la cara de personas de problemas comunes de hello al configurar un inicio de sesión único de contraseña para las aplicaciones no Galería personalizadas que no aparecen en hello Galería de aplicaciones de Azure AD"
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
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a>Problema en la configuración del inicio de sesión único con contraseña para una aplicación ajena a la galería

En este artículo le ayudará toounderstand Hola comunes problemas se enfrentan los usuarios al configurar **contraseña inicio de sesión único** con una aplicación no Galería.

## <a name="how-toocapture-sign-in-fields-for-an-application"></a>Cómo iniciar sesión toocapture campos para una aplicación

La captura de campos de inicio de sesión solo es posible en páginas de inicio de sesión compatibles con HTML y **no se admite para páginas de inicio de sesión no estándar**, como aquellas que usan Flash u otras tecnologías incompatibles con HTML.

Existen dos maneras de capturar campos de inicio de sesión para aplicaciones personalizadas:

-   Captura automática de campos de inicio de sesión

-   Captura manual de campos de inicio de sesión

**Captura de campo de inicio de sesión automático** funciona bien con la mayoría basadas en HTML en el inicio de sesión de las páginas, si usan **identificadores conocidos de DIV Hola nombre de usuario y una contraseña de entrada** campo. Hola que esto funciona de forma Hola de barrido de HTML en la página de hello toofind identificadores DIV que cumplan ciertos criterios y, a continuación, guardando que los metadatos para esta aplicación para podemos reproducir contraseñas tooit más tarde.

**Captura de campo de inicio de sesión manual** puede usarse en caso de Hola que Hola aplicación **proveedor no etiqueta** Hola campos utilizados para el inicio de sesión de entrada. Captura de campo de inicio de sesión manual también puede usarse en caso de hello cuando hello **proveedor presenta varios campos** que no puede ser detectado automáticamente. Azure AD puede almacenar datos para como muchos campos cuando estén en hello iniciar sesión en la página, siempre y cuando Díganos que esos campos se encuentran en página Hola.

En general, **si captura del campo de inicio de sesión automático no funciona, siempre se recomienda tratar de opción manual de Hola.**

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a>¿Cómo tooautomatically capturar campos de inicio de sesión para una aplicación

tooconfigure **basado en contraseña Single Sign-on** para una aplicación con **captura automática de inicio de sesión en campos**, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

  * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooconfigure inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Modo de hello seleccione **sesión basada en contraseña.**

9.  Escriba hello **dirección URL de inicio de sesión**. Se trata de dirección URL de Hola donde los usuarios escribir su toosign en nombre de usuario y contraseña a. **Asegúrese de inicio de sesión de hello en los campos está visible en la dirección URL de hello proporcionas**.

10. Haga clic en hello **guardar** botón.

11. Una vez que lo hace, se podrá extraer automáticamente esa dirección URL para un nombre de usuario y una contraseña cuadro de entrada y le permite toosecurely de Azure AD toouse transmitir aplicación toothat de contraseñas con la extensión de explorador del panel de acceso de Hola.

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a>¿Cómo toomanually capturar campos de inicio de sesión para una aplicación

inicio de sesión de captura de toomanually en campos, en primer lugar debe tener extensión de explorador del Panel de acceso de hello instalada y **no se esté ejecutando en modo de inPrivate, incognito o privado.** extensión del navegador tooinstall hello, siga los pasos de Hola Hola [cómo tooinstall Hola extensión de explorador del Panel de acceso](#i-cannot-manually-detect-sign-in-fields-for-my-application) sección.

tooconfigure **basado en contraseña Single Sign-on** para una aplicación con **captura manual campo**, siga estos pasos hello:

1.  Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**

2.  Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.

3.  Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.

4.  Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.

5.  Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.

   * Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**

6.  Seleccionar aplicación hello desea tooconfigure inicio de sesión único.

7.  Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.

8.  Modo de hello seleccione **sesión basada en contraseña.**

9.  Escriba hello **dirección URL de inicio de sesión**. Se trata de dirección URL de Hola donde los usuarios escribir su toosign en nombre de usuario y contraseña a. **Asegúrese de inicio de sesión de hello en los campos está visible en la dirección URL de hello proporcionas**.

10. Haga clic en hello **guardar** botón.

11. Una vez que lo hace, se podrá extraer automáticamente esa dirección URL para un nombre de usuario y una contraseña cuadro de entrada y le permite toosecurely de Azure AD toouse transmitir aplicación toothat de contraseñas con la extensión de explorador del panel de acceso de Hola. En caso de Hola que se produce un error, puede **Hola inicio de sesión en el modo toouse campo de inicio de sesión manual captura modificados** por continuar toostep 12.

12. Haga clic en **Establecer configuración de inicio de sesión único con contraseña de &lt;nombre de la aplicación&gt;**.

13. Seleccione hello **detectar manualmente los campos de inicio de sesión** opción de configuración.

14. Haga clic en **Aceptar**.

15. Haga clic en **Guardar**.

16. Siga hello en pantalla instrucciones toouse Hola Panel de acceso.

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a>Error "No pudimos encontrar ningún campo de inicio de sesión en esa URL"

Este error aparece cuando no funciona la detección automática de campos de inicio de sesión. tooresolve este problema, detección de campo de inicio de sesión manual de try por hello siguiendo los pasos de hello [cómo toomanually capturar campos de inicio de sesión para una aplicación](#how-to-manually-capture-sign-in-fields-for-an-application) sección.

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a>Aparece un error "no se puede toosave Single Sign-on configuración"

En algunos casos poco frecuentes, actualizando la configuración de inicio de sesión único de hello puede producir un error. tooresolve este intente guardar Hola único inicio de sesión en configuración de nuevo.

Si el problema persiste toofail de forma coherente, abrir un caso de soporte técnico y proporcione información de hello recopilada en hello [cómo toosee detalles de Hola de una notificación portal](#i-cannot-manually-detect-sign-in-fields-for-my-application) y [cómo ayudar tooget mediante el envío de notificaciones detalles tooa Ingeniero de soporte técnico](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) secciones.

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a>No se detectan manualmente campos de inicio de sesión para mi aplicación

Algunos de los comportamientos de Hola que puede ver al detección manual no funciona son:

-   proceso de captura manual de Hello parecía toowork pero campos Hola capturados no eran correctas

-   campos de la derecha de Hello no obtener resaltan al realizar el proceso de captura de Hola

-   proceso de captura de Hello toma mi página de inicio de sesión de la aplicación toohello según lo previsto, pero no ocurre nada

-   Captura manual aparece toowork, pero no ocurre SSO cuando mis usuarios naveguen toohello aplicación Hola Panel de acceso.

Compruebe la siguiente Hola si se produce alguno de estos problemas:

-   Asegúrese de que tiene la versión más reciente de Hola de extensión de explorador del panel de acceso de hello **instalado** y **habilitado** siguiendo los pasos de Hola Hola [cómo tooinstall Hola explorador del Panel de acceso extensión](#how-to-install-the-access-panel-browser-extension) sección.

-   Asegúrese de que no intenta realizar el proceso de captura de hello mientras el explorador en **incognito, inPrivate o Private modo**. no se admite la extensión del panel de acceso de Hello en estos modos.

-   Asegúrese de que los usuarios no están tratando de toosign en toohello aplicación desde el panel de acceso de hello en **incognito, inPrivate o Private modo**. no se admite la extensión del panel de acceso de Hello en estos modos.

-   Inténtelo de nuevo el proceso de captura manual de hello, asegurarse de marcadores de hello rojo sobre los campos correctos de Hola.

-   Si el proceso de captura manual de hello parece toohang o inicio de sesión de hello en la página no nada (caso 3 anteriormente), proceso de captura manual de hello vuelva a intentarlo. Pero, esta vez después de completar el proceso de hello, presione hello **F12** botón tooopen la consola para desarrolladores de su explorador. Una vez allí, abra hello **consola** y tipo **window.location= "&lt;escriba Hola inicio de sesión en la dirección url que ha especificado al configurar la aplicación hello&gt;"** y, a continuación, presione  **Escriba**. Esta fuerza una página redirigir que finalizar el proceso de captura de Hola y almacenar Hola campos que se han capturado.

Si ninguno de estos métodos funciona, podemos ayudarle. Abra un caso de soporte técnico con los detalles de Hola de lo que ha intentado, así como información de hello recopilada en hello [cómo toosee detalles de Hola de una notificación portal](#i-cannot-manually-detect-sign-in-fields-for-my-application) y [cómo ayudar tooget enviando detalles de notificación de soporte técnico de tooa ingeniería](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) secciones (si procede).

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>¿Cómo tooinstall Hola extensión de explorador del Panel de acceso

Hola tooinstall extensión de explorador del Panel de acceso, siga Hola pasos:

1.  Abra hello [Panel de acceso](https://myapps.microsoft.com) en uno de los exploradores compatibles de Hola y de inicio de sesión como un **usuario** en Azure AD.

2.  Haga clic en un **aplicación SSO de contraseña** Hola Panel de acceso.

3.  En hello símbolo del sistema que se pregunta tooinstall Hola software, seleccione **instalar ahora**.

4.  Basado en el explorador es que el vínculo de descarga de toohello dirigida. **Agregar** tooyour Explorador de hello extensión.

5.  Si el explorador solicita, seleccione tooeither **habilitar** o **permitir** Hola extensión.

6.  Una vez instalada, **reinicie** la sesión del explorador.

7.  Inicie sesión en el Panel de acceso de Hola y vea si puede **iniciar** las aplicaciones de SSO de contraseña.

También puede descargar extensión Hola para Chrome y Firefox de vínculos directos de Hola a continuación:

-   [Extensión del Panel de acceso para Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extensión del panel de acceso para Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a>¿Cómo toosee detalles de Hola de una notificación de portal

Puede ver detalles de Hola de cualquier notificación portal siguiendo estos pasos hello:

1.  Haga clic en hello **notificaciones** icono (campana Hola) en la esquina superior derecha de Hola de hello Portal de Azure

2.  Seleccione cualquier notificación de un **Error** estado (aquellos con un toothem siguiente (!) de color rojo).

  >[NOTA] No puede hacer clic en notificaciones con un estado **Correcto** o **En curso**.
  >
  >

3.  Este Hola abierto **detalles de la notificación** hoja.

4.  Utilice esta información usted mismo toounderstand más detalles sobre el problema de Hola.

5.  Si aún necesita ayuda, también puede compartir esta información con un soporte técnico o hello grupo tooget ayuda del producto con el problema.

6.  Haga clic en hello **copia** **icono** toohello derecha de hello **error al copiar** toocopy de cuadro de texto todos los Hola tooshare de detalles de notificación con un ingeniero de grupo de soporte técnico o el producto.

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a>Cómo ayudar tooget enviando el ingeniero de soporte técnico de notificación detalles tooa

Es muy importante que use para compartir **todos los detalles que se muestran a continuación de Hola** con un ingeniero de soporte técnico si necesita ayuda, por lo que pueden ayudarle rápidamente. Puede hacer esto fácilmente mediante **tomar una captura de pantalla,** o haciendo clic en hello **icono de error de copia**, encuentra toohello derecha de hello **error al copiar** cuadro de texto.

## <a name="notification-details-explained"></a>Explicación de los detalles de la notificación

Hola a continuación explica más cada uno de los elementos de notificación de hello significa y proporciona ejemplos de cada uno de ellos.

### <a name="essential-notification-items"></a>Elementos esenciales de notificación

-   **Título** : Hola título descriptivo de la notificación de Hola

    -   Por ejemplo: **Configuración del proxy de aplicación**

-   **Descripción** : Hola descripción de lo que se produjo como resultado de la operación de Hola

    -   Por ejemplo: **la dirección url interna especificada ya se está usando en otra aplicación**

-   **Identificador de notificación** : Id. único de Hola de notificación de Hola

    -   Por ejemplo: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **Id. de solicitud de cliente** : Id. de solicitud específico de hello realizado por el explorador

    -   Por ejemplo: **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **Hora UTC de marca** : Hola marca de tiempo durante el cual se produjo la notificación de hello, en UTC

    -   Por ejemplo: **2017-03-23T19:50:43.7583681Z**

-   **Id. de transacción interna** : Hola Id. interno que podemos usar error de hello toolook en nuestros sistemas

    -   Por ejemplo: **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **UPN** : usuario de Hola que realizó la operación de Hola

    -   Por ejemplo: **tperkins@f128.info**

-   **Identificador de inquilino** : Hola Id. único del inquilino Hola Hola usuario que realizó la operación de hello era miembro de

    -   Por ejemplo: **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **Id. de objeto de usuario** : Hola identificador único del usuario de Hola que realizó la operación de Hola

    -   Por ejemplo: **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>Elementos detallados de notificación

-   **Nombre para mostrar** : **(puede estar vacía)** un nombre para mostrar más detallado para el error de Hola

    -   Por ejemplo*: **Configuración del proxy de aplicación**

-   **Estado** : Hola estado específico de notificación de Hola

    -   Por ejemplo*: **Error**

-   **Id. de objeto** : **(puede estar vacía)** Hola Id. de objeto con qué Hola se realizó la operación

    -   Por ejemplo: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **Detalles** : Hola una descripción detallada de lo que se produjo como resultado de la operación de Hola

    -   Por ejemplo: **la dirección url interna 'http://bing.com/' no es válida puesto que ya está en uso**

-   **Error al copiar** : haga clic en hello **icono de copiar** toohello derecha de Hola **error al copiar** toocopy de cuadro de texto todos los Hola tooshare de detalles de notificación con un ingeniero de grupo de soporte técnico o el producto

    -   Por ejemplo: ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>Pasos siguientes
[Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación](active-directory-application-proxy-sso-using-kcd.md)


---
title: "Authenticator de aaaMicrosoft para teléfonos móviles | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooupgrade toohello versión más reciente de Azure Authenticator."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a>Introducción a la aplicación de Microsoft Authenticator hello
aplicación Microsoft Authenticator Hello proporciona un nivel adicional de seguridad en su cuenta profesional o educativa (por ejemplo, bsimon@contoso.com) o la cuenta de Microsoft (por ejemplo, bsimon@outlook.com).

funciona de la aplicación Hello en uno de dos maneras:

* **Notificación**. aplicación Hello puede ayudar a evitar accesos no autorizados tooaccounts y detener las transacciones fraudulentas insertando una tableta o smartphone tooyour de notificación. Simplemente ver notificación hello y, si es legítima, seleccione **compruebe**. De lo contrario, seleccione **Denegar**. 
* **Código de comprobación**. aplicación Hello puede usarse como un software de token toogenerate un código de comprobación de OAuth. Después de escribir el nombre de usuario y la contraseña, se escribe código de hello proporcionada por la aplicación hello en pantalla de inicio de sesión de bienvenida. código de comprobación de Hello proporciona una segunda forma de autenticación.

aplicación de Microsoft Authenticator Hello reemplaza la aplicación Azure Authenticator de hello. Hello Azure Authenticator aplicación todavía funciona, pero si decide toomove toohello la nueva aplicación de Microsoft Authenticator, este artículo le puede ayudar.  

## <a name="opt-in-for-two-step-verification"></a>Suscripción a la comprobación en dos pasos

aplicación de Microsoft Authenticator Hello no funciona por sí mismo. Configurar cada uno de los tooprompt de cuentas de un segundo método de comprobación después de iniciar sesión con su nombre de usuario y contraseña. 

Para una cuenta profesional o educativa, no por lo general obtendrá toochoose esta característica por sí mismo. En su lugar, un administrador de seguridad opts en su nombre y, a continuación, notifica a métodos de comprobación de tooregister para su cuenta. Si esta situación aplica tooyou, obtenga más información en [¿qué significa la autenticación multifactor Azure para mí](multi-factor-authentication-end-user.md).

Para una cuenta personal, deberá tooset configuraste la verificación por sí mismo. Si tiene una cuenta de Microsoft, esos pasos están disponibles en [Acerca de la verificación en dos pasos](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification). 

También puede utilizar Microsoft Authenticator Hola con cuentas de otros fabricantes. Puede llamar a Hola característica algo distinto de verificación en dos pasos, pero debe ser capaz de toofind en configuración de seguridad o inicio de sesión. 

## <a name="install-hello-app"></a>Instalar la aplicación hello
está disponible para la aplicación de Microsoft Authenticator Hello [de Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), y [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="add-accounts-toohello-app"></a>Agregar aplicación de cuentas toohello
Para cada cuenta que desea que la aplicación de Microsoft Authenticator toohello tooadd, use uno de hello procedimientos siguientes:

### <a name="add-a-personal-microsoft-account-toohello-app"></a>Agregar una aplicación de toohello de cuentas de Microsoft personal

Para una cuenta Microsoft personal (uno que use toosign en tooOutlook.com, Xbox, Skype, etc.), todo lo que tiene toodo es iniciar sesión en la cuenta de tooyour en la aplicación de Microsoft Authenticator hello.

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a>Agregar un trabajo o escuela cuenta toohello aplicación mediante el escáner de código de hello QR
1. Vaya pantalla de configuración de comprobación de seguridad toohello.  Para obtener información acerca de cómo tooget toothis pantalla, consulte [cambiar la configuración de seguridad](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).
2. Casilla de verificación Hola junto demasiado**aplicación Authenticator** , a continuación, seleccione **configurar**.

    ![botón configurar de Hello en pantalla de configuración de comprobación de seguridad de Hola](./media/authenticator-app-how-to/azureauthe.png)

    Aparecerá una pantalla con un código QR.

    ![Pantalla que proporcione el código QR Hola](./media/authenticator-app-how-to/barcode2.png)
3. Aplicación de Microsoft Authenticator de hello abierto. En hello **cuentas** pantalla, seleccione  **+** y, a continuación, especifique que desea tooadd una cuenta profesional o educativa.
4. Utilice el código de hello QR de hello cámara tooscan y, a continuación, seleccione **realiza** pantalla de código de hello QR tooclose.

    Si la cámara no funciona correctamente, puede [escribir código de hello QR y la dirección URL manualmente](#add-an-account-to-the-app-manually).

5. Cuando la aplicación hello muestra el nombre de cuenta con un código de seis dígitos aparecen debajo de él, ya ha terminado. 

    ![Pantalla Cuentas](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a>Agregar una aplicación de toohello de cuenta manualmente
1. Vaya pantalla de configuración de comprobación de seguridad toohello.  Para obtener información acerca de cómo tooget toothis pantalla, consulte [cambiar la configuración de seguridad](multi-factor-authentication-end-user-manage-settings.md).
2. Seleccione **Configurar**.

    ![botón configurar de Hello en pantalla de configuración de comprobación de seguridad de Hola](./media/authenticator-app-how-to/azureauthe.png)

    Aparecerá una pantalla con un código QR.  Tenga en cuenta el código de hello y la dirección URL.

    ![Pantalla que proporciona el código QR hello y la dirección URL](./media/authenticator-app-how-to/barcode2.png)
3. Aplicación de Microsoft Authenticator de hello abierto. En hello **cuentas** pantalla, seleccione  **+** y, a continuación, especifique que desea tooadd una cuenta profesional o educativa.

4. En el analizador de hello, seleccione **escribe código manualmente**.

    ![Pantalla para digitalizar un código QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. Escriba código de hello y la URL de hello en los cuadros adecuados de hello en la aplicación hello, a continuación, seleccione **finalizar**.

    ![Pantalla para escribir el código y la dirección URL](./media/authenticator-app-how-to/manual.png)

6. Cuando la aplicación hello muestra el nombre de cuenta con un código de seis dígitos aparecen debajo de él, ya ha terminado.

    ![Pantalla Cuentas](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a>Agregar una aplicación de toohello cuenta usa Touch ID
aplicación de Microsoft Authenticator Hello en iOS admite Touch Id.  La autenticación multifactor Azure permite a las organizaciones toorequire un PIN para dispositivos. Con Touch ID, los usuarios de iOS no es necesario tooenter un PIN. En su lugar, pueden digitalizar su huella y seleccionar **Aprobar**.

Configurar Touch ID con Microsoft Authenticator es sencillo. Un PIN supone un reto de comprobación normal. Si el dispositivo es compatible con Touch ID, Microsoft Authenticator lo configura automáticamente para esa cuenta.

![Comprobación de la configuración de Touch ID](./media/authenticator-app-how-to/touchid1.png)

Partir de ese punto en adelante, cuando esté necesario tooverify el inicio de sesión de, seleccione notificación de inserción de hello recibido y examinar su huella digital en lugar de escribir el código PIN.

![Notificación push](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a>Usar una aplicación Hola al iniciar sesión

Una vez que se agregue su cuenta de aplicación toohello, es posible que solicitadas toodo un toomake de comprobación de prueba que todo se ha configurado correctamente. Después de eso, habrá terminado. No es necesario toodo nada hasta que hello próxima vez inicie sesión.

Si elige toouse códigos de comprobación en la aplicación hello, iniciar toosee usarlas en la página de inicio de Hola. Como cambian cada 30 segundos, siempre tendrá un código nuevo cuando lo necesite. Pero no es necesario toodo nada con ellos hasta que inicie sesión y son tooenter solicitada un código de comprobación.  

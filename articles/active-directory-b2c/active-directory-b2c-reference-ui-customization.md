---
title: "Personalización de la interfaz de usuario - Azure AD B2C | Microsoft Docs"
description: "Un tema en características de personalización de interfaz de usuario de Hola en Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 99f5a391-5328-471d-a15c-a2fafafe233d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 04f8c5f1277f8d4409cd10971d22a0ebd2024785
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-customize-hello-azure-ad-b2c-user-interface-ui"></a>Azure B2C Directory Active: Personalizar la interfaz de usuario de hello Azure AD B2C (UI)

La experiencia del usuario es primordial en una aplicación de cliente.  Aumentar a su cliente base diseñando experiencias de usuario con hello apariencia y funcionamiento de la marca. Azure Active Directory B2C (Azure AD B2C) permite personalizar las páginas de registro, inicio de sesión, edición de perfil y restablecimiento de contraseña del cliente con control perfecto de píxeles.

> [!NOTE]
> característica de personalización de interfaz de usuario Hola página se describe en este artículo no aplica toohello inicio de sesión única directiva, su página de restablecimiento de contraseña que lo acompaña y correos electrónicos de comprobación.  Estas características utilizan hello [característica de personalización de marca de empresa](../active-directory/active-directory-add-company-branding.md) en su lugar.
>

En este artículo se trata Hola temas siguientes:

* característica de personalización de interfaz de usuario de página de Hola.
* Una herramienta para cargar tooAzure contenido HTML almacenamiento de blobs para su uso con la característica de personalización de interfaz de usuario de página de Hola.
* Hola elementos de interfaz de usuario utilizados por Azure AD B2C que se pueden personalizar con hojas de estilos en cascada (CSS).
* Prácticas recomendadas al usar esta característica.

## <a name="hello-page-ui-customization-feature"></a>característica de personalización de interfaz de usuario de página de Hola

Puede personalizar la apariencia y funcionamiento de Hola de contraseña de inicio de sesión, inicio de sesión de cliente restablecimiento y páginas de edición de perfiles (mediante la configuración de [directivas](active-directory-b2c-reference-policies.md)). Sus clientes tendrán experiencias más libres al navegar entre su aplicación y las páginas que Azure AD B2C sirve.

A diferencia de otros servicios donde opciones de interfaz de usuario, B2C de Azure AD utiliza un simple y modernas enfocan tooUI personalización.

Funciona de la siguiente manera: Azure AD B2C ejecuta código en el explorador del consumidor y usa un enfoque moderno denominado [Uso compartido de recursos entre orígenes (CORS)](http://www.w3.org/TR/cors/).  En tiempo de ejecución, el contenido se carga desde una dirección URL especificada en una directiva. Puede especificar diferentes direcciones URL para distintas páginas. Una vez cargado desde la dirección URL de contenido se combina con un fragmento HTML insertado de Azure AD B2C, página de hello es cliente de tooyour mostrado. Todo lo que necesita toodo es:

1. Crear contenido con vacío HTML5 correcto `<div id="api"></div>` elemento ubicado en algún lugar de hello `<body>`. Donde se inserta el contenido de Azure AD B2C hello las marcas de este elemento.
1. Hospedar el contenido en un punto de conexión HTTPS (donde se permite CORS). Tenga en cuenta que los métodos de solicitud GET y OPTIONS se deben habilitar al configurar CORS.
1. Use elementos de interfaz de usuario de Hola de toostyle CSS que Azure AD B2C inserta.

### <a name="a-basic-example-of-customized-html"></a>Un ejemplo básico de HTML personalizado

Hola siguiente ejemplo es contenido Hola HTML más básico que puede utilizar tootest esta capacidad. Hola de uso [herramienta de Ayudante](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload y configurar este contenido en el almacenamiento de blobs de Azure. A continuación, puede comprobar que los botones de basic, no en el estilo de hello & campos de formulario en cada página se muestran y funcional.

```HTML
<!DOCTYPE html>
<html>
    <head>
        <title>!Add your title here!</title>
    </head>
    <body>
        <div id="api"></div>   <!-- Leave this element empty because Azure AD B2C will insert content here. -->
    </body>
</html>
```

## <a name="test-out-hello-ui-customization-feature"></a>Pruebe la característica de personalización de interfaz de usuario de Hola

¿Deseado tootry característica de personalización de interfaz de usuario de hello mediante nuestro contenido HTML y CSS de ejemplo?  Hemos proporcionado [una herramienta auxiliar](active-directory-b2c-reference-ui-customization-helper-tool.md) que carga y configura el contenido de ejemplo en Azure Blob Storage.

> [!NOTE]
> El contenido de la interfaz de usuario se puede hospedar en cualquier lugar: en servidores web, CDN, AWS S3, sistemas de uso compartido de archivos, etc. Como contenido de hello está hospedado en un extremo HTTPS disponible públicamente con CORS habilitado, son buenas toogo. Almacenamiento de blobs de Azure se usa solo con fines ilustrativos.
>

## <a name="hello-ui-fragments-embedded-by-azure-ad-b2c"></a>fragmentos de interfaz de usuario de Hello incrustados por Azure AD B2C

Hello secciones siguientes enumeran los fragmentos de hello HTML5 que Azure AD B2C combina en hello `<div id="api"></div>` elemento ubicado en el contenido. **No inserte estos fragmentos en el contenido de HTML 5.** servicio de Azure AD B2C Hello en inserta en tiempo de ejecución. Use estos fragmentos como referencia al diseñar sus propias hojas de estilo CSS.

### <a name="fragment-inserted-into-hello-identity-provider-selection-page"></a>Fragmento inserta Hola "Página de selección del proveedor de identidades"

Esta página contiene una lista de proveedores que Hola usuario pueden elegir entre durante el inicio de sesión o inicio de sesión de identidad. Estos botones incluyen los proveedores de identidades sociales como Facebook y Google+ o las cuentas locales (basadas en una dirección de correo electrónico o un nombre de usuario).

```HTML
<div id="api" data-name="IdpSelections">
    <div class="intro">
         <p>Sign up</p>
    </div>

    <div>
        <ul>
            <li>
                <button class="accountButton" id="FacebookExchange">Facebook</button>
            </li>
            <li>
                <button class="accountButton" id="GoogleExchange">Google+</button>
            </li>
            <li>
                <button class="accountButton" id="SignUpWithLogonEmailExchange">Email</button>
            </li>
        </ul>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-local-account-sign-up-page"></a>Fragmento insertada Hola "página de inicio de sesión de cuenta Local"

Esta página contiene un formulario para el registro en una cuenta local basada en una dirección de correo electrónico o un nombre de usuario. formulario de Hello puede contener diferentes controles de entrada como cuadro de entrada de texto, cuadro de entrada de contraseña, botón de radio, cuadros de lista desplegable de selección única y casillas de verificación de selección múltiple.

```HTML
<div id="api" data-name="SelfAsserted">
    <div class="intro">
        <p>Create your account by providing hello following details</p>
    </div>

    <div id="attributeVerification">
        <div class="errorText" id="passwordEntryMismatch" style="display: none;">hello password entry fields do not match. Please enter hello same password in both fields and try again.</div>
        <div class="errorText" id="requiredFieldMissing" style="display: none;">A required field is missing. Please fill out all required fields and try again.</div>
        <div class="errorText" id="fieldIncorrect" style="display: none;">One or more fields are filled out incorrectly. Please check your entries and try again.</div>
        <div class="errorText" id="claimVerificationServerError" style="display: none;"></div>
        <div class="attr" id="attributeList">
            <ul>
                <li>
                    <div class="attrEntry validate">
                        <div>
                            <div class="verificationInfoText" id="email_intro" style="display: inline;">Verification is necessary. Please click Send button.</div>
                            <div class="verificationInfoText" id="email_info" style="display:none">Verification code has been sent tooyour inbox. Please copy it toohello input box below.</div>
                            <div class="verificationSuccessText" id="email_success" style="display:none">E-mail address verified. You can now continue.</div>
                            <div class="verificationErrorText" id="email_fail_retry" style="display:none">Incorrect code, try again.</div>
                            <div class="verificationErrorText" id="email_fail_no_retry" style="display:none">Exceeded number of retries you need toosend new code.</div>
                            <div class="verificationErrorText" id="email_fail_server" style="display:none">Server error, please try again</div>
                            <div class="verificationErrorText" id="email_incorrect_format" style="display:none">Incorect format.</div>
                        </div>

                    <div class="helpText show">This information is required</div>
                        <label>Email</label>
                        <input id="email" class="textInput" type="text" placeholder="Email" required="" autofocus=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Email address that can be used toocontact you.');" class="tiny">What is this?</a>

                    <div class="buttons verify" claim_id="email">
                        <div id="email_ver_wait" class="working" style="display: none;"></div>
                            <label id="email_ver_input_label" for="email_ver_input" style="display: none;">Verification code</label>
                            <input id="email_ver_input" type="text" placeholder="Verification code" style="display:none">
                            <button id="email_ver_but_send" class="sendButton" type="button" style="display: inline;">Send verification code</button>
                            <button id="email_ver_but_verify" class="verifyButton" type="button" style="display:none">Verify code</button>
                            <button id="email_ver_but_resend" class="sendButton" type="button" style="display:none">Send new code</button>
                            <button id="email_ver_but_edit" class="editButton" type="button" style="display:none">Change e-mail</button>
                            <button id="email_ver_but_default" class="defaultButton" type="button" style="display:none">Default</button>
                        </div>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ " ( ) ; .This information is required</div>
                        <label>Enter password</label>
                        <input id="password" class="textInput" type="password" placeholder="Enter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title="8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Enter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"> This information is required</div>
                        <label>Reenter password</label>
                        <input id="reenterPassword" class="textInput" type="password" placeholder="Reenter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title=" " required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Reenter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Name</label>
                        <input id="displayName" class="textInput" type="text" placeholder="Name" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your display name.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Gender</label>
                        <input id="extension_Gender_F" name="extension_Gender" type="radio" value="F" autofocus="">
                        <label for="extension_Gender_F">Female</label>
                        <input id="extension_Gender_M" name="extension_Gender" type="radio" value="M">
                        <label for="extension_Gender_M">Male</label>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Loyalty number</label>
                        <input id="extension_MemNum" class="textInput" type="text" placeholder="Loyalty number"><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Membership number');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>State</label>
                        <select class="dropdown_single" id="state">
                            <option style="display:none" disabled="disabled" value="placeholder" selected="">State</option>
                            <option value="WA">Washington</option>
                            <option value="NY">New York</option>
                            <option value="CA">California</option>
                        </select>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your residential state or province.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Zip code</label>
                        <input id="postalCode" class="textInput" type="text" placeholder="Zip code" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('hello postal code of your address.');" class="tiny">What is this?</a>
                    </div>
                </li>
            </ul>
        </div>
        <div class="buttons"> <button id="continue" disabled="">Create</button> <button id="cancel">Cancel</button></div>
    </div>
    <div class="verifying-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="verifying_blurb"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-social-account-sign-up-page"></a>Fragmento inserta Hola "" Social página de cuentas de inicio de sesión"

Esta página puede aparecer al registrarse con una cuenta existente de un proveedor de identidades de redes sociales, como Facebook o Google+.  Se utiliza cuando se debe recopilar información adicional de hello mediante un formulario de inicio de sesión del usuario final. Esta página es similar toohello cuenta local página de registro (que se muestra en la sección anterior de hello) con excepción de Hola de campos de entrada de contraseña de Hola.

### <a name="fragment-inserted-into-hello-unified-sign-up-or-sign-in-page"></a>Fragmento inserta Hola "Unificado la página de inicio de sesión o inicio de sesión"

Esta página controla tanto la suscripción como el inicio de sesión de los clientes, que pueden utilizar proveedores de identidades sociales como Facebook o Google +, o cuentas locales.

```HTML
<div id="api" data-name="Unified">
        <div class="social" role="form">
               <div class="intro">
                       <h2>Sign in with your social account</h2>
               </div>
               <div class="options">
                       <div><button class="accountButton firstButton" id="MicrosoftAccountExchange" tabindex="1">msa</button></div>
                       <div><button class="accountButton" id="FacebookExchange" tabindex="1">fb</button></div>
               </div>
        </div>
        <div class="divider">
               <h2>OR</h2>
        </div>
        <div class="localAccount" role="form">
               <div class="intro">
                       <h2>Sign in with your existing account</h2>
               </div>
               <div class="error pageLevel" aria-hidden="true" style="display: none;">
                       <p role="alert"></p>
               </div>
               <div class="entry">
                       <div class="entry-item">
                               <label for="logonIdentifier">Email Address</label> 
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="email" id="logonIdentifier" name="LogonIdentifier" pattern="^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$" placeholder="LogonIdentifier" value="" tabindex="1">
                       </div>
                       <div class="entry-item">
                               <div class="password-label"> <label for="password">Password</label><a id="forgotPassword" tabindex="2">Forgot your password?</a></div>
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="password" id="password" name="Password" placeholder="Password" tabindex="1">
                       </div>
                       <div class="working"></div>
                       <div class="buttons"> <button id="next" tabindex="1">Sign in</button> </div>
               </div>
               <div class="divider">
                       <h2>OR</h2>
               </div>
               <div class="create">
                       <p>Don't have an account?<a id="createAccount" tabindex="1">Sign up now</a> </p>
               </div>
        </div>
</div>
```

### <a name="fragment-inserted-into-hello-multi-factor-authentication-page"></a>Fragmento insertada Hola "página de la autenticación multifactor"

Esta página permite a los usuarios verificar sus números de teléfono (mediante texto o voz) durante el registro o el inicio de sesión.

```HTML
<div id="api" data-name="Phonefactor">
    <div id="phonefactor_initial">
        <div class="intro">
            <p>Enter a number below that we can send a code via SMS or phone tooauthenticate you.</p>
        </div>
        <div class="errorText" id="errorMessage" style="display:none"></div>
        <div class="phoneEntry" id="phoneEntry">
            <div class="phoneNumber">
                <select id="countryCode" style="display:inline-block">
                    <option value="+93">Afghanistan (+93)</option>
                    <!-- Not all country codes listed -->
                    <option value="+44">United Kingdom (+44)</option>
                    <option value="+1" selected="">United States (+1)</option>
                    <!-- Not all country codes listed -->
                </select>
            </div>
            <div class="phoneNumber">
                <input type="text" id="localNumber" style="display:inline-block" placeholder="Phone number">
            </div>
        </div>
        <div id="codeVerification" style="display:none">
            <div>
                <p>Enter your verification code below, or <button id="retryCode" class="textButton">send a new code</button></p>
                <input type="text" id="verificationCode" placeholder="Verification code">
            </div>
        </div>
        <div class="buttons">
            <button id="verifyCode" class="sendInitialCodeButton">Send Code</button>
            <button id="verifyPhone" style="display:inline-block">Call Me</button>
            <button id="cancel" style="display:inline-block">Cancel</button>
        </div>
    </div>
    <div class="dialing-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="dialing_blurb"></div><div id="dialing_number"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-error-page"></a>Fragmento inserta Hola "[NULL]"Página de Error de

```HTML
<div id="api" class="error-page-content" data-name="GlobalException">
    <h2>Sorry, but we're having trouble signing you in.</h2>
    <div class="error-page-help">We track these errors automatically, but if hello problem persists feel free toocontact us. In hello meantime, please try again.</div>
    <div class="error-page-messagedetails">Your administrator hasn't provided any contact details.</div>
    <div class="error-page-messagedetails">
        <div class="error-page-correlationid">Correlation ID:1c4f0397-c6e4-4afe-bf74-42f488f2f15f</div>
        <div>Timestamp:2015-09-14 23:22:35Z</div>
        <div class="error-page-detail">AADB2C90065: A B2C client-side error 'Access is denied.' has occurred requesting hello remote resource.</div>
    </div>
</div>
```

## <a name="localizing-your-html-content"></a>Localización del contenido HTML

Puede localizar el contenido HTML mediante la activación de la característica ["Personalización de idioma"](active-directory-b2c-reference-language-customization.md).  Si habilita esta característica permite que Azure AD B2C tooforward Hola conectarse de identificador abierto parámetro, `ui-locales`, tooyour extremo.  El servidor de contenido puede usar este páginas HTML tooprovide personalizado de parámetros que son específicos del idioma.

## <a name="things-tooremember-when-building-your-own-content"></a>Cosas tooremember al compilar su propio contenido

Si tiene previsto característica de personalización de interfaz de usuario de página de toouse hello, revise Hola seguir las prácticas recomendadas:

* No copiar el contenido del hello Azure AD B2C valor predeterminado e intente toomodify lo. Se está toobuild mejor su contenido de HTML5 desde el principio y toouse contenido predeterminado como referencia.
* Por motivos de seguridad, no permitimos tooinclude todo el código JavaScript en el contenido. La mayor parte de lo que necesita debe estar disponible fuera del cuadro de Hola. Si no es así, use [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest nueva funcionalidad.
* Versiones de explorador admitidas:
  * Internet Explorer 11, 10, Edge
  * Compatibilidad limitada con Internet Explorer 9, 8
  * Google Chrome 42.0 y versiones posteriores
  * Mozilla Firefox 38.0 y versiones posteriores

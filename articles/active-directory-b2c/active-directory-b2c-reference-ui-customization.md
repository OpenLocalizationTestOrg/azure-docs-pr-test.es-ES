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
# <a name="azure-active-directory-b2c-customize-hello-azure-ad-b2c-user-interface-ui"></a><span data-ttu-id="c50d1-103">Azure B2C Directory Active: Personalizar la interfaz de usuario de hello Azure AD B2C (UI)</span><span class="sxs-lookup"><span data-stu-id="c50d1-103">Azure Active Directory B2C: Customize hello Azure AD B2C user interface (UI)</span></span>

<span data-ttu-id="c50d1-104">La experiencia del usuario es primordial en una aplicación de cliente.</span><span class="sxs-lookup"><span data-stu-id="c50d1-104">User experience is paramount in a customer facing application.</span></span>  <span data-ttu-id="c50d1-105">Aumentar a su cliente base diseñando experiencias de usuario con hello apariencia y funcionamiento de la marca.</span><span class="sxs-lookup"><span data-stu-id="c50d1-105">Grow your customer base by crafting user experiences with hello look and feel of your brand.</span></span> <span data-ttu-id="c50d1-106">Azure Active Directory B2C (Azure AD B2C) permite personalizar las páginas de registro, inicio de sesión, edición de perfil y restablecimiento de contraseña del cliente con control perfecto de píxeles.</span><span class="sxs-lookup"><span data-stu-id="c50d1-106">Azure Active Directory B2C (Azure AD B2C) lets you customize sign-up, sign-in, profile editing, and password reset pages with pixel-perfect control.</span></span>

> [!NOTE]
> <span data-ttu-id="c50d1-107">característica de personalización de interfaz de usuario Hola página se describe en este artículo no aplica toohello inicio de sesión única directiva, su página de restablecimiento de contraseña que lo acompaña y correos electrónicos de comprobación.</span><span class="sxs-lookup"><span data-stu-id="c50d1-107">hello page UI customization feature described in this article does not apply toohello sign-in only policy, its accompanying password reset page, and verification emails.</span></span>  <span data-ttu-id="c50d1-108">Estas características utilizan hello [característica de personalización de marca de empresa](../active-directory/active-directory-add-company-branding.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="c50d1-108">These features use hello [company branding feature](../active-directory/active-directory-add-company-branding.md) instead.</span></span>
>

<span data-ttu-id="c50d1-109">En este artículo se trata Hola temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="c50d1-109">This article covers hello following topics:</span></span>

* <span data-ttu-id="c50d1-110">característica de personalización de interfaz de usuario de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="c50d1-110">hello page UI customization feature.</span></span>
* <span data-ttu-id="c50d1-111">Una herramienta para cargar tooAzure contenido HTML almacenamiento de blobs para su uso con la característica de personalización de interfaz de usuario de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="c50d1-111">A tool for uploading HTML content tooAzure Blob Storage for use with hello page UI customization feature.</span></span>
* <span data-ttu-id="c50d1-112">Hola elementos de interfaz de usuario utilizados por Azure AD B2C que se pueden personalizar con hojas de estilos en cascada (CSS).</span><span class="sxs-lookup"><span data-stu-id="c50d1-112">hello UI elements used by Azure AD B2C that you can customize using Cascading Style Sheets (CSS).</span></span>
* <span data-ttu-id="c50d1-113">Prácticas recomendadas al usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="c50d1-113">Best practices when exercising this feature.</span></span>

## <a name="hello-page-ui-customization-feature"></a><span data-ttu-id="c50d1-114">característica de personalización de interfaz de usuario de página de Hola</span><span class="sxs-lookup"><span data-stu-id="c50d1-114">hello page UI customization feature</span></span>

<span data-ttu-id="c50d1-115">Puede personalizar la apariencia y funcionamiento de Hola de contraseña de inicio de sesión, inicio de sesión de cliente restablecimiento y páginas de edición de perfiles (mediante la configuración de [directivas](active-directory-b2c-reference-policies.md)).</span><span class="sxs-lookup"><span data-stu-id="c50d1-115">You can customize hello look and feel of customer sign-up, sign-in, password reset, and profile-editing pages (by configuring [policies](active-directory-b2c-reference-policies.md)).</span></span> <span data-ttu-id="c50d1-116">Sus clientes tendrán experiencias más libres al navegar entre su aplicación y las páginas que Azure AD B2C sirve.</span><span class="sxs-lookup"><span data-stu-id="c50d1-116">Your customers get a seamless experience when navigating between your application and pages served by Azure AD B2C.</span></span>

<span data-ttu-id="c50d1-117">A diferencia de otros servicios donde opciones de interfaz de usuario, B2C de Azure AD utiliza un simple y modernas enfocan tooUI personalización.</span><span class="sxs-lookup"><span data-stu-id="c50d1-117">Unlike other services where UI options, Azure AD B2C uses a simple and modern approach tooUI customization.</span></span>

<span data-ttu-id="c50d1-118">Funciona de la siguiente manera: Azure AD B2C ejecuta código en el explorador del consumidor y usa un enfoque moderno denominado [Uso compartido de recursos entre orígenes (CORS)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="c50d1-118">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span>  <span data-ttu-id="c50d1-119">En tiempo de ejecución, el contenido se carga desde una dirección URL especificada en una directiva.</span><span class="sxs-lookup"><span data-stu-id="c50d1-119">At run-time, content is loaded from a URL that you specify in a policy.</span></span> <span data-ttu-id="c50d1-120">Puede especificar diferentes direcciones URL para distintas páginas.</span><span class="sxs-lookup"><span data-stu-id="c50d1-120">You can specify different URLs for different pages.</span></span> <span data-ttu-id="c50d1-121">Una vez cargado desde la dirección URL de contenido se combina con un fragmento HTML insertado de Azure AD B2C, página de hello es cliente de tooyour mostrado.</span><span class="sxs-lookup"><span data-stu-id="c50d1-121">After content loaded from your URL is merged with an HTML fragment inserted from Azure AD B2C, hello page is displayed tooyour customer.</span></span> <span data-ttu-id="c50d1-122">Todo lo que necesita toodo es:</span><span class="sxs-lookup"><span data-stu-id="c50d1-122">All you need toodo is:</span></span>

1. <span data-ttu-id="c50d1-123">Crear contenido con vacío HTML5 correcto `<div id="api"></div>` elemento ubicado en algún lugar de hello `<body>`.</span><span class="sxs-lookup"><span data-stu-id="c50d1-123">Create well-formed HTML5 content with an empty `<div id="api"></div>` element located somewhere in hello `<body>`.</span></span> <span data-ttu-id="c50d1-124">Donde se inserta el contenido de Azure AD B2C hello las marcas de este elemento.</span><span class="sxs-lookup"><span data-stu-id="c50d1-124">This element marks where hello Azure AD B2C content is inserted.</span></span>
1. <span data-ttu-id="c50d1-125">Hospedar el contenido en un punto de conexión HTTPS (donde se permite CORS).</span><span class="sxs-lookup"><span data-stu-id="c50d1-125">Host your content on an HTTPS endpoint (with CORS allowed).</span></span> <span data-ttu-id="c50d1-126">Tenga en cuenta que los métodos de solicitud GET y OPTIONS se deben habilitar al configurar CORS.</span><span class="sxs-lookup"><span data-stu-id="c50d1-126">Note both GET and OPTIONS request methods must be enabled when configuring CORS.</span></span>
1. <span data-ttu-id="c50d1-127">Use elementos de interfaz de usuario de Hola de toostyle CSS que Azure AD B2C inserta.</span><span class="sxs-lookup"><span data-stu-id="c50d1-127">Use CSS toostyle hello UI elements that Azure AD B2C inserts.</span></span>

### <a name="a-basic-example-of-customized-html"></a><span data-ttu-id="c50d1-128">Un ejemplo básico de HTML personalizado</span><span class="sxs-lookup"><span data-stu-id="c50d1-128">A basic example of customized HTML</span></span>

<span data-ttu-id="c50d1-129">Hola siguiente ejemplo es contenido Hola HTML más básico que puede utilizar tootest esta capacidad.</span><span class="sxs-lookup"><span data-stu-id="c50d1-129">hello following example is hello most basic HTML content that you can use tootest this capability.</span></span> <span data-ttu-id="c50d1-130">Hola de uso [herramienta de Ayudante](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload y configurar este contenido en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="c50d1-130">Use hello [helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload and configure this content on your Azure Blob storage.</span></span> <span data-ttu-id="c50d1-131">A continuación, puede comprobar que los botones de basic, no en el estilo de hello & campos de formulario en cada página se muestran y funcional.</span><span class="sxs-lookup"><span data-stu-id="c50d1-131">You can then verify that hello basic, non-stylized buttons & form fields on each page are displayed and functional.</span></span>

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

## <a name="test-out-hello-ui-customization-feature"></a><span data-ttu-id="c50d1-132">Pruebe la característica de personalización de interfaz de usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="c50d1-132">Test out hello UI customization feature</span></span>

<span data-ttu-id="c50d1-133">¿Deseado tootry característica de personalización de interfaz de usuario de hello mediante nuestro contenido HTML y CSS de ejemplo?</span><span class="sxs-lookup"><span data-stu-id="c50d1-133">Want tootry out hello UI customization feature by using our sample HTML and CSS content?</span></span>  <span data-ttu-id="c50d1-134">Hemos proporcionado [una herramienta auxiliar](active-directory-b2c-reference-ui-customization-helper-tool.md) que carga y configura el contenido de ejemplo en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c50d1-134">We've provided you [a helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures sample content on your Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="c50d1-135">El contenido de la interfaz de usuario se puede hospedar en cualquier lugar: en servidores web, CDN, AWS S3, sistemas de uso compartido de archivos, etc. Como contenido de hello está hospedado en un extremo HTTPS disponible públicamente con CORS habilitado, son buenas toogo.</span><span class="sxs-lookup"><span data-stu-id="c50d1-135">You can host your UI content anywhere: on web servers, CDNs, AWS S3, file sharing systems, etc. As long as hello content is hosted on a publicly available HTTPS endpoint with CORS enabled, you are good toogo.</span></span> <span data-ttu-id="c50d1-136">Almacenamiento de blobs de Azure se usa solo con fines ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="c50d1-136">We are using Azure Blob storage for illustrative purposes only.</span></span>
>

## <a name="hello-ui-fragments-embedded-by-azure-ad-b2c"></a><span data-ttu-id="c50d1-137">fragmentos de interfaz de usuario de Hello incrustados por Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c50d1-137">hello UI fragments embedded by Azure AD B2C</span></span>

<span data-ttu-id="c50d1-138">Hello secciones siguientes enumeran los fragmentos de hello HTML5 que Azure AD B2C combina en hello `<div id="api"></div>` elemento ubicado en el contenido.</span><span class="sxs-lookup"><span data-stu-id="c50d1-138">hello following sections list hello HTML5 fragments that Azure AD B2C merges into hello `<div id="api"></div>` element located in your content.</span></span> <span data-ttu-id="c50d1-139">**No inserte estos fragmentos en el contenido de HTML 5.**</span><span class="sxs-lookup"><span data-stu-id="c50d1-139">**Do not insert these fragments in your HTML 5 content.**</span></span> <span data-ttu-id="c50d1-140">servicio de Azure AD B2C Hello en inserta en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c50d1-140">hello Azure AD B2C service inserts them in at run-time.</span></span> <span data-ttu-id="c50d1-141">Use estos fragmentos como referencia al diseñar sus propias hojas de estilo CSS.</span><span class="sxs-lookup"><span data-stu-id="c50d1-141">Use these fragments as a reference when designing your own Cascading Style Sheets (CSS).</span></span>

### <a name="fragment-inserted-into-hello-identity-provider-selection-page"></a><span data-ttu-id="c50d1-142">Fragmento inserta Hola "Página de selección del proveedor de identidades"</span><span class="sxs-lookup"><span data-stu-id="c50d1-142">Fragment inserted into hello "Identity provider selection page"</span></span>

<span data-ttu-id="c50d1-143">Esta página contiene una lista de proveedores que Hola usuario pueden elegir entre durante el inicio de sesión o inicio de sesión de identidad.</span><span class="sxs-lookup"><span data-stu-id="c50d1-143">This page contains a list of identity providers that hello user can choose from during sign-up or sign-in.</span></span> <span data-ttu-id="c50d1-144">Estos botones incluyen los proveedores de identidades sociales como Facebook y Google+ o las cuentas locales (basadas en una dirección de correo electrónico o un nombre de usuario).</span><span class="sxs-lookup"><span data-stu-id="c50d1-144">These buttons include social identity providers such as Facebook and Google+, or local accounts (based on email address or user name).</span></span>

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

### <a name="fragment-inserted-into-hello-local-account-sign-up-page"></a><span data-ttu-id="c50d1-145">Fragmento insertada Hola "página de inicio de sesión de cuenta Local"</span><span class="sxs-lookup"><span data-stu-id="c50d1-145">Fragment inserted into hello "Local account sign-up page"</span></span>

<span data-ttu-id="c50d1-146">Esta página contiene un formulario para el registro en una cuenta local basada en una dirección de correo electrónico o un nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="c50d1-146">This page contains a form for local account sign-up based on an email address or a user name.</span></span> <span data-ttu-id="c50d1-147">formulario de Hello puede contener diferentes controles de entrada como cuadro de entrada de texto, cuadro de entrada de contraseña, botón de radio, cuadros de lista desplegable de selección única y casillas de verificación de selección múltiple.</span><span class="sxs-lookup"><span data-stu-id="c50d1-147">hello form can contain different input controls such as text input box, password entry box, radio button, single-select drop-down boxes, and multi-select check boxes.</span></span>

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

### <a name="fragment-inserted-into-hello-social-account-sign-up-page"></a><span data-ttu-id="c50d1-148">Fragmento inserta Hola "" Social página de cuentas de inicio de sesión"</span><span class="sxs-lookup"><span data-stu-id="c50d1-148">Fragment inserted into hello ""Social account sign-up page"</span></span>

<span data-ttu-id="c50d1-149">Esta página puede aparecer al registrarse con una cuenta existente de un proveedor de identidades de redes sociales, como Facebook o Google+.</span><span class="sxs-lookup"><span data-stu-id="c50d1-149">This page may appear when signing up using an existing account from a social identity provider such as Facebook or Google+.</span></span>  <span data-ttu-id="c50d1-150">Se utiliza cuando se debe recopilar información adicional de hello mediante un formulario de inicio de sesión del usuario final.</span><span class="sxs-lookup"><span data-stu-id="c50d1-150">It is used when additional information must be collected from hello end user using a sign-up form.</span></span> <span data-ttu-id="c50d1-151">Esta página es similar toohello cuenta local página de registro (que se muestra en la sección anterior de hello) con excepción de Hola de campos de entrada de contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="c50d1-151">This page is similar toohello local account sign-up page (shown in hello previous section) with hello exception of hello password entry fields.</span></span>

### <a name="fragment-inserted-into-hello-unified-sign-up-or-sign-in-page"></a><span data-ttu-id="c50d1-152">Fragmento inserta Hola "Unificado la página de inicio de sesión o inicio de sesión"</span><span class="sxs-lookup"><span data-stu-id="c50d1-152">Fragment inserted into hello "Unified sign-up or sign-in page"</span></span>

<span data-ttu-id="c50d1-153">Esta página controla tanto la suscripción como el inicio de sesión de los clientes, que pueden utilizar proveedores de identidades sociales como Facebook o Google +, o cuentas locales.</span><span class="sxs-lookup"><span data-stu-id="c50d1-153">This page handles both sign-up & sign-in of customers, who can use social identity providers such as Facebook or Google+, or local accounts.</span></span>

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

### <a name="fragment-inserted-into-hello-multi-factor-authentication-page"></a><span data-ttu-id="c50d1-154">Fragmento insertada Hola "página de la autenticación multifactor"</span><span class="sxs-lookup"><span data-stu-id="c50d1-154">Fragment inserted into hello "Multi-factor authentication page"</span></span>

<span data-ttu-id="c50d1-155">Esta página permite a los usuarios verificar sus números de teléfono (mediante texto o voz) durante el registro o el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="c50d1-155">On this page, users can verify their phone numbers (using text or voice) during sign-up or sign-in.</span></span>

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

### <a name="fragment-inserted-into-hello-error-page"></a><span data-ttu-id="c50d1-156">Fragmento inserta Hola "[NULL]"Página de Error de</span><span class="sxs-lookup"><span data-stu-id="c50d1-156">Fragment inserted into hello ""Error page"</span></span>

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

## <a name="localizing-your-html-content"></a><span data-ttu-id="c50d1-157">Localización del contenido HTML</span><span class="sxs-lookup"><span data-stu-id="c50d1-157">Localizing your HTML content</span></span>

<span data-ttu-id="c50d1-158">Puede localizar el contenido HTML mediante la activación de la característica ["Personalización de idioma"](active-directory-b2c-reference-language-customization.md).</span><span class="sxs-lookup"><span data-stu-id="c50d1-158">You can localize your HTML content by turning on ['Language customization'](active-directory-b2c-reference-language-customization.md).</span></span>  <span data-ttu-id="c50d1-159">Si habilita esta característica permite que Azure AD B2C tooforward Hola conectarse de identificador abierto parámetro, `ui-locales`, tooyour extremo.</span><span class="sxs-lookup"><span data-stu-id="c50d1-159">Enabling this feature allows Azure AD B2C tooforward hello Open ID Connect parameter, `ui-locales`, tooyour endpoint.</span></span>  <span data-ttu-id="c50d1-160">El servidor de contenido puede usar este páginas HTML tooprovide personalizado de parámetros que son específicos del idioma.</span><span class="sxs-lookup"><span data-stu-id="c50d1-160">Your content server can use this parameter tooprovide customized HTML pages that are language-specific.</span></span>

## <a name="things-tooremember-when-building-your-own-content"></a><span data-ttu-id="c50d1-161">Cosas tooremember al compilar su propio contenido</span><span class="sxs-lookup"><span data-stu-id="c50d1-161">Things tooremember when building your own content</span></span>

<span data-ttu-id="c50d1-162">Si tiene previsto característica de personalización de interfaz de usuario de página de toouse hello, revise Hola seguir las prácticas recomendadas:</span><span class="sxs-lookup"><span data-stu-id="c50d1-162">If you are planning toouse hello page UI customization feature, review hello following best practices:</span></span>

* <span data-ttu-id="c50d1-163">No copiar el contenido del hello Azure AD B2C valor predeterminado e intente toomodify lo.</span><span class="sxs-lookup"><span data-stu-id="c50d1-163">Don't copy hello Azure AD B2C's default content and attempt toomodify it.</span></span> <span data-ttu-id="c50d1-164">Se está toobuild mejor su contenido de HTML5 desde el principio y toouse contenido predeterminado como referencia.</span><span class="sxs-lookup"><span data-stu-id="c50d1-164">It is best toobuild your HTML5 content from scratch and toouse default content as reference.</span></span>
* <span data-ttu-id="c50d1-165">Por motivos de seguridad, no permitimos tooinclude todo el código JavaScript en el contenido.</span><span class="sxs-lookup"><span data-stu-id="c50d1-165">For security reasons, we don't allow you tooinclude any JavaScript in your content.</span></span> <span data-ttu-id="c50d1-166">La mayor parte de lo que necesita debe estar disponible fuera del cuadro de Hola.</span><span class="sxs-lookup"><span data-stu-id="c50d1-166">Most of what you need should be available out of hello box.</span></span> <span data-ttu-id="c50d1-167">Si no es así, use [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest nueva funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="c50d1-167">If not, use [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest new functionality.</span></span>
* <span data-ttu-id="c50d1-168">Versiones de explorador admitidas:</span><span class="sxs-lookup"><span data-stu-id="c50d1-168">Supported browser versions:</span></span>
  * <span data-ttu-id="c50d1-169">Internet Explorer 11, 10, Edge</span><span class="sxs-lookup"><span data-stu-id="c50d1-169">Internet Explorer 11, 10, Edge</span></span>
  * <span data-ttu-id="c50d1-170">Compatibilidad limitada con Internet Explorer 9, 8</span><span class="sxs-lookup"><span data-stu-id="c50d1-170">Limited support for Internet Explorer 9, 8</span></span>
  * <span data-ttu-id="c50d1-171">Google Chrome 42.0 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="c50d1-171">Google Chrome 42.0 and above</span></span>
  * <span data-ttu-id="c50d1-172">Mozilla Firefox 38.0 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="c50d1-172">Mozilla Firefox 38.0 and above</span></span>

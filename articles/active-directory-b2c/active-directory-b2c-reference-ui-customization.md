---
title: "Personalización de la interfaz de usuario - Azure AD B2C | Microsoft Docs"
description: "Tema sobre las características de personalización de la interfaz de usuario de Azure Active Directory B2C"
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
ms.openlocfilehash: 122fa997ea11b369aae3c59edf0043ab19d21aea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-customize-the-azure-ad-b2c-user-interface-ui"></a><span data-ttu-id="febc7-103">Azure Active Directory B2C: personalización de la interfaz de usuario de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="febc7-103">Azure Active Directory B2C: Customize the Azure AD B2C user interface (UI)</span></span>

<span data-ttu-id="febc7-104">La experiencia del usuario es primordial en una aplicación de cliente.</span><span class="sxs-lookup"><span data-stu-id="febc7-104">User experience is paramount in a customer facing application.</span></span>  <span data-ttu-id="febc7-105">Aumentar su base de clientes mediante el diseño de experiencias de usuario con la apariencia de su marca.</span><span class="sxs-lookup"><span data-stu-id="febc7-105">Grow your customer base by crafting user experiences with the look and feel of your brand.</span></span> <span data-ttu-id="febc7-106">Azure Active Directory B2C (Azure AD B2C) permite personalizar las páginas de registro, inicio de sesión, edición de perfil y restablecimiento de contraseña del cliente con control perfecto de píxeles.</span><span class="sxs-lookup"><span data-stu-id="febc7-106">Azure Active Directory B2C (Azure AD B2C) lets you customize sign-up, sign-in, profile editing, and password reset pages with pixel-perfect control.</span></span>

> [!NOTE]
> <span data-ttu-id="febc7-107">La característica de personalización de la interfaz de usuario de la página que se describe en este artículo no se aplica a la directiva de inicio de sesión único, a la página de restablecimiento de contraseña adjunta y a los correos electrónicos de verificación.</span><span class="sxs-lookup"><span data-stu-id="febc7-107">The page UI customization feature described in this article does not apply to the sign-in only policy, its accompanying password reset page, and verification emails.</span></span>  <span data-ttu-id="febc7-108">Estas características utilizan en su lugar la [característica de personalización de marca de empresa](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="febc7-108">These features use the [company branding feature](../active-directory/active-directory-add-company-branding.md) instead.</span></span>
>

<span data-ttu-id="febc7-109">En este artículo se tratan los temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="febc7-109">This article covers the following topics:</span></span>

* <span data-ttu-id="febc7-110">La característica de personalización de la interfaz de usuario de la página.</span><span class="sxs-lookup"><span data-stu-id="febc7-110">The page UI customization feature.</span></span>
* <span data-ttu-id="febc7-111">Una herramienta para cargar el contenido HTML en Azure Blob Storage para su uso con la característica de personalización de la interfaz de usuario de la página.</span><span class="sxs-lookup"><span data-stu-id="febc7-111">A tool for uploading HTML content to Azure Blob Storage for use with the page UI customization feature.</span></span>
* <span data-ttu-id="febc7-112">Los elementos de la interfaz de usuario que usa Azure AD B2C que se pueden personalizar con hojas de estilo CSS.</span><span class="sxs-lookup"><span data-stu-id="febc7-112">The UI elements used by Azure AD B2C that you can customize using Cascading Style Sheets (CSS).</span></span>
* <span data-ttu-id="febc7-113">Prácticas recomendadas al usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="febc7-113">Best practices when exercising this feature.</span></span>

## <a name="the-page-ui-customization-feature"></a><span data-ttu-id="febc7-114">La característica de personalización de la interfaz de usuario de la página</span><span class="sxs-lookup"><span data-stu-id="febc7-114">The page UI customization feature</span></span>

<span data-ttu-id="febc7-115">Puede personalizar la apariencia de las páginas de registro, inicio de sesión, restablecimiento de contraseña y edición de perfil del cliente (mediante la configuración de [directivas](active-directory-b2c-reference-policies.md)).</span><span class="sxs-lookup"><span data-stu-id="febc7-115">You can customize the look and feel of customer sign-up, sign-in, password reset, and profile-editing pages (by configuring [policies](active-directory-b2c-reference-policies.md)).</span></span> <span data-ttu-id="febc7-116">Sus clientes tendrán experiencias más libres al navegar entre su aplicación y las páginas que Azure AD B2C sirve.</span><span class="sxs-lookup"><span data-stu-id="febc7-116">Your customers get a seamless experience when navigating between your application and pages served by Azure AD B2C.</span></span>

<span data-ttu-id="febc7-117">A diferencia de otros servicios con opciones de interfaz de usuario, Azure AD B2C utiliza un enfoque simple y moderno a la personalización de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="febc7-117">Unlike other services where UI options, Azure AD B2C uses a simple and modern approach to UI customization.</span></span>

<span data-ttu-id="febc7-118">Funciona de la siguiente manera: Azure AD B2C ejecuta código en el explorador del consumidor y usa un enfoque moderno denominado [Uso compartido de recursos entre orígenes (CORS)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="febc7-118">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span>  <span data-ttu-id="febc7-119">En tiempo de ejecución, el contenido se carga desde una dirección URL especificada en una directiva.</span><span class="sxs-lookup"><span data-stu-id="febc7-119">At run-time, content is loaded from a URL that you specify in a policy.</span></span> <span data-ttu-id="febc7-120">Puede especificar diferentes direcciones URL para distintas páginas.</span><span class="sxs-lookup"><span data-stu-id="febc7-120">You can specify different URLs for different pages.</span></span> <span data-ttu-id="febc7-121">Cuando el contenido cargado desde la dirección URL se combina con un fragmento HTML insertado en Azure AD B2C, se muestra la página al cliente.</span><span class="sxs-lookup"><span data-stu-id="febc7-121">After content loaded from your URL is merged with an HTML fragment inserted from Azure AD B2C, the page is displayed to your customer.</span></span> <span data-ttu-id="febc7-122">Todo lo que necesita hacer es:</span><span class="sxs-lookup"><span data-stu-id="febc7-122">All you need to do is:</span></span>

1. <span data-ttu-id="febc7-123">Crear contenido HTML5 con un elemento `<div id="api"></div>` vacío ubicado en algún lugar de `<body>`.</span><span class="sxs-lookup"><span data-stu-id="febc7-123">Create well-formed HTML5 content with an empty `<div id="api"></div>` element located somewhere in the `<body>`.</span></span> <span data-ttu-id="febc7-124">Ese elemento marca el lugar en el que se inserta el contenido de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="febc7-124">This element marks where the Azure AD B2C content is inserted.</span></span>
1. <span data-ttu-id="febc7-125">Hospedar el contenido en un punto de conexión HTTPS (donde se permite CORS).</span><span class="sxs-lookup"><span data-stu-id="febc7-125">Host your content on an HTTPS endpoint (with CORS allowed).</span></span> <span data-ttu-id="febc7-126">Tenga en cuenta que los métodos de solicitud GET y OPTIONS se deben habilitar al configurar CORS.</span><span class="sxs-lookup"><span data-stu-id="febc7-126">Note both GET and OPTIONS request methods must be enabled when configuring CORS.</span></span>
1. <span data-ttu-id="febc7-127">Utilice CSS para aplicar estilo a los elementos de la interfaz de usuario que inserta Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="febc7-127">Use CSS to style the UI elements that Azure AD B2C inserts.</span></span>

### <a name="a-basic-example-of-customized-html"></a><span data-ttu-id="febc7-128">Un ejemplo básico de HTML personalizado</span><span class="sxs-lookup"><span data-stu-id="febc7-128">A basic example of customized HTML</span></span>

<span data-ttu-id="febc7-129">A continuación se muestra un ejemplo del contenido HTML más básico que se puede utilizar para probar esta funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="febc7-129">The following example is the most basic HTML content that you can use to test this capability.</span></span> <span data-ttu-id="febc7-130">Use la [herramienta auxiliar](active-directory-b2c-reference-ui-customization-helper-tool.md) para cargar y configurar este contenido en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="febc7-130">Use the [helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) to upload and configure this content on your Azure Blob storage.</span></span> <span data-ttu-id="febc7-131">A continuación, puede comprobar que los botones básicos, sin estilo y los campos de formulario de cada página se muestran y funcionan.</span><span class="sxs-lookup"><span data-stu-id="febc7-131">You can then verify that the basic, non-stylized buttons & form fields on each page are displayed and functional.</span></span>

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

## <a name="test-out-the-ui-customization-feature"></a><span data-ttu-id="febc7-132">Prueba de la característica de personalización de la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="febc7-132">Test out the UI customization feature</span></span>

<span data-ttu-id="febc7-133">¿Desea probar la característica de personalización de la interfaz de usuario con nuestro contenido HTML y CSS de ejemplo?</span><span class="sxs-lookup"><span data-stu-id="febc7-133">Want to try out the UI customization feature by using our sample HTML and CSS content?</span></span>  <span data-ttu-id="febc7-134">Hemos proporcionado [una herramienta auxiliar](active-directory-b2c-reference-ui-customization-helper-tool.md) que carga y configura el contenido de ejemplo en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="febc7-134">We've provided you [a helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures sample content on your Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="febc7-135">El contenido de la interfaz de usuario se puede hospedar en cualquier lugar: en servidores web, CDN, AWS S3, sistemas de uso compartido de archivos, etc. Mientras el contenido se hospede en un punto de conexión HTTPS disponible públicamente con CORS habilitado, puede continuar.</span><span class="sxs-lookup"><span data-stu-id="febc7-135">You can host your UI content anywhere: on web servers, CDNs, AWS S3, file sharing systems, etc. As long as the content is hosted on a publicly available HTTPS endpoint with CORS enabled, you are good to go.</span></span> <span data-ttu-id="febc7-136">Almacenamiento de blobs de Azure se usa solo con fines ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="febc7-136">We are using Azure Blob storage for illustrative purposes only.</span></span>
>

## <a name="the-ui-fragments-embedded-by-azure-ad-b2c"></a><span data-ttu-id="febc7-137">Fragmentos de la interfaz de usuario insertados por Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="febc7-137">The UI fragments embedded by Azure AD B2C</span></span>

<span data-ttu-id="febc7-138">En las secciones siguientes se muestran fragmentos de HTML5 que Azure AD B2C combina en el elemento `<div id="api"></div>` que se encuentra en su contenido.</span><span class="sxs-lookup"><span data-stu-id="febc7-138">The following sections list the HTML5 fragments that Azure AD B2C merges into the `<div id="api"></div>` element located in your content.</span></span> <span data-ttu-id="febc7-139">**No inserte estos fragmentos en el contenido de HTML 5.**</span><span class="sxs-lookup"><span data-stu-id="febc7-139">**Do not insert these fragments in your HTML 5 content.**</span></span> <span data-ttu-id="febc7-140">El servicio Azure AD B2C los inserta en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="febc7-140">The Azure AD B2C service inserts them in at run-time.</span></span> <span data-ttu-id="febc7-141">Use estos fragmentos como referencia al diseñar sus propias hojas de estilo CSS.</span><span class="sxs-lookup"><span data-stu-id="febc7-141">Use these fragments as a reference when designing your own Cascading Style Sheets (CSS).</span></span>

### <a name="fragment-inserted-into-the-identity-provider-selection-page"></a><span data-ttu-id="febc7-142">Fragmento insertado en la "página de selección de proveedores de identidades"</span><span class="sxs-lookup"><span data-stu-id="febc7-142">Fragment inserted into the "Identity provider selection page"</span></span>

<span data-ttu-id="febc7-143">Esta página contiene una lista de proveedores de identidades que el usuario puede elegir durante el registro o el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="febc7-143">This page contains a list of identity providers that the user can choose from during sign-up or sign-in.</span></span> <span data-ttu-id="febc7-144">Estos botones incluyen los proveedores de identidades sociales como Facebook y Google+ o las cuentas locales (basadas en una dirección de correo electrónico o un nombre de usuario).</span><span class="sxs-lookup"><span data-stu-id="febc7-144">These buttons include social identity providers such as Facebook and Google+, or local accounts (based on email address or user name).</span></span>

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

### <a name="fragment-inserted-into-the-local-account-sign-up-page"></a><span data-ttu-id="febc7-145">Fragmento insertado en la "página de registro de la cuenta local"</span><span class="sxs-lookup"><span data-stu-id="febc7-145">Fragment inserted into the "Local account sign-up page"</span></span>

<span data-ttu-id="febc7-146">Esta página contiene un formulario para el registro en una cuenta local basada en una dirección de correo electrónico o un nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="febc7-146">This page contains a form for local account sign-up based on an email address or a user name.</span></span> <span data-ttu-id="febc7-147">El formulario puede contener diferentes controles de entrada, como un cuadro de entrada de texto, un cuadro de entrada de contraseña, un botón de radio, cuadros desplegables de selección única y casillas de verificación de selección múltiple.</span><span class="sxs-lookup"><span data-stu-id="febc7-147">The form can contain different input controls such as text input box, password entry box, radio button, single-select drop-down boxes, and multi-select check boxes.</span></span>

```HTML
<div id="api" data-name="SelfAsserted">
    <div class="intro">
        <p>Create your account by providing the following details</p>
    </div>

    <div id="attributeVerification">
        <div class="errorText" id="passwordEntryMismatch" style="display: none;">The password entry fields do not match. Please enter the same password in both fields and try again.</div>
        <div class="errorText" id="requiredFieldMissing" style="display: none;">A required field is missing. Please fill out all required fields and try again.</div>
        <div class="errorText" id="fieldIncorrect" style="display: none;">One or more fields are filled out incorrectly. Please check your entries and try again.</div>
        <div class="errorText" id="claimVerificationServerError" style="display: none;"></div>
        <div class="attr" id="attributeList">
            <ul>
                <li>
                    <div class="attrEntry validate">
                        <div>
                            <div class="verificationInfoText" id="email_intro" style="display: inline;">Verification is necessary. Please click Send button.</div>
                            <div class="verificationInfoText" id="email_info" style="display:none">Verification code has been sent to your inbox. Please copy it to the input box below.</div>
                            <div class="verificationSuccessText" id="email_success" style="display:none">E-mail address verified. You can now continue.</div>
                            <div class="verificationErrorText" id="email_fail_retry" style="display:none">Incorrect code, try again.</div>
                            <div class="verificationErrorText" id="email_fail_no_retry" style="display:none">Exceeded number of retries you need to send new code.</div>
                            <div class="verificationErrorText" id="email_fail_server" style="display:none">Server error, please try again</div>
                            <div class="verificationErrorText" id="email_incorrect_format" style="display:none">Incorect format.</div>
                        </div>

                    <div class="helpText show">This information is required</div>
                        <label>Email</label>
                        <input id="email" class="textInput" type="text" placeholder="Email" required="" autofocus=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Email address that can be used to contact you.');" class="tiny">What is this?</a>

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
                        <div class="helpText">8-16 characters, containing 3 out of 4 of the following: Lowercase characters, uppercase characters, digits (0-9), and one or more of the following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ " ( ) ; .This information is required</div>
                        <label>Enter password</label>
                        <input id="password" class="textInput" type="password" placeholder="Enter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title="8-16 characters, containing 3 out of 4 of the following: Lowercase characters, uppercase characters, digits (0-9), and one or more of the following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Enter password');" class="tiny">What is this?</a>
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
                        <input id="postalCode" class="textInput" type="text" placeholder="Zip code" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('The postal code of your address.');" class="tiny">What is this?</a>
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

### <a name="fragment-inserted-into-the-social-account-sign-up-page"></a><span data-ttu-id="febc7-148">Fragmento insertado en la "página de registro de la cuenta de redes sociales"</span><span class="sxs-lookup"><span data-stu-id="febc7-148">Fragment inserted into the ""Social account sign-up page"</span></span>

<span data-ttu-id="febc7-149">Esta página puede aparecer al registrarse con una cuenta existente de un proveedor de identidades de redes sociales, como Facebook o Google+.</span><span class="sxs-lookup"><span data-stu-id="febc7-149">This page may appear when signing up using an existing account from a social identity provider such as Facebook or Google+.</span></span>  <span data-ttu-id="febc7-150">Se utiliza cuando se debe recopilar información adicional del usuario final mediante un formulario de registro.</span><span class="sxs-lookup"><span data-stu-id="febc7-150">It is used when additional information must be collected from the end user using a sign-up form.</span></span> <span data-ttu-id="febc7-151">Esta página es similar a la página de registro de cuenta local (que se muestra en la sección anterior) con la excepción de los campos de entrada de contraseña.</span><span class="sxs-lookup"><span data-stu-id="febc7-151">This page is similar to the local account sign-up page (shown in the previous section) with the exception of the password entry fields.</span></span>

### <a name="fragment-inserted-into-the-unified-sign-up-or-sign-in-page"></a><span data-ttu-id="febc7-152">Fragmento insertado en la "página de registro o de inicio de sesión unificada"</span><span class="sxs-lookup"><span data-stu-id="febc7-152">Fragment inserted into the "Unified sign-up or sign-in page"</span></span>

<span data-ttu-id="febc7-153">Esta página controla tanto la suscripción como el inicio de sesión de los clientes, que pueden utilizar proveedores de identidades sociales como Facebook o Google +, o cuentas locales.</span><span class="sxs-lookup"><span data-stu-id="febc7-153">This page handles both sign-up & sign-in of customers, who can use social identity providers such as Facebook or Google+, or local accounts.</span></span>

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

### <a name="fragment-inserted-into-the-multi-factor-authentication-page"></a><span data-ttu-id="febc7-154">Fragmento insertado en la "página de autenticación multifactor"</span><span class="sxs-lookup"><span data-stu-id="febc7-154">Fragment inserted into the "Multi-factor authentication page"</span></span>

<span data-ttu-id="febc7-155">Esta página permite a los usuarios verificar sus números de teléfono (mediante texto o voz) durante el registro o el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="febc7-155">On this page, users can verify their phone numbers (using text or voice) during sign-up or sign-in.</span></span>

```HTML
<div id="api" data-name="Phonefactor">
    <div id="phonefactor_initial">
        <div class="intro">
            <p>Enter a number below that we can send a code via SMS or phone to authenticate you.</p>
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

### <a name="fragment-inserted-into-the-error-page"></a><span data-ttu-id="febc7-156">Fragmento insertado en la ""página de error"</span><span class="sxs-lookup"><span data-stu-id="febc7-156">Fragment inserted into the ""Error page"</span></span>

```HTML
<div id="api" class="error-page-content" data-name="GlobalException">
    <h2>Sorry, but we're having trouble signing you in.</h2>
    <div class="error-page-help">We track these errors automatically, but if the problem persists feel free to contact us. In the meantime, please try again.</div>
    <div class="error-page-messagedetails">Your administrator hasn't provided any contact details.</div>
    <div class="error-page-messagedetails">
        <div class="error-page-correlationid">Correlation ID:1c4f0397-c6e4-4afe-bf74-42f488f2f15f</div>
        <div>Timestamp:2015-09-14 23:22:35Z</div>
        <div class="error-page-detail">AADB2C90065: A B2C client-side error 'Access is denied.' has occurred requesting the remote resource.</div>
    </div>
</div>
```

## <a name="localizing-your-html-content"></a><span data-ttu-id="febc7-157">Localización del contenido HTML</span><span class="sxs-lookup"><span data-stu-id="febc7-157">Localizing your HTML content</span></span>

<span data-ttu-id="febc7-158">Puede localizar el contenido HTML mediante la activación de la característica ["Personalización de idioma"](active-directory-b2c-reference-language-customization.md).</span><span class="sxs-lookup"><span data-stu-id="febc7-158">You can localize your HTML content by turning on ['Language customization'](active-directory-b2c-reference-language-customization.md).</span></span>  <span data-ttu-id="febc7-159">Al habilitar esta característica, Azure AD B2C puede reenviar el parámetro de OpenID Connect, `ui-locales`, al punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="febc7-159">Enabling this feature allows Azure AD B2C to forward the Open ID Connect parameter, `ui-locales`, to your endpoint.</span></span>  <span data-ttu-id="febc7-160">El servidor de contenido puede usar este parámetro para proporcionar páginas HTML personalizadas específicas del idioma.</span><span class="sxs-lookup"><span data-stu-id="febc7-160">Your content server can use this parameter to provide customized HTML pages that are language-specific.</span></span>

## <a name="things-to-remember-when-building-your-own-content"></a><span data-ttu-id="febc7-161">Elementos que debe recordar al crear su propio contenido</span><span class="sxs-lookup"><span data-stu-id="febc7-161">Things to remember when building your own content</span></span>

<span data-ttu-id="febc7-162">Si piensa usar la característica de personalización de la interfaz de usuario de la página, revise las siguientes prácticas recomendadas:</span><span class="sxs-lookup"><span data-stu-id="febc7-162">If you are planning to use the page UI customization feature, review the following best practices:</span></span>

* <span data-ttu-id="febc7-163">No copie el contenido predeterminado de Azure AD B2C ni intente modificarlo.</span><span class="sxs-lookup"><span data-stu-id="febc7-163">Don't copy the Azure AD B2C's default content and attempt to modify it.</span></span> <span data-ttu-id="febc7-164">Es preferible generar su propio contenido de HTML5 desde cero y usar la plantilla predeterminada como referencia.</span><span class="sxs-lookup"><span data-stu-id="febc7-164">It is best to build your HTML5 content from scratch and to use default content as reference.</span></span>
* <span data-ttu-id="febc7-165">Por motivos de seguridad, no le permitimos incluir cualquier código JavaScript en su contenido.</span><span class="sxs-lookup"><span data-stu-id="febc7-165">For security reasons, we don't allow you to include any JavaScript in your content.</span></span> <span data-ttu-id="febc7-166">La mayor parte de lo que necesita debería estar disponible de fábrica.</span><span class="sxs-lookup"><span data-stu-id="febc7-166">Most of what you need should be available out of the box.</span></span> <span data-ttu-id="febc7-167">De no ser así, utilice [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) para solicitar una nueva funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="febc7-167">If not, use [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) to request new functionality.</span></span>
* <span data-ttu-id="febc7-168">Versiones de explorador admitidas:</span><span class="sxs-lookup"><span data-stu-id="febc7-168">Supported browser versions:</span></span>
  * <span data-ttu-id="febc7-169">Internet Explorer 11, 10, Edge</span><span class="sxs-lookup"><span data-stu-id="febc7-169">Internet Explorer 11, 10, Edge</span></span>
  * <span data-ttu-id="febc7-170">Compatibilidad limitada con Internet Explorer 9, 8</span><span class="sxs-lookup"><span data-stu-id="febc7-170">Limited support for Internet Explorer 9, 8</span></span>
  * <span data-ttu-id="febc7-171">Google Chrome 42.0 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="febc7-171">Google Chrome 42.0 and above</span></span>
  * <span data-ttu-id="febc7-172">Mozilla Firefox 38.0 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="febc7-172">Mozilla Firefox 38.0 and above</span></span>

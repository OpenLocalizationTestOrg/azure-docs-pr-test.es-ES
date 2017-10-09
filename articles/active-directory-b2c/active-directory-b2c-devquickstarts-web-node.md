---
title: "aplicación del web Node.js aaaAdd tooa inicio de sesión para Azure B2C | Documentos de Microsoft"
description: "¿Cómo toobuild una aplicación web de Node.js que inicia sesión en los usuarios mediante el uso de un inquilino B2C."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: db97f84a-1f24-447b-b6d2-0265c6896b27
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 03/10/2017
ms.author: xerners
ms.openlocfilehash: b4c334b1f7a0669df2d0864140603dc55bbb5408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="5cc43-103">B2C de Azure AD: Agregar la aplicación web de inicio de sesión tooa Node.js</span><span class="sxs-lookup"><span data-stu-id="5cc43-103">Azure AD B2C: Add sign-in tooa Node.js web app</span></span>

<span data-ttu-id="5cc43-104">**Passport** es middleware de autenticación para Node.js.</span><span class="sxs-lookup"><span data-stu-id="5cc43-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="5cc43-105">Muy flexible y modular, Passport puede instalarse discretamente en cualquier aplicación web basada en Express o Restify.</span><span class="sxs-lookup"><span data-stu-id="5cc43-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="5cc43-106">Un conjunto completo de estrategias admite la autenticación mediante un nombre de usuario y contraseña, Facebook, Twitter, etc.</span><span class="sxs-lookup"><span data-stu-id="5cc43-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="5cc43-107">Hemos desarrollado una estrategia para Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5cc43-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="5cc43-108">Se instalará en este módulo y, a continuación, agregar hello Azure AD `passport-azure-ad` complemento.</span><span class="sxs-lookup"><span data-stu-id="5cc43-108">You will install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="5cc43-109">toodo, necesita:</span><span class="sxs-lookup"><span data-stu-id="5cc43-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="5cc43-110">Registrar una aplicación mediante Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5cc43-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="5cc43-111">Configurar el saludo de toouse aplicación `passport-azure-ad` complemento.</span><span class="sxs-lookup"><span data-stu-id="5cc43-111">Set up your app toouse hello `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="5cc43-112">Usar inicio de sesión de Passport tooissue y solicitudes de cierre de sesión tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="5cc43-112">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="5cc43-113">Imprimir los datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="5cc43-113">Print user data.</span></span>

<span data-ttu-id="5cc43-114">Hola código para este tutorial [se mantiene en GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="5cc43-114">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="5cc43-115">toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como un archivo .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="5cc43-115">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="5cc43-116">También puede clonar el esqueleto de hello:</span><span class="sxs-lookup"><span data-stu-id="5cc43-116">You can also clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="5cc43-117">aplicación Hello completado se proporciona al final de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="5cc43-117">hello completed application is provided at hello end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="5cc43-118">Obtener un directorio de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="5cc43-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="5cc43-119">Para poder usar Azure AD B2C, debe crear un directorio o inquilino.</span><span class="sxs-lookup"><span data-stu-id="5cc43-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="5cc43-120">Un directorio es un contenedor para todos los usuarios, las aplicaciones, los grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="5cc43-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="5cc43-121">Si aún no tiene uno, [cree un directorio B2C](active-directory-b2c-get-started.md) antes de continuar con esta guía.</span><span class="sxs-lookup"><span data-stu-id="5cc43-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="5cc43-122">Creación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="5cc43-122">Create an application</span></span>

<span data-ttu-id="5cc43-123">A continuación, debe toocreate una aplicación en el directorio B2C.</span><span class="sxs-lookup"><span data-stu-id="5cc43-123">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="5cc43-124">Esto proporciona información de Azure AD que necesita toocommunicate forma segura con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5cc43-124">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="5cc43-125">Ambos Hola aplicación cliente y API web se representará mediante un único **Id. de aplicación**, porque están formadas por una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="5cc43-125">Both hello client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="5cc43-126">toocreate una aplicación, siga [estas instrucciones](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="5cc43-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="5cc43-127">Asegúrese de:</span><span class="sxs-lookup"><span data-stu-id="5cc43-127">Be sure to:</span></span>

- <span data-ttu-id="5cc43-128">Incluir un **aplicación web**/**web API** en aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="5cc43-128">Include a **web app**/**web API** in hello application.</span></span>
- <span data-ttu-id="5cc43-129">Escribir `http://localhost:3000/auth/openid/return` como **Dirección URL de respuesta**.</span><span class="sxs-lookup"><span data-stu-id="5cc43-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="5cc43-130">Es dirección URL predeterminada de Hola para este ejemplo de código.</span><span class="sxs-lookup"><span data-stu-id="5cc43-130">It is hello default URL for this code sample.</span></span>
- <span data-ttu-id="5cc43-131">Crear un **secreto de aplicación** para la aplicación y copiarlo.</span><span class="sxs-lookup"><span data-stu-id="5cc43-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="5cc43-132">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="5cc43-132">You will need it later.</span></span> <span data-ttu-id="5cc43-133">Tenga en cuenta que este valor debe toobe [XML escape](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) antes de utilizarla.</span><span class="sxs-lookup"><span data-stu-id="5cc43-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="5cc43-134">Hola copia **Id. de aplicación** decir tooyour asignado aplicación.</span><span class="sxs-lookup"><span data-stu-id="5cc43-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="5cc43-135">También lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="5cc43-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="5cc43-136">Crear sus directivas</span><span class="sxs-lookup"><span data-stu-id="5cc43-136">Create your policies</span></span>

<span data-ttu-id="5cc43-137">En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="5cc43-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="5cc43-138">Esta aplicación contiene tres experiencias de identidad: registro, inicio de sesión e inicio de sesión mediante Facebook.</span><span class="sxs-lookup"><span data-stu-id="5cc43-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="5cc43-139">Deberá toocreate esta directiva de cada tipo, tal y como se describe en el [artículo de referencia de directiva](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="5cc43-139">You need toocreate this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="5cc43-140">Cuando cree las tres directivas, asegúrese de:</span><span class="sxs-lookup"><span data-stu-id="5cc43-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="5cc43-141">Elija hello **nombre para mostrar** y otros atributos de inicio de sesión en la directiva de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="5cc43-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="5cc43-142">Elija hello **nombre para mostrar** y **Id. de objeto** notificaciones de la aplicación en cada directiva.</span><span class="sxs-lookup"><span data-stu-id="5cc43-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="5cc43-143">Puede elegir también otras notificaciones.</span><span class="sxs-lookup"><span data-stu-id="5cc43-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="5cc43-144">Hola copia **nombre** de cada directiva después de haberlo creado.</span><span class="sxs-lookup"><span data-stu-id="5cc43-144">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="5cc43-145">Deberían tener el prefijo de hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="5cc43-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="5cc43-146">Necesitará estos nombres de directiva más adelante.</span><span class="sxs-lookup"><span data-stu-id="5cc43-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="5cc43-147">Después de crear las directivas de tres, está listo toobuild la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5cc43-147">After you create your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="5cc43-148">Tenga en cuenta que este artículo no cubre cómo las directivas de hello toouse que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="5cc43-148">Note that this article does not cover how toouse hello policies you just created.</span></span> <span data-ttu-id="5cc43-149">toolearn acerca de cómo funcionan las directivas en Azure AD B2C, comience con hello [.NET web app tutorial de introducción](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5cc43-149">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-tooyour-directory"></a><span data-ttu-id="5cc43-150">Agregar directorio tooyour de requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5cc43-150">Add prerequisites tooyour directory</span></span>

<span data-ttu-id="5cc43-151">Desde la línea de comandos de hello, cambiar carpeta de raíz de tooyour de directorios, si no está ya no existe.</span><span class="sxs-lookup"><span data-stu-id="5cc43-151">From hello command line, change directories tooyour root folder, if you're not already there.</span></span> <span data-ttu-id="5cc43-152">Ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="5cc43-152">Run hello following commands:</span></span>

- `npm install express`
- `npm install ejs`
- `npm install ejs-locals`
- `npm install restify`
- `npm install mongoose`
- `npm install bunyan`
- `npm install assert-plus`
- `npm install passport`
- `npm install webfinger`
- `npm install body-parser`
- `npm install express-session`
- `npm install cookie-parser`

<span data-ttu-id="5cc43-153">Además, hemos usado `passport-azure-ad` para la versión preliminar de esqueleto Hola de hello inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="5cc43-153">In addition, we used `passport-azure-ad` for our preview in hello skeleton of hello Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="5cc43-154">Este modo se instalará las bibliotecas de Hola que `passport-azure-ad` depende.</span><span class="sxs-lookup"><span data-stu-id="5cc43-154">This will install hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a><span data-ttu-id="5cc43-155">Configurar su Hola de toouse aplicación Node.js Passport estrategia</span><span class="sxs-lookup"><span data-stu-id="5cc43-155">Set up your app toouse hello Passport-Node.js strategy</span></span>
<span data-ttu-id="5cc43-156">Configurar Hola Express middleware toouse Hola protocolo de autenticación OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="5cc43-156">Configure hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="5cc43-157">Passport puede tooissue usa las solicitudes de inicio de sesión y cierre de sesión, administrar sesiones de usuario y obtener información acerca de los usuarios, entre otras acciones.</span><span class="sxs-lookup"><span data-stu-id="5cc43-157">Passport will be used tooissue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="5cc43-158">Abra hello `config.js` un archivo en la raíz de hello del proyecto de Hola y escriba los valores de configuración de la aplicación en hello `exports.creds` sección.</span><span class="sxs-lookup"><span data-stu-id="5cc43-158">Open hello `config.js` file in hello root of hello project and enter your app's configuration values in hello `exports.creds` section.</span></span>
- <span data-ttu-id="5cc43-159">`clientID`: Hola **Id. de aplicación** asignado tooyour aplicación de portal de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="5cc43-159">`clientID`: hello **Application ID** assigned tooyour app in hello registration portal.</span></span>
- <span data-ttu-id="5cc43-160">`returnURL`: Hola **URI de redireccionamiento** que especificó en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cc43-160">`returnURL`: hello **Redirect URI** you entered in hello portal.</span></span>
- <span data-ttu-id="5cc43-161">`tenantName`: nombre del inquilino hello de la aplicación, por ejemplo, **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="5cc43-161">`tenantName`: hello tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="5cc43-162">Abra hello `app.js` archivo en hello raíz del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cc43-162">Open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="5cc43-163">Agregar Hola después llamada tooinvoke hello `OIDCStrategy` estrategia que se incluye con `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="5cc43-163">Add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="5cc43-164">Usar estrategia Hola simplemente hace referencia a las solicitudes de inicio de sesión de toohandle.</span><span class="sxs-lookup"><span data-stu-id="5cc43-164">Use hello strategy you just referenced toohandle sign-in requests.</span></span>

```JavaScript
// Use hello OIDCStrategy in Passport (Section 2).
//
//   Strategies in Passport require a "validate" function that accepts
//   credentials (in this case, an OpenID identifier), and invokes a callback
//   by using a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    skipUserProfile: config.creds.skipUserProfile,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    tenantName: config.creds.tenantName
  },
  function(iss, sub, profile, accessToken, refreshToken, done) {
    log.info('Example: Email address we received was: ', profile.email);
    // asynchronous verification, for effect...
    process.nextTick(function () {
      findByEmail(profile.email, function(err, user) {
        if (err) {
          return done(err);
        }
        if (!user) {
          // "Auto-registration"
          users.push(profile);
          return done(null, profile);
        }
        return done(null, user);
      });
    });
  }
));
```
<span data-ttu-id="5cc43-165">Passport utiliza un patrón similar para todas sus estrategias (incluidos Twitter y Facebook).</span><span class="sxs-lookup"><span data-stu-id="5cc43-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="5cc43-166">Todos los escritores de estrategia cumplen toothis patrón.</span><span class="sxs-lookup"><span data-stu-id="5cc43-166">All strategy writers adhere toothis pattern.</span></span> <span data-ttu-id="5cc43-167">Al examinar la estrategia de hello, puede ver que se pasa un `function()` que tiene un símbolo (token) y un `done` como parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cc43-167">When you look at hello strategy, you can see that you pass it a `function()` that has a token and a `done` as hello parameters.</span></span> <span data-ttu-id="5cc43-168">estrategia de Hello vuelve a estar tooyou después de que lo ha hecho todo su trabajo.</span><span class="sxs-lookup"><span data-stu-id="5cc43-168">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="5cc43-169">Almacenar usuario hello y guardado provisional de token de Hola por lo que no es necesario tooask para este nuevo.</span><span class="sxs-lookup"><span data-stu-id="5cc43-169">Store hello user and stash hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="5cc43-170">Hello código anterior toma todos los usuarios que se autentica el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cc43-170">hello preceding code takes all users whom hello server authenticates.</span></span> <span data-ttu-id="5cc43-171">Esto se conoce como registro automático.</span><span class="sxs-lookup"><span data-stu-id="5cc43-171">This is autoregistration.</span></span> <span data-ttu-id="5cc43-172">Cuando se usan servidores de producción, no desea toolet en los usuarios a menos que han pasado por un proceso de registro que ha configurado.</span><span class="sxs-lookup"><span data-stu-id="5cc43-172">When you use production servers, you don’t want toolet in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="5cc43-173">Este patrón se puede ver a menudo en las aplicaciones de consumidor,</span><span class="sxs-lookup"><span data-stu-id="5cc43-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="5cc43-174">Estos permiten tooregister mediante el uso de Facebook, pero, a continuación, le piden toofill información adicional.</span><span class="sxs-lookup"><span data-stu-id="5cc43-174">These allow you tooregister by using Facebook, but then they ask you toofill out additional information.</span></span> <span data-ttu-id="5cc43-175">Si la aplicación no era un ejemplo, podríamos extraer una dirección de correo electrónico del objeto de símbolo (token) de Hola que se devuelve y a continuación, pida Hola usuario toofill información adicional.</span><span class="sxs-lookup"><span data-stu-id="5cc43-175">If our application wasn’t a sample, we could extract an email address from hello token object that is returned, and then ask hello user toofill out additional information.</span></span> <span data-ttu-id="5cc43-176">Dado que se trata de un servidor de prueba, sólo tenemos que agregar base de datos de los usuarios toohello en memoria.</span><span class="sxs-lookup"><span data-stu-id="5cc43-176">Because this is a test server, we simply add users toohello in-memory database.</span></span>

<span data-ttu-id="5cc43-177">Agregar métodos de Hola que le permiten tookeep realizar un seguimiento de los usuarios que iniciaron sesión, según sea necesario mediante la cuenta de Passport.</span><span class="sxs-lookup"><span data-stu-id="5cc43-177">Add hello methods that allow you tookeep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="5cc43-178">Esta operación incluye la serialización y deserialización de la información del usuario:</span><span class="sxs-lookup"><span data-stu-id="5cc43-178">This includes serializing and deserializing user information:</span></span>

```JavaScript

// Passport session setup. (Section 2)

//   toosupport persistent sign-in sessions, Passport needs toobe able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing hello user ID when Passport serializes a user
//   and finding hello user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array toohold users who have signed in
var users = [];

var findByEmail = function(email, fn) {
  for (var i = 0, len = users.length; i < len; i++) {
    var user = users[i];
    log.info('we are using user: ', user);
    if (user.email === email) {
      return fn(null, user);
    }
  }
  return fn(null, null);
};

```

<span data-ttu-id="5cc43-179">Agregar motor de hello código tooload Hola Express.</span><span class="sxs-lookup"><span data-stu-id="5cc43-179">Add hello code tooload hello Express engine.</span></span> <span data-ttu-id="5cc43-180">En los siguientes valores hello, puede ver que utilizamos predeterminado de hello `/views` y `/routes` patrón que Express proporciona.</span><span class="sxs-lookup"><span data-stu-id="5cc43-180">In hello following, you can see that we use hello default `/views` and `/routes` pattern that Express provides.</span></span>

```JavaScript

// configure Express (Section 2)

var app = express();


app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'ejs');
  app.use(express.logger());
  app.use(express.methodOverride());
  app.use(cookieParser());
  app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
  app.use(bodyParser.urlencoded({ extended : true }));
  // Initialize Passport!  Also use passport.session() middleware toosupport
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

<span data-ttu-id="5cc43-181">Agregar hello `POST` rutas que entregan hello las solicitudes de inicio de sesión real toohello `passport-azure-ad` motor:</span><span class="sxs-lookup"><span data-stu-id="5cc43-181">Add hello `POST` routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. hello first step in OpenID authentication involves redirecting
//   hello user tooan OpenID provider. After hello user is authenticated,
//   hello OpenID provider redirects hello user back toothis application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in hello Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it redirects hello user toohello home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it will redirect hello user toohello home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="5cc43-182">Usar inicio de sesión de Passport tooissue y solicitudes de cierre de sesión tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="5cc43-182">Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>

<span data-ttu-id="5cc43-183">La aplicación ya está configurada correctamente toocommunicate con el punto de conexión de hello v2.0 con el protocolo de autenticación de OpenID Connect de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cc43-183">Your app is now properly configured toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="5cc43-184">`passport-azure-ad`se ocupa de los detalles de Hola de transmitir mensajes de autenticación, validar los tokens de Azure AD y mantener la sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="5cc43-184">`passport-azure-ad` has taken care of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="5cc43-185">Lo único que queda es toogive a los usuarios una manera toosign en e inicie sesión fuera y toogather obtener información adicional sobre los usuarios que iniciaron sesión.</span><span class="sxs-lookup"><span data-stu-id="5cc43-185">All that remains is toogive your users a way toosign in and sign out, and toogather additional information on users who have signed in.</span></span>

<span data-ttu-id="5cc43-186">En primer lugar, agregue predeterminado de hello, inicio de sesión, cuenta y métodos de cierre de sesión tooyour `app.js` archivo:</span><span class="sxs-lookup"><span data-stu-id="5cc43-186">First, add hello default, sign-in, account, and sign-out methods tooyour `app.js` file:</span></span>

```JavaScript

//Routes (Section 4)

app.get('/', function(req, res){
  res.render('index', { user: req.user });
});

app.get('/account', ensureAuthenticated, function(req, res){
  res.render('account', { user: req.user });
});

app.get('/login',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Login was called in hello Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

<span data-ttu-id="5cc43-187">tooreview estos métodos en detalle:</span><span class="sxs-lookup"><span data-stu-id="5cc43-187">tooreview these methods in detail:</span></span>
- <span data-ttu-id="5cc43-188">Hola `/` ruta redirige toohello `index.ejs` vista pasando usuario hello en solicitud de hello (si existe).</span><span class="sxs-lookup"><span data-stu-id="5cc43-188">hello `/` route redirects toohello `index.ejs` view by passing hello user in hello request (if it exists).</span></span>
- <span data-ttu-id="5cc43-189">Hola `/account` ruta comprueba primero que se autentiquen (Hola implementación para está por debajo).</span><span class="sxs-lookup"><span data-stu-id="5cc43-189">hello `/account` route first verifies that you are authenticated (hello implementation for this is below).</span></span> <span data-ttu-id="5cc43-190">A continuación, pasa usuario hello en solicitud de Hola para que pueda obtener información adicional acerca del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cc43-190">It then passes hello user in hello request so that you can get additional information about hello user.</span></span>
- <span data-ttu-id="5cc43-191">Hola `/login` ruta llamadas hello `azuread-openidconnect` autenticador de `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="5cc43-191">hello `/login` route calls hello `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="5cc43-192">Si no tiene éxito, ruta de hello redirige nuevo usuario de hello demasiado`/login`.</span><span class="sxs-lookup"><span data-stu-id="5cc43-192">If it doesn't succeed, hello route redirects hello user back too`/login`.</span></span>
- <span data-ttu-id="5cc43-193">`/logout` simplemente llama a `logout.ejs` (y a su ruta).</span><span class="sxs-lookup"><span data-stu-id="5cc43-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="5cc43-194">Esto borra las cookies y, a continuación, devuelve Hola nuevo usuario demasiado`index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="5cc43-194">This clears cookies and then returns hello user back too`index.ejs`.</span></span>


<span data-ttu-id="5cc43-195">Para la última parte de Hola de `app.js`, agregar hello `EnsureAuthenticated` método que se usa en hello `/account` ruta.</span><span class="sxs-lookup"><span data-stu-id="5cc43-195">For hello last part of `app.js`, add hello `EnsureAuthenticated` method that is used in hello `/account` route.</span></span>

```JavaScript

// Simple route middleware tooensure that hello user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs toobe protected. If
//   hello request is authenticated (typically via a persistent sign-in session),
//   then hello request will proceed. Otherwise, hello user will be redirected toothe
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

<span data-ttu-id="5cc43-196">Por último, cree el propio servidor hello en `app.js`.</span><span class="sxs-lookup"><span data-stu-id="5cc43-196">Finally, create hello server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a><span data-ttu-id="5cc43-197">Crear vistas de Hola y enruta en Express toocall las directivas</span><span class="sxs-lookup"><span data-stu-id="5cc43-197">Create hello views and routes in Express toocall your policies</span></span>

<span data-ttu-id="5cc43-198">`app.js` ya está completa.</span><span class="sxs-lookup"><span data-stu-id="5cc43-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="5cc43-199">Solo tiene las rutas de hello tooadd y vistas que permiten directivas de inicio de sesión y registro de hello toocall.</span><span class="sxs-lookup"><span data-stu-id="5cc43-199">You just need tooadd hello routes and views that allow you toocall hello sign-in and sign-up policies.</span></span> <span data-ttu-id="5cc43-200">Éstos también controlen hello `/logout` y `/login` rutas que creó.</span><span class="sxs-lookup"><span data-stu-id="5cc43-200">These also handle hello `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="5cc43-201">Crear hello `/routes/index.js` ruta en el directorio raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cc43-201">Create hello `/routes/index.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="5cc43-202">Crear hello `/routes/user.js` ruta en el directorio raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cc43-202">Create hello `/routes/user.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="5cc43-203">Vistas de solicitudes tooyour pasan estas rutas simples.</span><span class="sxs-lookup"><span data-stu-id="5cc43-203">These simple routes pass along requests tooyour views.</span></span> <span data-ttu-id="5cc43-204">Incluyen usuario hello, si hay alguno.</span><span class="sxs-lookup"><span data-stu-id="5cc43-204">They include hello user, if one is present.</span></span>

<span data-ttu-id="5cc43-205">Crear hello `/views/index.ejs` vista bajo el directorio raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cc43-205">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="5cc43-206">Se trata de una página simple que llama a las directivas de inicio y cierre de sesión. También puede usarlo toograb la información de cuenta.</span><span class="sxs-lookup"><span data-stu-id="5cc43-206">This is a simple page that calls policies for sign-in and sign-out. You can also use it toograb account information.</span></span> <span data-ttu-id="5cc43-207">Tenga en cuenta que puede usar Hola condicional `if (!user)` como usuario de Hola se pasa a través de solicitud de hello tooprovide evidencia ese usuario Hola ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="5cc43-207">Note that you can use hello conditional `if (!user)` as hello user is passed through in hello request tooprovide evidence that hello user is signed in.</span></span>

```JavaScript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login/?p=your facebook policy">Sign in with Facebook</a>
    <a href="/login/?p=your email sign-in policy">Sign in with email</a>
    <a href="/login/?p=your email sign-up policy">Sign up with email</a>
<% } else { %>
    <h2>Hello, <%= user.displayName %>.</h2>
    <a href="/account">Account info</a></br>
    <a href="/logout">Log out</a>
<% } %>
```

<span data-ttu-id="5cc43-208">Crear hello `/views/account.ejs` ver en el directorio raíz de Hola para que pueda ver información adicional que `passport-azure-ad` colocar en la solicitud del usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="5cc43-208">Create hello `/views/account.ejs` view under hello root directory so that you can view additional information that `passport-azure-ad` put in hello user request.</span></span>

```Javascript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login">Sign in</a>
<% } else { %>
<p>displayName: <%= user.displayName %></p>
<p>givenName: <%= user.name.givenName %></p>
<p>familyName: <%= user.name.familyName %></p>
<p>UPN: <%= user._json.upn %></p>
<p>Profile ID: <%= user.id %></p>
<p>Full Claims</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

<span data-ttu-id="5cc43-209">Ya puede compilar y ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5cc43-209">You can now build and run your app.</span></span>

<span data-ttu-id="5cc43-210">Ejecute `node app.js` y navegue demasiado`http://localhost:3000`</span><span class="sxs-lookup"><span data-stu-id="5cc43-210">Run `node app.js` and navigate too`http://localhost:3000`</span></span>


<span data-ttu-id="5cc43-211">Registrarse o iniciar sesión en la aplicación de toohello mediante correo electrónico o Facebook.</span><span class="sxs-lookup"><span data-stu-id="5cc43-211">Sign up or sign in toohello app by using email or Facebook.</span></span> <span data-ttu-id="5cc43-212">Cierre la sesión y vuelva a iniciarla con otro usuario.</span><span class="sxs-lookup"><span data-stu-id="5cc43-212">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="5cc43-213">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5cc43-213">Next steps</span></span>

<span data-ttu-id="5cc43-214">Como referencia, Hola completado ejemplo (sin los valores de configuración) [se proporciona como un archivo .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5cc43-214">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="5cc43-215">También puede clonarlo desde GitHub:</span><span class="sxs-lookup"><span data-stu-id="5cc43-215">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="5cc43-216">Ahora puede mover en toomore temas avanzados.</span><span class="sxs-lookup"><span data-stu-id="5cc43-216">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="5cc43-217">Puede probar:</span><span class="sxs-lookup"><span data-stu-id="5cc43-217">You might try:</span></span>

[<span data-ttu-id="5cc43-218">Proteger una API web mediante el modelo de hello B2C en Node.js</span><span class="sxs-lookup"><span data-stu-id="5cc43-218">Secure a web API by using hello B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->

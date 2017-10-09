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
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a>B2C de Azure AD: Agregar la aplicación web de inicio de sesión tooa Node.js

**Passport** es middleware de autenticación para Node.js. Muy flexible y modular, Passport puede instalarse discretamente en cualquier aplicación web basada en Express o Restify. Un conjunto completo de estrategias admite la autenticación mediante un nombre de usuario y contraseña, Facebook, Twitter, etc.

Hemos desarrollado una estrategia para Azure Active Directory (Azure AD). Se instalará en este módulo y, a continuación, agregar hello Azure AD `passport-azure-ad` complemento.

toodo, necesita:

1. Registrar una aplicación mediante Azure AD.
2. Configurar el saludo de toouse aplicación `passport-azure-ad` complemento.
3. Usar inicio de sesión de Passport tooissue y solicitudes de cierre de sesión tooAzure AD.
4. Imprimir los datos de usuario.

Hola código para este tutorial [se mantiene en GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS). toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como un archivo .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip). También puede clonar el esqueleto de hello:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

aplicación Hello completado se proporciona al final de Hola de este tutorial.

## <a name="get-an-azure-ad-b2c-directory"></a>Obtener un directorio de Azure AD B2C

Para poder usar Azure AD B2C, debe crear un directorio o inquilino.  Un directorio es un contenedor para todos los usuarios, las aplicaciones, los grupos, etc. Si aún no tiene uno, [cree un directorio B2C](active-directory-b2c-get-started.md) antes de continuar con esta guía.

## <a name="create-an-application"></a>Creación de una aplicación

A continuación, debe toocreate una aplicación en el directorio B2C. Esto proporciona información de Azure AD que necesita toocommunicate forma segura con la aplicación. Ambos Hola aplicación cliente y API web se representará mediante un único **Id. de aplicación**, porque están formadas por una aplicación lógica. toocreate una aplicación, siga [estas instrucciones](active-directory-b2c-app-registration.md). Asegúrese de:

- Incluir un **aplicación web**/**web API** en aplicación hello.
- Escribir `http://localhost:3000/auth/openid/return` como **Dirección URL de respuesta**. Es dirección URL predeterminada de Hola para este ejemplo de código.
- Crear un **secreto de aplicación** para la aplicación y copiarlo. Lo necesitará más adelante. Tenga en cuenta que este valor debe toobe [XML escape](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) antes de utilizarla.
- Hola copia **Id. de aplicación** decir tooyour asignado aplicación. También lo necesitará más adelante.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Crear sus directivas

En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md). Esta aplicación contiene tres experiencias de identidad: registro, inicio de sesión e inicio de sesión mediante Facebook. Deberá toocreate esta directiva de cada tipo, tal y como se describe en el [artículo de referencia de directiva](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Cuando cree las tres directivas, asegúrese de:

- Elija hello **nombre para mostrar** y otros atributos de inicio de sesión en la directiva de inicio de sesión.
- Elija hello **nombre para mostrar** y **Id. de objeto** notificaciones de la aplicación en cada directiva. Puede elegir también otras notificaciones.
- Hola copia **nombre** de cada directiva después de haberlo creado. Deberían tener el prefijo de hello `b2c_1_`.  Necesitará estos nombres de directiva más adelante.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Después de crear las directivas de tres, está listo toobuild la aplicación.

Tenga en cuenta que este artículo no cubre cómo las directivas de hello toouse que acaba de crear. toolearn acerca de cómo funcionan las directivas en Azure AD B2C, comience con hello [.NET web app tutorial de introducción](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="add-prerequisites-tooyour-directory"></a>Agregar directorio tooyour de requisitos previos

Desde la línea de comandos de hello, cambiar carpeta de raíz de tooyour de directorios, si no está ya no existe. Ejecute hello siguientes comandos:

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

Además, hemos usado `passport-azure-ad` para la versión preliminar de esqueleto Hola de hello inicio rápido.

- `npm install passport-azure-ad`

Este modo se instalará las bibliotecas de Hola que `passport-azure-ad` depende.

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a>Configurar su Hola de toouse aplicación Node.js Passport estrategia
Configurar Hola Express middleware toouse Hola protocolo de autenticación OpenID Connect. Passport puede tooissue usa las solicitudes de inicio de sesión y cierre de sesión, administrar sesiones de usuario y obtener información acerca de los usuarios, entre otras acciones.

Abra hello `config.js` un archivo en la raíz de hello del proyecto de Hola y escriba los valores de configuración de la aplicación en hello `exports.creds` sección.
- `clientID`: Hola **Id. de aplicación** asignado tooyour aplicación de portal de registro de hello.
- `returnURL`: Hola **URI de redireccionamiento** que especificó en el portal de Hola.
- `tenantName`: nombre del inquilino hello de la aplicación, por ejemplo, **contoso.onmicrosoft.com**.

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

Abra hello `app.js` archivo en hello raíz del proyecto de Hola. Agregar Hola después llamada tooinvoke hello `OIDCStrategy` estrategia que se incluye con `passport-azure-ad`.


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

Usar estrategia Hola simplemente hace referencia a las solicitudes de inicio de sesión de toohandle.

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
Passport utiliza un patrón similar para todas sus estrategias (incluidos Twitter y Facebook). Todos los escritores de estrategia cumplen toothis patrón. Al examinar la estrategia de hello, puede ver que se pasa un `function()` que tiene un símbolo (token) y un `done` como parámetros de Hola. estrategia de Hello vuelve a estar tooyou después de que lo ha hecho todo su trabajo. Almacenar usuario hello y guardado provisional de token de Hola por lo que no es necesario tooask para este nuevo.

> [!IMPORTANT]
Hello código anterior toma todos los usuarios que se autentica el servidor de Hola. Esto se conoce como registro automático. Cuando se usan servidores de producción, no desea toolet en los usuarios a menos que han pasado por un proceso de registro que ha configurado. Este patrón se puede ver a menudo en las aplicaciones de consumidor, Estos permiten tooregister mediante el uso de Facebook, pero, a continuación, le piden toofill información adicional. Si la aplicación no era un ejemplo, podríamos extraer una dirección de correo electrónico del objeto de símbolo (token) de Hola que se devuelve y a continuación, pida Hola usuario toofill información adicional. Dado que se trata de un servidor de prueba, sólo tenemos que agregar base de datos de los usuarios toohello en memoria.

Agregar métodos de Hola que le permiten tookeep realizar un seguimiento de los usuarios que iniciaron sesión, según sea necesario mediante la cuenta de Passport. Esta operación incluye la serialización y deserialización de la información del usuario:

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

Agregar motor de hello código tooload Hola Express. En los siguientes valores hello, puede ver que utilizamos predeterminado de hello `/views` y `/routes` patrón que Express proporciona.

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

Agregar hello `POST` rutas que entregan hello las solicitudes de inicio de sesión real toohello `passport-azure-ad` motor:

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

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Usar inicio de sesión de Passport tooissue y solicitudes de cierre de sesión tooAzure AD

La aplicación ya está configurada correctamente toocommunicate con el punto de conexión de hello v2.0 con el protocolo de autenticación de OpenID Connect de Hola. `passport-azure-ad`se ocupa de los detalles de Hola de transmitir mensajes de autenticación, validar los tokens de Azure AD y mantener la sesión de usuario. Lo único que queda es toogive a los usuarios una manera toosign en e inicie sesión fuera y toogather obtener información adicional sobre los usuarios que iniciaron sesión.

En primer lugar, agregue predeterminado de hello, inicio de sesión, cuenta y métodos de cierre de sesión tooyour `app.js` archivo:

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

tooreview estos métodos en detalle:
- Hola `/` ruta redirige toohello `index.ejs` vista pasando usuario hello en solicitud de hello (si existe).
- Hola `/account` ruta comprueba primero que se autentiquen (Hola implementación para está por debajo). A continuación, pasa usuario hello en solicitud de Hola para que pueda obtener información adicional acerca del usuario de Hola.
- Hola `/login` ruta llamadas hello `azuread-openidconnect` autenticador de `passport-azure-ad`. Si no tiene éxito, ruta de hello redirige nuevo usuario de hello demasiado`/login`.
- `/logout` simplemente llama a `logout.ejs` (y a su ruta). Esto borra las cookies y, a continuación, devuelve Hola nuevo usuario demasiado`index.ejs`.


Para la última parte de Hola de `app.js`, agregar hello `EnsureAuthenticated` método que se usa en hello `/account` ruta.

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

Por último, cree el propio servidor hello en `app.js`.

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a>Crear vistas de Hola y enruta en Express toocall las directivas

`app.js` ya está completa. Solo tiene las rutas de hello tooadd y vistas que permiten directivas de inicio de sesión y registro de hello toocall. Éstos también controlen hello `/logout` y `/login` rutas que creó.

Crear hello `/routes/index.js` ruta en el directorio raíz de Hola.

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

Crear hello `/routes/user.js` ruta en el directorio raíz de Hola.

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

Vistas de solicitudes tooyour pasan estas rutas simples. Incluyen usuario hello, si hay alguno.

Crear hello `/views/index.ejs` vista bajo el directorio raíz de Hola. Se trata de una página simple que llama a las directivas de inicio y cierre de sesión. También puede usarlo toograb la información de cuenta. Tenga en cuenta que puede usar Hola condicional `if (!user)` como usuario de Hola se pasa a través de solicitud de hello tooprovide evidencia ese usuario Hola ha iniciado sesión.

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

Crear hello `/views/account.ejs` ver en el directorio raíz de Hola para que pueda ver información adicional que `passport-azure-ad` colocar en la solicitud del usuario Hola.

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

Ya puede compilar y ejecutar la aplicación.

Ejecute `node app.js` y navegue demasiado`http://localhost:3000`


Registrarse o iniciar sesión en la aplicación de toohello mediante correo electrónico o Facebook. Cierre la sesión y vuelva a iniciarla con otro usuario.

##<a name="next-steps"></a>Pasos siguientes

Como referencia, Hola completado ejemplo (sin los valores de configuración) [se proporciona como un archivo .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip). También puede clonarlo desde GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

Ahora puede mover en toomore temas avanzados. Puede probar:

[Proteger una API web mediante el modelo de hello B2C en Node.js](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->

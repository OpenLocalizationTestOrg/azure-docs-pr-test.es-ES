---
title: "v2.0 de Active Directory de aaaAzure inicio de sesión en aplicaciones de web de Node.js | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toobuild una Node.js web aplicación que inicia sesión un usuario con una cuenta Microsoft personal y una cuenta profesional o educativa."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 1b889e72-f5c3-464a-af57-79abf5e2e147
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f8ce6e2b841c215cb14e82bcf444fe849634cc88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-nodejs-web-app"></a>Agregar la aplicación web de inicio de sesión tooa Node.js

> [!NOTE]
> No todas las características y escenarios de Azure Active Directory funcionan con el punto de conexión de hello v2.0. toodetermine si debe utilizar Hola v2.0 extremo u Hola v1.0, conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
> 

En este tutorial, usamos Hola de Passport toodo siguientes tareas:

* En una aplicación web, inicie sesión en usuario hello mediante Azure Active Directory (Azure AD) y Hola v2.0 extremo.
* Mostrar información acerca del usuario de Hola.
* Inicio de sesión Hola usuario fuera de la aplicación hello.

**Passport** es middleware de autenticación para Node.js. Passport, flexible y modular, se puede usar discretamente en cualquier aplicación web de Restify o basada en Express. En esta herramienta, un conjunto completo de estrategias admite la autenticación mediante nombre de usuario y contraseña, Facebook, Twitter y mucho más. Hemos desarrollado una estrategia para Azure AD. En este artículo, le mostramos cómo tooinstall Hola módulo y, a continuación, agregue hello Azure AD `passport-azure-ad` complemento.

## <a name="download"></a>Descargar
código de Hello para este tutorial se mantiene [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs). tutorial de hello toofollow, puede [descargar el esqueleto de la aplicación hello como un archivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) o esqueleto de Hola de clon:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

También puede obtener la aplicación hello completado final Hola de este tutorial.

## <a name="1-register-an-app"></a>1: Registro de una aplicación
Crear una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o seguir [estos pasos detallan](active-directory-v2-app-registration.md) tooregister una aplicación. Asegúrese de lo siguiente:

* Hola copia **Id. de aplicación** asignado tooyour aplicación. Lo necesitará en este tutorial.
* Agregar hello **Web** plataforma para la aplicación.
* Hola copia **URI de redireccionamiento** desde el portal de Hola. Debe usar el valor de identificador URI predeterminado de Hola de `urn:ietf:wg:oauth:2.0:oob`.

## <a name="2-add-prerequisities-tooyour-directory"></a>2: Agregar directorio tooyour de requisitos previos
En un símbolo del sistema, cambie la carpeta raíz de directorios toogo tooyour, si no está ya no existe. Ejecute hello siguientes comandos:

* `npm install express`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install restify`
* `npm install mongoose`
* `npm install bunyan`
* `npm install assert-plus`
* `npm install passport`
* `npm install webfinger`
* `npm install body-parser`
* `npm install express-session`
* `npm install cookie-parser`

Además, usamos `passport-azure-ad` en esqueleto Hola de inicio rápido de hello:

* `npm install passport-azure-ad`

Esto instala las bibliotecas de Hola que `passport-azure-ad` utiliza.

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>3: configurar la estrategia de aplicación toouse Hola js de nodo de passport
Configurar Hola Express middleware toouse Hola protocolo de autenticación OpenID Connect. Usar solicitudes de inicio de sesión y cierre de sesión de Passport tooissue, administrar la sesión del usuario de Hola y obtener información acerca del usuario de hello, entre otras cosas.

1.  En la raíz de hello del proyecto de hello, abra el archivo de Config.js de Hola. Hola `exports.creds` sección, escriba los valores de configuración de la aplicación.
  
  * `clientID`: Hola **identificador de la aplicación** que está asignado tooyour aplicación Hola portal de Azure.
  * `returnURL`: Hola **URI de redireccionamiento** especificado en el portal de Hola.
  * `clientSecret`: secreto de Hola que generó en el portal de Hola.

2.  En la raíz de hello del proyecto de hello, abra el archivo de App.js de Hola. tooinvoke hello OIDCStrategy stratey, que se incluye con `passport-azure-ad`, agregar Hola siguiente llamada:

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  toohandle, sus solicitudes de inicio de sesión, utilice estrategia de hello simplemente hace referencia:

  ```JavaScript
  // Use hello OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. hello function accepts
  //   credentials (in this case, an OpenID identifier), and invokes a callback
  //   with a user object.
  passport.use( new OIDCStrategy({
      callbackURL: config.creds.returnURL,
      realm: config.creds.realm,
      clientID: config.creds.clientID,
      clientSecret: config.creds.clientSecret,
      oidcIssuer: config.creds.issuer,
      identityMetadata: config.creds.identityMetadata,
      responseType: config.creds.responseType,
      responseMode: config.creds.responseMode,
      skipUserProfile: config.creds.skipUserProfile
      scope: config.creds.scope
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
      log.info('Example: Email address we received was: ', profile.email);
      // Asynchronous verification, for effect...
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

Passport usa un patrón similar para todas sus estrategias (Twitter, Facebook, etc.). Todos los escritores de estrategia cumplen toohello patrón. Pasar la estrategia de hello un `function()` que usa un token y `done` como parámetros. estrategia de Hola se devuelve cuando hace todo su trabajo. Almacenar usuario hello y token de hello complementario por lo que no necesita tooask para ella de nuevo.

  > [!IMPORTANT]
  > Hello código anterior toma cualquier usuario que puede autenticar el servidor de tooyour. Esto se conoce como registro automático. En un servidor de producción, desearía toolet cualquiera sin tener primero que les vaya a través de un proceso de registro que elija. Esto suele ser el patrón de Hola que se ve en aplicaciones de consumidor. aplicación Hello podrían tooregister con Facebook, pero, a continuación, le pide que tooenter obtener información adicional. Si no usa un programa de línea de comandos para este tutorial, podría extraer correo electrónico de Hola de objeto de símbolo (token) de Hola que se devuelve. A continuación, podría solicitar información adicional de hello usuario tooenter. Dado que se trata de un servidor de prueba, agregar usuario Hola directamente toohello en la memoria de base de datos.
  > 
  > 

4.  Agregue los métodos de Hola que realice un seguimiento de tookeep de los usuarios que han iniciado sesión, según sea necesario mediante la cuenta de Passport. Esto incluye serializar y deserializar la información del usuario de hello:

  ```JavaScript

  // Passport session setup (section 2)

  //   toosupport persistent login sessions, Passport needs toobe able to
  //   serialize users into, and deserialize users out of, hello session. Typically,
  //   this is as simple as storing hello user ID when serializing, and finding
  //   hello user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array toohold signed-in users
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

5.  Agregue el código de hello que carga el motor de hello Express. Usar saludo predeterminado /views y patrón /routes que expresan proporciona:

  ```JavaScript

  // Set up Express (section 2)

  var app = express();

  app.configure(function() {
    app.set('views', __dirname + '/views');
    app.set('view engine', 'ejs');
    app.use(express.logger());
    app.use(express.methodOverride());
    app.use(cookieParser());
    app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
    app.use(bodyParser.urlencoded({ extended : true }));
    // Initialize Passport!  Also use passport.session() middleware, toosupport
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  Agregar Hola POST enruta que entrega hello las solicitudes de inicio de sesión real toohello `passport-azure-ad` motor:

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. hello first step in OpenID authentication involves redirecting
  //   hello user toohello user's OpenID provider. After authenticating, hello OpenID
  //   provider redirects hello user back toothis application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in hello sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called.
  //   In this example, it redirects hello user toohello home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called. 
  //   In this example, it redirects hello user toohello home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>4: usar Passport tooissue inicio de sesión y cierre de sesión solicita tooAzure AD
La aplicación se ha establecido por toocommunicate con el punto de conexión de hello v2.0 con el protocolo de autenticación de OpenID Connect de Hola. Hola `passport-azure-ad` estrategia se encarga de todos los detalles de Hola de transmitir mensajes de autenticación, validar los tokens de Azure AD y mantener la sesión de usuario de Hola. Todo lo que queda toodo es toogive a los usuarios una manera toosign en e inicie sesión horizontal y toogather obtener más información acerca del usuario de Hola que ha iniciado sesión.

1.  Agregar hello **predeterminado**, **inicio de sesión**, **cuenta**, y **logout** métodos tooyour App.js archivo:

  ```JavaScript

  //Routes (section 4)

  app.get('/', function(req, res){
    res.render('index', { user: req.user });
  });

  app.get('/account', ensureAuthenticated, function(req, res){
    res.render('account', { user: req.user });
  });

  app.get('/login',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Login was called in hello sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  A continuación encontrará los detalles de hello:
    
    * Hola `/` ruta redirige toohello index.ejs vista. Pasa usuario hello en solicitud de hello (si existe).
    * Hola `/account` enrutar primero *garantiza que se autentican* (implementar que en el siguiente código de hello). A continuación, transferirlos usuario hello en solicitud de saludo. Esto es por lo que puede obtener más información acerca del usuario de Hola.
    * Hola `/login` enrutar las llamadas su `azuread-openidconnect` autenticador de `passport-azuread`. Si no que no tiene éxito, redirige nuevo usuario de hello demasiado`/login`.
    * Hola `/logout` ruta llama hello logout.ejs vista (y ruta). Esto borra las cookies y, a continuación, devuelve Hola tooindex.ejs atrás de usuario.

2.  Agregar hello **EnsureAuthenticated** método que se utilizó anteriormente en `/account`:

  ```JavaScript

  // Route middleware tooensure hello user is authenticated (section 4)

  //   Use this route middleware on any resource that needs toobe protected. If
  //   hello request is authenticated (typically via a persistent login session),
  //   hello request proceeds. Otherwise, hello user is redirected toothe
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  En App.js, crear Hola servidor:

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a>5: crear vistas de Hola y rutas de Express que muestra el usuario en el sitio Web de Hola
Agregar rutas de Hola y vistas que muestran información toohello usuario. rutas de Hola y vistas también controlan hello `/logout` y `/login` rutas que ha creado.

1. En el directorio raíz de hello, crear hello `/routes/index.js` ruta.

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  En el directorio raíz de hello, crear hello `/routes/user.js` ruta.

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  `/routes/index.js`y `/routes/user.js` son rutas simples que pasan a lo largo de vistas de tooyour una solicitud hello, incluido el usuario de hello, si está presente.

3.  En el directorio raíz de hello, crear hello `/views/index.ejs` vista. Esta página llama a los métodos **login** y **logout**. También usar hello `/views/index.ejs` ver información de la cuenta de toocapture. Puede usar Hola condicional `if (!user)` como usuario de Hola que se pasan a través de solicitud de saludo. Se evidencia que hay un usuario con sesión iniciada.

  ```JavaScript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
      <h2>Hello, <%= user.displayName %>.</h2>
      <a href="/account">Account info</a></br>
      <a href="/logout">Sign out</a>
  <% } %>
  ```

4.  En el directorio raíz de hello, crear hello `/views/account.ejs` vista. Hola `/views/account.ejs` vista le permite obtener información adicional de tooview que `passport-azuread` coloca en la solicitud del usuario Hola.

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
  <p>Full Claimes</p>
  <%- JSON.stringify(user) %>
  <p></p>
  <a href="/logout">Sign out</a>
  <% } %>
  ```

5.  Agregue un diseño. En el directorio raíz de hello, crear hello `/views/layout.ejs` vista.

  ```HTML

  <!DOCTYPE html>
  <html>
      <head>
          <title>Passport-OpenID Example</title>
      </head>
      <body>
          <% if (!user) { %>
              <p>
              <a href="/">Home</a> |
              <a href="/login">Sign in</a>
              </p>
          <% } else { %>
              <p>
              <a href="/">Home</a> |
              <a href="/account">Account</a> |
              <a href="/logout">Sign out</a>
              </p>
          <% } %>
          <%- body %>
      </body>
  </html>
  ```

6.  toobuild y ejecutar la aplicación, ejecutar `node app.js`. A continuación, ir demasiado`http://localhost:3000`.

7.  Inicie sesión con una cuenta personal, profesional o educativa de Microsoft. Tenga en cuenta que la identidad del usuario de Hola se refleja en lista de AccountType de Hola. 

Ahora tiene una aplicación web que está protegida mediante protocolos estándar del sector. Puede autenticar a los usuarios de la aplicación con sus cuentas personales y profesionales o educativas.

## <a name="next-steps"></a>Pasos siguientes
Como referencia, ejemplo de Hola finalizado (sin los valores de configuración) se proporciona como [un archivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip). También puede clonarlo desde GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

A continuación, puede mover en toomore temas avanzados. Puede ser conveniente tootry:

[Proteger una API web de Node.js mediante el punto de conexión de hello v2.0](active-directory-v2-devquickstarts-node-api.md)

Estos son algunos recursos adicionales:

* [Guía del desarrollador de Azure AD v2.0](active-directory-appmodel-v2-overview.md)
* [Etiqueta "azure-active-directory" de Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>Obtención de actualizaciones de seguridad para nuestros productos
Recomendamos que toosign una toobe una notificación cuando se produzcan incidentes de seguridad. En hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) página, subscribe tooSecurity avisos de alertas.


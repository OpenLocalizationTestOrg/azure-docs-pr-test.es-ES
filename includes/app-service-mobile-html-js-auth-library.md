### <a name="server-auth"></a>Autenticación con un proveedor (flujo de servidor)
Aplicaciones de Mobile toohave administre el proceso de autenticación de hello en la aplicación, debe registrar la aplicación con el proveedor de identidad. A continuación, en el servicio de aplicación de Azure, debe tooconfigure Hola identificador de la aplicación y el secreto proporcionada por el proveedor.
Para obtener más información, vea el tutorial de hello [agregar autenticación tooyour aplicación](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).

Una vez que ha registrado el proveedor de identidad, llame a hello `.login()` método con nombre hello del proveedor. Por ejemplo, toologin con Facebook usar hello siguiente código:

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

los valores válidos para el proveedor de Hola Hola son 'aad', 'facebook', 'google', 'cuenta de Microsoft' y 'twitter'.

> [!NOTE]
> Autenticación de Google no funciona actualmente a través del flujo de servidor.  tooauthenticate con Google, debe usar un [método de flujo de cliente](#client-auth).

En este caso, el servicio de aplicaciones de Azure administra flujo de autenticación de hello OAuth 2.0.  Muestra la página de inicio de sesión de Hola de proveedor seleccionado hello y genera un token de autenticación de servicio de aplicaciones después de iniciar sesión correctamente con el proveedor de identidades de Hola. función de inicio de sesión de Hello, cuando haya finalizado, devuelve un objeto JSON que expone el Id. de usuario de Hola y el servicio de aplicaciones de token de autenticación en los campos de identificador de usuario y authenticationToken hello, respectivamente. El token puede almacenarse en caché y volver a usarse hasta que expire.

###<a name="client-auth"></a>Autenticación con un proveedor (flujo de cliente)

La aplicación puede también independientemente en contacto con el proveedor de identidades de hello y, a continuación, proporcionar Hola devuelve token tooyour servicio de aplicaciones para la autenticación. Este flujo de cliente le permite tooprovide una experiencia de inicio de sesión única para los usuarios o los datos de usuario adicionales tooretrieve Hola del proveedor de identidades.

#### <a name="social-authentication-basic-example"></a>Ejemplo básico de autenticación social

Este ejemplo usa el SDK de cliente de Facebook para la autenticación:

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
En este ejemplo se da por supuesto ese token Hola proporcionado por el proveedor respectivos Hola SDK se almacena en la variable de token de Hola.

#### <a name="microsoft-account-example"></a>Ejemplo de Cuenta Microsoft

Hola siguiendo el ejemplo se utiliza Hola SDK de Live, que admite el inicio de sesión único para aplicaciones de la tienda de Windows mediante Account de Microsoft:

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

Este ejemplo obtiene un token de Live Connect, que es proporcionado tooyour servicio de aplicaciones mediante una llamada a función de inicio de sesión de hello.

###<a name="auth-getinfo"></a>Cómo: obtener información acerca del usuario autenticado de Hola

se puede recuperar la información de autenticación de Hola de hello `/.auth/me` llamar al punto de conexión mediante HTTP con cualquier biblioteca de AJAX.  Asegúrese de establecer hello `X-ZUMO-AUTH` token de autenticación de encabezado tooyour.  token de autenticación Hello se almacena una en `client.currentUser.mobileServiceAuthenticationToken`.  Por ejemplo, toouse Hola fetch API:

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

La captura está disponible como [un paquete npm](https://www.npmjs.com/package/whatwg-fetch) o para descarga desde el explorador desde [CDNJS](https://cdnjs.com/libraries/fetch). También podría usar jQuery u otra información de Hola de toofetch de API de AJAX.  Los datos se recibieron como un objeto JSON.

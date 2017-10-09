inicio de sesión en tooenable en su aplicación, deberá toocreate un inicio de sesión de directiva. Esta directiva describe experiencias de Hola que recorrerá los consumidores durante el inicio de sesión y contenido de Hola de tokens que Hola aplicación recibirá en inicios de sesión correctos.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

En la sección de hello directivas de configuración, seleccione **directivas de inicio de sesión o inicio de sesión** y haga clic en **+ agregar**.

![Seleccionar directivas de registro o inicio de sesión y hacer clic en el botón Agregar](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

Escriba una directiva **nombre** para su tooreference de aplicación. Por ejemplo, escriba: `SiUpIn`.

Seleccione **Proveedores de identidades** y **Registro por correo electrónico**. También puede seleccionar proveedores de identidades sociales, si ya se han configurado. Haga clic en **Aceptar**.

![Seleccione la suscripción de correo electrónico como proveedor de identidades y haga clic en el botón de Aceptar Hola](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

Seleccione **Atributos de registro**. Seleccione los atributos que desee toocollect de consumidor de Hola durante la suscripción. Por ejemplo, seleccione **País o región**, **Nombre para mostrar** y **Código postal**. Haga clic en **Aceptar**.

![Seleccione algunos atributos y haga clic en el botón de Aceptar Hola](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

Seleccione **Notificaciones de aplicación**. Elegir notificaciones que desea que se devuelvan en tokens de autorización de Hola envían atrás tooyour aplicación después de una experiencia de inicio de sesión o inicio de sesión correcta. Por ejemplo, seleccione **Nombre para mostrar**, **Proveedor de identidades**, **Código postal**, **El usuario es nuevo** e **Id. de objeto del usuario**.

![Seleccionar algunas notificaciones de aplicación y hacer clic en el botón Aceptar](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

Haga clic en **crear** tooadd directiva de Hola. Directiva de Hello aparece como **B2C_1_SiUpIn**. Hola **B2C_1_** prefijo es el nombre de toohello anexado.

Para abrir Directiva de hello, seleccione **B2C_1_SiUpIn**. Compruebe la configuración de hello especificado en la tabla de hello, a continuación, haga clic en **ejecutar ahora**.

![Seleccionar la directiva y ejecutarla](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| Configuración      | Valor  |
| ------------ | ------ |
| **Aplicaciones** | Aplicación B2C de Contoso |
| **Seleccionar dirección URL de respuesta** | `https://localhost:44316/` |

Se abre una nueva pestaña de explorador, y puede comprobar la experiencia de usuario de inicio de sesión o inicio de sesión de hello conforme a la configuración.

> [!NOTE]
> Ocupa tooa minuto para la creación de directivas y actualiza tootake efecto.
>
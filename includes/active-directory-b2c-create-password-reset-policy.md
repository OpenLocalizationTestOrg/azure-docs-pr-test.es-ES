tooenable restablecimiento en la aplicación de contraseña específica, deberá toocreate una directiva de restablecimiento de contraseña. Tenga en cuenta esa contraseña para todo el inquilino Hola restablece se especificó una opción [aquí](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md). Esta directiva describe experiencias de Hola que recorrerá los consumidores de Hola durante el restablecimiento de contraseña y contenido de Hola de tokens que Hola aplicación recibirá cuando se finaliza correctamente.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

En la sección de hello directivas de configuración, seleccione **directivas de restablecimiento de contraseña** y haga clic en **+ agregar**.

![Seleccione las directivas de inicio de sesión o inicio de sesión y haga clic en el botón de agregar Hola](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

Escriba una directiva **nombre** para su tooreference de aplicación. Por ejemplo, escriba: `SSPR`.

Seleccione **Proveedores de identidades** y active la opción **Reset password using email address** (Restablecer contraseña mediante la dirección de correo electrónico). Haga clic en **Aceptar**.

![Seleccione restablecer contraseña utilizando la dirección de correo electrónico como proveedor de identidades y haga clic en el botón de Aceptar Hola](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

Seleccione **Notificaciones de aplicación**. Elegir notificaciones que desea que se devuelvan en tokens de autorización de Hola envían tooyour atrás aplicación una vez experiencia para restablecer una contraseña correcta. Por ejemplo, seleccione **Id. de objeto del usuario**.

![Seleccionar algunas notificaciones de aplicación y hacer clic en el botón Aceptar](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

Haga clic en **crear** tooadd directiva de Hola. Directiva de Hello aparece como **B2C_1_SSPR**. Hola **B2C_1_** prefijo es el nombre de toohello anexado.

Para abrir Directiva de hello, seleccione **B2C_1_SSPR**. Compruebe la configuración de hello especificado en la tabla de hello, a continuación, haga clic en **ejecutar ahora**.

![Seleccionar la directiva y ejecutarla](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| Configuración      | Valor  |
| ------------ | ------ |
| **Aplicaciones** | Aplicación B2C de Contoso |
| **Seleccionar dirección URL de respuesta** | `https://localhost:44316/` |

Se abre una nueva pestaña de explorador, y puede comprobar la experiencia del consumidor en la aplicación de restablecimiento de contraseña de Hola.

> [!NOTE]
> Ocupa tooa minuto para la creación de directivas y actualiza tootake efecto.
>

[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister su API web, use la configuración de hello especificado en la tabla de Hola.

![Ejemplo de configuración de registro para la nueva api web](./media/active-directory-b2c-register-web-api/b2c-new-web-api-settings.png)

| Configuración      | Valor de ejemplo  | Descripción                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Name** | API de B2C de Contoso | Escriba un **nombre** para la aplicación hello que describe la API tooconsumers. | 
| **Incluir aplicación web o API web** | Sí | Seleccione **Sí** para una API web. |
| **Permitir flujo implícito** | Sí | Seleccione **Sí** si su aplicación usa el [inicio de sesión de OpenID Connect](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md). |
| **URL de respuesta** | `https://localhost:44316/` | Las direcciones URL de respuesta son puntos de conexión en los que Azure AD B2C devolverá los tokens que su aplicación solicite. Escriba una **dirección URL de respuesta** [adecuada](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url). En este ejemplo, la API web es local y la escucha se realiza en el puerto 44316. |
| **URI de id. de aplicación** | api | Hola App ID URI es el identificador de Hola que se usa para la API web. Hola completa identificador URI, incluido el dominio de Hola se genera automáticamente. |

Haga clic en **crear** tooregister la aplicación.

La aplicación recién registrada se muestra en la lista de aplicaciones de hello para el inquilino de hello B2C. Seleccione su API web de lista de Hola. se muestra el panel de propiedades de la API de Hola.

![Propiedades de la API web](./media/active-directory-b2c-register-web-api/b2c-web-api-properties.png)

Tome nota de hello globalmente único **Id. de cliente de aplicación**. Usar identificador hello en el código de la aplicación.

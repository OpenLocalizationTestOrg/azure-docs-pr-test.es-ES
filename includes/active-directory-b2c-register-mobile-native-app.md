[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister la aplicación móvil o nativo, usar la configuración de hello especificada en la tabla de Hola.

![Ejemplo de configuración de registro para la nueva aplicación móvil o nativa](./media/active-directory-b2c-register-mobile-native-app/b2c-new-mobile-native-app-settings.png)

| Configuración      | Valor de ejemplo  | Descripción                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Name** | Aplicación B2C de Contoso | Escriba un **nombre** para aplicación Hola que describe la tooconsumers de aplicación. |
| **Cliente nativo** | Sí | Seleccione **Sí** para una aplicación móvil o nativa. |
| **URI de redireccionamiento personalizado** | `com.onmicrosoft.contoso.appname://redirect/path` | Escriba un URI de redirección con un esquema personalizado. Asegúrese de elegir un [buen identificador URI de redireccionamiento](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri) y no incluya caracteres especiales, como caracteres de subrayado. |

Haga clic en **crear** tooregister la aplicación.

La aplicación recién registrada se muestra en la lista de aplicaciones de hello para el inquilino de hello B2C. Seleccione la aplicación móvil o nativo de hello lista. se muestra el panel de propiedades de la aplicación Hello.

![Propiedades de la aplicación](./media/active-directory-b2c-register-mobile-native-app/b2c-mobile-native-app-properties.png)

Tome nota de hello globalmente único **Id. de cliente de aplicación**. Usar identificador hello en el código de la aplicación.

Si la aplicación nativa llama a una API web protegida por Azure AD B2C, siga estos pasos:
   1. Crear un secreto de aplicación va toohello **claves** hoja y haga clic en hello **generar clave** botón. Tome nota de hello **clave de aplicación** valor. Utilice el valor de hello como secreto de aplicación hello en el código de la aplicación.
   2. Haga clic en **Acceso de API**, en **Agregar** y seleccione la API web y los ámbitos (permisos).

> [!NOTE]
> Un **secreto de aplicación** es una credencial de seguridad importante y debe protegerse correctamente.
> 

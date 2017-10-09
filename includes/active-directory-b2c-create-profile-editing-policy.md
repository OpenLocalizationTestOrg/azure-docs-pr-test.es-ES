perfil de tooenable editar en la aplicación, deberá toocreate un perfil de directiva de edición. Esta directiva describe experiencias de Hola que recorrerá los consumidores durante el contenido de perfil hello y edición de tokens que van a recibir aplicación hello cuando se finaliza correctamente.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

En la sección de hello directivas de configuración, seleccione **directivas de edición de perfiles de** y haga clic en **+ agregar**.

![Seleccione las directivas de edición de perfiles y haga clic en el botón de agregar Hola](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

Escriba una directiva **nombre** para su tooreference de aplicación. Por ejemplo, escriba: `SiPe`.

Seleccione **Proveedores de identidades** y active **Inicio de sesión de cuenta local**. También puede seleccionar proveedores de identidades sociales, si ya se han configurado. Haga clic en **Aceptar**.

![Seleccione inicio de sesión de cuenta Local como proveedor de identidades y haga clic en el botón de Aceptar Hola](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

Seleccione **Atributos de perfil**. Elija el consumidor de Hola de atributos puede ver y editar en su perfil. Por ejemplo, seleccione **País o región**, **Nombre para mostrar** y **Código postal**. Haga clic en **Aceptar**.

![Seleccione algunos atributos y haga clic en el botón de Aceptar Hola](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

Seleccione **Notificaciones de aplicación**. Elegir notificaciones que desea que se devuelvan en tokens de autorización de Hola envían atrás tooyour aplicación después de una experiencia de edición de perfiles correcta. Por ejemplo, seleccione **Nombre para mostrar** y **Código postal**.

![Seleccionar algunas notificaciones de aplicación y hacer clic en el botón Aceptar](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

Haga clic en **crear** tooadd directiva de Hola. Directiva de Hello aparece como **B2C_1_SiPe**. Hola **B2C_1_** prefijo es el nombre de toohello anexado.

Para abrir Directiva de hello, seleccione **B2C_1_SiPe**. Compruebe la configuración de hello especificado en la tabla de hello, a continuación, haga clic en **ejecutar ahora**.

![Seleccionar la directiva y ejecutarla](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| Configuración      | Valor  |
| ------------ | ------ |
| **Aplicaciones** | Aplicación B2C de Contoso |
| **Seleccionar dirección URL de respuesta** | `https://localhost:44316/` |

Se abre una nueva pestaña de explorador, y puede comprobar la experiencia del consumidor de edición conforme a la configuración de perfiles de Hola.

> [!NOTE]
> Ocupa tooa minuto para la creación de directivas y actualiza tootake efecto.
>
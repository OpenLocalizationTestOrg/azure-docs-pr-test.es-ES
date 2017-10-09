inicio de sesión en tooenable en su aplicación, deberá toocreate un inicio de sesión de directiva. Esta directiva describe experiencias de Hola que recorrerá los consumidores durante el inicio de sesión y contenido de Hola de tokens que Hola aplicación recibirá en inicios de sesión correctos.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)] Haga clic en **Directivas de inicio de sesión**.

Haga clic en **+ agregar** princip Hola de hoja de Hola.

Hola **nombre** determina el nombre de inicio de sesión de la directiva de hello utilizado por la aplicación. Por ejemplo, escriba **SiIn**.

Haga clic en **Proveedores de identidades** y seleccione **Inicio de sesión de cuenta local**. También puede seleccionar proveedores de identidades sociales, si ya se han configurado. Haga clic en **OK**.

Haga clic en **Notificaciones de aplicación**. Aquí se eligen notificaciones que desean que se devuelvan en tokens de Hola envían atrás tooyour aplicación después de una experiencia de inicio de sesión correcta. Por ejemplo, seleccione **Nombre para mostrar**, **Proveedor de identidades**, **Código Postal** e **Id. de objeto del usuario**. Haga clic en **Aceptar**.

Haga clic en **Crear**. Tenga en cuenta que la directiva de Hola que acaba de crear aparece como **B2C_1_SiIn** (hello **B2C\_1\_**  fragmento se agrega automáticamente) en hello **directivas de inicio de sesión**hoja.

Abrir directiva de hello haciendo clic en **B2C_1_SiIn**.

Seleccione **aplicación Contoso B2C** en hello **aplicaciones** desplegable y `https://localhost:44321/` en hello **dirección URL de respuesta / URI de redireccionamiento** lista desplegable.

Haga clic en **Ejecutar ahora**. Se abre una nueva pestaña de explorador y puede ejecutar a través de la experiencia del consumidor Hola de inicio de sesión en la aplicación.

> [!NOTE]
> Ocupa tooa minuto para la creación de directivas y actualiza tootake efecto.
>
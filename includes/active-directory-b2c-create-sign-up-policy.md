tooenable inicio de sesión en la aplicación, deberá toocreate una directiva de inicio de sesión. Esta directiva describe experiencias de Hola que los consumidores contemplar al realizar el registro y contenido de Hola de tokens que Hola aplicación recibe en Inicio de sesión de seguridad correcta.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Haga clic en **Directivas de registro**.

Haga clic en **+ agregar** princip Hola de hoja de Hola.

Hola **nombre** determina el nombre de la directiva registro de hello utilizado por la aplicación. Por ejemplo, escriba **SiUp**.

Haga clic en **Proveedores de identidades** y seleccione **Registro por correo electrónico**. También puede seleccionar proveedores de identidades sociales, si ya se han configurado. Haga clic en **OK**.

Haga clic en **Atributos de registro**. Aquí se eligen atributos que desea toocollect de consumidor de Hola durante la suscripción. Por ejemplo, seleccione **País o región**, **Nombre para mostrar** y **Código postal**. Haga clic en **Aceptar**.

Haga clic en **Notificaciones de aplicación**. Aquí se eligen notificaciones que desean que se devuelvan en tokens de hello envían atrás tooyour aplicación después de una experiencia de inicio de sesión correcta. Por ejemplo, seleccione **Nombre para mostrar**, **Proveedor de identidades**, **Código postal**, **El usuario es nuevo** e **Id. de objeto del usuario**.

Haga clic en **Crear**. las directivas de Hello creado aparece como **B2C_1_SiUp** (hello **B2C\_1\_**  fragmento se agrega automáticamente) en hello **directivas de suscripción** hoja.

Abrir directiva de hello haciendo clic en **B2C_1_SiUp**.

Seleccione **aplicación Contoso B2C** en hello **aplicaciones** desplegable y `https://localhost:44321/` en hello **dirección URL de respuesta / URI de redireccionamiento** lista desplegable.

Haga clic en **Ejecutar ahora**. Se abre una nueva pestaña de explorador y puede ejecutar a través de la experiencia del consumidor Hola de suscribirse a la aplicación.

> [!NOTE]
> Ocupa tooa minuto para la creación de directivas y actualiza tootake efecto.
>
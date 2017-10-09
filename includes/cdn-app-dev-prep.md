## <a name="prerequisites"></a>Requisitos previos
Antes de que podemos escribir código de administración de red CDN, necesitamos toodo algunos tooenable preparación nuestro toointeract de código con hello Azure Resource Manager.  toodo esto, necesitará:

* Crear un hello toocontain de grupo de recursos perfil de CDN se creará en este tutorial
* Configurar la autenticación de Azure Active Directory tooprovide para nuestra aplicación
* Aplicar los permisos de grupo de recursos de toohello para que solo los usuarios desde el inquilino de Azure AD autorizados puede interactuar con nuestro perfil de CDN

### <a name="creating-hello-resource-group"></a>Creando grupo de recursos de Hola
1. Inicie sesión en hello [Portal de Azure](https://portal.azure.com).
2. Haga clic en hello **New** en la parte superior izquierda de hello, botón y, a continuación, **administración**, y **grupo de recursos**.

    ![Crear un grupo de recursos](./media/cdn-app-dev-prep/cdn-new-rg-1-include.png)
3. Llame a su grupo de recursos *CdnConsoleTutorial*.  Seleccione la suscripción y elija una ubicación cercana.  Si lo desea, puede hacer clic en hello **toodashboard Pin** casilla toopin Hola recursos grupo toohello panel Hola portal.  Esto hará que sea más fácil toofind más tarde.  Cuando termine las selecciones, haga clic en **Crear**.

    ![Grupo de recursos de nomenclatura Hola](./media/cdn-app-dev-prep/cdn-new-rg-2-include.png)
4. Después de crea grupo de recursos de hello, si no ancla tooyour panel, puede buscarlo haciendo clic en **examinar**, a continuación, **grupos de recursos**.  Haga clic en tooopen de grupo de recursos de Hola.  Tome nota del valor en **Id. de suscripción**.  lo necesitará más adelante.

    ![Grupo de recursos de nomenclatura Hola](./media/cdn-app-dev-prep/cdn-subscription-id-include.png)

### <a name="creating-hello-azure-ad-application-and-applying-permissions"></a>Crear aplicación hello Azure AD y aplicar los permisos
Existen dos enfoques tooapp autenticación con Azure Active Directory: usuarios individuales o a una entidad de servicio. Una entidad de servicio es la cuenta de servicio de tooa similares en Windows.  En lugar de conceder un toointeract de permisos de usuario determinado con perfiles de red CDN Hola, en su lugar, concedemos a permisos de hello toohello servicio principal.  Las entidades de servicio se suelen utilizar para procesos automatizados no interactivos.  Aunque este tutorial está escribiendo una aplicación de consola interactiva, nos centraremos en el enfoque principal de servicio de Hola.

Para crear una entidad de servicio, se siguen varios pasos, incluida la creación de una aplicación de Azure Active Directory.  toodo, vamos a demasiado[seguir este tutorial](../articles/resource-group-create-service-principal-portal.md).

> [!IMPORTANT]
> Ser seguro toofollow todos los pasos de Hola Hola [tutorial vinculado](../articles/resource-group-create-service-principal-portal.md).  Es *muy importante* que lo complete exactamente como se describe.  Realizar toonote seguro su **identificador de inquilino**, **nombre_de_dominio_de** (habitualmente un *. onmicrosoft.com* dominio a menos que haya especificado un dominio personalizado), **Id. de cliente** , y **clave de autenticación de cliente**, tal y como se necesitará más adelante.  Tener mucho cuidado tooguard su **Id. de cliente** y **clave de autenticación de cliente**, ya que estas credenciales pueden ser usado por alguien tooexecute operaciones como entidad de servicio de Hola.
>
> Cuando obtenga paso toohello denominado Configurar aplicación multiempresa, seleccione **No**.
>
> Al obtener paso toohello [asignar aplicaciones toorole](../articles/azure-resource-manager/resource-group-create-service-principal-portal.md#assign-application-to-role), grupo de recursos de uso Hola hemos creado con anterioridad, *CdnConsoleTutorial*, pero en lugar de hello **lector** rol, asignar Hola **colaborador de perfil de CDN** rol.  Después de asignar Hola de aplicación Hola **colaborador de perfil de CDN** rol en el grupo de recursos, tutorial toothis devuelto. 
>
>

Una vez que ha creado su Hola de servicio principal y que se asignaron **colaborador de perfil de CDN** rol, hello **usuarios** hoja para el grupo de recursos debe tener un aspecto similar toothis.

![Hoja Usuarios](./media/cdn-app-dev-prep/cdn-service-principal-include.png)

### <a name="interactive-user-authentication"></a>Autenticación interactiva de usuarios
Si, en lugar de una entidad de servicio, que prefiere tener autenticación de usuario individuales interactivo, el proceso de hello es toothat muy similar para una entidad de servicio.  De hecho, necesitará toofollow Hola mismo procedimiento, pero realizar algunos cambios menores.

> [!IMPORTANT]
> Sólo siga estos pasos si elige toouse autenticación de usuario individuales en lugar de una entidad de servicio.
>
>

1. Al crear la aplicación, en lugar de **Aplicación web**, elija **Aplicación nativa**.

    ![Aplicación nativa](./media/cdn-app-dev-prep/cdn-native-application-include.png)
2. En la página siguiente de hello, se le pedirá una **URI de redireccionamiento**.  Hola URI no puede validar, pero recuerde lo que ha escrito.  Lo necesitará más adelante.
3. No hay ninguna necesidad de toocreate una **clave de autenticación de cliente**.
4. En lugar de asignar una toohello de entidad de seguridad de servicio **colaborador de perfil de CDN** rol, vamos a grupos o usuarios individuales de tooassign.  En este ejemplo, puede ver que asigné *CDN demostración usuario* toohello **colaborador de perfil de CDN** rol.  

    ![Acceso de usuario individual](./media/cdn-app-dev-prep/cdn-aad-user-include.png)

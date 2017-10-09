<span data-ttu-id="7bca6-101">tooenable restablecimiento en la aplicación de contraseña específica, deberá toocreate una directiva de restablecimiento de contraseña.</span><span class="sxs-lookup"><span data-stu-id="7bca6-101">tooenable fine-grained password reset on your application, you will need toocreate a password reset policy.</span></span> <span data-ttu-id="7bca6-102">Tenga en cuenta esa contraseña para todo el inquilino Hola restablece se especificó una opción [aquí](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="7bca6-102">Note that hello tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="7bca6-103">Esta directiva describe experiencias de Hola que recorrerá los consumidores de Hola durante el restablecimiento de contraseña y contenido de Hola de tokens que Hola aplicación recibirá cuando se finaliza correctamente.</span><span class="sxs-lookup"><span data-stu-id="7bca6-103">This policy describes hello experiences that hello consumers will go through during password reset and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="7bca6-104">En la sección de hello directivas de configuración, seleccione **directivas de restablecimiento de contraseña** y haga clic en **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="7bca6-104">In hello policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![Seleccione las directivas de inicio de sesión o inicio de sesión y haga clic en el botón de agregar Hola](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="7bca6-106">Escriba una directiva **nombre** para su tooreference de aplicación.</span><span class="sxs-lookup"><span data-stu-id="7bca6-106">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="7bca6-107">Por ejemplo, escriba: `SSPR`.</span><span class="sxs-lookup"><span data-stu-id="7bca6-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="7bca6-108">Seleccione **Proveedores de identidades** y active la opción **Reset password using email address** (Restablecer contraseña mediante la dirección de correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="7bca6-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="7bca6-109">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7bca6-109">Click **OK**.</span></span>

![Seleccione restablecer contraseña utilizando la dirección de correo electrónico como proveedor de identidades y haga clic en el botón de Aceptar Hola](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="7bca6-111">Seleccione **Notificaciones de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="7bca6-111">Select **Application claims**.</span></span> <span data-ttu-id="7bca6-112">Elegir notificaciones que desea que se devuelvan en tokens de autorización de Hola envían tooyour atrás aplicación una vez experiencia para restablecer una contraseña correcta.</span><span class="sxs-lookup"><span data-stu-id="7bca6-112">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful password reset experience.</span></span> <span data-ttu-id="7bca6-113">Por ejemplo, seleccione **Id. de objeto del usuario**.</span><span class="sxs-lookup"><span data-stu-id="7bca6-113">For example, select **User's Object ID**.</span></span>

![Seleccionar algunas notificaciones de aplicación y hacer clic en el botón Aceptar](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="7bca6-115">Haga clic en **crear** tooadd directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bca6-115">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="7bca6-116">Directiva de Hello aparece como **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="7bca6-116">hello policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="7bca6-117">Hola **B2C_1_** prefijo es el nombre de toohello anexado.</span><span class="sxs-lookup"><span data-stu-id="7bca6-117">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="7bca6-118">Para abrir Directiva de hello, seleccione **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="7bca6-118">Open hello policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="7bca6-119">Compruebe la configuración de hello especificado en la tabla de hello, a continuación, haga clic en **ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="7bca6-119">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Seleccionar la directiva y ejecutarla](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="7bca6-121">Configuración</span><span class="sxs-lookup"><span data-stu-id="7bca6-121">Setting</span></span>      | <span data-ttu-id="7bca6-122">Valor</span><span class="sxs-lookup"><span data-stu-id="7bca6-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="7bca6-123">**Aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="7bca6-123">**Applications**</span></span> | <span data-ttu-id="7bca6-124">Aplicación B2C de Contoso</span><span class="sxs-lookup"><span data-stu-id="7bca6-124">Contoso B2C app</span></span> |
| <span data-ttu-id="7bca6-125">**Seleccionar dirección URL de respuesta**</span><span class="sxs-lookup"><span data-stu-id="7bca6-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="7bca6-126">Se abre una nueva pestaña de explorador, y puede comprobar la experiencia del consumidor en la aplicación de restablecimiento de contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="7bca6-126">A new browser tab opens, and you can verify hello password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="7bca6-127">Ocupa tooa minuto para la creación de directivas y actualiza tootake efecto.</span><span class="sxs-lookup"><span data-stu-id="7bca6-127">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>

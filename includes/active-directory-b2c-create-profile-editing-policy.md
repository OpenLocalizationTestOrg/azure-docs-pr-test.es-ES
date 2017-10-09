<span data-ttu-id="0d65c-101">perfil de tooenable editar en la aplicación, deberá toocreate un perfil de directiva de edición.</span><span class="sxs-lookup"><span data-stu-id="0d65c-101">tooenable profile editing on your application, you will need toocreate a profile editing policy.</span></span> <span data-ttu-id="0d65c-102">Esta directiva describe experiencias de Hola que recorrerá los consumidores durante el contenido de perfil hello y edición de tokens que van a recibir aplicación hello cuando se finaliza correctamente.</span><span class="sxs-lookup"><span data-stu-id="0d65c-102">This policy describes hello experiences that consumers will go through during profile editing and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="0d65c-103">En la sección de hello directivas de configuración, seleccione **directivas de edición de perfiles de** y haga clic en **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="0d65c-103">In hello policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![Seleccione las directivas de edición de perfiles y haga clic en el botón de agregar Hola](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="0d65c-105">Escriba una directiva **nombre** para su tooreference de aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d65c-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="0d65c-106">Por ejemplo, escriba: `SiPe`.</span><span class="sxs-lookup"><span data-stu-id="0d65c-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="0d65c-107">Seleccione **Proveedores de identidades** y active **Inicio de sesión de cuenta local**.</span><span class="sxs-lookup"><span data-stu-id="0d65c-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="0d65c-108">También puede seleccionar proveedores de identidades sociales, si ya se han configurado.</span><span class="sxs-lookup"><span data-stu-id="0d65c-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="0d65c-109">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0d65c-109">Click **OK**.</span></span>

![Seleccione inicio de sesión de cuenta Local como proveedor de identidades y haga clic en el botón de Aceptar Hola](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="0d65c-111">Seleccione **Atributos de perfil**.</span><span class="sxs-lookup"><span data-stu-id="0d65c-111">Select **Profile attributes**.</span></span> <span data-ttu-id="0d65c-112">Elija el consumidor de Hola de atributos puede ver y editar en su perfil.</span><span class="sxs-lookup"><span data-stu-id="0d65c-112">Choose attributes hello consumer can view and edit in their profile.</span></span> <span data-ttu-id="0d65c-113">Por ejemplo, seleccione **País o región**, **Nombre para mostrar** y **Código postal**.</span><span class="sxs-lookup"><span data-stu-id="0d65c-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="0d65c-114">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0d65c-114">Click **OK**.</span></span>

![Seleccione algunos atributos y haga clic en el botón de Aceptar Hola](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="0d65c-116">Seleccione **Notificaciones de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="0d65c-116">Select **Application claims**.</span></span> <span data-ttu-id="0d65c-117">Elegir notificaciones que desea que se devuelvan en tokens de autorización de Hola envían atrás tooyour aplicación después de una experiencia de edición de perfiles correcta.</span><span class="sxs-lookup"><span data-stu-id="0d65c-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful profile editing experience.</span></span> <span data-ttu-id="0d65c-118">Por ejemplo, seleccione **Nombre para mostrar** y **Código postal**.</span><span class="sxs-lookup"><span data-stu-id="0d65c-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Seleccionar algunas notificaciones de aplicación y hacer clic en el botón Aceptar](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="0d65c-120">Haga clic en **crear** tooadd directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d65c-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="0d65c-121">Directiva de Hello aparece como **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="0d65c-121">hello policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="0d65c-122">Hola **B2C_1_** prefijo es el nombre de toohello anexado.</span><span class="sxs-lookup"><span data-stu-id="0d65c-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="0d65c-123">Para abrir Directiva de hello, seleccione **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="0d65c-123">Open hello policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="0d65c-124">Compruebe la configuración de hello especificado en la tabla de hello, a continuación, haga clic en **ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="0d65c-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Seleccionar la directiva y ejecutarla](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="0d65c-126">Configuración</span><span class="sxs-lookup"><span data-stu-id="0d65c-126">Setting</span></span>      | <span data-ttu-id="0d65c-127">Valor</span><span class="sxs-lookup"><span data-stu-id="0d65c-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="0d65c-128">**Aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="0d65c-128">**Applications**</span></span> | <span data-ttu-id="0d65c-129">Aplicación B2C de Contoso</span><span class="sxs-lookup"><span data-stu-id="0d65c-129">Contoso B2C app</span></span> |
| <span data-ttu-id="0d65c-130">**Seleccionar dirección URL de respuesta**</span><span class="sxs-lookup"><span data-stu-id="0d65c-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="0d65c-131">Se abre una nueva pestaña de explorador, y puede comprobar la experiencia del consumidor de edición conforme a la configuración de perfiles de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d65c-131">A new browser tab opens, and you can verify hello profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="0d65c-132">Ocupa tooa minuto para la creación de directivas y actualiza tootake efecto.</span><span class="sxs-lookup"><span data-stu-id="0d65c-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>
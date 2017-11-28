<span data-ttu-id="2c879-101">Para habilitar la edición de perfiles en su aplicación, deberá crear una directiva de edición de perfiles.</span><span class="sxs-lookup"><span data-stu-id="2c879-101">To enable profile editing on your application, you will need to create a profile editing policy.</span></span> <span data-ttu-id="2c879-102">Esta directiva describe las experiencias que tendrán los consumidores durante la edición de perfiles y el contenido de los tokens que recibirá la aplicación al finalizar correctamente.</span><span class="sxs-lookup"><span data-stu-id="2c879-102">This policy describes the experiences that consumers will go through during profile editing and the contents of tokens that the application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="2c879-103">En la sección de directivas de configuración, seleccione **Directivas de edición de perfil** y haga clic en **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2c879-103">In the policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![Seleccionar directivas de edición de perfil y hacer clic en el botón Agregar](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="2c879-105">Escriba un **nombre** de directiva al que la aplicación haga referencia.</span><span class="sxs-lookup"><span data-stu-id="2c879-105">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="2c879-106">Por ejemplo, escriba: `SiPe`.</span><span class="sxs-lookup"><span data-stu-id="2c879-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="2c879-107">Seleccione **Proveedores de identidades** y active **Inicio de sesión de cuenta local**.</span><span class="sxs-lookup"><span data-stu-id="2c879-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="2c879-108">También puede seleccionar proveedores de identidades sociales, si ya se han configurado.</span><span class="sxs-lookup"><span data-stu-id="2c879-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="2c879-109">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2c879-109">Click **OK**.</span></span>

![Seleccionar inicio de sesión de cuenta local como proveedor de identidades y hacer clic en el botón Aceptar](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="2c879-111">Seleccione **Atributos de perfil**.</span><span class="sxs-lookup"><span data-stu-id="2c879-111">Select **Profile attributes**.</span></span> <span data-ttu-id="2c879-112">Elija los atributos que el consumidor puede ver y editar en su perfil.</span><span class="sxs-lookup"><span data-stu-id="2c879-112">Choose attributes the consumer can view and edit in their profile.</span></span> <span data-ttu-id="2c879-113">Por ejemplo, seleccione **País o región**, **Nombre para mostrar** y **Código postal**.</span><span class="sxs-lookup"><span data-stu-id="2c879-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="2c879-114">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2c879-114">Click **OK**.</span></span>

![Seleccionar algunos atributos y hacer clic en el botón Aceptar](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="2c879-116">Seleccione **Notificaciones de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="2c879-116">Select **Application claims**.</span></span> <span data-ttu-id="2c879-117">Aquí puede elegir las notificaciones que quiere que se devuelvan en los tokens de autorización a su aplicación después de una experiencia de edición de perfiles correcta.</span><span class="sxs-lookup"><span data-stu-id="2c879-117">Choose claims you want returned in the authorization tokens sent back to your application after a successful profile editing experience.</span></span> <span data-ttu-id="2c879-118">Por ejemplo, seleccione **Nombre para mostrar** y **Código postal**.</span><span class="sxs-lookup"><span data-stu-id="2c879-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Seleccionar algunas notificaciones de aplicación y hacer clic en el botón Aceptar](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="2c879-120">Haga clic en **Crear** para agregar la directiva.</span><span class="sxs-lookup"><span data-stu-id="2c879-120">Click **Create** to add the policy.</span></span> <span data-ttu-id="2c879-121">La directiva aparece como **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="2c879-121">The policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="2c879-122">El prefijo **B2C_1_** se anexa al nombre.</span><span class="sxs-lookup"><span data-stu-id="2c879-122">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="2c879-123">Para abrir la directiva, haga clic en **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="2c879-123">Open the policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="2c879-124">Compruebe la configuración especificada en la tabla y haga clic en **Ejecutar ahora**.</span><span class="sxs-lookup"><span data-stu-id="2c879-124">Verify the settings specified in the table then click **Run now**.</span></span>

![Seleccionar la directiva y ejecutarla](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="2c879-126">Configuración</span><span class="sxs-lookup"><span data-stu-id="2c879-126">Setting</span></span>      | <span data-ttu-id="2c879-127">Valor</span><span class="sxs-lookup"><span data-stu-id="2c879-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="2c879-128">**Aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="2c879-128">**Applications**</span></span> | <span data-ttu-id="2c879-129">Aplicación B2C de Contoso</span><span class="sxs-lookup"><span data-stu-id="2c879-129">Contoso B2C app</span></span> |
| <span data-ttu-id="2c879-130">**Seleccionar dirección URL de respuesta**</span><span class="sxs-lookup"><span data-stu-id="2c879-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="2c879-131">Se abrirá una nueva pestaña del explorador y podrá comprobar la experiencia del consumidor de edición de perfiles que configuró.</span><span class="sxs-lookup"><span data-stu-id="2c879-131">A new browser tab opens, and you can verify the profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="2c879-132">Se tarda hasta un minuto en que la creación de directivas y las actualizaciones surtan efecto.</span><span class="sxs-lookup"><span data-stu-id="2c879-132">It takes up to a minute for policy creation and updates to take effect.</span></span>
>
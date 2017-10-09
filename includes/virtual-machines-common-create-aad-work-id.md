
<br>

> [!NOTE]
> <span data-ttu-id="1eed4-101">Si un administrador le ha asignado un nombre de usuario y una contraseña, hay muchas posibilidades de que ya disponga de un identificador profesional o educativo (también denominado en ocasiones *id. organizativo*).</span><span class="sxs-lookup"><span data-stu-id="1eed4-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="1eed4-102">Si es así, puede empezar inmediatamente toouse los recursos de Azure que necesitan una tooaccess de cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="1eed4-102">If so, you can immediately begin toouse your Azure account tooaccess Azure resources that require one.</span></span> <span data-ttu-id="1eed4-103">Si encuentra que no puede usar esos recursos, deberá tooreturn toothis artículo para obtener ayuda.</span><span class="sxs-lookup"><span data-stu-id="1eed4-103">If you find that you cannot use those resources, you may need tooreturn toothis article for help.</span></span> <span data-ttu-id="1eed4-104">Para obtener más información, consulte [cuentas que puede usar para iniciar sesión en](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) y [suscripción de Azure cómo está relacionado tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="1eed4-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="1eed4-105">pasos de Hello es simple.</span><span class="sxs-lookup"><span data-stu-id="1eed4-105">hello steps are simple.</span></span> <span data-ttu-id="1eed4-106">Necesita toolocate su firmado en identidad Hola portal de Azure clásico, detectar el dominio de Active Directory de Azure de forma predeterminada y se agrega un nuevo tooit de usuario como un Coadministrador de Azure.</span><span class="sxs-lookup"><span data-stu-id="1eed4-106">You need toolocate your signed on identity in hello Azure classic portal, discover your default Azure Active Directory domain, and add a new user tooit as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a><span data-ttu-id="1eed4-107">Busque el directorio predeterminado en hello portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="1eed4-107">Locate your default directory in hello Azure classic portal</span></span>
<span data-ttu-id="1eed4-108">Iniciar sesión toohello [portal de Azure clásico](https://manage.windowsazure.com) con la identidad de la cuenta de Microsoft personal.</span><span class="sxs-lookup"><span data-stu-id="1eed4-108">Start by logging in toohello [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="1eed4-109">Una vez que haya iniciado sesión, desplácese hacia abajo el panel de hello azul en el lado izquierdo de Hola y haga clic en **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="1eed4-109">After you are logged in, scroll down hello blue panel on hello left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="1eed4-111">Empecemos buscando información sobre su identidad en Azure.</span><span class="sxs-lookup"><span data-stu-id="1eed4-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="1eed4-112">Debería ver algo parecido a Hola siguiente en el panel principal de hello, que muestra que tiene un directorio predeterminado.</span><span class="sxs-lookup"><span data-stu-id="1eed4-112">You should see something like hello following in hello main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="1eed4-113">Vamos a averiguar más información sobre él.</span><span class="sxs-lookup"><span data-stu-id="1eed4-113">Let's find out some more information about it.</span></span> <span data-ttu-id="1eed4-114">Haga clic en la fila de directorio predeterminada hello, que se pone en Propiedades del directorio predeterminado Hola.</span><span class="sxs-lookup"><span data-stu-id="1eed4-114">Click hello default directory row, which brings you into hello default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="1eed4-115">nombre de dominio de tooview Hola predeterminado, haga clic en **dominios**.</span><span class="sxs-lookup"><span data-stu-id="1eed4-115">tooview hello default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="1eed4-116">Aquí debe ser capaz de toosee que cuando se creó Hola cuenta de Azure, Azure Active Directory creado en un dominio personal predeterminado que es un valor de hash (es decir, un número generado a partir de una cadena de texto) de un identificador personal que se utiliza como un subdominio de onmicrosoft.com. Que es Hola dominio toowhich ahora, agregará un nuevo usuario.</span><span class="sxs-lookup"><span data-stu-id="1eed4-116">Here you should be able toosee that when hello Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com. That's hello domain toowhich you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-hello-default-domain"></a><span data-ttu-id="1eed4-117">Crear un nuevo usuario en el dominio predeterminado de Hola</span><span class="sxs-lookup"><span data-stu-id="1eed4-117">Creating a new user in hello default domain</span></span>
<span data-ttu-id="1eed4-118">Haga clic en **USUARIOS** y busque su cuenta personal única.</span><span class="sxs-lookup"><span data-stu-id="1eed4-118">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="1eed4-119">Debería ver Hola **con origen en** columna que es un **cuenta de Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="1eed4-119">You should see in hello **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="1eed4-120">Queremos toocreate un usuario en su valor predeterminado. onmicrosoft.com dominio de Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="1eed4-120">We want toocreate a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="1eed4-121">Vamos a toofollow [estas instrucciones](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) en Hola pasos siguientes, pero usa un ejemplo concreto.</span><span class="sxs-lookup"><span data-stu-id="1eed4-121">We're going toofollow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in hello next few steps, but use a specific example.</span></span>

<span data-ttu-id="1eed4-122">En la parte inferior de Hola de página de hello, haga clic en **+ Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="1eed4-122">At hello bottom of hello page, click **+ADD USER**.</span></span> <span data-ttu-id="1eed4-123">En la página de Hola que aparece, escriba el nombre de usuario nuevo de Hola y asegúrese de hello **tipo de usuario** una **nuevo usuario de su organización**.</span><span class="sxs-lookup"><span data-stu-id="1eed4-123">In hello page that appears, type hello new user name, and make hello **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="1eed4-124">En este ejemplo, es el nombre de usuario nuevo de hello `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="1eed4-124">In this example, hello new user name is `ahmet`.</span></span> <span data-ttu-id="1eed4-125">Seleccione dominio predeterminado de Hola que detectó previamente como dominio de hello para la dirección de correo electrónico del ahmet.</span><span class="sxs-lookup"><span data-stu-id="1eed4-125">Select hello default domain that you discovered previously as hello domain for ahmet's email address.</span></span> <span data-ttu-id="1eed4-126">Haga clic en la flecha siguiente de hello cuando termine.</span><span class="sxs-lookup"><span data-stu-id="1eed4-126">Click hello next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="1eed4-127">Agregar más detalles para Ahmet, pero que sean seguro hello tooselect adecuados **rol** valor.</span><span class="sxs-lookup"><span data-stu-id="1eed4-127">Add more details for Ahmet, but make sure tooselect hello appropriate **ROLE** value.</span></span> <span data-ttu-id="1eed4-128">Es fácil toouse **administrador Global** toomake seguro todo funciona, pero si puede usar un rol menor, que es una buena idea.</span><span class="sxs-lookup"><span data-stu-id="1eed4-128">It's easy toouse **Global Admin** toomake sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="1eed4-129">Este ejemplo utiliza hello **usuario** rol.</span><span class="sxs-lookup"><span data-stu-id="1eed4-129">This example uses hello **User** role.</span></span> <span data-ttu-id="1eed4-130">(para más información, consulte [Asignación de roles de administrador en Azure Active Directory](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1)). No habilite la autenticación multifactor a menos que desee toouse la autenticación multifactor para cada registro en la operación.</span><span class="sxs-lookup"><span data-stu-id="1eed4-130">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want toouse multifactor authentication for each log in operation.</span></span> <span data-ttu-id="1eed4-131">Cuando haya terminado, haga clic en flecha siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="1eed4-131">Click hello next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="1eed4-132">Haga clic en hello **crear** botón toogenerate y mostrar una contraseña temporal para Ahmet.</span><span class="sxs-lookup"><span data-stu-id="1eed4-132">Click hello **create** button toogenerate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="1eed4-133">Copiar dirección de correo electrónico de nombre de usuario de Hola o **enviar el correo de electrónico de contraseña en**.</span><span class="sxs-lookup"><span data-stu-id="1eed4-133">Copy hello user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="1eed4-134">Será necesario Hola información toolog en poco tiempo.</span><span class="sxs-lookup"><span data-stu-id="1eed4-134">You'll need hello information toolog on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="1eed4-135">Ahora debería ver el nuevo usuario hello, **Ahmet Hola Developer**, origen de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1eed4-135">Now you should see hello new user, **Ahmet hello Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="1eed4-136">Ha creado nuevos trabajos de Hola o la identidad de la escuela con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1eed4-136">You've created hello new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="1eed4-137">Sin embargo, esta identidad todavía no tiene permisos toouse Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="1eed4-137">However, this identity does not yet have permissions toouse Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="1eed4-138">Si usa **enviar el correo de electrónico de contraseña en**, Hola después el tipo de correo electrónico se envía.</span><span class="sxs-lookup"><span data-stu-id="1eed4-138">If you use **SEND PASSWORD IN EMAIL**, hello following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="1eed4-139">Agregar derechos de coadministrador de Azure para suscripciones</span><span class="sxs-lookup"><span data-stu-id="1eed4-139">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="1eed4-140">Ahora necesita tooadd Hola nuevo usuario como Coadministrador de la suscripción para que usuario nuevo de hello puedan iniciar sesión en toohello Portal de administración.</span><span class="sxs-lookup"><span data-stu-id="1eed4-140">Now you need tooadd hello new user as a co-administrator of your subscription so hello new user can sign in toohello Management Portal.</span></span> <span data-ttu-id="1eed4-141">toodo, en el panel de hello inferior izquierda, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="1eed4-141">toodo this, in hello lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="1eed4-142">En el área de configuración principal de hello, haga clic en **administradores** en hello parte superior y debería ver sólo su identidad personal de la cuenta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1eed4-142">In hello main settings area, click **ADMINISTRATORS** at hello top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="1eed4-143">En la parte inferior de Hola de página de hello, haga clic en **+ agregar** toospecify un Coadministrador.</span><span class="sxs-lookup"><span data-stu-id="1eed4-143">At hello bottom of hello page, click **+ADD** toospecify a co-administrator.</span></span> <span data-ttu-id="1eed4-144">En este caso, escriba la dirección de correo electrónico de Hola de nuevo usuario de Hola que había creado, incluidos su dominio predeterminado.</span><span class="sxs-lookup"><span data-stu-id="1eed4-144">Here, enter hello email address of hello new user you had created, including your default domain.</span></span> <span data-ttu-id="1eed4-145">Tal y como se muestra en la siguiente captura de pantalla de hello, una marca de verificación verde aparece el siguiente usuario toohello directorio predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="1eed4-145">As shown in hello next screenshot, a green check mark appears next toohello user for hello default directory.</span></span> <span data-ttu-id="1eed4-146">Recuerde tooselect todas las suscripciones de Hola que quiere que esta tooadminister capaz de toobe de usuario.</span><span class="sxs-lookup"><span data-stu-id="1eed4-146">Remember tooselect all of hello subscriptions that you would like this user toobe able tooadminister.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="1eed4-147">Cuando haya terminado, debería ahora ver dos usuarios, incluida la nueva identidad de coadministrador.</span><span class="sxs-lookup"><span data-stu-id="1eed4-147">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="1eed4-148">Cierre sesión en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="1eed4-148">Log out of hello portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a><span data-ttu-id="1eed4-149">Inicio de sesión y cambiar la contraseña del usuario nuevo de Hola</span><span class="sxs-lookup"><span data-stu-id="1eed4-149">Logging in and changing hello new user's password</span></span>
<span data-ttu-id="1eed4-150">Inicie sesión como usuario nuevo de Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="1eed4-150">Log in as hello new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="1eed4-151">Inmediatamente será solicitada toocreate una nueva contraseña.</span><span class="sxs-lookup"><span data-stu-id="1eed4-151">You will immediately be prompted toocreate a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="1eed4-152">Aparecerá con éxito similar Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="1eed4-152">You should be rewarded with success that looks like hello following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="1eed4-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1eed4-153">Next steps</span></span>
<span data-ttu-id="1eed4-154">Ahora puede usar su nuevo toouse de identidad de Azure Active Directory [plantillas de grupo de recursos de Azure](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1eed4-154">You can now use your new Azure Active Directory identity toouse [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how tooset them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@aztrainpassxxxxxoutlook.onmicrosoft.com
    Password: *********
    /info:    Added subscription Azure Pass
    info:    Setting subscription Azure Pass as default
    +
    info:    login command OK
    ralph@local:~$ azure config mode arm
    info:    New mode is arm
    ralph@local:~$ azure group list
    info:    Executing command group list
    + Listing resource groups
    info:    No matched resource groups were found
    info:    group list command OK
    ralph@local:~$ azure group create newgroup westus
    info:    Executing command group create
    + Getting resource group newgroup
    + Creating resource group newgroup
    info:    Created resource group newgroup
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/newgroup
    data:    Name:                newgroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags:
    data:
    info:    group create command OK

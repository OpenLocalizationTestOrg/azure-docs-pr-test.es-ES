
<br>

> [!NOTE]
> <span data-ttu-id="70e9f-101">Si un administrador le ha asignado un nombre de usuario y una contraseña, hay muchas posibilidades de que ya disponga de un identificador profesional o educativo (también denominado en ocasiones *id. organizativo*).</span><span class="sxs-lookup"><span data-stu-id="70e9f-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="70e9f-102">Si es así, puede comenzar inmediatamente a usar su cuenta de Azure para acceder a recursos de Azure que lo requieran.</span><span class="sxs-lookup"><span data-stu-id="70e9f-102">If so, you can immediately begin to use your Azure account to access Azure resources that require one.</span></span> <span data-ttu-id="70e9f-103">Si descubre que no puede usar esos recursos, puede que necesite volver a este artículo para obtener ayuda.</span><span class="sxs-lookup"><span data-stu-id="70e9f-103">If you find that you cannot use those resources, you may need to return to this article for help.</span></span> <span data-ttu-id="70e9f-104">Para más información, consulte [Cuentas que puede utilizar para iniciar sesión](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) y [Qué relación tiene Azure con Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="70e9f-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related to Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="70e9f-105">Los pasos son sencillos.</span><span class="sxs-lookup"><span data-stu-id="70e9f-105">The steps are simple.</span></span> <span data-ttu-id="70e9f-106">Necesita encontrar la identidad con la que ha iniciado sesión en el portal de Azure clásico, descubrir su dominio de Azure Active Directory predeterminado y agregarle un nuevo usuario como coadministrador de Azure.</span><span class="sxs-lookup"><span data-stu-id="70e9f-106">You need to locate your signed on identity in the Azure classic portal, discover your default Azure Active Directory domain, and add a new user to it as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-the-azure-classic-portal"></a><span data-ttu-id="70e9f-107">Buscar el directorio predeterminado en el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="70e9f-107">Locate your default directory in the Azure classic portal</span></span>
<span data-ttu-id="70e9f-108">Empiece por iniciar sesión en el [Portal de Azure clásico](https://manage.windowsazure.com) con su identidad de la cuenta de Microsoft personal.</span><span class="sxs-lookup"><span data-stu-id="70e9f-108">Start by logging in to the [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="70e9f-109">Cuando haya iniciado sesión, desplácese hacia abajo en el panel azul del lado izquierdo y haga clic en **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="70e9f-109">After you are logged in, scroll down the blue panel on the left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="70e9f-111">Empecemos buscando información sobre su identidad en Azure.</span><span class="sxs-lookup"><span data-stu-id="70e9f-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="70e9f-112">Debería ver algo parecido a lo siguiente en el panel principal, que muestra que tiene un directorio predeterminado.</span><span class="sxs-lookup"><span data-stu-id="70e9f-112">You should see something like the following in the main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="70e9f-113">Vamos a averiguar más información sobre él.</span><span class="sxs-lookup"><span data-stu-id="70e9f-113">Let's find out some more information about it.</span></span> <span data-ttu-id="70e9f-114">Haga clic en la fila de directorio predeterminada, lo que le lleva a las propiedades de directorio predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="70e9f-114">Click the default directory row, which brings you into the default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="70e9f-115">Para ver el nombre de dominio predeterminado, haga clic en **DOMINIOS**.</span><span class="sxs-lookup"><span data-stu-id="70e9f-115">To view the default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="70e9f-116">Aquí debería ver que cuando se creó la cuenta de Azure, Azure Active Directory creó un dominio predeterminado personal que es un valor de hash (un número generado a partir de una cadena de texto) de su id. personal usado como subdominio de onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="70e9f-116">Here you should be able to see that when the Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com.</span></span> <span data-ttu-id="70e9f-117">Ese es el dominio en el que va a agregar ahora un nuevo usuario.</span><span class="sxs-lookup"><span data-stu-id="70e9f-117">That's the domain to which you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-the-default-domain"></a><span data-ttu-id="70e9f-118">Creación de un nuevo usuario en el dominio predeterminado</span><span class="sxs-lookup"><span data-stu-id="70e9f-118">Creating a new user in the default domain</span></span>
<span data-ttu-id="70e9f-119">Haga clic en **USUARIOS** y busque su cuenta personal única.</span><span class="sxs-lookup"><span data-stu-id="70e9f-119">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="70e9f-120">En la columna **CON ORIGEN EN** debería ver que es una **cuenta Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="70e9f-120">You should see in the **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="70e9f-121">Queremos crear un usuario en su dominio .onmicrosoft.com de Azure Active Directory predeterminado.</span><span class="sxs-lookup"><span data-stu-id="70e9f-121">We want to create a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="70e9f-122">Vamos a seguir [estas instrucciones](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) en los pasos siguientes, pero con un ejemplo concreto.</span><span class="sxs-lookup"><span data-stu-id="70e9f-122">We're going to follow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in the next few steps, but use a specific example.</span></span>

<span data-ttu-id="70e9f-123">En la parte inferior de la página, haga clic en **+AGREGAR USUARIO**.</span><span class="sxs-lookup"><span data-stu-id="70e9f-123">At the bottom of the page, click **+ADD USER**.</span></span> <span data-ttu-id="70e9f-124">En la página que aparece, escriba el nuevo nombre de usuario y en **Tipo de usuario** seleccione **Nuevo usuario de la organización**.</span><span class="sxs-lookup"><span data-stu-id="70e9f-124">In the page that appears, type the new user name, and make the **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="70e9f-125">En este ejemplo, el nuevo nombre de usuario es `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="70e9f-125">In this example, the new user name is `ahmet`.</span></span> <span data-ttu-id="70e9f-126">Seleccione el dominio predeterminado que detectó anteriormente como el dominio para la dirección de correo electrónico de ahmet.</span><span class="sxs-lookup"><span data-stu-id="70e9f-126">Select the default domain that you discovered previously as the domain for ahmet's email address.</span></span> <span data-ttu-id="70e9f-127">Haga clic en la siguiente flecha cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="70e9f-127">Click the next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="70e9f-128">Agregue más detalles para Ahmet, pero asegúrese de seleccionar el valor de **ROL** adecuado.</span><span class="sxs-lookup"><span data-stu-id="70e9f-128">Add more details for Ahmet, but make sure to select the appropriate **ROLE** value.</span></span> <span data-ttu-id="70e9f-129">Es sencillo usar **Administrador global** para asegurarse de que todo funciona, pero si se puede utilizar un rol menor, se recomienda hacerlo.</span><span class="sxs-lookup"><span data-stu-id="70e9f-129">It's easy to use **Global Admin** to make sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="70e9f-130">En este ejemplo se usa el rol **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="70e9f-130">This example uses the **User** role.</span></span> <span data-ttu-id="70e9f-131">(para más información, consulte [Asignación de roles de administrador en Azure Active Directory](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1)). No habilite la autenticación multifactor a menos que quiera usar la autenticación multifactor para cada registro de la operación.</span><span class="sxs-lookup"><span data-stu-id="70e9f-131">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want to use multifactor authentication for each log in operation.</span></span> <span data-ttu-id="70e9f-132">Haga clic en la siguiente flecha cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="70e9f-132">Click the next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="70e9f-133">Haga clic en el botón **crear** para generar y mostrar una contraseña temporal para Ahmet.</span><span class="sxs-lookup"><span data-stu-id="70e9f-133">Click the **create** button to generate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="70e9f-134">Copie la dirección de correo electrónico del nombre de usuario o use **ENVIAR CONTRASEÑA EN CORREO ELECTRÓNICO**.</span><span class="sxs-lookup"><span data-stu-id="70e9f-134">Copy the user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="70e9f-135">Necesitará la información para iniciar sesión en breve.</span><span class="sxs-lookup"><span data-stu-id="70e9f-135">You'll need the information to log on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="70e9f-136">Ahora debe ver el nuevo usuario **Ahmet el desarrollador**, con origen en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="70e9f-136">Now you should see the new user, **Ahmet the Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="70e9f-137">Ha creado la nueva identidad profesional o educativa con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="70e9f-137">You've created the new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="70e9f-138">Sin embargo, esta identidad no tiene permisos todavía para usar recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="70e9f-138">However, this identity does not yet have permissions to use Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="70e9f-139">Si usa **ENVIAR CONTRASEÑA EN CORREO ELECTRÓNICO**, se enviará el siguiente tipo de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="70e9f-139">If you use **SEND PASSWORD IN EMAIL**, the following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="70e9f-140">Agregar derechos de coadministrador de Azure para suscripciones</span><span class="sxs-lookup"><span data-stu-id="70e9f-140">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="70e9f-141">Ahora debe agregar el nuevo usuario como coadministrador de su suscripción para que el nuevo usuario pueda iniciar sesión en el Portal de administración.</span><span class="sxs-lookup"><span data-stu-id="70e9f-141">Now you need to add the new user as a co-administrator of your subscription so the new user can sign in to the Management Portal.</span></span> <span data-ttu-id="70e9f-142">Para ello, en el panel inferior izquierdo, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="70e9f-142">To do this, in the lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="70e9f-143">En el área de configuración principal, haga clic en **ADMINISTRADORES** de la parte superior y solo debería ver su identidad de la cuenta Microsoft personal.</span><span class="sxs-lookup"><span data-stu-id="70e9f-143">In the main settings area, click **ADMINISTRATORS** at the top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="70e9f-144">En la parte inferior de la página, haga clic en **+ AGREGAR** para especificar un coadministrador.</span><span class="sxs-lookup"><span data-stu-id="70e9f-144">At the bottom of the page, click **+ADD** to specify a co-administrator.</span></span> <span data-ttu-id="70e9f-145">Aquí, escriba la dirección de correo electrónico del nuevo usuario que haya creado, incluido el dominio predeterminado.</span><span class="sxs-lookup"><span data-stu-id="70e9f-145">Here, enter the email address of the new user you had created, including your default domain.</span></span> <span data-ttu-id="70e9f-146">Como se muestra en la siguiente captura de pantalla, aparecerá una marca de verificación verde junto al usuario para el directorio predeterminado.</span><span class="sxs-lookup"><span data-stu-id="70e9f-146">As shown in the next screenshot, a green check mark appears next to the user for the default directory.</span></span> <span data-ttu-id="70e9f-147">Recuerde seleccionar todas las suscripciones que le gustaría que este usuario pudiera administrar.</span><span class="sxs-lookup"><span data-stu-id="70e9f-147">Remember to select all of the subscriptions that you would like this user to be able to administer.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="70e9f-148">Cuando haya terminado, debería ahora ver dos usuarios, incluida la nueva identidad de coadministrador.</span><span class="sxs-lookup"><span data-stu-id="70e9f-148">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="70e9f-149">Cierre sesión en el portal.</span><span class="sxs-lookup"><span data-stu-id="70e9f-149">Log out of the portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-the-new-users-password"></a><span data-ttu-id="70e9f-150">Inicio de sesión y cambio de la contraseña del nuevo usuario</span><span class="sxs-lookup"><span data-stu-id="70e9f-150">Logging in and changing the new user's password</span></span>
<span data-ttu-id="70e9f-151">Inicie sesión como el nuevo usuario que ha creado.</span><span class="sxs-lookup"><span data-stu-id="70e9f-151">Log in as the new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="70e9f-152">Se le pedirá inmediatamente que cree una nueva contraseña.</span><span class="sxs-lookup"><span data-stu-id="70e9f-152">You will immediately be prompted to create a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="70e9f-153">Al realizarse la operación correctamente, aparecerá algo similar a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="70e9f-153">You should be rewarded with success that looks like the following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="70e9f-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="70e9f-154">Next steps</span></span>
<span data-ttu-id="70e9f-155">Ahora puede usar su nueva identidad de Azure Active Directory para usar [plantillas de grupo de recursos de Azure](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="70e9f-155">You can now use your new Azure Active Directory identity to use [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how to set them up, please read http://aka.ms/Dhf67j.
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

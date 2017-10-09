
<br>

> [!NOTE]
> Si un administrador le ha asignado un nombre de usuario y una contraseña, hay muchas posibilidades de que ya disponga de un identificador profesional o educativo (también denominado en ocasiones *id. organizativo*). Si es así, puede empezar inmediatamente toouse los recursos de Azure que necesitan una tooaccess de cuenta de Azure. Si encuentra que no puede usar esos recursos, deberá tooreturn toothis artículo para obtener ayuda. Para obtener más información, consulte [cuentas que puede usar para iniciar sesión en](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) y [suscripción de Azure cómo está relacionado tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).
> 
> 

pasos de Hello es simple. Necesita toolocate su firmado en identidad Hola portal de Azure clásico, detectar el dominio de Active Directory de Azure de forma predeterminada y se agrega un nuevo tooit de usuario como un Coadministrador de Azure.

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a>Busque el directorio predeterminado en hello portal de Azure clásico
Iniciar sesión toohello [portal de Azure clásico](https://manage.windowsazure.com) con la identidad de la cuenta de Microsoft personal. Una vez que haya iniciado sesión, desplácese hacia abajo el panel de hello azul en el lado izquierdo de Hola y haga clic en **ACTIVE DIRECTORY**.

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

Empecemos buscando información sobre su identidad en Azure. Debería ver algo parecido a Hola siguiente en el panel principal de hello, que muestra que tiene un directorio predeterminado.

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

Vamos a averiguar más información sobre él. Haga clic en la fila de directorio predeterminada hello, que se pone en Propiedades del directorio predeterminado Hola.  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

nombre de dominio de tooview Hola predeterminado, haga clic en **dominios**.

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

Aquí debe ser capaz de toosee que cuando se creó Hola cuenta de Azure, Azure Active Directory creado en un dominio personal predeterminado que es un valor de hash (es decir, un número generado a partir de una cadena de texto) de un identificador personal que se utiliza como un subdominio de onmicrosoft.com. Que es Hola dominio toowhich ahora, agregará un nuevo usuario.

## <a name="creating-a-new-user-in-hello-default-domain"></a>Crear un nuevo usuario en el dominio predeterminado de Hola
Haga clic en **USUARIOS** y busque su cuenta personal única. Debería ver Hola **con origen en** columna que es un **cuenta de Microsoft**. Queremos toocreate un usuario en su valor predeterminado. onmicrosoft.com dominio de Active Directory de Azure.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

Vamos a toofollow [estas instrucciones](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) en Hola pasos siguientes, pero usa un ejemplo concreto.

En la parte inferior de Hola de página de hello, haga clic en **+ Agregar usuario**. En la página de Hola que aparece, escriba el nombre de usuario nuevo de Hola y asegúrese de hello **tipo de usuario** una **nuevo usuario de su organización**. En este ejemplo, es el nombre de usuario nuevo de hello `ahmet`. Seleccione dominio predeterminado de Hola que detectó previamente como dominio de hello para la dirección de correo electrónico del ahmet. Haga clic en la flecha siguiente de hello cuando termine.

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

Agregar más detalles para Ahmet, pero que sean seguro hello tooselect adecuados **rol** valor. Es fácil toouse **administrador Global** toomake seguro todo funciona, pero si puede usar un rol menor, que es una buena idea. Este ejemplo utiliza hello **usuario** rol. (para más información, consulte [Asignación de roles de administrador en Azure Active Directory](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1)). No habilite la autenticación multifactor a menos que desee toouse la autenticación multifactor para cada registro en la operación. Cuando haya terminado, haga clic en flecha siguiente Hola.

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

Haga clic en hello **crear** botón toogenerate y mostrar una contraseña temporal para Ahmet.

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

Copiar dirección de correo electrónico de nombre de usuario de Hola o **enviar el correo de electrónico de contraseña en**. Será necesario Hola información toolog en poco tiempo.

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

Ahora debería ver el nuevo usuario hello, **Ahmet Hola Developer**, origen de Azure Active Directory. Ha creado nuevos trabajos de Hola o la identidad de la escuela con Azure Active Directory. Sin embargo, esta identidad todavía no tiene permisos toouse Azure recursos.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

Si usa **enviar el correo de electrónico de contraseña en**, Hola después el tipo de correo electrónico se envía.

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a>Agregar derechos de coadministrador de Azure para suscripciones
Ahora necesita tooadd Hola nuevo usuario como Coadministrador de la suscripción para que usuario nuevo de hello puedan iniciar sesión en toohello Portal de administración. toodo, en el panel de hello inferior izquierda, haga clic en **configuración**.

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

En el área de configuración principal de hello, haga clic en **administradores** en hello parte superior y debería ver sólo su identidad personal de la cuenta Microsoft. En la parte inferior de Hola de página de hello, haga clic en **+ agregar** toospecify un Coadministrador. En este caso, escriba la dirección de correo electrónico de Hola de nuevo usuario de Hola que había creado, incluidos su dominio predeterminado. Tal y como se muestra en la siguiente captura de pantalla de hello, una marca de verificación verde aparece el siguiente usuario toohello directorio predeterminado de Hola. Recuerde tooselect todas las suscripciones de Hola que quiere que esta tooadminister capaz de toobe de usuario.

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

Cuando haya terminado, debería ahora ver dos usuarios, incluida la nueva identidad de coadministrador. Cierre sesión en el portal de Hola.

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a>Inicio de sesión y cambiar la contraseña del usuario nuevo de Hola
Inicie sesión como usuario nuevo de Hola que ha creado.

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

Inmediatamente será solicitada toocreate una nueva contraseña.

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

Aparecerá con éxito similar Hola siguiente.

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a>Pasos siguientes
Ahora puede usar su nuevo toouse de identidad de Azure Active Directory [plantillas de grupo de recursos de Azure](../articles/xplat-cli-azure-resource-manager.md).

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

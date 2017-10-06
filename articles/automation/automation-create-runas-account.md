---
title: "aaaCreate Azure Automation cuentas de ejecución | Documentos de Microsoft"
description: "Este artículo se describe cómo tooupdate la automatización de la cuenta y crear cuentas de ejecución con PowerShell o desde el portal de Hola."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 94eb54fa0b518056a726d17146c63411e248273b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="97bd3-103">Actualizar la autenticación de la cuenta de Automation con cuentas de ejecución</span><span class="sxs-lookup"><span data-stu-id="97bd3-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="97bd3-104">Puede actualizar su cuenta de automatización existente desde el portal de Hola o usar PowerShell si:</span><span class="sxs-lookup"><span data-stu-id="97bd3-104">You can update your existing Automation account from hello portal or use PowerShell if:</span></span>

* <span data-ttu-id="97bd3-105">Crear una cuenta de automatización, pero rechazar toocreate Hola cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="97bd3-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="97bd3-106">Ya utiliza un administrador de recursos toomanage cuenta recursos de automatización y desea tooupdate Hola cuenta tooinclude Hola cuenta de ejecución para la autenticación de runbook.</span><span class="sxs-lookup"><span data-stu-id="97bd3-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="97bd3-107">Ya utiliza un recursos clásicos de automatización de la cuenta toomanage y desea tooupdate se toouse Hola clásico cuenta de ejecución en lugar de crear una cuenta nueva y migrar su tooit runbooks y activos.</span><span class="sxs-lookup"><span data-stu-id="97bd3-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="97bd3-108">Toocreate que desee ejecutar como y una cuenta de identificación clásico mediante el uso de un certificado emitido por la entidad de certificación (CA) empresarial.</span><span class="sxs-lookup"><span data-stu-id="97bd3-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97bd3-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="97bd3-109">Prerequisites</span></span>

* <span data-ttu-id="97bd3-110">script de Hola puede ejecutar solo en Windows 10 y Windows Server 2016 con módulos de Azure Resource Manager 3.0.0 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="97bd3-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="97bd3-111">No se admite en versiones anteriores de Windows.</span><span class="sxs-lookup"><span data-stu-id="97bd3-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="97bd3-112">Azure PowerShell 1.0 y versiones superiores.</span><span class="sxs-lookup"><span data-stu-id="97bd3-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="97bd3-113">Para obtener información acerca de la versión de Hola PowerShell 1.0, vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="97bd3-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="97bd3-114">Una cuenta de automatización, que se hace referencia como valor de Hola de hello *: AutomationAccountName* y *- ApplicationDisplayName* parámetros Hola siguiente script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97bd3-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="97bd3-115">Hola tooget los valores de *SubscriptionID*, *ResourceGroup*, y *AutomationAccountName*, que son parámetros necesarios para la secuencia de comandos de hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="97bd3-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello script, do hello following:</span></span>

1. <span data-ttu-id="97bd3-116">En el portal de Azure de Hola, seleccione su cuenta de automatización en hello **cuenta de automatización** hoja y, a continuación, seleccione **toda la configuración de**.</span><span class="sxs-lookup"><span data-stu-id="97bd3-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="97bd3-117">En hello **toda la configuración de** hoja, en **configuración de la cuenta**, seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="97bd3-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="97bd3-118">Tenga en cuenta los valores de hello en hello **propiedades** hoja.</span><span class="sxs-lookup"><span data-stu-id="97bd3-118">Note hello values on hello **Properties** blade.</span></span><br><br> <span data-ttu-id="97bd3-119">![hoja de "Propiedades" de cuenta de automatización de Hola](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="97bd3-119">![hello Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-tooupdate-your-automation-account"></a><span data-ttu-id="97bd3-120">Requiere permisos tooupdate su cuenta de automatización</span><span class="sxs-lookup"><span data-stu-id="97bd3-120">Required permissions tooupdate your Automation account</span></span>
<span data-ttu-id="97bd3-121">tooupdate una cuenta de automatización, debe tener Hola después determinados privilegios y permisos necesarios toocomplete en este tema.</span><span class="sxs-lookup"><span data-stu-id="97bd3-121">tooupdate an Automation account, you must have hello following specific privileges and permissions required toocomplete this topic.</span></span>   
 
* <span data-ttu-id="97bd3-122">Su cuenta de usuario de AD necesita toobe tooa agregado rol con el rol de colaborador de toohello equivalente de permisos para recursos de Microsoft.Automation tal como se describe en el artículo [control de acceso basado en roles en automatización de Azure](automation-role-based-access-control.md#contributor-role-permissions).</span><span class="sxs-lookup"><span data-stu-id="97bd3-122">Your AD user account needs toobe added tooa role with permissions equivalent toohello Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="97bd3-123">Los usuarios sin privilegios de administrador en el inquilino de Azure AD pueden [registrar aplicaciones AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) si los registros de aplicación Hola configuración se establece demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="97bd3-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if hello App registrations setting is set too**Yes**.</span></span>  <span data-ttu-id="97bd3-124">Si los registros de aplicación Hola configuración se establece demasiado**n**, usuario Hola realizar esta acción debe ser un administrador global de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97bd3-124">If hello app registrations setting is set too**No**, hello user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="97bd3-125">Si no eres un miembro de instancia de Active Directory de la suscripción de hello antes de que se agreguen toohello global administrador o coadministrator-administrator roles de suscripción de hello, se agregan tooActive directorio como invitado.</span><span class="sxs-lookup"><span data-stu-id="97bd3-125">If you are not a member of hello subscription’s Active Directory instance before you are added toohello global administrator/co-administrator role of hello subscription, you are added tooActive Directory as a guest.</span></span> <span data-ttu-id="97bd3-126">En este caso, recibirá un "no tiene permisos toocreate..."</span><span class="sxs-lookup"><span data-stu-id="97bd3-126">In this situation, you receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="97bd3-127">Advertencia de hello **agregar una cuenta de automatización** hoja.</span><span class="sxs-lookup"><span data-stu-id="97bd3-127">warning on hello **Add Automation Account** blade.</span></span> <span data-ttu-id="97bd3-128">Los usuarios que se agregaron toohello global administrador o coadministrator-administrator roles en primer lugar se pueden quitar de la instancia de Active Directory de la suscripción de Hola y vuelva a agregan toomake a un usuario en Active Directory completo.</span><span class="sxs-lookup"><span data-stu-id="97bd3-128">Users who were added toohello global administrator/co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="97bd3-129">tooverify esta situación, hello **Azure Active Directory** panel Hola portal de Azure, seleccione **usuarios y grupos**, seleccione **todos los usuarios** y, después de seleccionar Hola un usuario específico, seleccione **perfil**.</span><span class="sxs-lookup"><span data-stu-id="97bd3-129">tooverify this situation, from hello **Azure Active Directory** pane in hello Azure portal, select **Users and groups**, select **All users** and, after you select hello specific user, select **Profile**.</span></span> <span data-ttu-id="97bd3-130">Hola valo hello **tipo de usuario** atributo en el perfil de los usuarios de hello no debería ser igual **invitado**.</span><span class="sxs-lookup"><span data-stu-id="97bd3-130">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-hello-portal"></a><span data-ttu-id="97bd3-131">Crear cuenta de ejecución desde el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="97bd3-131">Create Run As account from hello portal</span></span>
<span data-ttu-id="97bd3-132">En esta sección, realizar Hola siguiendo los pasos tooupdate su cuenta de automatización de Azure desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="97bd3-132">In this section, perform hello following steps tooupdate your Azure Automation account from  hello Azure portal.</span></span>  <span data-ttu-id="97bd3-133">Crear Hola identificación clásico y ejecutar como cuentas individualmente y si no necesita recursos toomanage en portal de Azure clásico hello, solo puede crear hello Azure cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="97bd3-133">You create hello Run As and Classic Run As accounts individually, and if you don't need toomanage resources in hello classic Azure portal, you can just create hello Azure Run As account.</span></span>  

<span data-ttu-id="97bd3-134">proceso de Hello crea Hola siguientes elementos en su cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="97bd3-134">hello process creates hello following items in your Automation account.</span></span>

<span data-ttu-id="97bd3-135">**Para cuentas de ejecución:**</span><span class="sxs-lookup"><span data-stu-id="97bd3-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="97bd3-136">Crea una aplicación de Azure AD con un certificado autofirmado, crea una cuenta de entidad de servicio para la aplicación hello en Azure AD y asigna el rol de colaborador de hello para la cuenta de hello en su suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="97bd3-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="97bd3-137">Puede cambiar esta configuración tooOwner o cualquier otro rol.</span><span class="sxs-lookup"><span data-stu-id="97bd3-137">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="97bd3-138">Para más información, consulte [Control de acceso basado en rol en Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="97bd3-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="97bd3-139">Crea un activo de certificado de automatización denominado *AzureRunAsCertificate* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="97bd3-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="97bd3-140">activo de certificado de Hello contiene la clave privada de hello certificado utilizado por la aplicación hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97bd3-140">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="97bd3-141">Crea un recurso de conexión de automatización denominado *AzureRunAsConnection* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="97bd3-141">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="97bd3-142">activo de conexión de Hello contiene applicationId hello, tenantId, Id. de suscripción y la huella digital del certificado.</span><span class="sxs-lookup"><span data-stu-id="97bd3-142">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="97bd3-143">**Para cuentas de ejecución clásicas:**</span><span class="sxs-lookup"><span data-stu-id="97bd3-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="97bd3-144">Crea un activo de certificado de automatización denominado *AzureClassicRunAsCertificate* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="97bd3-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="97bd3-145">activo de certificado de Hello contiene la clave privada del certificado Hola utilizado por el certificado de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="97bd3-145">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="97bd3-146">Crea un recurso de conexión de automatización denominado *AzureClassicRunAsConnection* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="97bd3-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="97bd3-147">activo de conexión de Hello contiene el nombre de la suscripción de hello, Id. de suscripción y el nombre del recurso de certificado.</span><span class="sxs-lookup"><span data-stu-id="97bd3-147">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="97bd3-148">Inicie sesión en toohello portal de Azure con una cuenta que sea miembro del rol de los administradores de suscripciones de Hola y Coadministrador de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="97bd3-148">Sign in toohello Azure portal with an account that is a member of hello Subscription Admins role and co-administrator of hello subscription.</span></span>
2. <span data-ttu-id="97bd3-149">En la hoja de la cuenta de automatización de hello, seleccione **cuentas de ejecución** en la sección de hello **configuración de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="97bd3-149">From hello Automation account blade, select **Run As Accounts** under hello section **Account Settings**.</span></span>  
3. <span data-ttu-id="97bd3-150">En función de la cuenta que necesite, seleccione **Cuenta de ejecución de Azure** o **Cuenta de ejecución de Azure clásica**.</span><span class="sxs-lookup"><span data-stu-id="97bd3-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="97bd3-151">Después de seleccionar cualquier hello **agregar Azure identificación** o **agregar clásico ejecutar como cuenta de Azure** hoja aparece y después de revisar la información general de hello, haga clic en **crear** tooproceed con la creación de cuentas de ejecución.</span><span class="sxs-lookup"><span data-stu-id="97bd3-151">After selecting either hello **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing hello overview information, click **Create** tooproceed with Run As account creation.</span></span>  
4. <span data-ttu-id="97bd3-152">Mientras Azure crea la cuenta de identificación de hello, puede seguir el progreso de hello en **notificaciones** de hello menú y un banner se muestra que indica que se está creando la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="97bd3-152">While Azure creates hello Run As account, you can track hello progress under **Notifications** from hello menu and a banner is displayed stating hello account is being created.</span></span>  <span data-ttu-id="97bd3-153">Este proceso puede tardar unos toocomplete minutos.</span><span class="sxs-lookup"><span data-stu-id="97bd3-153">This process can take a few minutes toocomplete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="97bd3-154">Creación de una cuenta de ejecución con un script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="97bd3-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="97bd3-155">Este script de PowerShell incluye compatibilidad para hello siguiendo configuraciones:</span><span class="sxs-lookup"><span data-stu-id="97bd3-155">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="97bd3-156">Creación de una cuenta de ejecución mediante un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="97bd3-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="97bd3-157">Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="97bd3-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="97bd3-158">Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado de empresa.</span><span class="sxs-lookup"><span data-stu-id="97bd3-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="97bd3-159">Crear una cuenta de ejecución y una cuenta de identificación clásico mediante un certificado autofirmado en hello en la nube Azure Government.</span><span class="sxs-lookup"><span data-stu-id="97bd3-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="97bd3-160">Dependiendo de la opción de configuración de Hola que seleccione, el script de Hola crea Hola siguientes elementos.</span><span class="sxs-lookup"><span data-stu-id="97bd3-160">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="97bd3-161">**Para cuentas de ejecución:**</span><span class="sxs-lookup"><span data-stu-id="97bd3-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="97bd3-162">Crea un Azure AD aplicación toobe exportado con cualquier hello autofirmado o clave pública del certificado de la empresa, crea una cuenta de entidad de servicio para la aplicación hello en Azure AD y asigna Hola rol Colaborador para cuenta de hello en el actual suscripción.</span><span class="sxs-lookup"><span data-stu-id="97bd3-162">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="97bd3-163">Puede cambiar esta configuración tooOwner o cualquier otro rol.</span><span class="sxs-lookup"><span data-stu-id="97bd3-163">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="97bd3-164">Para más información, consulte [Control de acceso basado en rol en Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="97bd3-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="97bd3-165">Crea un activo de certificado de automatización denominado *AzureRunAsCertificate* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="97bd3-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="97bd3-166">activo de certificado de Hello contiene la clave privada de hello certificado utilizado por la aplicación hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97bd3-166">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="97bd3-167">Crea un recurso de conexión de automatización denominado *AzureRunAsConnection* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="97bd3-167">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="97bd3-168">activo de conexión de Hello contiene applicationId hello, tenantId, Id. de suscripción y la huella digital del certificado.</span><span class="sxs-lookup"><span data-stu-id="97bd3-168">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="97bd3-169">**Para cuentas de ejecución clásicas:**</span><span class="sxs-lookup"><span data-stu-id="97bd3-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="97bd3-170">Crea un activo de certificado de automatización denominado *AzureClassicRunAsCertificate* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="97bd3-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="97bd3-171">activo de certificado de Hello contiene la clave privada del certificado Hola utilizado por el certificado de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="97bd3-171">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="97bd3-172">Crea un recurso de conexión de automatización denominado *AzureClassicRunAsConnection* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="97bd3-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="97bd3-173">activo de conexión de Hello contiene el nombre de la suscripción de hello, Id. de suscripción y el nombre del recurso de certificado.</span><span class="sxs-lookup"><span data-stu-id="97bd3-173">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="97bd3-174">Si selecciona cualquiera de las opciones para crear una cuenta de identificación clásico, después de ejecuta script de Hola, carga Hola certificado público almacén de administración de toohello (extensión de nombre de archivo .cer) para suscripción Hola esa cuenta de automatización de Hola se creó en.</span><span class="sxs-lookup"><span data-stu-id="97bd3-174">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="97bd3-175">Guardar Hola siguiente secuencia de comandos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="97bd3-175">Save hello following script on your computer.</span></span> <span data-ttu-id="97bd3-176">En este ejemplo, guárdelo con el nombre de archivo de hello *RunAsAccount.ps1 nuevo*.</span><span class="sxs-lookup"><span data-stu-id="97bd3-176">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
        Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                       [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
            -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
            -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate = Get-Date $PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
            Sleep -s 10
            New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
            $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
            $Retries++;
        }
            return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
            return
        }

        Login-AzureRmAccount -Environment $EnvironmentName 
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
           $CertificateName = $AutomationAccountName+$CertifcateAssetName
           $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
           $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
           $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
           CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
             # Create a Run As account by using a service principal
             $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
             $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
             $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
             $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                     "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                     "Then click Upload and upload hello .cer format of #CERT#"

              if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
              $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
              $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
              $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
              $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
              $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
              $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
              $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
              $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
              CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="97bd3-177">En el equipo, inicie **Windows PowerShell** de hello **iniciar** pantalla con derechos de usuario elevados.</span><span class="sxs-lookup"><span data-stu-id="97bd3-177">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="97bd3-178">De hello elevado shell de línea de comandos, vaya toohello carpeta que contiene el script de Hola que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="97bd3-178">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="97bd3-179">Ejecutar script de Hola mediante el uso de valores de parámetro de hello para la configuración de Hola que necesite.</span><span class="sxs-lookup"><span data-stu-id="97bd3-179">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="97bd3-180">**Creación de una cuenta de ejecución mediante un certificado autofirmado**</span><span class="sxs-lookup"><span data-stu-id="97bd3-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="97bd3-181">**Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado**</span><span class="sxs-lookup"><span data-stu-id="97bd3-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="97bd3-182">**Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado de empresa**</span><span class="sxs-lookup"><span data-stu-id="97bd3-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="97bd3-183">**Crear una cuenta de ejecución y una cuenta de identificación clásico mediante un certificado autofirmado en hello en la nube Azure Government**</span><span class="sxs-lookup"><span data-stu-id="97bd3-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="97bd3-184">Una vez ejecutado el script de Hola, será tooauthenticate solicitada con Azure.</span><span class="sxs-lookup"><span data-stu-id="97bd3-184">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="97bd3-185">Inicie sesión con una cuenta que sea miembro del rol de administradores de suscripción de Hola y Coadministrador de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="97bd3-185">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="97bd3-186">Después de que el script de Hola se ha ejecutado correctamente, observe Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="97bd3-186">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="97bd3-187">Si ha creado una cuenta de identificación clásico con un certificado autofirmado público (archivo .cer), el script de Hola crea y guarda toohello carpeta de archivos temporales en el equipo en el perfil de usuario de hello *%USERPROFILE%\AppData\Local\Temp*, que ya ha utilizado la sesión de PowerShell de tooexecute Hola.</span><span class="sxs-lookup"><span data-stu-id="97bd3-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="97bd3-188">Si creó una cuenta de identificación clásica con un certificado público de empresa (archivo .cer) , use este certificado.</span><span class="sxs-lookup"><span data-stu-id="97bd3-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="97bd3-189">Siga las instrucciones de Hola para [cargar una toohello de certificado de la API de administración portal de Azure clásico](../azure-api-management-certs.md)y, a continuación, validar configuración de credencial de hello con recursos de implementación clásica mediante hello [código de ejemplo tooauthenticate con recursos de implementación de Azure clásico](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="97bd3-189">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="97bd3-190">Si lo hizo *no* crear una cuenta de identificación clásico, autenticar con recursos de administrador de recursos y validar la configuración de credencial de hello mediante hello [código de ejemplo para autenticar con la administración de servicios recursos](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="97bd3-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="97bd3-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97bd3-191">Next steps</span></span>
* <span data-ttu-id="97bd3-192">Para obtener más información acerca de las entidades de servicio, consulte demasiado[objetos de entidad de servicio y aplicación](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="97bd3-192">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="97bd3-193">Para obtener más información sobre los certificados y servicios de Azure, consulte demasiado[Introducción a los certificados para servicios en la nube](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="97bd3-193">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>

---
title: aaaConfigure ejecutar como cuentas de Azure | Documentos de Microsoft
description: "Este tutorial le guía a través del uso de creación, las pruebas y ejemplo de Hola de autenticación de la entidad de seguridad en la automatización de Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "nombre de la entidad de servicio, setspn, autenticación de azure"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="fbe49-104">Autenticación de Runbooks con una cuenta de ejecución de Azure</span><span class="sxs-lookup"><span data-stu-id="fbe49-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="fbe49-105">Este artículo muestra cómo tooconfigure una automatización de Azure cuenta Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe49-105">This article shows you how tooconfigure an Azure Automation account in hello Azure portal.</span></span> <span data-ttu-id="fbe49-106">toodo por lo tanto, se usan Hola ejecutar como cuenta característica tooauthenticate runbooks administrar recursos de Azure Resource Manager o administración de servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe49-106">toodo so, you use hello Run As account feature tooauthenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="fbe49-107">Cuando se crea una cuenta de automatización en hello portal de Azure, se crean automáticamente dos cuentas:</span><span class="sxs-lookup"><span data-stu-id="fbe49-107">When you create an Automation account in hello Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="fbe49-108">Una cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="fbe49-108">A Run As account.</span></span> <span data-ttu-id="fbe49-109">Esta cuenta crea una entidad de servicio en Azure Active Directory (Azure AD) y un certificado.</span><span class="sxs-lookup"><span data-stu-id="fbe49-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="fbe49-110">También asigna control de acceso basado en roles de colaborador de hello (RBAC), que administra los recursos del Administrador de recursos mediante el uso de runbooks.</span><span class="sxs-lookup"><span data-stu-id="fbe49-110">It also assigns hello Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="fbe49-111">Una cuenta de ejecución clásica.</span><span class="sxs-lookup"><span data-stu-id="fbe49-111">A Classic Run As account.</span></span> <span data-ttu-id="fbe49-112">Esta cuenta carga un certificado de administración, que es usar toomanage administración de servicios o recursos clásicos mediante runbooks.</span><span class="sxs-lookup"><span data-stu-id="fbe49-112">This account uploads a management certificate, which is used toomanage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="fbe49-113">Debe crear una automatización cuenta simplifica el proceso de Hola para usted y le ayuda a que empezar rápidamente compilar e implementar runbooks toosupport la automatización.</span><span class="sxs-lookup"><span data-stu-id="fbe49-113">Creating an Automation account simplifies hello process for you and helps you quickly start building and deploying runbooks toosupport your automation needs.</span></span>

<span data-ttu-id="fbe49-114">Con una cuenta de ejecución y una cuenta de ejecución clásica puede:</span><span class="sxs-lookup"><span data-stu-id="fbe49-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="fbe49-115">Proporcionan una manera normalizada tooauthenticate con Azure para administrar el Administrador de recursos o los recursos de administración de servicios desde los runbooks en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe49-115">Provide a standardized way tooauthenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in hello Azure portal.</span></span>
* <span data-ttu-id="fbe49-116">Automatice el uso de Hola de runbooks globales, que puede configurar en las alertas de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe49-116">Automate hello use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="fbe49-117">Hola [característica de integración de Azure alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) con la automatización de runbooks global requiere una cuenta de automatización que se configura con una cuenta de ejecución y una cuenta de identificación clásico.</span><span class="sxs-lookup"><span data-stu-id="fbe49-117">hello [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="fbe49-118">Puede seleccionar una cuenta de automatización que ya ha definido las cuentas de ejecución e identificación clásico o puede elegir toocreate una nueva cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="fbe49-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose toocreate a new Automation account.</span></span>
>  

<span data-ttu-id="fbe49-119">Este artículo muestra cómo toocreate una cuenta de automatización de hello portal de Azure, actualizar una cuenta de automatización mediante el uso de PowerShell de Azure, administrar la configuración de la cuenta de hello y autenticarse en sus runbooks.</span><span class="sxs-lookup"><span data-stu-id="fbe49-119">This article shows how toocreate an Automation account from hello Azure portal, update an Automation account by using Azure PowerShell, manage hello account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="fbe49-120">Antes de empezar a crear una cuenta de automatización, es una buena idea toounderstand y tenga en cuenta Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="fbe49-120">Before you begin creating an Automation account, it's a good idea toounderstand and consider hello following:</span></span>

* <span data-ttu-id="fbe49-121">Crear una cuenta de automatización no afecta a las cuentas de automatización que se podría haber creado ya en hello clásico o modelo de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="fbe49-121">Creating an Automation account does not affect Automation accounts you might have already created in either hello classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="fbe49-122">Hola proceso solo funciona para las cuentas de automatización que se crean en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe49-122">hello process works only for Automation accounts that you create in hello Azure portal.</span></span> <span data-ttu-id="fbe49-123">Intentar toocreate una cuenta de hello portal de Azure clásico no replica Hola cuenta configuración de ejecución.</span><span class="sxs-lookup"><span data-stu-id="fbe49-123">Attempting toocreate an account from hello Azure classic portal does not replicate hello Run As account configuration.</span></span>
* <span data-ttu-id="fbe49-124">Si ya dispone de runbooks y activos (por ejemplo, programaciones o variables) en lugar toomanage los recursos clásicos, y desea tooauthenticate runbooks con hello nueva clásico cuenta de ejecución, realice una de las siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="fbe49-124">If you already have runbooks and assets (such as schedules or variables) in place toomanage classic resources, and you want runbooks tooauthenticate with hello new Classic Run As account, do either of hello following:</span></span>

  * <span data-ttu-id="fbe49-125">toocreate una cuenta de identificación clásico, siga las instrucciones de hello en la sección "Administración de la cuenta de ejecución" de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-125">toocreate a Classic Run As account, follow hello instructions in hello "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="fbe49-126">la cuenta existente, use Hola PowerShell tooupdate secuencia de comandos en la sección de "Actualizar su cuenta de automatización mediante PowerShell" Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-126">tooupdate your existing account, use hello PowerShell script in hello "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="fbe49-127">tooauthenticate mediante Hola nueva cuenta de ejecución y clásico ejecutar como cuenta de automatización de, deberá toomodify Hola de los runbooks existentes con código de ejemplo proporcionado en la sección de hello [ejemplos de código de autenticación](#authentication-code-examples).</span><span class="sxs-lookup"><span data-stu-id="fbe49-127">tooauthenticate by using hello new Run As account and Classic Run As Automation account, you  need toomodify your existing runbooks with hello example code provided in hello section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="fbe49-128">Hola cuenta de ejecución es para la autenticación con recursos de administrador de recursos con la entidad de servicio basada en certificados de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-128">hello Run As account is for authentication against Resource Manager resources using hello certificate-based service principal.</span></span> <span data-ttu-id="fbe49-129">Hola clásico cuenta de ejecución es para autenticar con recursos de administración de servicios con un certificado de administración.</span><span class="sxs-lookup"><span data-stu-id="fbe49-129">hello Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-hello-azure-portal"></a><span data-ttu-id="fbe49-130">Crear una cuenta de automatización de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="fbe49-130">Create an Automation account from hello Azure portal</span></span>
<span data-ttu-id="fbe49-131">En esta sección, creará una cuenta de automatización de Azure de hello portal de Azure, que a su vez crea una cuenta de ejecución y una cuenta de identificación clásico.</span><span class="sxs-lookup"><span data-stu-id="fbe49-131">In this section, you create an Azure Automation account from hello Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="fbe49-132">toocreate una cuenta de automatización, debe ser miembro del rol de administradores de servicios de Hola o Coadministrador de suscripción de Hola que concede el acceso toohello suscripción.</span><span class="sxs-lookup"><span data-stu-id="fbe49-132">toocreate an Automation account, you must be a member of hello Service Admins role or co-administrator of hello subscription that is granting access toohello subscription.</span></span> <span data-ttu-id="fbe49-133">Debe agregarse como instancia de Active Directory de una suscripción de toothat de usuario predeterminada.</span><span class="sxs-lookup"><span data-stu-id="fbe49-133">You must also be added as a user toothat subscription's default Active Directory instance.</span></span> <span data-ttu-id="fbe49-134">cuenta de Hello no es necesario toobe asignado un rol con privilegios.</span><span class="sxs-lookup"><span data-stu-id="fbe49-134">hello account does not need toobe assigned a privileged role.</span></span>
>
><span data-ttu-id="fbe49-135">Si no eres un miembro de instancia de Active Directory de la suscripción de hello antes de que se agreguen toohello rol de Coadministrador de suscripción de hello, se agregarán tooActive directorio como invitado.</span><span class="sxs-lookup"><span data-stu-id="fbe49-135">If you are not a member of hello subscription’s Active Directory instance before you are added toohello co-administrator role of hello subscription, you will be added tooActive Directory as a guest.</span></span> <span data-ttu-id="fbe49-136">En este caso, recibirá un "no tiene permisos toocreate..."</span><span class="sxs-lookup"><span data-stu-id="fbe49-136">In this instance, you will receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="fbe49-137">Advertencia de hello **agregar una cuenta de automatización** hoja.</span><span class="sxs-lookup"><span data-stu-id="fbe49-137">warning on hello **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="fbe49-138">Los usuarios que se agregaron rol de Coadministrador toohello en primer lugar se puede quitar de la instancia de Active Directory de la suscripción de Hola y vuelva a agrega toomake a un usuario en Active Directory completo.</span><span class="sxs-lookup"><span data-stu-id="fbe49-138">Users who were added toohello co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="fbe49-139">tooverify esta situación de hello **Azure Active Directory** panel en el portal de Azure mediante la selección de hello **usuarios y grupos**, seleccione **todos los usuarios** y, después de seleccionar usuario específico de Hello, seleccionar **perfil**.</span><span class="sxs-lookup"><span data-stu-id="fbe49-139">tooverify this situation from hello **Azure Active Directory** pane in hello Azure portal by selecting **Users and groups**, selecting **All users** and, after you select hello specific user, selecting **Profile**.</span></span> <span data-ttu-id="fbe49-140">Hola valo hello **tipo de usuario** atributo en el perfil de los usuarios de hello no debería ser igual **invitado**.</span><span class="sxs-lookup"><span data-stu-id="fbe49-140">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="fbe49-141">Inicie sesión en el portal de Azure con una cuenta que sea miembro del rol de administradores de suscripción de Hola y Coadministrador de suscripción de hello toohello.</span><span class="sxs-lookup"><span data-stu-id="fbe49-141">Sign in toohello Azure portal with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>

2. <span data-ttu-id="fbe49-142">Seleccione **Cuentas de Automation**.</span><span class="sxs-lookup"><span data-stu-id="fbe49-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="fbe49-143">En hello **cuentas de automatización** hoja, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="fbe49-143">On hello **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="fbe49-144">Hola **agregar una cuenta de automatización** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="fbe49-144">hello **Add Automation Account** blade opens.</span></span>

 ![hoja de "Agregar cuenta de automatización" Hello](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="fbe49-146">Si la cuenta no es miembro del rol de administradores de suscripción de Hola y Coadministrador de suscripción de hello, Hola después de advertencia se muestra en hello **agregar una cuenta de automatización** hoja:</span><span class="sxs-lookup"><span data-stu-id="fbe49-146">If your account is not a member of hello subscription administrators role and co-administrator of hello subscription, hello following warning is displayed on hello **Add Automation Account** blade:</span></span>
   >
   >![Advertencia para agregar cuenta de Automation](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="fbe49-148">En hello **agregar una cuenta de automatización** hoja en hello **nombre** , escriba un nombre para la nueva cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="fbe49-148">On hello **Add Automation Account** blade, in hello **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="fbe49-149">Si tiene más de una suscripción, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fbe49-149">If you have more than one subscription, do hello following:</span></span>

    <span data-ttu-id="fbe49-150">a.</span><span class="sxs-lookup"><span data-stu-id="fbe49-150">a.</span></span> <span data-ttu-id="fbe49-151">En **suscripción**, especifique una nueva cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="fbe49-151">Under **Subscription**, specify one for hello new account.</span></span>

    <span data-ttu-id="fbe49-152">b.</span><span class="sxs-lookup"><span data-stu-id="fbe49-152">b.</span></span> <span data-ttu-id="fbe49-153">En **Grupo de recursos**, haga clic en **Create new** (Crear nuevo) o **Use existing** (Usar existente).</span><span class="sxs-lookup"><span data-stu-id="fbe49-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="fbe49-154">c.</span><span class="sxs-lookup"><span data-stu-id="fbe49-154">c.</span></span> <span data-ttu-id="fbe49-155">En **Ubicación**, especifique un centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe49-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="fbe49-156">En **Crear cuenta de ejecución de Azure**, seleccione **Sí** y luego haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fbe49-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fbe49-157">Si decide no toocreate Hola cuenta de ejecución seleccionando **No**, se muestra un mensaje de advertencia hello **agregar una cuenta de automatización** hoja.</span><span class="sxs-lookup"><span data-stu-id="fbe49-157">If you choose not toocreate hello Run As account by selecting **No**, a warning message is displayed hello **Add Automation Account** blade.</span></span> <span data-ttu-id="fbe49-158">Aunque se crea la cuenta de hello en hello portal de Azure, no tiene una identidad de autenticación correspondiente en el clásico o el servicio de directorio de suscripción de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="fbe49-158">Although hello account is created in hello Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="fbe49-159">Por lo tanto, la cuenta de hello no tiene ningún tooresources de acceso en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="fbe49-159">Consequently, hello account has no access tooresources in your subscription.</span></span> <span data-ttu-id="fbe49-160">Este escenario evita que los runbooks que hacen referencia a esta cuenta puedan autenticarse y realizar tareas con los recursos en dichos modelos de implementación.</span><span class="sxs-lookup"><span data-stu-id="fbe49-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > ![Mensaje de advertencia en la hoja de "Agregar cuenta de automatización" hello](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="fbe49-162">Además, dado que no se crea la entidad de servicio de hello, rol de colaborador de hello no está asignado.</span><span class="sxs-lookup"><span data-stu-id="fbe49-162">Additionally, because hello service principal is not created, hello Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="fbe49-163">Mientras Azure crea la cuenta de automatización de hello, puede seguir el progreso de hello en **notificaciones** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-163">While Azure creates hello Automation account, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="resources"></a><span data-ttu-id="fbe49-164">Recursos</span><span class="sxs-lookup"><span data-stu-id="fbe49-164">Resources</span></span>
<span data-ttu-id="fbe49-165">Cuando se crea correctamente la cuenta de automatización de hello, varios recursos se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="fbe49-165">When hello Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="fbe49-166">recursos de Hola se resumen en hello las dos tablas siguientes:</span><span class="sxs-lookup"><span data-stu-id="fbe49-166">hello resources are summarized in hello following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="fbe49-167">Recursos de la cuenta de ejecución</span><span class="sxs-lookup"><span data-stu-id="fbe49-167">Run As account resources</span></span>

| <span data-ttu-id="fbe49-168">Recurso</span><span class="sxs-lookup"><span data-stu-id="fbe49-168">Resource</span></span> | <span data-ttu-id="fbe49-169">Descripción</span><span class="sxs-lookup"><span data-stu-id="fbe49-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fbe49-170">Runbook AzureAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="fbe49-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="fbe49-171">Runbook gráfico de ejemplo que muestra cómo tooauthenticate mediante el uso de Hola cuenta de ejecución y hace que todos los recursos del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-171">An example graphical runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="fbe49-172">Runbook AzureAutomationTutorialScript</span><span class="sxs-lookup"><span data-stu-id="fbe49-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="fbe49-173">Un runbook de PowerShell de ejemplo que muestra cómo tooauthenticate mediante el uso de Hola cuenta de ejecución y hace que todos los recursos del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-173">An example PowerShell runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="fbe49-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="fbe49-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="fbe49-175">activo de certificado de Hola que se crea automáticamente al crear una cuenta de automatización o usar hello siguiente script de PowerShell para una cuenta existente.</span><span class="sxs-lookup"><span data-stu-id="fbe49-175">hello certificate asset that's automatically created when you create an Automation account or use hello following PowerShell script for an existing account.</span></span> <span data-ttu-id="fbe49-176">certificado de Hello le permite tooauthenticate con Azure, por lo que puede administrar los recursos de Azure Resource Manager desde los runbooks.</span><span class="sxs-lookup"><span data-stu-id="fbe49-176">hello certificate allows you tooauthenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="fbe49-177">certificado de Hello tiene una duración de un año.</span><span class="sxs-lookup"><span data-stu-id="fbe49-177">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="fbe49-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="fbe49-178">AzureRunAsConnection</span></span> | <span data-ttu-id="fbe49-179">activo de conexión de Hola que se crea automáticamente al crear una cuenta de automatización o usar el script de PowerShell de Hola para una cuenta existente.</span><span class="sxs-lookup"><span data-stu-id="fbe49-179">hello connection asset that's automatically created when you create an Automation account or use hello PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="fbe49-180">Recursos de la cuenta de ejecución clásica</span><span class="sxs-lookup"><span data-stu-id="fbe49-180">Classic Run As account resources</span></span>

| <span data-ttu-id="fbe49-181">Recurso</span><span class="sxs-lookup"><span data-stu-id="fbe49-181">Resource</span></span> | <span data-ttu-id="fbe49-182">Descripción</span><span class="sxs-lookup"><span data-stu-id="fbe49-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fbe49-183">Runbook AzureClassicAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="fbe49-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="fbe49-184">Un runbook gráfico de ejemplo que obtiene todas las máquinas virtuales de Hola que se crean utilizando el modelo de implementación clásica de hello en una suscripción mediante el uso de hello clásico cuenta de ejecución (certificado) y, a continuación, escribe el nombre de la máquina virtual de Hola y el estado.</span><span class="sxs-lookup"><span data-stu-id="fbe49-184">An example graphical runbook that gets all hello VMs that are created using hello classic deployment model in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="fbe49-185">Runbook AzureClassicAutomationTutorial Script</span><span class="sxs-lookup"><span data-stu-id="fbe49-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="fbe49-186">Un runbook de PowerShell de ejemplo que obtiene todos Hola clásicas máquinas virtuales en una suscripción mediante el uso de hello clásico cuenta de ejecución (certificado) y, a continuación, escribe Hola estado y el nombre de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fbe49-186">An example PowerShell runbook that gets all hello classic VMs in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="fbe49-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="fbe49-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="fbe49-188">activo de certificado de Hello creada automáticamente usar tooauthenticate con Azure para que pueda administrar los recursos clásicos Azure desde los runbooks.</span><span class="sxs-lookup"><span data-stu-id="fbe49-188">hello automatically created certificate asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="fbe49-189">certificado de Hello tiene una duración de un año.</span><span class="sxs-lookup"><span data-stu-id="fbe49-189">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="fbe49-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="fbe49-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="fbe49-191">activo de conexión creado automáticamente de Hello usar tooauthenticate con Azure para que pueda administrar los recursos clásicos Azure desde los runbooks.</span><span class="sxs-lookup"><span data-stu-id="fbe49-191">hello automatically created connection asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="fbe49-192">Comprobación de la autenticación de ejecución</span><span class="sxs-lookup"><span data-stu-id="fbe49-192">Verify Run As authentication</span></span>
<span data-ttu-id="fbe49-193">Realizar una tooconfirm prueba pequeñas que pueda autenticar correctamente mediante el uso de hello nueva cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="fbe49-193">Perform a small test tooconfirm that you can successfully authenticate by using hello new Run As account.</span></span>

1. <span data-ttu-id="fbe49-194">Hola portal de Azure, abra la cuenta de automatización de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fbe49-194">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="fbe49-195">Haga clic en hello **Runbooks** icono tooopen Hola lista de runbooks.</span><span class="sxs-lookup"><span data-stu-id="fbe49-195">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="fbe49-196">Seleccione hello **AzureAutomationTutorialScript** runbook y, a continuación, haga clic en **iniciar** toostart Hola runbook.</span><span class="sxs-lookup"><span data-stu-id="fbe49-196">Select hello **AzureAutomationTutorialScript** runbook, and then click **Start** toostart hello runbook.</span></span> <span data-ttu-id="fbe49-197">se produce Hola siguientes eventos:</span><span class="sxs-lookup"><span data-stu-id="fbe49-197">hello following events occur:</span></span>
 * <span data-ttu-id="fbe49-198">A [trabajo del runbook](automation-runbook-execution.md) se crea, hello **trabajo** hoja se muestra y se muestra el estado del trabajo de Hola Hola **resumen de trabajos** icono.</span><span class="sxs-lookup"><span data-stu-id="fbe49-198">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="fbe49-199">estado del trabajo Hello, comienza siendo **en cola**, lo que indica que está esperando un runbook worker en hello toobecome de nube disponible.</span><span class="sxs-lookup"><span data-stu-id="fbe49-199">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="fbe49-200">Hola estado pasa a ser **iniciando** cuando un trabajador notificaciones trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-200">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="fbe49-201">Hola estado pasa a ser **ejecuta** cuando Hola runbook comienza a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="fbe49-201">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="fbe49-202">Cuando el trabajo del runbook Hola ha terminado de ejecutarse, debería ver un estado de **completado**.</span><span class="sxs-lookup"><span data-stu-id="fbe49-202">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="fbe49-203">toosee Hola resultados detallados de hello runbook, haga clic en hello **salida** icono.</span><span class="sxs-lookup"><span data-stu-id="fbe49-203">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="fbe49-204">Hola **salida** hoja se muestra, que muestra ese runbook Hola correctamente ha autenticado y devuelve una lista de todos los recursos disponibles en el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-204">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all resources available in hello resource group.</span></span>

5. <span data-ttu-id="fbe49-205">Hola cerrar **salida** hoja tooreturn toohello **resumen de trabajos** hoja.</span><span class="sxs-lookup"><span data-stu-id="fbe49-205">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="fbe49-206">Hola cerrar **resumen de trabajos** hoja y Hola correspondiente **AzureAutomationTutorialScript** hoja de runbooks.</span><span class="sxs-lookup"><span data-stu-id="fbe49-206">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="fbe49-207">Comprobación de la autenticación de ejecución de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="fbe49-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="fbe49-208">Realizar una pequeña similar tooconfirm que pueda autenticar correctamente mediante el uso de hello nueva clásico cuenta de ejecución de pruebas.</span><span class="sxs-lookup"><span data-stu-id="fbe49-208">Perform a similar small test tooconfirm that you can successfully authenticate by using hello new Classic Run As account.</span></span>

1. <span data-ttu-id="fbe49-209">Hola portal de Azure, abra la cuenta de automatización de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fbe49-209">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="fbe49-210">Haga clic en hello **Runbooks** icono tooopen Hola lista de runbooks.</span><span class="sxs-lookup"><span data-stu-id="fbe49-210">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="fbe49-211">Seleccione hello **AzureClassicAutomationTutorialScript** runbook y, a continuación, haga clic en **iniciar** demasiado iniciar runbook Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-211">Select hello **AzureClassicAutomationTutorialScript** runbook, and then click **Start** too start hello runbook.</span></span> <span data-ttu-id="fbe49-212">se produce Hola siguientes eventos:</span><span class="sxs-lookup"><span data-stu-id="fbe49-212">hello following events occur:</span></span>

 * <span data-ttu-id="fbe49-213">A [trabajo del runbook](automation-runbook-execution.md) se crea, hello **trabajo** hoja se muestra y se muestra el estado del trabajo de Hola Hola **resumen de trabajos** icono.</span><span class="sxs-lookup"><span data-stu-id="fbe49-213">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="fbe49-214">estado del trabajo Hello, comienza siendo **en cola**, lo que indica que está esperando un runbook worker en hello toobecome de nube disponible.</span><span class="sxs-lookup"><span data-stu-id="fbe49-214">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="fbe49-215">Hola estado pasa a ser **iniciando** cuando un trabajador notificaciones trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-215">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="fbe49-216">Hola estado pasa a ser **ejecuta** cuando Hola runbook comienza a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="fbe49-216">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="fbe49-217">Cuando el trabajo del runbook Hola ha terminado de ejecutarse, debería ver un estado de **completado**.</span><span class="sxs-lookup"><span data-stu-id="fbe49-217">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![Prueba de Runbook de entidad de seguridad](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="fbe49-219">toosee Hola resultados detallados de hello runbook, haga clic en hello **salida** icono.</span><span class="sxs-lookup"><span data-stu-id="fbe49-219">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="fbe49-220">Hola **salida** hoja se muestra, que muestra ese runbook Hola correctamente ha autenticado y devuelve una lista de todas las máquinas virtuales clásicas en la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-220">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all classic VMs in hello subscription.</span></span>

5. <span data-ttu-id="fbe49-221">Hola cerrar **salida** hoja tooreturn toohello **resumen de trabajos** hoja.</span><span class="sxs-lookup"><span data-stu-id="fbe49-221">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="fbe49-222">Hola cerrar **resumen de trabajos** hoja y Hola correspondiente **AzureAutomationTutorialScript** hoja de runbooks.</span><span class="sxs-lookup"><span data-stu-id="fbe49-222">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="fbe49-223">Administración de la cuenta de ejecución</span><span class="sxs-lookup"><span data-stu-id="fbe49-223">Managing your Run As account</span></span>
<span data-ttu-id="fbe49-224">En algún momento antes de que expire su cuenta de automatización, necesitará toorenew Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="fbe49-224">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="fbe49-225">Si cree que Hola cuenta de ejecución está en peligro, puede eliminar y volver a crearla.</span><span class="sxs-lookup"><span data-stu-id="fbe49-225">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="fbe49-226">Esta sección se describe cómo tooperform estas operaciones.</span><span class="sxs-lookup"><span data-stu-id="fbe49-226">This section discusses how tooperform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="fbe49-227">Renovación de certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="fbe49-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="fbe49-228">certificado autofirmado de Hola que creó para la cuenta de ejecución de Hola expira un año a partir de la fecha de Hola de creación.</span><span class="sxs-lookup"><span data-stu-id="fbe49-228">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="fbe49-229">Se puede renovar en cualquier momento antes de que expire.</span><span class="sxs-lookup"><span data-stu-id="fbe49-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="fbe49-230">Cuando renovarlo, certificado válido de hello actual es retenido tooensure que los runbooks que se ponen en cola hasta o activamente ejecutándose y que autenticarse con hello cuenta de ejecución, no se afecta negativamente.</span><span class="sxs-lookup"><span data-stu-id="fbe49-230">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="fbe49-231">certificado de Hello sigue siendo válido hasta la fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="fbe49-231">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="fbe49-232">Si ha configurado su toouse de cuenta automatización ejecutar como un certificado emitido por la entidad de certificación de empresa y use esta opción, certificado de empresa de Hola se reemplazará por un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="fbe49-232">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="fbe49-233">Hola toorenew certificados, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fbe49-233">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="fbe49-234">Hola portal de Azure, abrir cuenta de automatización de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-234">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="fbe49-235">En hello **cuenta de automatización** hoja en hello **cuenta propiedades** panel, en **configuración de la cuenta**, seleccione **cuentas de ejecución**.</span><span class="sxs-lookup"><span data-stu-id="fbe49-235">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Panel de propiedades de la cuenta de Automation](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="fbe49-237">En hello **cuentas de ejecución** hoja de propiedades, seleccione cualquier Hola ejecutar como cuenta u Hola clásico cuenta de ejecución que desea toorenew Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="fbe49-237">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="fbe49-238">En hello **propiedades** hoja para hello seleccionado cuenta, haga clic en **renovar certificado**.</span><span class="sxs-lookup"><span data-stu-id="fbe49-238">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Renovación del certificado para una cuenta de ejecución](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="fbe49-240">Mientras se que se va a renovar el certificado de hello, puede seguir el progreso de hello en **notificaciones** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-240">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="fbe49-241">Eliminación de una cuenta de ejecución o de ejecución clásica</span><span class="sxs-lookup"><span data-stu-id="fbe49-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="fbe49-242">Esta sección se describe cómo toodelete y volver a crear una cuenta de ejecución o identificación clásico.</span><span class="sxs-lookup"><span data-stu-id="fbe49-242">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="fbe49-243">Al realizar esta acción, se conserva Hola cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="fbe49-243">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="fbe49-244">Después de eliminar una cuenta de ejecución o identificación clásico, puede volver a crearla en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe49-244">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="fbe49-245">Hola portal de Azure, abrir cuenta de automatización de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-245">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="fbe49-246">En hello **cuenta de automatización** hoja, en el panel de propiedades de cuenta hello, seleccione **cuentas de ejecución**.</span><span class="sxs-lookup"><span data-stu-id="fbe49-246">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="fbe49-247">En hello **cuentas de ejecución** hoja de propiedades, seleccione cualquier Hola ejecutar como cuenta de ejecución de o clásico como la cuenta que desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="fbe49-247">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="fbe49-248">A continuación, en hello **propiedades** hoja para hello seleccionado cuenta, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="fbe49-248">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Eliminación de una cuenta de ejecución](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="fbe49-250">Mientras se está eliminando la cuenta de hello, puede seguir el progreso de hello en **notificaciones** en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-250">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="fbe49-251">Después de que se ha eliminado la cuenta de hello, se puede volver a crear en hello **cuentas de ejecución** opción de creación de la hoja de propiedades seleccionando hello **ejecutar como cuenta de Azure**.</span><span class="sxs-lookup"><span data-stu-id="fbe49-251">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Volver a crear Hola automatización de la cuenta de ejecución](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="fbe49-253">Error de configuración</span><span class="sxs-lookup"><span data-stu-id="fbe49-253">Misconfiguration</span></span>
<span data-ttu-id="fbe49-254">Algunos elementos de configuración necesarios para toofunction de cuenta de identificación o identificación clásico Hola correctamente podrían se han eliminado o creó incorrectamente durante la instalación inicial.</span><span class="sxs-lookup"><span data-stu-id="fbe49-254">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="fbe49-255">Hola elementos incluyen:</span><span class="sxs-lookup"><span data-stu-id="fbe49-255">hello items include:</span></span>

* <span data-ttu-id="fbe49-256">Recurso de certificado</span><span class="sxs-lookup"><span data-stu-id="fbe49-256">Certificate asset</span></span>
* <span data-ttu-id="fbe49-257">Recurso de conexión</span><span class="sxs-lookup"><span data-stu-id="fbe49-257">Connection asset</span></span>
* <span data-ttu-id="fbe49-258">Se ha quitado la cuenta de ejecución de rol de colaborador de Hola</span><span class="sxs-lookup"><span data-stu-id="fbe49-258">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="fbe49-259">Entidad de servicio o aplicación en Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbe49-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="fbe49-260">Hola anterior y otras instancias de una configuración incorrecta, Hola cuenta de automatización detecta Hola cambia y muestra un estado de *incompleta* en hello **cuentas de ejecución** hoja de propiedades para hello cuenta.</span><span class="sxs-lookup"><span data-stu-id="fbe49-260">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![Estado de configuración incompleta de la cuenta de ejecución](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="fbe49-262">Cuando se selecciona la cuenta de identificación de hello, Hola cuenta **propiedades** panel muestra hello mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="fbe49-262">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Mensaje de advertencia de configuración incompleta de la cuenta de ejecución](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="fbe49-264">.</span><span class="sxs-lookup"><span data-stu-id="fbe49-264">.</span></span>

<span data-ttu-id="fbe49-265">Rápidamente puede resolver estos problemas de la cuenta ejecutar como eliminar y volver a crear la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="fbe49-265">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="fbe49-266">Actualización de la cuenta de Automation mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbe49-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="fbe49-267">Puede usar PowerShell tooupdate su cuenta de automatización existente si:</span><span class="sxs-lookup"><span data-stu-id="fbe49-267">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="fbe49-268">Crear una cuenta de automatización, pero rechazar toocreate Hola cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="fbe49-268">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="fbe49-269">Ya utiliza un administrador de recursos toomanage cuenta recursos de automatización y desea tooupdate Hola cuenta tooinclude Hola cuenta de ejecución para la autenticación de runbook.</span><span class="sxs-lookup"><span data-stu-id="fbe49-269">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="fbe49-270">Ya utiliza un recursos clásicos de automatización de la cuenta toomanage y desea tooupdate se toouse Hola clásico cuenta de ejecución en lugar de crear una cuenta nueva y migrar su tooit runbooks y activos.</span><span class="sxs-lookup"><span data-stu-id="fbe49-270">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="fbe49-271">Toocreate que desee ejecutar como y una cuenta de identificación clásico mediante el uso de un certificado emitido por la entidad de certificación (CA) empresarial.</span><span class="sxs-lookup"><span data-stu-id="fbe49-271">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="fbe49-272">script de Hola tiene Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="fbe49-272">hello script has hello following prerequisites:</span></span>

* <span data-ttu-id="fbe49-273">script de Hola se puede ejecutar solo en Windows 10 y Windows Server 2016 con módulos de Azure Resource Manager 2.01 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="fbe49-273">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="fbe49-274">No se admite en versiones anteriores de Windows.</span><span class="sxs-lookup"><span data-stu-id="fbe49-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="fbe49-275">Azure PowerShell 1.0 y versiones superiores.</span><span class="sxs-lookup"><span data-stu-id="fbe49-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="fbe49-276">Para obtener información acerca de la versión de Hola PowerShell 1.0, vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fbe49-276">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="fbe49-277">Una cuenta de automatización, que se hace referencia como valor de Hola de hello *: AutomationAccountName* y *- ApplicationDisplayName* parámetros Hola siguiente script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fbe49-277">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="fbe49-278">Hola tooget los valores de *SubscriptionID*, *ResourceGroup*, y *AutomationAccountName*, que son parámetros necesarios para las secuencias de comandos de hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fbe49-278">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="fbe49-279">En el portal de Azure de Hola, seleccione su cuenta de automatización en hello **cuenta de automatización** hoja y, a continuación, seleccione **toda la configuración de**.</span><span class="sxs-lookup"><span data-stu-id="fbe49-279">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="fbe49-280">En hello **toda la configuración de** hoja, en **configuración de la cuenta**, seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="fbe49-280">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="fbe49-281">Tenga en cuenta los valores de hello en hello **propiedades** hoja.</span><span class="sxs-lookup"><span data-stu-id="fbe49-281">Note hello values on hello **Properties** blade.</span></span>

![hoja de "Propiedades" de cuenta de automatización de Hola](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="fbe49-283">Creación de un script de PowerShell de una cuenta de ejecución</span><span class="sxs-lookup"><span data-stu-id="fbe49-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="fbe49-284">Este script de PowerShell incluye compatibilidad para hello siguiendo configuraciones:</span><span class="sxs-lookup"><span data-stu-id="fbe49-284">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="fbe49-285">Creación de una cuenta de ejecución mediante un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="fbe49-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="fbe49-286">Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="fbe49-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="fbe49-287">Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado de empresa.</span><span class="sxs-lookup"><span data-stu-id="fbe49-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="fbe49-288">Crear una cuenta de ejecución y una cuenta de identificación clásico mediante un certificado autofirmado en hello en la nube Azure Government.</span><span class="sxs-lookup"><span data-stu-id="fbe49-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="fbe49-289">Dependiendo de la opción de configuración de Hola que seleccione, el script de Hola crea Hola siguientes elementos.</span><span class="sxs-lookup"><span data-stu-id="fbe49-289">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="fbe49-290">**Para cuentas de ejecución:**</span><span class="sxs-lookup"><span data-stu-id="fbe49-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="fbe49-291">Crea un Azure AD aplicación toobe exportado con cualquier hello autofirmado o clave pública del certificado de la empresa, crea una cuenta de entidad de servicio para la aplicación hello en Azure AD y asigna Hola rol Colaborador para cuenta de hello en el actual suscripción.</span><span class="sxs-lookup"><span data-stu-id="fbe49-291">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="fbe49-292">Puede cambiar esta configuración tooOwner o cualquier otro rol.</span><span class="sxs-lookup"><span data-stu-id="fbe49-292">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="fbe49-293">Para más información, consulte [Control de acceso basado en rol en Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="fbe49-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="fbe49-294">Crea un activo de certificado de automatización denominado *AzureRunAsCertificate* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="fbe49-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="fbe49-295">activo de certificado de Hello contiene la clave privada de hello certificado utilizado por la aplicación hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbe49-295">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="fbe49-296">Crea un recurso de conexión de automatización denominado *AzureRunAsConnection* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="fbe49-296">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="fbe49-297">activo de conexión de Hello contiene applicationId hello, tenantId, Id. de suscripción y la huella digital del certificado.</span><span class="sxs-lookup"><span data-stu-id="fbe49-297">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="fbe49-298">**Para cuentas de ejecución clásicas:**</span><span class="sxs-lookup"><span data-stu-id="fbe49-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="fbe49-299">Crea un activo de certificado de automatización denominado *AzureClassicRunAsCertificate* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="fbe49-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="fbe49-300">activo de certificado de Hello contiene la clave privada del certificado Hola utilizado por el certificado de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-300">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="fbe49-301">Crea un recurso de conexión de automatización denominado *AzureClassicRunAsConnection* en hello especifica la cuenta de automatización.</span><span class="sxs-lookup"><span data-stu-id="fbe49-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="fbe49-302">activo de conexión de Hello contiene el nombre de la suscripción de hello, Id. de suscripción y el nombre del recurso de certificado.</span><span class="sxs-lookup"><span data-stu-id="fbe49-302">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="fbe49-303">Si selecciona cualquiera de las opciones para crear una cuenta de identificación clásico, después de ejecuta script de Hola, carga Hola certificado público almacén de administración de toohello (extensión de nombre de archivo .cer) para suscripción Hola esa cuenta de automatización de Hola se creó en.</span><span class="sxs-lookup"><span data-stu-id="fbe49-303">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

<span data-ttu-id="fbe49-304">tooexecute Hola script y cargar el certificado de hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fbe49-304">tooexecute hello script and upload hello certificate, do hello following:</span></span>

1. <span data-ttu-id="fbe49-305">Guardar Hola siguiente secuencia de comandos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="fbe49-305">Save hello following script on your computer.</span></span> <span data-ttu-id="fbe49-306">En este ejemplo, guárdelo con el nombre de archivo de hello *RunAsAccount.ps1 nuevo*.</span><span class="sxs-lookup"><span data-stu-id="fbe49-306">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

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
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
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
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
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
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="fbe49-307">En el equipo, haga clic en **Inicio** y luego inicie **Windows PowerShell** con derechos de usuario elevados.</span><span class="sxs-lookup"><span data-stu-id="fbe49-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="fbe49-308">De hello elevado shell de línea de comandos de PowerShell, vaya toohello carpeta que contiene el script de Hola que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="fbe49-308">From hello elevated PowerShell command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>

4. <span data-ttu-id="fbe49-309">Ejecutar script de Hola mediante el uso de valores de parámetro de hello para la configuración de Hola que necesite.</span><span class="sxs-lookup"><span data-stu-id="fbe49-309">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="fbe49-310">**Creación de una cuenta de ejecución mediante un certificado autofirmado**</span><span class="sxs-lookup"><span data-stu-id="fbe49-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="fbe49-311">**Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado**</span><span class="sxs-lookup"><span data-stu-id="fbe49-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="fbe49-312">**Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado de empresa**</span><span class="sxs-lookup"><span data-stu-id="fbe49-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="fbe49-313">**Crear una cuenta de ejecución y una cuenta de identificación clásico mediante un certificado autofirmado en hello en la nube Azure Government**</span><span class="sxs-lookup"><span data-stu-id="fbe49-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="fbe49-314">Una vez ejecutado el script de Hola, será tooauthenticate solicitada con Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe49-314">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="fbe49-315">Inicie sesión con una cuenta que sea miembro del rol de administradores de suscripción de Hola y Coadministrador de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-315">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="fbe49-316">Después de que el script de Hola se ha ejecutado correctamente, observe Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="fbe49-316">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="fbe49-317">Si ha creado una cuenta de identificación clásico con un certificado autofirmado público (archivo .cer), el script de Hola crea y guarda toohello carpeta de archivos temporales en el equipo en el perfil de usuario de hello *%USERPROFILE%\AppData\Local\Temp*, que ya ha utilizado la sesión de PowerShell de tooexecute Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="fbe49-318">Si creó una cuenta de identificación clásica con un certificado público de empresa (archivo .cer) , use este certificado.</span><span class="sxs-lookup"><span data-stu-id="fbe49-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="fbe49-319">Siga las instrucciones de Hola para [cargar una toohello de certificado de la API de administración portal de Azure clásico](../azure-api-management-certs.md)y, a continuación, validar configuración de credencial de hello con recursos de administración de servicios mediante hello [código de ejemplo tooauthenticate con recursos de administración del servicio](#sample-code-to-authenticate-with-service-management-resources).</span><span class="sxs-lookup"><span data-stu-id="fbe49-319">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with Service Management resources by using hello [sample code tooauthenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="fbe49-320">Si lo hizo *no* crear una cuenta de identificación clásico, autenticar con recursos de administrador de recursos y validar la configuración de credencial de hello mediante hello [código de ejemplo para autenticar con la administración de servicios recursos](#sample-code-to-authenticate-with-resource-manager-resources).</span><span class="sxs-lookup"><span data-stu-id="fbe49-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a><span data-ttu-id="fbe49-321">Tooauthenticate de código de ejemplo con los recursos del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="fbe49-321">Sample code tooauthenticate with Resource Manager resources</span></span>
<span data-ttu-id="fbe49-322">Puede usar los siguientes Hola actualizar código, tomado de Hola de ejemplo *AzureAutomationTutorialScript* runbook de ejemplo, tooauthenticate con hello ejecutar como cuenta toomanage el Administrador de recursos recursos con sus runbooks.</span><span class="sxs-lookup"><span data-stu-id="fbe49-322">You can use hello following updated sample code, taken from hello *AzureAutomationTutorialScript* example runbook, tooauthenticate by using hello Run As account toomanage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

<span data-ttu-id="fbe49-323">toohelp tooeasily funcionan entre varias suscripciones, el script de Hola incluye dos líneas adicionales de código que admiten que hacen referencia a un contexto de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="fbe49-323">toohelp you tooeasily work between multiple subscriptions, hello script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="fbe49-324">Un activo de variable denominado *SubscriptionId* contiene Hola identificador de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-324">A variable asset named *SubscriptionId* contains hello ID of hello subscription.</span></span> <span data-ttu-id="fbe49-325">Después de hello `Add-AzureRmAccount` instrucción de cmdlet, hello [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet se ha indicado con el conjunto de parámetros de hello *- Id. de suscripción*.</span><span class="sxs-lookup"><span data-stu-id="fbe49-325">After hello `Add-AzureRmAccount` cmdlet statement, hello [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with hello parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="fbe49-326">Si el nombre de la variable hello es demasiado genérico, puede revisar tooinclude un prefijo o usar otro toomake de convención de nomenclatura sea más fácil tooidentify.</span><span class="sxs-lookup"><span data-stu-id="fbe49-326">If hello variable name is too generic, you can revise it tooinclude a prefix or use another naming convention toomake it easier tooidentify.</span></span> <span data-ttu-id="fbe49-327">O bien, puede usar el conjunto de parámetros de Hola *- SubscriptionName* en lugar de *- Id. de suscripción* a un activo de variable correspondiente.</span><span class="sxs-lookup"><span data-stu-id="fbe49-327">Alternatively, you can use hello parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="fbe49-328">Hola cmdlet que utilice para la autenticación en runbook hello, `Add-AzureRmAccount`, usa hello *ServicePrincipalCertificate* conjunto de parámetros.</span><span class="sxs-lookup"><span data-stu-id="fbe49-328">hello cmdlet that you use for authenticating in hello runbook, `Add-AzureRmAccount`, uses hello *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="fbe49-329">Autentica mediante el certificado de entidad de seguridad de servicio de hello, no las credenciales de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbe49-329">It authenticates by using hello service principal certificate, not hello user credentials.</span></span>

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a><span data-ttu-id="fbe49-330">Tooauthenticate de código de ejemplo con los recursos de administración de servicios</span><span class="sxs-lookup"><span data-stu-id="fbe49-330">Sample code tooauthenticate with Service Management resources</span></span>
<span data-ttu-id="fbe49-331">Puede usar Hola después el código de ejemplo actualizado, que procede de hello *AzureClassicAutomationTutorialScript* runbook de ejemplo, tooauthenticate mediante el uso de hello clásico cuenta de ejecución toomanage recursos clásicos con su runbooks.</span><span class="sxs-lookup"><span data-stu-id="fbe49-331">You can use hello following updated sample code, which is taken from hello *AzureClassicAutomationTutorialScript* example runbook, tooauthenticate by using hello Classic Run As account toomanage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="fbe49-332">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fbe49-332">Next steps</span></span>
* [<span data-ttu-id="fbe49-333">Objetos de aplicación y de entidad de servicio en Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbe49-333">Application and service principal objects in Azure AD</span></span>](../active-directory/active-directory-application-objects.md)
* [<span data-ttu-id="fbe49-334">Control de acceso basado en rol en Azure Automation</span><span class="sxs-lookup"><span data-stu-id="fbe49-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* [<span data-ttu-id="fbe49-335">Introducción a los certificados para Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="fbe49-335">Certificates overview for Azure Cloud Services</span></span>](../cloud-services/cloud-services-certs-create.md)

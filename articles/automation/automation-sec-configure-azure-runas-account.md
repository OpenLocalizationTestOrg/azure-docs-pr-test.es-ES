---
title: "Configuración de una cuenta de ejecución de Azure | Microsoft Docs"
description: "Este tutorial le guía en la creación, la prueba y el ejemplo de uso de la autenticación de la entidad de seguridad en Azure Automation."
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
redirect_document_id: TRUE
ms.openlocfilehash: f88c775eba19bb227d0e206d6420c08b57305b92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="2430b-104">Autenticación de Runbooks con una cuenta de ejecución de Azure</span><span class="sxs-lookup"><span data-stu-id="2430b-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="2430b-105">En este artículo se muestra cómo configurar una cuenta de Azure Automation en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2430b-105">This article shows you how to configure an Azure Automation account in the Azure portal.</span></span> <span data-ttu-id="2430b-106">Para ello, usará la característica de cuentas de ejecución para autenticar runbooks que administran recursos de Azure Resource Manager o Azure Service Management.</span><span class="sxs-lookup"><span data-stu-id="2430b-106">To do so, you use the Run As account feature to authenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="2430b-107">Al crear una cuenta de Automation en el portal de Azure, crea automáticamente dos cuentas:</span><span class="sxs-lookup"><span data-stu-id="2430b-107">When you create an Automation account in the Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="2430b-108">Una cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="2430b-108">A Run As account.</span></span> <span data-ttu-id="2430b-109">Esta cuenta crea una entidad de servicio en Azure Active Directory (Azure AD) y un certificado.</span><span class="sxs-lookup"><span data-stu-id="2430b-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="2430b-110">También asigna el control de acceso basado en rol (RBAC) del colaborador, que administra recursos de Resource Manager mediante runbooks.</span><span class="sxs-lookup"><span data-stu-id="2430b-110">It also assigns the Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="2430b-111">Una cuenta de ejecución clásica.</span><span class="sxs-lookup"><span data-stu-id="2430b-111">A Classic Run As account.</span></span> <span data-ttu-id="2430b-112">Esta cuenta carga un certificado de administración, que se usa para administrar recursos clásicos o de Service Management mediante runbooks.</span><span class="sxs-lookup"><span data-stu-id="2430b-112">This account uploads a management certificate, which is used to manage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="2430b-113">La creación de una cuenta de Automation simplifica el proceso y ayuda a empezar rápidamente a generar e implementar runbooks que respalden sus necesidades de automatización.</span><span class="sxs-lookup"><span data-stu-id="2430b-113">Creating an Automation account simplifies the process for you and helps you quickly start building and deploying runbooks to support your automation needs.</span></span>

<span data-ttu-id="2430b-114">Con una cuenta de ejecución y una cuenta de ejecución clásica puede:</span><span class="sxs-lookup"><span data-stu-id="2430b-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="2430b-115">Proporcionar una forma normalizada de autenticarse en Azure cuando administra recursos de Azure Resource Manager o de Azure Service Management desde runbooks en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2430b-115">Provide a standardized way to authenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in the Azure portal.</span></span>
* <span data-ttu-id="2430b-116">Automatizar el uso de runbooks globales, que puede configurar en Azure Alerts.</span><span class="sxs-lookup"><span data-stu-id="2430b-116">Automate the use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="2430b-117">La [característica de integración de Azure Alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) con Automation Global Runbooks necesita una cuenta de Automation que esté configurada como una cuenta de ejecución y una cuenta de ejecución clásica.</span><span class="sxs-lookup"><span data-stu-id="2430b-117">The [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="2430b-118">Puede seleccionar una cuenta de Automation que tenga una cuenta de ejecución o una cuenta de ejecución clásica ya definida, o bien crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="2430b-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose to create a new Automation account.</span></span>
>  

<span data-ttu-id="2430b-119">En este artículo se muestra cómo crear una cuenta de Automation desde el portal de Azure, actualizarla mediante Azure PowerShell, administrar la configuración de la cuenta y autenticarla en sus runbooks.</span><span class="sxs-lookup"><span data-stu-id="2430b-119">This article shows how to create an Automation account from the Azure portal, update an Automation account by using Azure PowerShell, manage the account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="2430b-120">Antes de empezar a crear una cuenta de Automation, es una buena idea entender y tener en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2430b-120">Before you begin creating an Automation account, it's a good idea to understand and consider the following:</span></span>

* <span data-ttu-id="2430b-121">Crear una cuenta de Automation no afecta a las cuentas de Automation que se podrían haber ya creado en el modelo de implementación clásica o de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2430b-121">Creating an Automation account does not affect Automation accounts you might have already created in either the classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="2430b-122">El proceso funciona únicamente para las cuentas de Automation que se crean en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2430b-122">The process works only for Automation accounts that you create in the Azure portal.</span></span> <span data-ttu-id="2430b-123">El intento de crear una cuenta desde el Portal de Azure clásico no replicará la configuración de la cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="2430b-123">Attempting to create an account from the Azure classic portal does not replicate the Run As account configuration.</span></span>
* <span data-ttu-id="2430b-124">Si ya tiene runbooks y recursos (por ejemplo, variables o programaciones) para administrar recursos clásicos y quiere que los runbooks se autentiquen con la nueva cuenta de ejecución clásica, realice una de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="2430b-124">If you already have runbooks and assets (such as schedules or variables) in place to manage classic resources, and you want runbooks to authenticate with the new Classic Run As account, do either of the following:</span></span>

  * <span data-ttu-id="2430b-125">Para crear una cuenta de ejecución clásica, siga las instrucciones que aparecen en la sección "Administración de la cuenta de ejecución".</span><span class="sxs-lookup"><span data-stu-id="2430b-125">To create a Classic Run As account, follow the instructions in the "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="2430b-126">Para actualizar la cuenta existente, use el script de PowerShell de la sección "Actualización de la cuenta de Automation mediante PowerShell".</span><span class="sxs-lookup"><span data-stu-id="2430b-126">To update your existing account, use the PowerShell script in the "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="2430b-127">Para realizar la autenticación con la nueva cuenta de ejecución y la cuenta de Automation de ejecución clásica, debe modificar los runbooks existentes con código de ejemplo proporcionado en la sección [Código de ejemplo de autenticación](#authentication-code-examples).</span><span class="sxs-lookup"><span data-stu-id="2430b-127">To authenticate by using the new Run As account and Classic Run As Automation account, you  need to modify your existing runbooks with the example code provided in the section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="2430b-128">La cuenta de ejecución se usa para la autenticación con los recursos de Resource Manager mediante la entidad de servicio basada en certificados.</span><span class="sxs-lookup"><span data-stu-id="2430b-128">The Run As account is for authentication against Resource Manager resources using the certificate-based service principal.</span></span> <span data-ttu-id="2430b-129">La cuenta de ejecución clásica se usa para la autenticación con los recursos de Service Management mediante el certificado de administración.</span><span class="sxs-lookup"><span data-stu-id="2430b-129">The Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-the-azure-portal"></a><span data-ttu-id="2430b-130">Creación de una cuenta de Automation desde el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2430b-130">Create an Automation account from the Azure portal</span></span>
<span data-ttu-id="2430b-131">En esta sección, creará una cuenta de Azure Automation desde el portal de Azure, que a su vez crea una cuenta de ejecución y una cuenta de ejecución clásica.</span><span class="sxs-lookup"><span data-stu-id="2430b-131">In this section, you create an Azure Automation account from the Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="2430b-132">Para crear una cuenta de Automation, debe ser miembro del rol Administradores de servicios o coadministrador de la suscripción que concede el acceso a la suscripción.</span><span class="sxs-lookup"><span data-stu-id="2430b-132">To create an Automation account, you must be a member of the Service Admins role or co-administrator of the subscription that is granting access to the subscription.</span></span> <span data-ttu-id="2430b-133">También se le debe agregar como usuario a la instancia predeterminada de Active Directory de esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="2430b-133">You must also be added as a user to that subscription's default Active Directory instance.</span></span> <span data-ttu-id="2430b-134">No es necesario asignar a la cuenta un rol con privilegios.</span><span class="sxs-lookup"><span data-stu-id="2430b-134">The account does not need to be assigned a privileged role.</span></span>
>
><span data-ttu-id="2430b-135">Si no es miembro de la instancia de Active Directory de la suscripción antes de que le agreguen al rol de coadministrador de la suscripción, se le agregará a Active Directory como invitado.</span><span class="sxs-lookup"><span data-stu-id="2430b-135">If you are not a member of the subscription’s Active Directory instance before you are added to the co-administrator role of the subscription, you will be added to Active Directory as a guest.</span></span> <span data-ttu-id="2430b-136">En este caso, recibirá una advertencia "No tiene permisos para crear..."</span><span class="sxs-lookup"><span data-stu-id="2430b-136">In this instance, you will receive a “You do not have permissions to create…”</span></span> <span data-ttu-id="2430b-137">en la hoja **Agregar cuenta de Automation**.</span><span class="sxs-lookup"><span data-stu-id="2430b-137">warning on the **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="2430b-138">Los usuarios que primero se agregaron al rol de coadministrador se pueden quitar de la instancia de Active Directory de la suscripción y volverse a agregar para convertirlos en usuarios completos en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2430b-138">Users who were added to the co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span></span> <span data-ttu-id="2430b-139">Para comprobar esta situación, en el panel de **Azure Active Directory** del portal de Azure, seleccione **Usuarios y grupos**, **Todos los usuarios** y, después de seleccionar el usuario específico, seleccione **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="2430b-139">To verify this situation from the **Azure Active Directory** pane in the Azure portal by selecting **Users and groups**, selecting **All users** and, after you select the specific user, selecting **Profile**.</span></span> <span data-ttu-id="2430b-140">El valor del atributo **Tipo de usuario** del perfil de los usuarios no debería ser **Invitado**.</span><span class="sxs-lookup"><span data-stu-id="2430b-140">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="2430b-141">Inicie sesión en el portal de Azure con una cuenta que sea miembro del rol Administradores de la suscripción y coadministrador de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="2430b-141">Sign in to the Azure portal with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>

2. <span data-ttu-id="2430b-142">Seleccione **Cuentas de Automatización**.</span><span class="sxs-lookup"><span data-stu-id="2430b-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="2430b-143">En la hoja **Cuentas de Automation**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2430b-143">On the **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="2430b-144">Se abre la hoja **Agregar cuenta de Automation**.</span><span class="sxs-lookup"><span data-stu-id="2430b-144">The **Add Automation Account** blade opens.</span></span>

 ![La hoja "Agregar cuenta de Automation"](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="2430b-146">Si la cuenta no es miembro del rol Administradores de la suscripción ni del rol de coadministrador de la suscripción, aparece la siguiente advertencia en la hoja **Agregar cuenta de Automation**:</span><span class="sxs-lookup"><span data-stu-id="2430b-146">If your account is not a member of the subscription administrators role and co-administrator of the subscription, the following warning is displayed on the **Add Automation Account** blade:</span></span>
   >
   >![Advertencia para agregar cuenta de Automatización](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="2430b-148">En la hoja **Agregar cuenta de Automation**, en el cuadro **Nombre**, escriba el nombre de la nueva cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="2430b-148">On the **Add Automation Account** blade, in the **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="2430b-149">Si tiene más de una suscripción, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2430b-149">If you have more than one subscription, do the following:</span></span>

    <span data-ttu-id="2430b-150">a.</span><span class="sxs-lookup"><span data-stu-id="2430b-150">a.</span></span> <span data-ttu-id="2430b-151">En **Suscripción**, especifique una para la nueva cuenta.</span><span class="sxs-lookup"><span data-stu-id="2430b-151">Under **Subscription**, specify one for the new account.</span></span>

    <span data-ttu-id="2430b-152">b.</span><span class="sxs-lookup"><span data-stu-id="2430b-152">b.</span></span> <span data-ttu-id="2430b-153">En **Grupo de recursos**, haga clic en **Create new** (Crear nuevo) o **Use existing** (Usar existente).</span><span class="sxs-lookup"><span data-stu-id="2430b-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="2430b-154">c.</span><span class="sxs-lookup"><span data-stu-id="2430b-154">c.</span></span> <span data-ttu-id="2430b-155">En **Ubicación**, especifique un centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2430b-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="2430b-156">En **Crear cuenta de ejecución de Azure**, seleccione **Sí** y luego haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2430b-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2430b-157">Si decide no crear la cuenta de ejecución, al seleccionar **No** aparecerá un mensaje de advertencia en la hoja **Agregar cuenta de Automation**.</span><span class="sxs-lookup"><span data-stu-id="2430b-157">If you choose not to create the Run As account by selecting **No**, a warning message is displayed the **Add Automation Account** blade.</span></span> <span data-ttu-id="2430b-158">Aunque la cuenta se crea en el portal de Azure, no tiene una identidad de autenticación correspondiente en el servicio de directorio de suscripción clásico o de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2430b-158">Although the account is created in the Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="2430b-159">Por lo tanto, la cuenta no tiene acceso a los recursos de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="2430b-159">Consequently, the account has no access to resources in your subscription.</span></span> <span data-ttu-id="2430b-160">Este escenario evita que los runbooks que hacen referencia a esta cuenta puedan autenticarse y realizar tareas con los recursos en dichos modelos de implementación.</span><span class="sxs-lookup"><span data-stu-id="2430b-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > ![Mensaje de advertencia de la hoja "Agregar cuenta de Automation"](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="2430b-162">Además, dado que no se crea la entidad de servicio, no se asigna el rol de colaborador.</span><span class="sxs-lookup"><span data-stu-id="2430b-162">Additionally, because the service principal is not created, the Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="2430b-163">Mientras Azure crea la cuenta de Automatización, se puede seguir el progreso de **Notificaciones** desde el menú.</span><span class="sxs-lookup"><span data-stu-id="2430b-163">While Azure creates the Automation account, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="resources"></a><span data-ttu-id="2430b-164">Recursos</span><span class="sxs-lookup"><span data-stu-id="2430b-164">Resources</span></span>
<span data-ttu-id="2430b-165">Una vez que se crea la cuenta de Automatización, se también varios recursos automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2430b-165">When the Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="2430b-166">Los recursos se resumen en las dos tablas siguientes:</span><span class="sxs-lookup"><span data-stu-id="2430b-166">The resources are summarized in the following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="2430b-167">Recursos de la cuenta de ejecución</span><span class="sxs-lookup"><span data-stu-id="2430b-167">Run As account resources</span></span>

| <span data-ttu-id="2430b-168">Recurso</span><span class="sxs-lookup"><span data-stu-id="2430b-168">Resource</span></span> | <span data-ttu-id="2430b-169">Descripción</span><span class="sxs-lookup"><span data-stu-id="2430b-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2430b-170">Runbook AzureAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="2430b-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="2430b-171">Un runbook gráfico de ejemplo que muestra cómo realizar la autenticación mediante la cuenta de ejecución y que obtiene todos los recursos de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2430b-171">An example graphical runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="2430b-172">Runbook AzureAutomationTutorialScript</span><span class="sxs-lookup"><span data-stu-id="2430b-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="2430b-173">Un runbook de PowerShell de ejemplo que muestra cómo realizar la autenticación mediante la cuenta de ejecución y que obtiene todos los recursos de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2430b-173">An example PowerShell runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="2430b-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="2430b-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="2430b-175">El recurso de certificado que se crea automáticamente al crear una cuenta de Automation. También puede usar el siguiente script de PowerShell para una cuenta existente.</span><span class="sxs-lookup"><span data-stu-id="2430b-175">The certificate asset that's automatically created when you create an Automation account or use the following PowerShell script for an existing account.</span></span> <span data-ttu-id="2430b-176">El certificado le permite realizar la autenticación en Azure, de modo que puede administrar los recursos de Azure Resource Manager desde los runbooks.</span><span class="sxs-lookup"><span data-stu-id="2430b-176">The certificate allows you to authenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="2430b-177">Este certificado tiene una duración de un año.</span><span class="sxs-lookup"><span data-stu-id="2430b-177">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="2430b-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="2430b-178">AzureRunAsConnection</span></span> | <span data-ttu-id="2430b-179">El recurso de conexión que se crea automáticamente al crear una cuenta de Automation; también puede usar el script de PowerShell para una cuenta existente.</span><span class="sxs-lookup"><span data-stu-id="2430b-179">The connection asset that's automatically created when you create an Automation account or use the PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="2430b-180">Recursos de la cuenta de ejecución clásica</span><span class="sxs-lookup"><span data-stu-id="2430b-180">Classic Run As account resources</span></span>

| <span data-ttu-id="2430b-181">Recurso</span><span class="sxs-lookup"><span data-stu-id="2430b-181">Resource</span></span> | <span data-ttu-id="2430b-182">Descripción</span><span class="sxs-lookup"><span data-stu-id="2430b-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2430b-183">Runbook AzureClassicAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="2430b-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="2430b-184">Un runbook gráfico de ejemplo que obtiene todas las máquinas virtuales que se crean con el modelo de implementación clásica en una suscripción mediante la cuenta de ejecución clásica (certificado) y luego escribe el nombre y el estado de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2430b-184">An example graphical runbook that gets all the VMs that are created using the classic deployment model in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="2430b-185">Runbook AzureClassicAutomationTutorial Script</span><span class="sxs-lookup"><span data-stu-id="2430b-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="2430b-186">Un runbook de PowerShell de ejemplo que obtiene todas las máquinas virtuales clásicas de una suscripción mediante la cuenta de ejecución clásica (certificado) y luego escribe el nombre y el estado de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2430b-186">An example PowerShell runbook that gets all the classic VMs in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="2430b-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="2430b-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="2430b-188">Un recurso de certificado creado automáticamente que se usa para realizar la autenticación en Azure, de modo que pueda administrar los recursos del modelo clásico de Azure mediante runbooks.</span><span class="sxs-lookup"><span data-stu-id="2430b-188">The automatically created certificate asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="2430b-189">Este certificado tiene una duración de un año.</span><span class="sxs-lookup"><span data-stu-id="2430b-189">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="2430b-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="2430b-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="2430b-191">El recurso de conexión creado automáticamente que se usa para realizar la autenticación en Azure, de modo que pueda administrar los recursos del modelo clásico de Azure mediante runbooks.</span><span class="sxs-lookup"><span data-stu-id="2430b-191">The automatically created connection asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="2430b-192">Comprobación de la autenticación de ejecución</span><span class="sxs-lookup"><span data-stu-id="2430b-192">Verify Run As authentication</span></span>
<span data-ttu-id="2430b-193">Realice una pequeña prueba para confirmar que puede autenticarse correctamente mediante la nueva cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="2430b-193">Perform a small test to confirm that you can successfully authenticate by using the new Run As account.</span></span>

1. <span data-ttu-id="2430b-194">En el Portal de Azure, abra la cuenta de Automatización que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2430b-194">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="2430b-195">Haga clic en el icono **Runbooks** para abrir la lista de runbooks.</span><span class="sxs-lookup"><span data-stu-id="2430b-195">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="2430b-196">Seleccione el runbook **AzureAutomationTutorialScript** y haga clic en **Iniciar** para abrirlo.</span><span class="sxs-lookup"><span data-stu-id="2430b-196">Select the **AzureAutomationTutorialScript** runbook, and then click **Start** to start the runbook.</span></span> <span data-ttu-id="2430b-197">Se producen los siguientes eventos:</span><span class="sxs-lookup"><span data-stu-id="2430b-197">The following events occur:</span></span>
 * <span data-ttu-id="2430b-198">Se crea un [trabajo de runbook](automation-runbook-execution.md), se muestra la hoja **Trabajo** y el estado del trabajo aparece en el icono **Resumen del trabajo**.</span><span class="sxs-lookup"><span data-stu-id="2430b-198">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="2430b-199">El estado del trabajo comienza como **En cola**, lo que indica que está esperando a que haya algún trabajo de runbook disponible en la nube.</span><span class="sxs-lookup"><span data-stu-id="2430b-199">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="2430b-200">El estado pasa a ser **Iniciando** cuando un trabajo de runbook solicita el trabajo.</span><span class="sxs-lookup"><span data-stu-id="2430b-200">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="2430b-201">El estado pasa a ser **En ejecución** cuando el runbook comienza a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="2430b-201">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="2430b-202">Cuando el trabajo del runbook ha terminado de ejecutarse, debería ver un estado de **Completado**.</span><span class="sxs-lookup"><span data-stu-id="2430b-202">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="2430b-203">Para ver los resultados detallados del runbook, haga clic en el icono **Salida**.</span><span class="sxs-lookup"><span data-stu-id="2430b-203">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="2430b-204">Aparece la hoja **Salida**, que muestra que ese runbook se ha autenticado correctamente y ha devuelto una lista de todos los recursos disponibles en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2430b-204">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all resources available in the resource group.</span></span>

5. <span data-ttu-id="2430b-205">Cierre la hoja **Salida** para volver a la hoja **Resumen del trabajo**.</span><span class="sxs-lookup"><span data-stu-id="2430b-205">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="2430b-206">Cierre la hoja **Resumen del trabajo** y la hoja del runbook **AzureAutomationTutorialScript** correspondiente.</span><span class="sxs-lookup"><span data-stu-id="2430b-206">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="2430b-207">Comprobación de la autenticación de ejecución de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="2430b-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="2430b-208">Realice una pequeña prueba para confirmar que puede autenticarse correctamente mediante la nueva cuenta de ejecución clásica.</span><span class="sxs-lookup"><span data-stu-id="2430b-208">Perform a similar small test to confirm that you can successfully authenticate by using the new Classic Run As account.</span></span>

1. <span data-ttu-id="2430b-209">En el Portal de Azure, abra la cuenta de Automatización que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2430b-209">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="2430b-210">Haga clic en el icono **Runbooks** para abrir la lista de runbooks.</span><span class="sxs-lookup"><span data-stu-id="2430b-210">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="2430b-211">Seleccione el runbook **AzureClassicAutomationTutorialScript** y haga clic en **Iniciar** para abrirlo.</span><span class="sxs-lookup"><span data-stu-id="2430b-211">Select the **AzureClassicAutomationTutorialScript** runbook, and then click **Start** to  start the runbook.</span></span> <span data-ttu-id="2430b-212">Se producen los siguientes eventos:</span><span class="sxs-lookup"><span data-stu-id="2430b-212">The following events occur:</span></span>

 * <span data-ttu-id="2430b-213">Se crea un [trabajo de runbook](automation-runbook-execution.md), se muestra la hoja **Trabajo** y el estado del trabajo aparece en el icono **Resumen del trabajo**.</span><span class="sxs-lookup"><span data-stu-id="2430b-213">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="2430b-214">El estado del trabajo comienza como **En cola**, lo que indica que está esperando a que haya algún trabajo de runbook disponible en la nube.</span><span class="sxs-lookup"><span data-stu-id="2430b-214">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="2430b-215">El estado pasa a ser **Iniciando** cuando un trabajo de runbook solicita el trabajo.</span><span class="sxs-lookup"><span data-stu-id="2430b-215">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="2430b-216">El estado pasa a ser **En ejecución** cuando el runbook comienza a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="2430b-216">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="2430b-217">Cuando el trabajo del runbook ha terminado de ejecutarse, debería ver un estado de **Completado**.</span><span class="sxs-lookup"><span data-stu-id="2430b-217">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![Prueba de Runbook de entidad de seguridad](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="2430b-219">Para ver los resultados detallados del runbook, haga clic en el icono **Salida**.</span><span class="sxs-lookup"><span data-stu-id="2430b-219">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="2430b-220">Aparece la hoja **Salida**, que muestra que el runbook se ha autenticado correctamente y ha devuelto una lista de todas las máquinas virtuales clásicas de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="2430b-220">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all classic VMs in the subscription.</span></span>

5. <span data-ttu-id="2430b-221">Cierre la hoja **Salida** para volver a la hoja **Resumen del trabajo**.</span><span class="sxs-lookup"><span data-stu-id="2430b-221">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="2430b-222">Cierre la hoja **Resumen del trabajo** y la hoja del runbook **AzureAutomationTutorialScript** correspondiente.</span><span class="sxs-lookup"><span data-stu-id="2430b-222">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="2430b-223">Administración de la cuenta de ejecución</span><span class="sxs-lookup"><span data-stu-id="2430b-223">Managing your Run As account</span></span>
<span data-ttu-id="2430b-224">En algún momento antes de que expire su cuenta de Automation, deberá renovar el certificado.</span><span class="sxs-lookup"><span data-stu-id="2430b-224">At some point before your Automation account expires, you will need to renew the certificate.</span></span> <span data-ttu-id="2430b-225">Si cree que se ha puesto en peligro la cuenta de ejecución, puede eliminarla y volver a crearla.</span><span class="sxs-lookup"><span data-stu-id="2430b-225">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="2430b-226">En esta sección se describe cómo realizar estas operaciones.</span><span class="sxs-lookup"><span data-stu-id="2430b-226">This section discusses how to perform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="2430b-227">Renovación de certificado autofirmado</span><span class="sxs-lookup"><span data-stu-id="2430b-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="2430b-228">El certificado autofirmado que creó para la cuenta de ejecución expira un año a partir de la fecha de creación.</span><span class="sxs-lookup"><span data-stu-id="2430b-228">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="2430b-229">Se puede renovar en cualquier momento antes de que expire.</span><span class="sxs-lookup"><span data-stu-id="2430b-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="2430b-230">Cuando se renueva, el certificado válido actual se conserva para tener la seguridad de que los runbooks que están en cola o que se están ejecutando activamente y que se autentican con la cuenta de ejecución, no resultan afectados negativamente.</span><span class="sxs-lookup"><span data-stu-id="2430b-230">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="2430b-231">El certificado es válido hasta la fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="2430b-231">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="2430b-232">Si ha configurado la cuenta de ejecución de Automation para que use un certificado emitido por una entidad de certificación de empresa y usa esta opción, ese certificado se reemplazará por un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="2430b-232">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="2430b-233">Para renovar el certificado, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2430b-233">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="2430b-234">Abra la cuenta de Automation en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2430b-234">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="2430b-235">En la hoja **Cuenta de Automation**, en el panel **Account properties** (Propiedades de la cuenta), en **Account Settings** (Configuración de la cuenta), seleccione **Run As Accounts** (Cuentas de ejecución).</span><span class="sxs-lookup"><span data-stu-id="2430b-235">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Panel de propiedades de la cuenta de Automation](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="2430b-237">En la hoja de propiedades **Run As Accounts** (Cuentas de ejecución), seleccione la cuenta de ejecución o la cuenta de ejecución clásica para la que quiere renovar el certificado.</span><span class="sxs-lookup"><span data-stu-id="2430b-237">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

4. <span data-ttu-id="2430b-238">En la hoja **Propiedades** de la cuenta seleccionada, haga clic en **Renovar certificado**.</span><span class="sxs-lookup"><span data-stu-id="2430b-238">On the **Properties** blade for the selected account, click **Renew certificate**.</span></span>

    ![Renovación del certificado para una cuenta de ejecución](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="2430b-240">Mientras se está renovando el certificado, puede seguir el progreso desde el menú, en **Notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="2430b-240">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="2430b-241">Eliminación de una cuenta de ejecución o de ejecución clásica</span><span class="sxs-lookup"><span data-stu-id="2430b-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="2430b-242">En esta sección se describe cómo eliminar y volver a crear una cuenta de ejecución o de ejecución clásica.</span><span class="sxs-lookup"><span data-stu-id="2430b-242">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="2430b-243">Al realizar esta acción, la cuenta de Automation se conserva.</span><span class="sxs-lookup"><span data-stu-id="2430b-243">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="2430b-244">Después de eliminar una cuenta de ejecución o de ejecución clásica, puede volver a crearla en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2430b-244">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="2430b-245">Abra la cuenta de Automation en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2430b-245">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="2430b-246">En la hoja **Cuenta de Automation**, en el panel de propiedades de la cuenta, seleccione **Run As Accounts** (Cuentas de ejecución).</span><span class="sxs-lookup"><span data-stu-id="2430b-246">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="2430b-247">En la hoja de propiedades **Run As Accounts** (Cuentas de ejecución), seleccione la cuenta de ejecución o la cuenta de ejecución clásica que quiere eliminar.</span><span class="sxs-lookup"><span data-stu-id="2430b-247">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="2430b-248">A continuación, en la hoja **Propiedades** de la cuenta seleccionada, haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="2430b-248">Then, on the **Properties** blade for the selected account, click **Delete**.</span></span>

 ![Eliminación de una cuenta de ejecución](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="2430b-250">Mientras se está eliminando la cuenta, puede seguir el progreso desde el menú, en **Notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="2430b-250">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

5. <span data-ttu-id="2430b-251">Después de eliminar la cuenta, puede volver a crearla en la hoja de propiedades **Run As Accounts** (Cuentas de ejecución) mediante la selección de la opción de creación **Cuenta de ejecución de Azure**.</span><span class="sxs-lookup"><span data-stu-id="2430b-251">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span></span>

 ![Nueva creación de la cuenta de ejecución de Automation](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="2430b-253">Error de configuración</span><span class="sxs-lookup"><span data-stu-id="2430b-253">Misconfiguration</span></span>
<span data-ttu-id="2430b-254">Puede que alguno de los elementos de configuración necesarios para que la cuenta de ejecución o la cuenta de ejecución clásica funcionen correctamente se haya eliminado o no se haya creado correctamente durante la configuración inicial.</span><span class="sxs-lookup"><span data-stu-id="2430b-254">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="2430b-255">Estos elementos son:</span><span class="sxs-lookup"><span data-stu-id="2430b-255">The items include:</span></span>

* <span data-ttu-id="2430b-256">Recurso de certificado</span><span class="sxs-lookup"><span data-stu-id="2430b-256">Certificate asset</span></span>
* <span data-ttu-id="2430b-257">Recurso de conexión</span><span class="sxs-lookup"><span data-stu-id="2430b-257">Connection asset</span></span>
* <span data-ttu-id="2430b-258">La cuenta de ejecución se ha quitado del rol de colaborador</span><span class="sxs-lookup"><span data-stu-id="2430b-258">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="2430b-259">Entidad de servicio o aplicación en Azure AD</span><span class="sxs-lookup"><span data-stu-id="2430b-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="2430b-260">En los casos anteriores y otros casos de errores de configuración, la cuenta de Automation detecta los cambios y muestra el estado *Incomplete* (Incompleto) en la hoja de propiedades **Run As Accounts** (Cuentas de ejecución) de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="2430b-260">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span></span>

![Estado de configuración incompleta de la cuenta de ejecución](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="2430b-262">Al seleccionar la cuenta de ejecución, el panel **Propiedades** muestra el mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="2430b-262">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

![Mensaje de advertencia de configuración incompleta de la cuenta de ejecución](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="2430b-264">.</span><span class="sxs-lookup"><span data-stu-id="2430b-264">.</span></span>

<span data-ttu-id="2430b-265">Rápidamente puede resolver estos problemas de la cuenta de ejecución con solo eliminarla cuenta y volver a crearla.</span><span class="sxs-lookup"><span data-stu-id="2430b-265">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="2430b-266">Actualización de la cuenta de Automation mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="2430b-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="2430b-267">Puede usar PowerShell para actualizar su cuenta de Automation existente si:</span><span class="sxs-lookup"><span data-stu-id="2430b-267">You can use PowerShell to update your existing Automation account if:</span></span>

* <span data-ttu-id="2430b-268">Crea una cuenta de Automation, pero se rechaza la creación de la cuenta de ejecución.</span><span class="sxs-lookup"><span data-stu-id="2430b-268">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="2430b-269">Ya usa una cuenta de Automation para administrar recursos de Resource Manager y quiere actualizarla para incluir la cuenta de ejecución para la autenticación de runbooks.</span><span class="sxs-lookup"><span data-stu-id="2430b-269">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="2430b-270">Ya usa una cuenta de Automation para administrar recursos del modelo clásico y quiere actualizarla para usar la cuenta de ejecución en lugar de crear una nueva cuenta y migrar los runbooks y recursos a ella.</span><span class="sxs-lookup"><span data-stu-id="2430b-270">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="2430b-271">Quiere crear una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado emitido por una entidad de certificación (CA) de empresa.</span><span class="sxs-lookup"><span data-stu-id="2430b-271">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="2430b-272">Este script tiene los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="2430b-272">The script has the following prerequisites:</span></span>

* <span data-ttu-id="2430b-273">El script solo se puede ejecutar en Windows 10 y Windows Server 2016 con módulos de Azure Resource Manager 2.01 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="2430b-273">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="2430b-274">No se admite en versiones anteriores de Windows.</span><span class="sxs-lookup"><span data-stu-id="2430b-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="2430b-275">Azure PowerShell 1.0 y versiones superiores.</span><span class="sxs-lookup"><span data-stu-id="2430b-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="2430b-276">Para más información sobre la versión 1.0 de PowerShell, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2430b-276">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="2430b-277">Una cuenta de Automation, a la que se hace referencia como el valor de los parámetros *: -AutomationAccountName* y *- ApplicationDisplayName* en el siguiente script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2430b-277">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="2430b-278">Para obtener los valores de *SubscriptionID*, *ResourceGroup* y *AutomationAccountName*, que son parámetros necesarios para los scripts, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2430b-278">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the scripts, do the following:</span></span>
1. <span data-ttu-id="2430b-279">En el portal de Azure, seleccione su cuenta de Automation en la hoja **Cuenta de Automation** y luego seleccione **All settings** (Toda la configuración).</span><span class="sxs-lookup"><span data-stu-id="2430b-279">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="2430b-280">En la hoja **All settings** (Toda la configuración), en **Account Settings** (Configuración de la cuenta), seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="2430b-280">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="2430b-281">Tenga en cuenta los valores de la hoja **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="2430b-281">Note the values on the **Properties** blade.</span></span>

![Hoja "Propiedades" de la cuenta de Automation](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="2430b-283">Creación de un script de PowerShell de una cuenta de ejecución</span><span class="sxs-lookup"><span data-stu-id="2430b-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="2430b-284">Este script de PowerShell incluye compatibilidad con las siguientes configuraciones:</span><span class="sxs-lookup"><span data-stu-id="2430b-284">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="2430b-285">Creación de una cuenta de ejecución mediante un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="2430b-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="2430b-286">Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="2430b-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="2430b-287">Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado de empresa.</span><span class="sxs-lookup"><span data-stu-id="2430b-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="2430b-288">Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado en la nube de Azure Government.</span><span class="sxs-lookup"><span data-stu-id="2430b-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="2430b-289">Dependiendo de la opción de configuración seleccionada, el script crea los siguientes elementos.</span><span class="sxs-lookup"><span data-stu-id="2430b-289">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="2430b-290">**Para cuentas de ejecución:**</span><span class="sxs-lookup"><span data-stu-id="2430b-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="2430b-291">Crea una aplicación de Azure AD que se exporta con la clave pública del certificado autofirmado o de empresa, crea una cuenta de entidad de servicio para esta aplicación en Azure AD y asigna el rol Colaborador para esta cuenta en su suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="2430b-291">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="2430b-292">Puede cambiar esta configuración a Propietario o cualquier otro rol.</span><span class="sxs-lookup"><span data-stu-id="2430b-292">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="2430b-293">Para más información, consulte [Control de acceso basado en rol en Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="2430b-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="2430b-294">Crea un recurso de certificado de Automation llamado *AzureRunAsCertificate* en la cuenta de Automation especificada.</span><span class="sxs-lookup"><span data-stu-id="2430b-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="2430b-295">El recurso de certificado contiene la clave privada del certificado que usa la aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2430b-295">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="2430b-296">Crea un recurso de conexión de Automation llamado *AzureRunAsConnection* en la cuenta de Automation especificada.</span><span class="sxs-lookup"><span data-stu-id="2430b-296">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="2430b-297">El recurso de conexión contiene el id. de aplicación, el id. de inquilino, el id. de suscripción y la huella digital de certificado.</span><span class="sxs-lookup"><span data-stu-id="2430b-297">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="2430b-298">**Para cuentas de ejecución clásicas:**</span><span class="sxs-lookup"><span data-stu-id="2430b-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="2430b-299">Crea un recurso de certificado de Automation llamado *AzureClassicRunAsCertificate* en la cuenta de Automation especificada.</span><span class="sxs-lookup"><span data-stu-id="2430b-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="2430b-300">El recurso de certificado contiene la clave privada del certificado que usa el certificado de administración.</span><span class="sxs-lookup"><span data-stu-id="2430b-300">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="2430b-301">Crea un recurso de conexión de Automation llamado *AzureClassicRunAsConnection* en la cuenta de Automation especificada.</span><span class="sxs-lookup"><span data-stu-id="2430b-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="2430b-302">El recurso de conexión contiene el nombre de la suscripción, el id. de suscripción y el nombre del recurso de certificado.</span><span class="sxs-lookup"><span data-stu-id="2430b-302">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="2430b-303">Si selecciona cualquiera de las opciones para crear una cuenta de ejecución clásica, cargue el certificado público (extensión de nombre del archivo .cer) en el almacén de administración para la suscripción en la que se creó la cuenta de Automation.</span><span class="sxs-lookup"><span data-stu-id="2430b-303">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

<span data-ttu-id="2430b-304">Para ejecutar el script y cargar el certificado, realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2430b-304">To execute the script and upload the certificate, do the following:</span></span>

1. <span data-ttu-id="2430b-305">Guarde el script siguiente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2430b-305">Save the following script on your computer.</span></span> <span data-ttu-id="2430b-306">En este ejemplo, guárdelo con el nombre *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="2430b-306">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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

        # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
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
           Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate the ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
                    "Log in to the Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload the .cer format of #CERT#"

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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate the ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="2430b-307">En el equipo, haga clic en **Inicio** y luego inicie **Windows PowerShell** con derechos de usuario elevados.</span><span class="sxs-lookup"><span data-stu-id="2430b-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="2430b-308">Desde el shell de línea de comandos de PowerShell con privilegios elevados, vaya a la carpeta que contiene el script que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="2430b-308">From the elevated PowerShell command-line shell, go to the folder that contains the script you created in step 1.</span></span>

4. <span data-ttu-id="2430b-309">Ejecute el script mediante los valores de parámetro de la configuración que necesita.</span><span class="sxs-lookup"><span data-stu-id="2430b-309">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="2430b-310">**Creación de una cuenta de ejecución mediante un certificado autofirmado**</span><span class="sxs-lookup"><span data-stu-id="2430b-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="2430b-311">**Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado**</span><span class="sxs-lookup"><span data-stu-id="2430b-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="2430b-312">**Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado de empresa**</span><span class="sxs-lookup"><span data-stu-id="2430b-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="2430b-313">**Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado en la nube de Azure Government**</span><span class="sxs-lookup"><span data-stu-id="2430b-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="2430b-314">Después de ejecutar el script, se le pedirá que se autentique en Azure.</span><span class="sxs-lookup"><span data-stu-id="2430b-314">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="2430b-315">Inicie sesión con una cuenta que sea miembro del rol Administradores de suscripciones y coadministrador de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="2430b-315">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="2430b-316">Una vez que el script se ejecuta correctamente, observe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2430b-316">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="2430b-317">Si creó una cuenta de ejecución clásica con un certificado público autofirmado (formato .cer), el script lo crea y lo guarda en la carpeta de archivos temporales del equipo con el perfil de usuario *%USERPROFILE%\AppData\Local\Temp*, que se usa para ejecutar la sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2430b-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="2430b-318">Si creó una cuenta de identificación clásica con un certificado público de empresa (archivo .cer) , use este certificado.</span><span class="sxs-lookup"><span data-stu-id="2430b-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="2430b-319">Siga las instrucciones para [cargar un certificado de API de administración en el Portal de Azure clásico](../azure-api-management-certs.md) y luego valide la configuración de credenciales con recursos de Service Management mediante el [código de ejemplo para realizar la autenticación con recursos de Service Management](#sample-code-to-authenticate-with-service-management-resources).</span><span class="sxs-lookup"><span data-stu-id="2430b-319">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with Service Management resources by using the [sample code to authenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="2430b-320">Si *no* creó una cuenta de ejecución clásica, realice la autenticación con recursos de Resource Manager y valide la configuración de credenciales mediante el [código de ejemplo para la autenticación con recursos de Service Management](#sample-code-to-authenticate-with-resource-manager-resources).</span><span class="sxs-lookup"><span data-stu-id="2430b-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-to-authenticate-with-resource-manager-resources"></a><span data-ttu-id="2430b-321">Código de ejemplo para autenticarse con recursos de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2430b-321">Sample code to authenticate with Resource Manager resources</span></span>
<span data-ttu-id="2430b-322">Puede usar el código de ejemplo actualizado siguiente, procedente del runbook de ejemplo *AzureAutomationTutorialScript*, para realizar la autenticación con la cuenta de ejecución y administrar los recursos de Resource Manager con sus runbooks.</span><span class="sxs-lookup"><span data-stu-id="2430b-322">You can use the following updated sample code, taken from the *AzureAutomationTutorialScript* example runbook, to authenticate by using the Run As account to manage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get the connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in to Azure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context to a specific subscription"     
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

<span data-ttu-id="2430b-323">Para ayudar a trabajar fácilmente entre varias suscripciones, el script incluye dos líneas adicionales de código que admiten la referencia a un contexto de suscripción.</span><span class="sxs-lookup"><span data-stu-id="2430b-323">To help you to easily work between multiple subscriptions, the script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="2430b-324">Un recurso de variable llamado *SubscriptionId* contiene el id. de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="2430b-324">A variable asset named *SubscriptionId* contains the ID of the subscription.</span></span> <span data-ttu-id="2430b-325">Después de la instrucción del cmdlet `Add-AzureRmAccount`, el cmdlet [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) se declara con el conjunto de parámetros *-SubscriptionId*.</span><span class="sxs-lookup"><span data-stu-id="2430b-325">After the `Add-AzureRmAccount` cmdlet statement, the [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with the parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="2430b-326">Si el nombre de variable es demasiado genérico, puede revisarlo para incluir un prefijo o usar otra convención de nomenclatura para que resulte más fácil de identificar.</span><span class="sxs-lookup"><span data-stu-id="2430b-326">If the variable name is too generic, you can revise it to include a prefix or use another naming convention to make it easier to identify.</span></span> <span data-ttu-id="2430b-327">Como alternativa, puede usar el conjunto de parámetros *-SubscriptionName* en lugar de *-SubscriptionId* con un recurso de variable correspondiente.</span><span class="sxs-lookup"><span data-stu-id="2430b-327">Alternatively, you can use the parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="2430b-328">El cmdlet que usa para la autenticación en el runbook, `Add-AzureRmAccount`, emplea el conjunto de parámetros *ServicePrincipalCertificate*.</span><span class="sxs-lookup"><span data-stu-id="2430b-328">The cmdlet that you use for authenticating in the runbook, `Add-AzureRmAccount`, uses the *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="2430b-329">La autenticación se realiza mediante el certificado de la entidad de servicio, y no con las credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="2430b-329">It authenticates by using the service principal certificate, not the user credentials.</span></span>

## <a name="sample-code-to-authenticate-with-service-management-resources"></a><span data-ttu-id="2430b-330">Código de ejemplo para autenticarse con los recursos de Service Management</span><span class="sxs-lookup"><span data-stu-id="2430b-330">Sample code to authenticate with Service Management resources</span></span>
<span data-ttu-id="2430b-331">Puede usar el código de ejemplo actualizado siguiente, procedente del runbook de ejemplo *AzureClassicAutomationTutorialScript*, para realizar la autenticación mediante la cuenta de ejecución clásica y administrar los recursos del modelo clásico con sus runbooks.</span><span class="sxs-lookup"><span data-stu-id="2430b-331">You can use the following updated sample code, which is taken from the *AzureClassicAutomationTutorialScript* example runbook, to authenticate by using the Classic Run As account to manage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get the connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate to Azure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in the Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting the certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in the Automation account."
    }

    Write-Verbose "Authenticating to Azure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="2430b-332">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2430b-332">Next steps</span></span>
* [<span data-ttu-id="2430b-333">Objetos de aplicación y de entidad de servicio en Azure AD</span><span class="sxs-lookup"><span data-stu-id="2430b-333">Application and service principal objects in Azure AD</span></span>](../active-directory/active-directory-application-objects.md)
* [<span data-ttu-id="2430b-334">Control de acceso basado en rol en Azure Automation</span><span class="sxs-lookup"><span data-stu-id="2430b-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* [<span data-ttu-id="2430b-335">Introducción a los certificados para Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="2430b-335">Certificates overview for Azure Cloud Services</span></span>](../cloud-services/cloud-services-certs-create.md)

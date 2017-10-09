---
title: "aaaCreate identidad de aplicación de portal de Azure | Documentos de Microsoft"
description: "Describe cómo toocreate una nueva aplicación de Azure Active Directory y el servicio principal que se puede utilizar con control de acceso basado en roles de hello en Azure Resource Manager toomanage obtener acceso a tooresources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="c9615-103">Usar portal toocreate una aplicación de Azure Active Directory y la entidad de servicio que puede tener acceso a recursos</span><span class="sxs-lookup"><span data-stu-id="c9615-103">Use portal toocreate an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="c9615-104">Cuando haya una aplicación que necesita tooaccess o modificar recursos, debe configurar una aplicación de Azure Active Directory (AD) y asignar Hola requerido permisos tooit.</span><span class="sxs-lookup"><span data-stu-id="c9615-104">When you have an application that needs tooaccess or modify resources, you must set up an Azure Active Directory (AD) application and assign hello required permissions tooit.</span></span> <span data-ttu-id="c9615-105">Este enfoque es preferible toorunning Hola aplicación bajo sus propias credenciales porque:</span><span class="sxs-lookup"><span data-stu-id="c9615-105">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="c9615-106">Puede asignar permisos de identidad de aplicación de toohello que son diferentes de sus propios permisos.</span><span class="sxs-lookup"><span data-stu-id="c9615-106">You can assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="c9615-107">Normalmente, estos permisos son tooexactly restringido qué aplicación hello necesita toodo.</span><span class="sxs-lookup"><span data-stu-id="c9615-107">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="c9615-108">No tiene credenciales de la aplicación de toochange Hola si cambian sus responsabilidades.</span><span class="sxs-lookup"><span data-stu-id="c9615-108">You do not have toochange hello app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="c9615-109">Puede usar una autenticación de certificado tooautomate al ejecutar un script de instalación desatendida.</span><span class="sxs-lookup"><span data-stu-id="c9615-109">You can use a certificate tooautomate authentication when executing an unattended script.</span></span>

<span data-ttu-id="c9615-110">Este tema muestra cómo tooperform los pasos a través de portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9615-110">This topic shows you how tooperform those steps through hello portal.</span></span> <span data-ttu-id="c9615-111">Se centra en una aplicación de inquilino único donde la aplicación hello es toorun previsto dentro de un único de organización.</span><span class="sxs-lookup"><span data-stu-id="c9615-111">It focuses on a single-tenant application where hello application is intended toorun within only one organization.</span></span> <span data-ttu-id="c9615-112">Normalmente, utiliza aplicaciones de inquilino único para aplicaciones de línea de negocio que se ejecutan dentro de su organización.</span><span class="sxs-lookup"><span data-stu-id="c9615-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="c9615-113">Permisos necesarios</span><span class="sxs-lookup"><span data-stu-id="c9615-113">Required permissions</span></span>
<span data-ttu-id="c9615-114">toocomplete en este tema, debe tener tooregister de permisos suficientes en una aplicación con el inquilino de Azure AD y asignar el rol de tooa de aplicación hello en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9615-114">toocomplete this topic, you must have sufficient permissions tooregister an application with your Azure AD tenant, and assign hello application tooa role in your Azure subscription.</span></span> <span data-ttu-id="c9615-115">Asegurémonos de que tienes Hola permisos adecuados tooperform esos pasos.</span><span class="sxs-lookup"><span data-stu-id="c9615-115">Let's make sure you have hello right permissions tooperform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="c9615-116">Comprobación de los permisos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9615-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="c9615-117">Inicie sesión en tooyour cuenta de Azure a través de hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c9615-117">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c9615-118">Seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9615-118">Select **Azure Active Directory**.</span></span>

     ![seleccionar azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="c9615-120">En su instancia de Azure Active Directory, seleccione **Configuración de usuario**.</span><span class="sxs-lookup"><span data-stu-id="c9615-120">In Azure Active Directory, select **User settings**.</span></span>

     ![seleccionar configuración de usuario](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="c9615-122">Comprobar hello **registros de aplicación** configuración.</span><span class="sxs-lookup"><span data-stu-id="c9615-122">Check hello **App registrations** setting.</span></span> <span data-ttu-id="c9615-123">Si establece demasiado**Sí**, usuarios no administrativos pueden registrar aplicaciones de AD.</span><span class="sxs-lookup"><span data-stu-id="c9615-123">If set too**Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="c9615-124">Este valor significa que cualquier usuario de inquilino de Azure AD Hola puede registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9615-124">This setting means any user in hello Azure AD tenant can register an app.</span></span> <span data-ttu-id="c9615-125">Puede continuar demasiado[permisos de suscripción de Azure compruebe](#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="c9615-125">You can proceed too[Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![ver registros de aplicaciones](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="c9615-127">Si los registros de aplicación Hola configuración se establece demasiado**n**, solo los usuarios administradores pueden registrar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c9615-127">If hello app registrations setting is set too**No**, only admin users can register apps.</span></span> <span data-ttu-id="c9615-128">Debe toocheck si su cuenta es un administrador de inquilinos de Azure AD Hola.</span><span class="sxs-lookup"><span data-stu-id="c9615-128">You need toocheck whether your account is an admin for hello Azure AD tenant.</span></span> <span data-ttu-id="c9615-129">Seleccione **Introducción** y **Buscar un usuario** en Quick tasks (Tareas rápidas).</span><span class="sxs-lookup"><span data-stu-id="c9615-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![encontrar usuario](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="c9615-131">Busque la cuenta y selecciónela cuando la encuentre.</span><span class="sxs-lookup"><span data-stu-id="c9615-131">Search for your account, and select it when you find it.</span></span>

     ![buscar usuario](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="c9615-133">Para la cuenta, seleccione **Directory role** (Rol de directorio).</span><span class="sxs-lookup"><span data-stu-id="c9615-133">For your account, select **Directory role**.</span></span> 

     ![rol de directorio](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="c9615-135">Vea el rol de directorio asignado en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9615-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="c9615-136">Si su cuenta se asigna el rol de usuario de toohello pero hello configuración de registro de aplicación (a través de Hola pasos anteriores) es tooadmin limitado a los usuarios, pida a su administrador tooeither asignar rol Administrador tooan o tooenable usuarios tooregister aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c9615-136">If your account is assigned toohello User role, but hello app registration setting (from hello preceding steps) is limited tooadmin users, ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

     ![rol de vista](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="c9615-138">Comprobación de los permisos de suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="c9615-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="c9615-139">En su suscripción de Azure, su cuenta debe tener `Microsoft.Authorization/*/Write` acceso tooassign un rol de tooa de aplicación de AD.</span><span class="sxs-lookup"><span data-stu-id="c9615-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access tooassign an AD app tooa role.</span></span> <span data-ttu-id="c9615-140">Esta acción se concede a través de hello [propietario](../active-directory/role-based-access-built-in-roles.md#owner) rol o [Administrador de acceso de usuario](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) rol.</span><span class="sxs-lookup"><span data-stu-id="c9615-140">This action is granted through hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="c9615-141">Si su cuenta se asigna toohello **colaborador** rol, no tiene los permisos adecuados.</span><span class="sxs-lookup"><span data-stu-id="c9615-141">If your account is assigned toohello **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="c9615-142">Recibirá un error al tratar de rol de tooa principal de servicio de tooassign Hola.</span><span class="sxs-lookup"><span data-stu-id="c9615-142">You will receive an error when attempting tooassign hello service principal tooa role.</span></span> 

<span data-ttu-id="c9615-143">toocheck sus permisos de suscripción:</span><span class="sxs-lookup"><span data-stu-id="c9615-143">toocheck your subscription permissions:</span></span>

1. <span data-ttu-id="c9615-144">Si no ya desea en su cuenta de Azure AD de hello pasos anteriores, seleccione **Azure Active Directory** en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9615-144">If you are not already looking at your Azure AD account from hello preceding steps, select **Azure Active Directory** from hello left pane.</span></span>

2. <span data-ttu-id="c9615-145">Encuentre la cuenta de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9615-145">Find your Azure AD account.</span></span> <span data-ttu-id="c9615-146">Seleccione **Introducción** y **Buscar un usuario** en Quick tasks (Tareas rápidas).</span><span class="sxs-lookup"><span data-stu-id="c9615-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![encontrar usuario](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="c9615-148">Busque la cuenta y selecciónela cuando la encuentre.</span><span class="sxs-lookup"><span data-stu-id="c9615-148">Search for your account, and select it when you find it.</span></span>

     ![buscar usuario](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="c9615-150">Seleccione **Azure resources** (Recursos de Azure).</span><span class="sxs-lookup"><span data-stu-id="c9615-150">Select **Azure resources**.</span></span>

     ![seleccionar recursos](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="c9615-152">Ver los roles asignados y determine si tiene los permisos adecuados tooassign un rol de tooa de aplicación de AD.</span><span class="sxs-lookup"><span data-stu-id="c9615-152">View your assigned roles, and determine if you have adequate permissions tooassign an AD app tooa role.</span></span> <span data-ttu-id="c9615-153">Si no es así, pida su tooadd de administrador de suscripción rol Administrador de acceso tooUser.</span><span class="sxs-lookup"><span data-stu-id="c9615-153">If not, ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span> <span data-ttu-id="c9615-154">Hola después de la imagen, usuario de hello es rol de propietario de toohello asignado para las dos suscripciones, lo que significa que el usuario tiene los permisos adecuados.</span><span class="sxs-lookup"><span data-stu-id="c9615-154">In hello following image, hello user is assigned toohello Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![mostrar permisos](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="c9615-156">Creación de una aplicación de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9615-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="c9615-157">Inicie sesión en tooyour cuenta de Azure a través de hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c9615-157">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c9615-158">Seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9615-158">Select **Azure Active Directory**.</span></span>

     ![seleccionar azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="c9615-160">Seleccione **App registrations** (Registros de aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="c9615-160">Select **App registrations**.</span></span>   

     ![seleccionar registros de aplicaciones](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="c9615-162">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c9615-162">Select **Add**.</span></span>

     ![agregar aplicación](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="c9615-164">Proporcione un nombre y la dirección URL para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c9615-164">Provide a name and URL for hello application.</span></span> <span data-ttu-id="c9615-165">Seleccione **aplicación Web / API** o **nativo** para el tipo de saludo de aplicación desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="c9615-165">Select either **Web app / API** or **Native** for hello type of application you want toocreate.</span></span> <span data-ttu-id="c9615-166">Después de establecer valores de hello, seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="c9615-166">After setting hello values, select **Create**.</span></span>

     ![aplicación de nombre](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="c9615-168">Ha creado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9615-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="c9615-169">Obtención del id. y la clave de autenticación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c9615-169">Get application ID and authentication key</span></span>
<span data-ttu-id="c9615-170">Al iniciar sesión mediante programación, se necesita Id. de hello para la aplicación y una clave de autenticación.</span><span class="sxs-lookup"><span data-stu-id="c9615-170">When programmatically logging in, you need hello ID for your application and an authentication key.</span></span> <span data-ttu-id="c9615-171">tooget los valores, Hola uso pasos:</span><span class="sxs-lookup"><span data-stu-id="c9615-171">tooget those values, use hello following steps:</span></span>

1. <span data-ttu-id="c9615-172">En **Registros de aplicaciones**, en Azure Active Directory, seleccione su aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9615-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![seleccionar aplicación](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="c9615-174">Hola copia **Id. de aplicación** y almacenarlo en el código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9615-174">Copy hello **Application ID** and store it in your application code.</span></span> <span data-ttu-id="c9615-175">Hola aplicaciones Hola [aplicaciones de ejemplo](#sample-applications) sección hacen referencia a valor toothis como identificador de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9615-175">hello applications in hello [sample applications](#sample-applications) section refer toothis value as hello client id.</span></span>

     ![ID. DE CLIENTE](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="c9615-177">toogenerate una clave de autenticación, seleccione **claves**.</span><span class="sxs-lookup"><span data-stu-id="c9615-177">toogenerate an authentication key, select **Keys**.</span></span>

     ![seleccionar claves](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="c9615-179">Proporcione una descripción de clave de hello y una duración para la clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9615-179">Provide a description of hello key, and a duration for hello key.</span></span> <span data-ttu-id="c9615-180">Cuando haya terminado, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c9615-180">When done, select **Save**.</span></span>

     ![guardar clave](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="c9615-182">Después de guardar la clave de hello, se muestra el valor de Hola de clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9615-182">After saving hello key, hello value of hello key is displayed.</span></span> <span data-ttu-id="c9615-183">Copie este valor porque no es capaz de tooretrieve clave de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="c9615-183">Copy this value because you are not able tooretrieve hello key later.</span></span> <span data-ttu-id="c9615-184">Proporcionar valor de clave de hello con toolog de Id. de aplicación hello en como aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c9615-184">You provide hello key value with hello application ID toolog in as hello application.</span></span> <span data-ttu-id="c9615-185">Almacene el valor de clave de Hola donde la aplicación pueda recuperarlos.</span><span class="sxs-lookup"><span data-stu-id="c9615-185">Store hello key value where your application can retrieve it.</span></span>

     ![clave guardada](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="c9615-187">Obtención del identificador de inquilino</span><span class="sxs-lookup"><span data-stu-id="c9615-187">Get tenant ID</span></span>
<span data-ttu-id="c9615-188">Al iniciar sesión mediante programación, deberá Id. de inquilino de hello toopass con su solicitud de autenticación.</span><span class="sxs-lookup"><span data-stu-id="c9615-188">When programmatically logging in, you need toopass hello tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="c9615-189">Id. de inquilino de hello tooget, seleccione **propiedades** para su inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9615-189">tooget hello tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![Selección de las propiedades de Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="c9615-191">Hola copia **Id. de directorio**.</span><span class="sxs-lookup"><span data-stu-id="c9615-191">Copy hello **Directory ID**.</span></span> <span data-ttu-id="c9615-192">Este valor es el id. de inquilino.</span><span class="sxs-lookup"><span data-stu-id="c9615-192">This value is your tenant ID.</span></span>

     ![id. de inquilino](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a><span data-ttu-id="c9615-194">Asignar toorole de aplicación</span><span class="sxs-lookup"><span data-stu-id="c9615-194">Assign application toorole</span></span>
<span data-ttu-id="c9615-195">tooaccess recursos de la suscripción, debe asignar el rol de tooa de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="c9615-195">tooaccess resources in your subscription, you must assign hello application tooa role.</span></span> <span data-ttu-id="c9615-196">Decidir qué rol representa permisos adecuados de hello para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c9615-196">Decide which role represents hello right permissions for hello application.</span></span> <span data-ttu-id="c9615-197">toolearn sobre los roles disponibles de hello, consulte [RBAC: integrada en Roles](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="c9615-197">toolearn about hello available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="c9615-198">Puede establecer el ámbito de hello en nivel de Hola de suscripción de hello, el grupo de recursos o el recurso.</span><span class="sxs-lookup"><span data-stu-id="c9615-198">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="c9615-199">Los permisos son heredados toolower niveles de ámbito.</span><span class="sxs-lookup"><span data-stu-id="c9615-199">Permissions are inherited toolower levels of scope.</span></span> <span data-ttu-id="c9615-200">Por ejemplo, agregar que un rol de lector de toohello de aplicación para un grupo de recursos indica que puede leer el grupo de recursos de Hola y los recursos que contenga.</span><span class="sxs-lookup"><span data-stu-id="c9615-200">For example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains.</span></span>

1. <span data-ttu-id="c9615-201">Navegue toohello nivel de ámbito que se va tooassign aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="c9615-201">Navigate toohello level of scope you wish tooassign hello application to.</span></span> <span data-ttu-id="c9615-202">Por ejemplo, tooassign un rol en el ámbito de la suscripción de hello, seleccione **suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="c9615-202">For example, tooassign a role at hello subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="c9615-203">También puede seleccionar un grupo de recursos o un recurso.</span><span class="sxs-lookup"><span data-stu-id="c9615-203">You could instead select a resource group or resource.</span></span>

     ![seleccionar suscripción](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="c9615-205">Seleccionar Hola suscripción en particular (grupo de recursos o recursos) tooassign Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9615-205">Select hello particular subscription (resource group or resource) tooassign hello application to.</span></span>

     ![seleccionar suscripción para la asignación](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="c9615-207">Seleccione **Access Control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="c9615-207">Select **Access Control (IAM)**.</span></span>

     ![seleccionar acceso](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="c9615-209">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c9615-209">Select **Add**.</span></span>

     ![seleccionar agregar](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="c9615-211">Seleccione rol Hola desea tooassign toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9615-211">Select hello role you wish tooassign toohello application.</span></span> <span data-ttu-id="c9615-212">Hello siguiente imagen muestra hello **lector** rol.</span><span class="sxs-lookup"><span data-stu-id="c9615-212">hello following image shows hello **Reader** role.</span></span>

     ![seleccionar rol](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="c9615-214">Busque la aplicación y selecciónela.</span><span class="sxs-lookup"><span data-stu-id="c9615-214">Search for your application, and select it.</span></span>

     ![buscar aplicación](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="c9615-216">Seleccione **Aceptar** toofinish asignación de rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9615-216">Select **OK** toofinish assigning hello role.</span></span> <span data-ttu-id="c9615-217">Verá que su aplicación en la lista de Hola de los usuarios asignados a roles tooa para ese ámbito.</span><span class="sxs-lookup"><span data-stu-id="c9615-217">You see your application in hello list of users assigned tooa role for that scope.</span></span>

## <a name="log-in-as-hello-application"></a><span data-ttu-id="c9615-218">Inicie sesión como aplicación hello</span><span class="sxs-lookup"><span data-stu-id="c9615-218">Log in as hello application</span></span>

<span data-ttu-id="c9615-219">La aplicación está ahora configurada en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c9615-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="c9615-220">Tiene un Id. y clave toouse para iniciar sesión como aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c9615-220">You have an ID and key toouse for signing in as hello application.</span></span> <span data-ttu-id="c9615-221">aplicación Hello se asigna el rol de tooa que le da algunas acciones que puede realizar.</span><span class="sxs-lookup"><span data-stu-id="c9615-221">hello application is assigned tooa role that gives it certain actions it can perform.</span></span> <span data-ttu-id="c9615-222">Para obtener información sobre cómo iniciar sesión como aplicación Hola a través de distintas plataformas, vea:</span><span class="sxs-lookup"><span data-stu-id="c9615-222">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="c9615-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9615-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="c9615-224">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c9615-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="c9615-225">REST</span><span class="sxs-lookup"><span data-stu-id="c9615-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="c9615-226">.NET</span><span class="sxs-lookup"><span data-stu-id="c9615-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="c9615-227">Java</span><span class="sxs-lookup"><span data-stu-id="c9615-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="c9615-228">Node.js</span><span class="sxs-lookup"><span data-stu-id="c9615-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="c9615-229">Python</span><span class="sxs-lookup"><span data-stu-id="c9615-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="c9615-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="c9615-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="c9615-231">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9615-231">Next steps</span></span>
* <span data-ttu-id="c9615-232">tooset de una aplicación de varios inquilinos, consulte [tooauthorization de guía del desarrollador con hello API de Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c9615-232">tooset up a multi-tenant application, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="c9615-233">toolearn acerca de cómo especificar directivas de seguridad, consulte [el Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c9615-233">toolearn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="c9615-234">Para obtener una lista de las acciones disponibles que puede otorgar o denegar toousers, consulte [las operaciones de proveedor de recursos del Administrador de recursos de Azure](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="c9615-234">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

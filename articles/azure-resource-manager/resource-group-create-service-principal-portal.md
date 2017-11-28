---
title: "Creación de la identidad de la aplicación de Azure en el portal | Microsoft Docs"
description: "Describe cómo crear una nueva aplicación de Azure Active Directory y una entidad de servicio que puede utilizarse con el control de acceso basado en rol en Azure Resource Manager para administrar el acceso a los recursos."
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
ms.openlocfilehash: 5d24fb99e1095d53e5ea547e53b80178d9cb77c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-portal-to-create-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="3e319-103">Uso del portal para crear una aplicación de Azure Active Directory y una entidad de servicio con acceso a los recursos</span><span class="sxs-lookup"><span data-stu-id="3e319-103">Use portal to create an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="3e319-104">Si tiene una aplicación que necesita tener acceso a ciertos recursos o modificarlos, puede configurar una aplicación de Azure Active Directory (AD) y asignarle los permisos requeridos.</span><span class="sxs-lookup"><span data-stu-id="3e319-104">When you have an application that needs to access or modify resources, you must set up an Azure Active Directory (AD) application and assign the required permissions to it.</span></span> <span data-ttu-id="3e319-105">Este enfoque es preferible a ejecutar la aplicación con sus propias credenciales por los siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="3e319-105">This approach is preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="3e319-106">Puede asignar permisos a la identidad de aplicación que sean diferentes a los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="3e319-106">You can assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="3e319-107">Normalmente, estos permisos están restringidos a exactamente aquello que la aplicación debe hacer.</span><span class="sxs-lookup"><span data-stu-id="3e319-107">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="3e319-108">No es necesario cambiar las credenciales de la aplicación si las responsabilidades cambian.</span><span class="sxs-lookup"><span data-stu-id="3e319-108">You do not have to change the app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="3e319-109">Puede usar un certificado para automatizar la autenticación al ejecutar un script desatendido.</span><span class="sxs-lookup"><span data-stu-id="3e319-109">You can use a certificate to automate authentication when executing an unattended script.</span></span>

<span data-ttu-id="3e319-110">En este tema se muestra cómo realizar tales pasos a través del portal.</span><span class="sxs-lookup"><span data-stu-id="3e319-110">This topic shows you how to perform those steps through the portal.</span></span> <span data-ttu-id="3e319-111">Se centra en una aplicación de un único inquilino donde la aplicación está diseñada para ejecutarse en una sola organización.</span><span class="sxs-lookup"><span data-stu-id="3e319-111">It focuses on a single-tenant application where the application is intended to run within only one organization.</span></span> <span data-ttu-id="3e319-112">Normalmente, utiliza aplicaciones de inquilino único para aplicaciones de línea de negocio que se ejecutan dentro de su organización.</span><span class="sxs-lookup"><span data-stu-id="3e319-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="3e319-113">Permisos necesarios</span><span class="sxs-lookup"><span data-stu-id="3e319-113">Required permissions</span></span>
<span data-ttu-id="3e319-114">Para completar este tema, debe tener permisos suficientes para registrar una aplicación en su inquilino de Azure AD y asignar la aplicación a un rol en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e319-114">To complete this topic, you must have sufficient permissions to register an application with your Azure AD tenant, and assign the application to a role in your Azure subscription.</span></span> <span data-ttu-id="3e319-115">Vamos a asegurarnos de que tiene los permisos adecuados para realizar esos pasos.</span><span class="sxs-lookup"><span data-stu-id="3e319-115">Let's make sure you have the right permissions to perform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="3e319-116">Comprobación de los permisos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e319-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="3e319-117">Inicie sesión en su cuenta de Azure mediante [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3e319-117">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3e319-118">Seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3e319-118">Select **Azure Active Directory**.</span></span>

     ![seleccionar azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="3e319-120">En su instancia de Azure Active Directory, seleccione **Configuración de usuario**.</span><span class="sxs-lookup"><span data-stu-id="3e319-120">In Azure Active Directory, select **User settings**.</span></span>

     ![seleccionar configuración de usuario](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="3e319-122">Compruebe la configuración de **App registrations** (Registros de aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="3e319-122">Check the **App registrations** setting.</span></span> <span data-ttu-id="3e319-123">Si está establecida en **Sí**, los usuarios que no sean administradores pueden registrar aplicaciones de AD.</span><span class="sxs-lookup"><span data-stu-id="3e319-123">If set to **Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="3e319-124">Esta configuración significa que ningún usuario en el inquilino de Azure Active Directory puede registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e319-124">This setting means any user in the Azure AD tenant can register an app.</span></span> <span data-ttu-id="3e319-125">Puede continuar con [Check Azure subscription permissions](#check-azure-subscription-permissions) (Comprobar permisos de suscripción de Azure).</span><span class="sxs-lookup"><span data-stu-id="3e319-125">You can proceed to [Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![ver registros de aplicaciones](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="3e319-127">Si la configuración de registros de aplicaciones está establecida en **No**, solo los usuarios administradores pueden registrar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3e319-127">If the app registrations setting is set to **No**, only admin users can register apps.</span></span> <span data-ttu-id="3e319-128">Debe comprobar si la cuenta es un administrador del inquilino de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3e319-128">You need to check whether your account is an admin for the Azure AD tenant.</span></span> <span data-ttu-id="3e319-129">Seleccione **Introducción** y **Buscar un usuario** en Quick tasks (Tareas rápidas).</span><span class="sxs-lookup"><span data-stu-id="3e319-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![encontrar usuario](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="3e319-131">Busque la cuenta y selecciónela cuando la encuentre.</span><span class="sxs-lookup"><span data-stu-id="3e319-131">Search for your account, and select it when you find it.</span></span>

     ![buscar usuario](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="3e319-133">Para la cuenta, seleccione **Directory role** (Rol de directorio).</span><span class="sxs-lookup"><span data-stu-id="3e319-133">For your account, select **Directory role**.</span></span> 

     ![rol de directorio](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="3e319-135">Vea el rol de directorio asignado en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e319-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="3e319-136">Si su cuenta está asignada al rol Usuario pero la configuración del registro de aplicaciones (de los pasos anteriores) está limitada a los usuarios administradores, pida a su administrador que le asigne un rol de administrador o que permita a los usuarios registrar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3e319-136">If your account is assigned to the User role, but the app registration setting (from the preceding steps) is limited to admin users, ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

     ![rol de vista](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="3e319-138">Comprobación de los permisos de suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="3e319-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="3e319-139">En su suscripción de Azure, su cuenta debe tener acceso a `Microsoft.Authorization/*/Write` para asignar una aplicación de AD a un rol.</span><span class="sxs-lookup"><span data-stu-id="3e319-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access to assign an AD app to a role.</span></span> <span data-ttu-id="3e319-140">Esta acción se concede mediante el rol [Propietario](../active-directory/role-based-access-built-in-roles.md#owner) o el rol [Administrador de acceso de usuario](../active-directory/role-based-access-built-in-roles.md#user-access-administrator).</span><span class="sxs-lookup"><span data-stu-id="3e319-140">This action is granted through the [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="3e319-141">Si su cuenta está asignada al rol **Colaborador**, no tiene los permisos adecuados.</span><span class="sxs-lookup"><span data-stu-id="3e319-141">If your account is assigned to the **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="3e319-142">Al intentar asignar la entidad de servicio a un rol, se muestra un error.</span><span class="sxs-lookup"><span data-stu-id="3e319-142">You will receive an error when attempting to assign the service principal to a role.</span></span> 

<span data-ttu-id="3e319-143">Para comprobar los permisos de su suscripción:</span><span class="sxs-lookup"><span data-stu-id="3e319-143">To check your subscription permissions:</span></span>

1. <span data-ttu-id="3e319-144">Si los pasos anteriores no le han llevado a su cuenta de Azure AD, seleccione **Azure Active Directory** en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="3e319-144">If you are not already looking at your Azure AD account from the preceding steps, select **Azure Active Directory** from the left pane.</span></span>

2. <span data-ttu-id="3e319-145">Encuentre la cuenta de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e319-145">Find your Azure AD account.</span></span> <span data-ttu-id="3e319-146">Seleccione **Introducción** y **Buscar un usuario** en Quick tasks (Tareas rápidas).</span><span class="sxs-lookup"><span data-stu-id="3e319-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![encontrar usuario](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="3e319-148">Busque la cuenta y selecciónela cuando la encuentre.</span><span class="sxs-lookup"><span data-stu-id="3e319-148">Search for your account, and select it when you find it.</span></span>

     ![buscar usuario](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="3e319-150">Seleccione **Azure resources** (Recursos de Azure).</span><span class="sxs-lookup"><span data-stu-id="3e319-150">Select **Azure resources**.</span></span>

     ![seleccionar recursos](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="3e319-152">Vea los roles asignados y determine si tiene los permisos adecuados para asignar una aplicación de AD a un rol.</span><span class="sxs-lookup"><span data-stu-id="3e319-152">View your assigned roles, and determine if you have adequate permissions to assign an AD app to a role.</span></span> <span data-ttu-id="3e319-153">En caso contrario, pida al administrador de suscripciones que le agregue al rol Administrador de acceso de usuario.</span><span class="sxs-lookup"><span data-stu-id="3e319-153">If not, ask your subscription administrator to add you to User Access Administrator role.</span></span> <span data-ttu-id="3e319-154">En la siguiente imagen, el usuario está asignado al rol Propietario en dos suscripciones, lo que significa que el usuario tiene los permisos adecuados.</span><span class="sxs-lookup"><span data-stu-id="3e319-154">In the following image, the user is assigned to the Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![mostrar permisos](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="3e319-156">Creación de una aplicación de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e319-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="3e319-157">Inicie sesión en su cuenta de Azure mediante [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3e319-157">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3e319-158">Seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3e319-158">Select **Azure Active Directory**.</span></span>

     ![seleccionar azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="3e319-160">Seleccione **App registrations** (Registros de aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="3e319-160">Select **App registrations**.</span></span>   

     ![seleccionar registros de aplicaciones](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="3e319-162">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3e319-162">Select **Add**.</span></span>

     ![agregar aplicación](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="3e319-164">Proporcione un nombre y una dirección URL para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e319-164">Provide a name and URL for the application.</span></span> <span data-ttu-id="3e319-165">Seleccione either **Web app / API** (Aplicación web/API) o **Nativa** para el tipo de aplicación que quiere crear.</span><span class="sxs-lookup"><span data-stu-id="3e319-165">Select either **Web app / API** or **Native** for the type of application you want to create.</span></span> <span data-ttu-id="3e319-166">Después de configurar los valores, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3e319-166">After setting the values, select **Create**.</span></span>

     ![aplicación de nombre](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="3e319-168">Ha creado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e319-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="3e319-169">Obtención del id. y la clave de autenticación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3e319-169">Get application ID and authentication key</span></span>
<span data-ttu-id="3e319-170">Al iniciar sesión mediante programación, necesitará el identificador de la aplicación y una clave de autenticación.</span><span class="sxs-lookup"><span data-stu-id="3e319-170">When programmatically logging in, you need the ID for your application and an authentication key.</span></span> <span data-ttu-id="3e319-171">Para obtener estos valores, use los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3e319-171">To get those values, use the following steps:</span></span>

1. <span data-ttu-id="3e319-172">En **Registros de aplicaciones**, en Azure Active Directory, seleccione su aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e319-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![seleccionar aplicación](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="3e319-174">Copie el **id. de aplicación** y almacénelo en el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e319-174">Copy the **Application ID** and store it in your application code.</span></span> <span data-ttu-id="3e319-175">Las aplicaciones de la sección de [aplicaciones de ejemplo](#sample-applications) hacen referencia a este valor como el id. de cliente.</span><span class="sxs-lookup"><span data-stu-id="3e319-175">The applications in the [sample applications](#sample-applications) section refer to this value as the client id.</span></span>

     ![ID. DE CLIENTE](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="3e319-177">Para generar una clave de autenticación, seleccione **Claves**.</span><span class="sxs-lookup"><span data-stu-id="3e319-177">To generate an authentication key, select **Keys**.</span></span>

     ![seleccionar claves](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="3e319-179">Proporcione una descripción de la clave y una duración.</span><span class="sxs-lookup"><span data-stu-id="3e319-179">Provide a description of the key, and a duration for the key.</span></span> <span data-ttu-id="3e319-180">Cuando haya terminado, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3e319-180">When done, select **Save**.</span></span>

     ![guardar clave](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="3e319-182">Después de guardar la clave, se muestra el valor de la clave.</span><span class="sxs-lookup"><span data-stu-id="3e319-182">After saving the key, the value of the key is displayed.</span></span> <span data-ttu-id="3e319-183">Copie este valor porque no podrá recuperarlo más adelante.</span><span class="sxs-lookup"><span data-stu-id="3e319-183">Copy this value because you are not able to retrieve the key later.</span></span> <span data-ttu-id="3e319-184">Proporcione el valor de clave junto con el id. de aplicación para iniciar sesión con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e319-184">You provide the key value with the application ID to log in as the application.</span></span> <span data-ttu-id="3e319-185">Guarde el valor de clave donde la aplicación pueda recuperarlo.</span><span class="sxs-lookup"><span data-stu-id="3e319-185">Store the key value where your application can retrieve it.</span></span>

     ![clave guardada](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="3e319-187">Obtención del identificador de inquilino</span><span class="sxs-lookup"><span data-stu-id="3e319-187">Get tenant ID</span></span>
<span data-ttu-id="3e319-188">Al iniciar sesión mediante programación, deberá pasar el id. de inquilino con la solicitud de autenticación.</span><span class="sxs-lookup"><span data-stu-id="3e319-188">When programmatically logging in, you need to pass the tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="3e319-189">Para obtener el identificador de inquilino, seleccione **Propiedades** en el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e319-189">To get the tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![Selección de las propiedades de Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="3e319-191">Copie el **id. de directorio**.</span><span class="sxs-lookup"><span data-stu-id="3e319-191">Copy the **Directory ID**.</span></span> <span data-ttu-id="3e319-192">Este valor es el id. de inquilino.</span><span class="sxs-lookup"><span data-stu-id="3e319-192">This value is your tenant ID.</span></span>

     ![id. de inquilino](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-to-role"></a><span data-ttu-id="3e319-194">Asignación de aplicación a un rol</span><span class="sxs-lookup"><span data-stu-id="3e319-194">Assign application to role</span></span>
<span data-ttu-id="3e319-195">Para acceder a los recursos de la suscripción, debe asignarle a la aplicación un rol.</span><span class="sxs-lookup"><span data-stu-id="3e319-195">To access resources in your subscription, you must assign the application to a role.</span></span> <span data-ttu-id="3e319-196">Decida qué rol representa los permisos adecuados para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e319-196">Decide which role represents the right permissions for the application.</span></span> <span data-ttu-id="3e319-197">Para obtener más información sobre los roles disponibles, vea [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="3e319-197">To learn about the available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="3e319-198">Puede establecer el ámbito en el nivel de suscripción, grupo de recursos o recurso.</span><span class="sxs-lookup"><span data-stu-id="3e319-198">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="3e319-199">Los permisos se heredan en los niveles inferiores del ámbito.</span><span class="sxs-lookup"><span data-stu-id="3e319-199">Permissions are inherited to lower levels of scope.</span></span> <span data-ttu-id="3e319-200">Por ejemplo, el hecho de agregar una aplicación al rol Lector para un grupo de recursos significa que esta puede leer el grupo de recursos y los recursos que contenga.</span><span class="sxs-lookup"><span data-stu-id="3e319-200">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span></span>

1. <span data-ttu-id="3e319-201">Desplácese hasta el nivel de ámbito al que desea asignar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e319-201">Navigate to the level of scope you wish to assign the application to.</span></span> <span data-ttu-id="3e319-202">Por ejemplo, para asignar un rol en el ámbito de suscripción, seleccione **Suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="3e319-202">For example, to assign a role at the subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="3e319-203">También puede seleccionar un grupo de recursos o un recurso.</span><span class="sxs-lookup"><span data-stu-id="3e319-203">You could instead select a resource group or resource.</span></span>

     ![seleccionar suscripción](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="3e319-205">Seleccione la suscripción específica (grupo de recursos o recurso) a la que quiere asignar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e319-205">Select the particular subscription (resource group or resource) to assign the application to.</span></span>

     ![seleccionar suscripción para la asignación](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="3e319-207">Seleccione **Access Control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="3e319-207">Select **Access Control (IAM)**.</span></span>

     ![seleccionar acceso](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="3e319-209">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3e319-209">Select **Add**.</span></span>

     ![seleccionar agregar](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="3e319-211">Seleccione el rol que quiere asignar a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e319-211">Select the role you wish to assign to the application.</span></span> <span data-ttu-id="3e319-212">En la imagen siguiente se muestra el rol **Lector**.</span><span class="sxs-lookup"><span data-stu-id="3e319-212">The following image shows the **Reader** role.</span></span>

     ![seleccionar rol](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="3e319-214">Busque la aplicación y selecciónela.</span><span class="sxs-lookup"><span data-stu-id="3e319-214">Search for your application, and select it.</span></span>

     ![buscar aplicación](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="3e319-216">Seleccione **Aceptar** para finalizar la asignación del rol.</span><span class="sxs-lookup"><span data-stu-id="3e319-216">Select **OK** to finish assigning the role.</span></span> <span data-ttu-id="3e319-217">Verá la aplicación en la lista de usuarios asignados a un rol para ese ámbito.</span><span class="sxs-lookup"><span data-stu-id="3e319-217">You see your application in the list of users assigned to a role for that scope.</span></span>

## <a name="log-in-as-the-application"></a><span data-ttu-id="3e319-218">Inicio de sesión con la aplicación</span><span class="sxs-lookup"><span data-stu-id="3e319-218">Log in as the application</span></span>

<span data-ttu-id="3e319-219">La aplicación está ahora configurada en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3e319-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="3e319-220">Tiene un id. y una clave para usar en el inicio de sesión con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3e319-220">You have an ID and key to use for signing in as the application.</span></span> <span data-ttu-id="3e319-221">A la aplicación se le asigna un rol que le proporciona determinadas acciones que puede realizar.</span><span class="sxs-lookup"><span data-stu-id="3e319-221">The application is assigned to a role that gives it certain actions it can perform.</span></span> <span data-ttu-id="3e319-222">Para información sobre el inicio de sesión como en la aplicación a través de distintas plataformas, consulte:</span><span class="sxs-lookup"><span data-stu-id="3e319-222">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="3e319-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e319-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="3e319-224">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="3e319-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="3e319-225">REST</span><span class="sxs-lookup"><span data-stu-id="3e319-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="3e319-226">.NET</span><span class="sxs-lookup"><span data-stu-id="3e319-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="3e319-227">Java</span><span class="sxs-lookup"><span data-stu-id="3e319-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="3e319-228">Node.js</span><span class="sxs-lookup"><span data-stu-id="3e319-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="3e319-229">Python</span><span class="sxs-lookup"><span data-stu-id="3e319-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="3e319-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="3e319-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="3e319-231">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3e319-231">Next steps</span></span>
* <span data-ttu-id="3e319-232">Para configurar una aplicación multiinquilino, consulte [Guía del desarrollador para la autorización con la API de Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3e319-232">To set up a multi-tenant application, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="3e319-233">Para obtener información sobre cómo especificar directivas de seguridad, consulte [Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="3e319-233">To learn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="3e319-234">Para obtener una lista de las acciones que puede conceder o denegar a los usuarios, consulte [Operaciones del proveedor de recursos de Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="3e319-234">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

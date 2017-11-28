---
title: Conjunto de aplicaciones de IoT de Azure y Azure Active Directory | Microsoft Docs
description: Describe la forma en que el conjunto de aplicaciones Azure IoT usa Azure Active Directory para administrar permisos.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 518e6a481ab6385b03dd3ddc2e155fb724e677fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-on-the-azureiotsuitecom-site"></a><span data-ttu-id="a120d-103">Permisos en el sitio azureiotsuite.com</span><span class="sxs-lookup"><span data-stu-id="a120d-103">Permissions on the azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="a120d-104">Qué ocurre al iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="a120d-104">What happens when you sign in</span></span>

<span data-ttu-id="a120d-105">La primera vez que inicie sesión en [azureiotsuite.com][lnk-azureiotsuite], el sitio determinará los niveles de permiso que tiene según el inquilino de Azure Active Directory (AAD) seleccionado actualmente y la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a120d-105">The first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], the site determines the permission levels you have based on the currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="a120d-106">En primer lugar, para rellenar la lista de los inquilinos que aparece junto al nombre de usuario, el sitio descubre en Azure a qué inquilinos de AAD pertenece el usuario.</span><span class="sxs-lookup"><span data-stu-id="a120d-106">First, to populate the list of tenants seen next to your username, the site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="a120d-107">Actualmente, el sitio no puede obtener tokens de usuario para más de un solo inquilino a la vez.</span><span class="sxs-lookup"><span data-stu-id="a120d-107">Currently, the site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="a120d-108">Por tanto, al cambiar inquilinos mediante la lista desplegable de la esquina superior derecha, el sitio inicia si sesión en dicho inquilino para obtener los tokens de este.</span><span class="sxs-lookup"><span data-stu-id="a120d-108">Therefore, when you switch tenants using the dropdown in the top right corner, the site logs you in to that tenant to obtain the tokens for that tenant.</span></span>

2. <span data-ttu-id="a120d-109">A continuación, el sitio descubre en Azure qué suscripciones ha asociado al inquilino seleccionado.</span><span class="sxs-lookup"><span data-stu-id="a120d-109">Next, the site finds out from Azure which subscriptions you have associated with the selected tenant.</span></span> <span data-ttu-id="a120d-110">Las suscripciones disponibles se ven cuando se crea una nueva solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="a120d-110">You see the available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="a120d-111">Por último, el sitio recupera todos los recursos de las suscripciones y los grupos de recursos etiquetados como soluciones preconfiguradas y rellena los iconos de la página principal.</span><span class="sxs-lookup"><span data-stu-id="a120d-111">Finally, the site retrieves all the resources in the subscriptions and resource groups tagged as preconfigured solutions and populates the tiles on the home page.</span></span>

<span data-ttu-id="a120d-112">En las secciones siguientes se describen los roles que controlan el acceso a las soluciones preconfiguradas.</span><span class="sxs-lookup"><span data-stu-id="a120d-112">The following sections describe the roles that control access to the preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="a120d-113">Roles de AAD</span><span class="sxs-lookup"><span data-stu-id="a120d-113">AAD roles</span></span>

<span data-ttu-id="a120d-114">Los roles de AAD controlan las soluciones preconfiguradas de aprovisionamiento de capacidades y administran los usuarios en una solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="a120d-114">The AAD roles control the ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="a120d-115">Puede encontrar más información sobre los roles del administrador en AAD en [Asignación de roles de administrador en Azure Active Directory][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="a120d-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="a120d-116">El artículo actual se centra en los roles de **administrador global** y de directorio de **usuario** que utilizan las soluciones preconfiguradas.</span><span class="sxs-lookup"><span data-stu-id="a120d-116">The current article focuses on the **Global Administrator** and the **User** directory roles as used by the preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="a120d-117">Administrador global</span><span class="sxs-lookup"><span data-stu-id="a120d-117">Global administrator</span></span>

<span data-ttu-id="a120d-118">Puede haber muchos administradores globales por inquilino de AAD:</span><span class="sxs-lookup"><span data-stu-id="a120d-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="a120d-119">Al crear un inquilino de AAD, quien lo crea es de forma predeterminada el administrador global del mismo.</span><span class="sxs-lookup"><span data-stu-id="a120d-119">When you create an AAD tenant, you are by default the global administrator of that tenant.</span></span>
* <span data-ttu-id="a120d-120">El administrador global puede aprovisionar una solución preconfigurada y se le asigna el rol **Admin** para la aplicación dentro de su inquilino de AAD.</span><span class="sxs-lookup"><span data-stu-id="a120d-120">The global administrator can provision a preconfigured solution and is assigned an **Admin** role for the application inside their AAD tenant.</span></span>
* <span data-ttu-id="a120d-121">Si otro usuario del mismo inquilino de AAD crea una aplicación, el rol predeterminado que se concede al administrador global es **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="a120d-121">If another user in the same AAD tenant creates an application, the default role granted to the global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="a120d-122">Un administrador global pueden asignar a los usuarios roles para aplicaciones mediante [Azure Portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="a120d-122">A global administrator can assign users to roles for applications using the [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="a120d-123">Usuario de dominio</span><span class="sxs-lookup"><span data-stu-id="a120d-123">Domain user</span></span>

<span data-ttu-id="a120d-124">Puede haber muchos usuarios de dominio por inquilino de AAD:</span><span class="sxs-lookup"><span data-stu-id="a120d-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="a120d-125">Un usuario de dominio puede aprovisionar una solución preconfigurada mediante el sitio [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="a120d-125">A domain user can provision a preconfigured solution through the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="a120d-126">De forma predeterminada, se concede al usuario de dominio el rol de **administrador** en la aplicación aprovisionada.</span><span class="sxs-lookup"><span data-stu-id="a120d-126">By default, the domain user is granted the **Admin** role in the provisioned application.</span></span>
* <span data-ttu-id="a120d-127">Un usuario de dominio puede crear una aplicación con el script build.cmd en el repositorio [azure-iot-remote-monitoring][lnk-rm-github-repo], [azure-iot-predictive-maintenance][lnk-pm-github-repo] o [azure-iot-connected-factory][lnk-cf-github-repo].</span><span class="sxs-lookup"><span data-stu-id="a120d-127">A domain user can create an application using the build.cmd script in the [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="a120d-128">Sin embargo, la función predeterminada concedida al usuario de dominio es **ReadOnly**, ya que un usuario de dominio no tiene permiso para asignar roles.</span><span class="sxs-lookup"><span data-stu-id="a120d-128">However, the default role granted to the domain user is **ReadOnly**, because a domain user does not have permission to assign roles.</span></span>
* <span data-ttu-id="a120d-129">Si otro usuario del inquilino de AAD crea una aplicación, al usuario de dominio se le asignará el rol **ReadOnly** de forma predeterminada para dicha aplicación.</span><span class="sxs-lookup"><span data-stu-id="a120d-129">If another user in the AAD tenant creates an application, the domain user is assigned the **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="a120d-130">El usuario de dominio no puede asignar roles para aplicaciones; por consiguiente, no puede agregar usuarios o roles a usuarios para una aplicación, aunque la haya aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="a120d-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="a120d-131">Usuario invitado</span><span class="sxs-lookup"><span data-stu-id="a120d-131">Guest User</span></span>

<span data-ttu-id="a120d-132">Puede haber muchos usuarios invitados por inquilino de AAD.</span><span class="sxs-lookup"><span data-stu-id="a120d-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="a120d-133">Los usuarios invitados tienen un conjunto de derechos limitado en el inquilino de AAD.</span><span class="sxs-lookup"><span data-stu-id="a120d-133">Guest users have a limited set of rights in the AAD tenant.</span></span> <span data-ttu-id="a120d-134">Como consecuencia, los usuarios invitados no pueden aprovisionar una solución preconfigurada en el inquilino de AAD.</span><span class="sxs-lookup"><span data-stu-id="a120d-134">As a result, guest users cannot provision a preconfigured solution in the AAD tenant.</span></span>

<span data-ttu-id="a120d-135">Para más información acerca de los usuarios y roles de AAD, consulte estos recursos:</span><span class="sxs-lookup"><span data-stu-id="a120d-135">For more information about users and roles in AAD, see the following resources:</span></span>

* <span data-ttu-id="a120d-136">[Creación de usuarios en Azure AD][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="a120d-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="a120d-137">[Asignación de usuarios a aplicaciones][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="a120d-137">[Assign users to apps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="a120d-138">Roles de administrador de suscripciones de Azure</span><span class="sxs-lookup"><span data-stu-id="a120d-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="a120d-139">Los roles de administrador de Azure controlan la capacidad para asignar una suscripción de Azure a un inquilino de AD.</span><span class="sxs-lookup"><span data-stu-id="a120d-139">The Azure admin roles control the ability to map an Azure subscription to an AD tenant.</span></span>

<span data-ttu-id="a120d-140">Encuentre más información sobre los roles de administrador de Azure en el artículo [Adición o cambio de roles de administrador de Azure que administran la suscripción o servicios][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="a120d-140">Find out more about the Azure admin roles in the article [How to add or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="a120d-141">Roles de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a120d-141">Application roles</span></span>

<span data-ttu-id="a120d-142">Los roles de aplicación controlan el acceso a los dispositivos de las soluciones preconfiguradas.</span><span class="sxs-lookup"><span data-stu-id="a120d-142">The application roles control access to devices in your preconfigured solution.</span></span>

<span data-ttu-id="a120d-143">Hay dos roles definidos y una función implícita definida en una aplicación aprovisionada:</span><span class="sxs-lookup"><span data-stu-id="a120d-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="a120d-144">**Admin:** tiene control total para agregar, administrar y quitar dispositivos, y modificar la configuración.</span><span class="sxs-lookup"><span data-stu-id="a120d-144">**Admin:** Has full control to add, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="a120d-145">**ReadOnly:** puede ver dispositivos, reglas, acciones, trabajos y telemetría.</span><span class="sxs-lookup"><span data-stu-id="a120d-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="a120d-146">Puede encontrar los permisos asignados a cada rol en el archivo de origen [RolePermissions.cs][lnk-resource-cs].</span><span class="sxs-lookup"><span data-stu-id="a120d-146">You can find the permissions assigned to each role in the [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="a120d-147">Cambio de roles de aplicación para un usuario</span><span class="sxs-lookup"><span data-stu-id="a120d-147">Changing application roles for a user</span></span>

<span data-ttu-id="a120d-148">Puede utilizar el siguiente procedimiento para convertir a un usuario en Active Directory en el administrador de la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="a120d-148">You can use the following procedure to make a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="a120d-149">Para cambiar los roles de los usuarios, es preciso ser administrador global de AAD:</span><span class="sxs-lookup"><span data-stu-id="a120d-149">You must be an AAD global administrator to change roles for a user:</span></span>

1. <span data-ttu-id="a120d-150">Vaya a [Azure Portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="a120d-150">Go to the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="a120d-151">Seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a120d-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="a120d-152">Asegúrese de que utiliza el directorio que eligió en azureiotsuite.com al aprovisionar la solución.</span><span class="sxs-lookup"><span data-stu-id="a120d-152">Make sure you are using the directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="a120d-153">Si tiene varios directorios asociados a su suscripción, puede cambiar entre ellos si hace clic en el nombre de cuenta en la parte superior derecha del portal.</span><span class="sxs-lookup"><span data-stu-id="a120d-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at the top-right of the portal.</span></span>
4. <span data-ttu-id="a120d-154">Haga clic en **Aplicaciones empresariales** y en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a120d-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="a120d-155">Muestre **Todas las aplicaciones** con **Cualquier** estado.</span><span class="sxs-lookup"><span data-stu-id="a120d-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="a120d-156">A continuación, busque una aplicación con el nombre de la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="a120d-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="a120d-157">Haga clic en el nombre de la aplicación que coincida con el nombre de la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="a120d-157">Click the name of the application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="a120d-158">Haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a120d-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="a120d-159">Seleccione el usuario cuyos roles desea cambiar.</span><span class="sxs-lookup"><span data-stu-id="a120d-159">Select the user you want to switch roles.</span></span>
8. <span data-ttu-id="a120d-160">Haga clic en **Asignar**, seleccione el rol (por ejemplo **Admin**) que desea asignar al usuario y haga clic en la marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="a120d-160">Click **Assign** and select the role (such as **Admin**) you'd like to assign to the user, click the check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="a120d-161">P+F</span><span class="sxs-lookup"><span data-stu-id="a120d-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-to-change-the-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="a120d-162">Soy administrador de servicios y deseo cambiar la asignación de directorio entre mi suscripción y un inquilino de AAD específico.</span><span class="sxs-lookup"><span data-stu-id="a120d-162">I'm a service administrator and I'd like to change the directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="a120d-163">¿Cómo completo esta tarea?</span><span class="sxs-lookup"><span data-stu-id="a120d-163">How do I complete this task?</span></span>

1. <span data-ttu-id="a120d-164">Vaya al [Portal de Azure clásico][lnk-classic-portal] y haga clic en **Configuración** en la lista de servicios situada a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="a120d-164">Go to the [Azure classic portal][lnk-classic-portal], click **Settings** in the list of services on the left-hand side.</span></span>
2. <span data-ttu-id="a120d-165">Seleccione la suscripción a la que desea cambiar la asignación de directorio.</span><span class="sxs-lookup"><span data-stu-id="a120d-165">Select the subscription you'd like to change the directory mapping to.</span></span>
3. <span data-ttu-id="a120d-166">Haga clic en **Editar directorio**.</span><span class="sxs-lookup"><span data-stu-id="a120d-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="a120d-167">En la lista desplegable, seleccione el **directorio** que le desea usar.</span><span class="sxs-lookup"><span data-stu-id="a120d-167">Select the **Directory** you would like to use in the dropdown.</span></span> <span data-ttu-id="a120d-168">Haga clic en la flecha hacia adelante.</span><span class="sxs-lookup"><span data-stu-id="a120d-168">Click the forward arrow.</span></span>
5. <span data-ttu-id="a120d-169">Confirme la asignación de directorio y los coadministradores afectados.</span><span class="sxs-lookup"><span data-stu-id="a120d-169">Confirm the directory mapping and affected co-administrators.</span></span> <span data-ttu-id="a120d-170">Si se mueve desde otro directorio, se quitan todos los coadministradores del directorio original.</span><span class="sxs-lookup"><span data-stu-id="a120d-170">If you are moving from another directory, all the co-administrators from the original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-the-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="a120d-171">Soy miembro o usuario de dominio en el inquilino de AAD y he creado una solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="a120d-171">I'm a domain user/member on the AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="a120d-172">¿Cómo se asigna un rol en mi aplicación?</span><span class="sxs-lookup"><span data-stu-id="a120d-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="a120d-173">Pida al administrador global que le nombre administrador global en el inquilino de AAD y, después, podrá asignar roles a los usuarios usted mismo.</span><span class="sxs-lookup"><span data-stu-id="a120d-173">Ask a global administrator to make you a global administrator on the AAD tenant and then assign roles to users yourself.</span></span> <span data-ttu-id="a120d-174">O bien, pida al administrador global que le asigne un rol directamente.</span><span class="sxs-lookup"><span data-stu-id="a120d-174">Alternatively, ask a global administrator to assign you a role directly.</span></span> <span data-ttu-id="a120d-175">Si desea cambiar el inquilino de AAD, en la que se implementó la solución preconfigurada, consulte la siguiente pregunta.</span><span class="sxs-lookup"><span data-stu-id="a120d-175">If you'd like to change the AAD tenant your preconfigured solution has been deployed to, see the next question.</span></span>

### <a name="how-do-i-switch-the-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="a120d-176">¿Cómo cambio el inquilino de AAD al que están asignadas mi solución preconfigurada de supervisión remota y mi aplicación?</span><span class="sxs-lookup"><span data-stu-id="a120d-176">How do I switch the AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="a120d-177">Puede ejecutar una implementación en la nube desde <https://github.com/Azure/azure-iot-remote-monitoring> e implementar de nuevo con un inquilino de ADD recién creado.</span><span class="sxs-lookup"><span data-stu-id="a120d-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="a120d-178">Dado que, de manera predeterminada, ya es administrador global cuando crea un inquilino de AAD, tiene permisos para agregar usuarios y asignarles roles.</span><span class="sxs-lookup"><span data-stu-id="a120d-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions to add users and assign roles to those users.</span></span>

1. <span data-ttu-id="a120d-179">Cree un directorio de AAD en [Azure Portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="a120d-179">Create an AAD directory in the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="a120d-180">Vaya a <https://github.com/Azure/azure-iot-remote-monitoring>.</span><span class="sxs-lookup"><span data-stu-id="a120d-180">Go to <https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="a120d-181">Ejecute `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (por ejemplo, `build.cmd cloud debug myRMSolution`)</span><span class="sxs-lookup"><span data-stu-id="a120d-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="a120d-182">Cuando se le solicite, establezca que **tenantid** sea el inquilino recién creado, en lugar del inquilino anterior.</span><span class="sxs-lookup"><span data-stu-id="a120d-182">When prompted, set the **tenantid** to be your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-to-change-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="a120d-183">Deseo cambiar un administrador de servicios o coadministrador cuando haya iniciado sesión con una cuenta de la organización</span><span class="sxs-lookup"><span data-stu-id="a120d-183">I want to change a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="a120d-184">Consulte el artículo de asistencia [Cambiar el administrador de servicios y el coadministrador cuando ha iniciado sesión con una cuenta organizativa][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="a120d-184">See the support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-the-proper-permissions-to-create-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="a120d-185">¿Por qué veo este error?</span><span class="sxs-lookup"><span data-stu-id="a120d-185">Why am I seeing this error?</span></span> <span data-ttu-id="a120d-186">"Su cuenta no tiene los permisos adecuados para crear una solución.</span><span class="sxs-lookup"><span data-stu-id="a120d-186">"Your account does not have the proper permissions to create a solution.</span></span> <span data-ttu-id="a120d-187">Póngase en contacto con el administrador de cuentas o inténtelo con otra cuenta."</span><span class="sxs-lookup"><span data-stu-id="a120d-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="a120d-188">Observe el diagrama siguiente para obtener instrucciones:</span><span class="sxs-lookup"><span data-stu-id="a120d-188">Look at the following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="a120d-189">Si sigue viendo el error después de validar que usted es un administrador global en el inquilino de AAD y un coadministrador de la suscripción, haga que el administrador de cuenta quite el usuario y vuelva a asignar los permisos necesarios en este orden.</span><span class="sxs-lookup"><span data-stu-id="a120d-189">If you continue to see the error after validating you are a global administrator on the AAD tenant and a co-administrator on the subscription, have your account administrator remove the user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="a120d-190">En primer lugar, agregue al usuario como administrador global y luego agregue al usuario como coadministrador de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a120d-190">First, add the user as a global administrator and then add user as a co-administrator on the Azure subscription.</span></span> <span data-ttu-id="a120d-191">Si los problemas persisten, póngase en contacto con [Ayuda y soporte técnico][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="a120d-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-to-create-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="a120d-192">¿Por qué veo este error cuando tengo una suscripción de Azure?</span><span class="sxs-lookup"><span data-stu-id="a120d-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="a120d-193">"Para crear soluciones preconfiguradas se requiere una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a120d-193">"An Azure subscription is required to create pre-configured solutions.</span></span> <span data-ttu-id="a120d-194">Puede crear una cuenta de evaluación gratuita en pocos minutos".</span><span class="sxs-lookup"><span data-stu-id="a120d-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="a120d-195">Si está seguro de que tiene una suscripción de Azure, valide la asignación del inquilino de la suscripción y asegúrese de que se ha seleccionado el inquilino correcto en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="a120d-195">If you're certain you have an Azure subscription, validate the tenant mapping for your subscription and ensure the correct tenant is selected in the dropdown.</span></span> <span data-ttu-id="a120d-196">Si ha validado que el inquilino deseado es el correcto, siga el diagrama anterior y valide la asignación de la suscripción y de este inquilino de AAD.</span><span class="sxs-lookup"><span data-stu-id="a120d-196">If you’ve validated the desired tenant is correct, follow the preceding diagram and validate the mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a120d-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a120d-197">Next steps</span></span>
<span data-ttu-id="a120d-198">Para obtener más información sobre el Conjunto de aplicaciones de IoT, consulte cómo puede [personalizar una solución preconfigurada][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="a120d-198">To continue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md

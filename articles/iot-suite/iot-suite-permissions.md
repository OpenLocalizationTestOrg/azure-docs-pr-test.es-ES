---
title: aaaAzure IoT Suite y Azure Active Directory | Documentos de Microsoft
description: "Describe cómo el conjunto de IoT de Azure utiliza permisos toomanage de Azure Active Directory."
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
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a><span data-ttu-id="2db19-103">Permisos en el sitio de hello azureiotsuite.com</span><span class="sxs-lookup"><span data-stu-id="2db19-103">Permissions on hello azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="2db19-104">Qué ocurre al iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="2db19-104">What happens when you sign in</span></span>

<span data-ttu-id="2db19-105">Hola la primera vez que inicie sesión en [azureiotsuite.com][lnk-azureiotsuite], sitio de hello determina seleccionados los niveles de permiso de hello tener en función de hello actualmente el inquilino de Azure Active Directory (AAD) y Azure suscripción.</span><span class="sxs-lookup"><span data-stu-id="2db19-105">hello first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], hello site determines hello permission levels you have based on hello currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="2db19-106">En primer lugar, lista de hello toopopulate del nombre de usuario de los inquilinos vistos siguiente tooyour, sitio Hola averigua de Azure que los inquilinos AAD que pertenece.</span><span class="sxs-lookup"><span data-stu-id="2db19-106">First, toopopulate hello list of tenants seen next tooyour username, hello site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="2db19-107">Actualmente, el sitio de hello solo puede obtener tokens de usuario para un solo inquilino a la vez.</span><span class="sxs-lookup"><span data-stu-id="2db19-107">Currently, hello site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="2db19-108">Por lo tanto, cuando se cambia de inquilinos mediante la lista desplegable de hello en la esquina superior derecha de hello, sitio Hola la sesión en tokens de toothat inquilino tooobtain Hola para ese inquilino.</span><span class="sxs-lookup"><span data-stu-id="2db19-108">Therefore, when you switch tenants using hello dropdown in hello top right corner, hello site logs you in toothat tenant tooobtain hello tokens for that tenant.</span></span>

2. <span data-ttu-id="2db19-109">A continuación, el sitio de hello averigua de las suscripciones que tienen asociados con hello seleccionado inquilino de Azure.</span><span class="sxs-lookup"><span data-stu-id="2db19-109">Next, hello site finds out from Azure which subscriptions you have associated with hello selected tenant.</span></span> <span data-ttu-id="2db19-110">Vea las suscripciones disponibles de hello cuando se crea una nueva solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="2db19-110">You see hello available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="2db19-111">Por último, sitio Hola recupera todos los recursos de hello en suscripciones de Hola y grupos de recursos etiquetados como soluciones preconfiguradas y rellena los iconos de hello en la página de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2db19-111">Finally, hello site retrieves all hello resources in hello subscriptions and resource groups tagged as preconfigured solutions and populates hello tiles on hello home page.</span></span>

<span data-ttu-id="2db19-112">Hola siguientes secciones describe los roles de Hola que controlan el acceso toohello preconfigurado soluciones.</span><span class="sxs-lookup"><span data-stu-id="2db19-112">hello following sections describe hello roles that control access toohello preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="2db19-113">Roles de AAD</span><span class="sxs-lookup"><span data-stu-id="2db19-113">AAD roles</span></span>

<span data-ttu-id="2db19-114">roles AAD de Hola Hola capacidad aprovisionar preconfigurado soluciones de control y administración de usuarios en una solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="2db19-114">hello AAD roles control hello ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="2db19-115">Puede encontrar más información sobre los roles del administrador en AAD en [Asignación de roles de administrador en Azure Active Directory][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="2db19-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="2db19-116">artículo actual de Hola se centra en hello **administrador Global** hello y **usuario** roles de directorio, como se hace Hola soluciones preconfiguradas.</span><span class="sxs-lookup"><span data-stu-id="2db19-116">hello current article focuses on hello **Global Administrator** and hello **User** directory roles as used by hello preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="2db19-117">Administrador global</span><span class="sxs-lookup"><span data-stu-id="2db19-117">Global administrator</span></span>

<span data-ttu-id="2db19-118">Puede haber muchos administradores globales por inquilino de AAD:</span><span class="sxs-lookup"><span data-stu-id="2db19-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="2db19-119">Cuando se crea un inquilino de AAD, eres por un administrador global de hello predeterminado de ese inquilino.</span><span class="sxs-lookup"><span data-stu-id="2db19-119">When you create an AAD tenant, you are by default hello global administrator of that tenant.</span></span>
* <span data-ttu-id="2db19-120">Administrador global de Hello puede aprovisionar una solución preconfigurada y se le asigna un **administración** rol de aplicación Hola dentro de su inquilino AAD.</span><span class="sxs-lookup"><span data-stu-id="2db19-120">hello global administrator can provision a preconfigured solution and is assigned an **Admin** role for hello application inside their AAD tenant.</span></span>
* <span data-ttu-id="2db19-121">Si otro usuario de Hola mismo inquilino AAD crea una aplicación, rol predeterminado de hello es concedido de administrador global de toohello **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="2db19-121">If another user in hello same AAD tenant creates an application, hello default role granted toohello global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="2db19-122">Un administrador global puede asignar usuarios tooroles para las aplicaciones que usan hello [portal de Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="2db19-122">A global administrator can assign users tooroles for applications using hello [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="2db19-123">Usuario de dominio</span><span class="sxs-lookup"><span data-stu-id="2db19-123">Domain user</span></span>

<span data-ttu-id="2db19-124">Puede haber muchos usuarios de dominio por inquilino de AAD:</span><span class="sxs-lookup"><span data-stu-id="2db19-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="2db19-125">Un usuario de dominio puede proporcionar una solución preconfigurada a través de hello [azureiotsuite.com] [ lnk-azureiotsuite] sitio.</span><span class="sxs-lookup"><span data-stu-id="2db19-125">A domain user can provision a preconfigured solution through hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="2db19-126">De forma predeterminada, se concede a los usuario de dominio de Hola Hola **administración** rol Hola aprovisiona la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2db19-126">By default, hello domain user is granted hello **Admin** role in hello provisioned application.</span></span>
* <span data-ttu-id="2db19-127">Un usuario de dominio puede crear una aplicación con script build.cmd de Hola Hola [-iot-remoto-supervisión de azure][lnk-rm-github-repo], [azure iot-predictivo mantenimiento] [ lnk-pm-github-repo], o [-iot-conectado-factory de azure] [ lnk-cf-github-repo] repositorio.</span><span class="sxs-lookup"><span data-stu-id="2db19-127">A domain user can create an application using hello build.cmd script in hello [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="2db19-128">Sin embargo, rol predeterminado de hello concedido es de usuario del dominio toohello **ReadOnly**, ya que un usuario de dominio no tiene permiso tooassign roles.</span><span class="sxs-lookup"><span data-stu-id="2db19-128">However, hello default role granted toohello domain user is **ReadOnly**, because a domain user does not have permission tooassign roles.</span></span>
* <span data-ttu-id="2db19-129">Si otro usuario de inquilino de AAD Hola crea una aplicación, usuario de dominio de Hola se asigna hello **ReadOnly** función predeterminada para esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="2db19-129">If another user in hello AAD tenant creates an application, hello domain user is assigned hello **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="2db19-130">El usuario de dominio no puede asignar roles para aplicaciones; por consiguiente, no puede agregar usuarios o roles a usuarios para una aplicación, aunque la haya aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="2db19-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="2db19-131">Usuario invitado</span><span class="sxs-lookup"><span data-stu-id="2db19-131">Guest User</span></span>

<span data-ttu-id="2db19-132">Puede haber muchos usuarios invitados por inquilino de AAD.</span><span class="sxs-lookup"><span data-stu-id="2db19-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="2db19-133">Usuarios invitados tienen un conjunto limitado de derechos en el inquilino de AAD Hola.</span><span class="sxs-lookup"><span data-stu-id="2db19-133">Guest users have a limited set of rights in hello AAD tenant.</span></span> <span data-ttu-id="2db19-134">Como resultado, los usuarios invitados no pueden proporcionar una solución preconfigurada en el inquilino de AAD Hola.</span><span class="sxs-lookup"><span data-stu-id="2db19-134">As a result, guest users cannot provision a preconfigured solution in hello AAD tenant.</span></span>

<span data-ttu-id="2db19-135">Para obtener más información sobre los usuarios y roles en AAD, consulte Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2db19-135">For more information about users and roles in AAD, see hello following resources:</span></span>

* <span data-ttu-id="2db19-136">[Creación de usuarios en Azure AD][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="2db19-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="2db19-137">[Asignar usuarios tooapps][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="2db19-137">[Assign users tooapps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="2db19-138">Roles de administrador de suscripciones de Azure</span><span class="sxs-lookup"><span data-stu-id="2db19-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="2db19-139">las funciones de administración de Azure Hola controlan Hola capacidad toomap un inquilino de tooan AD de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2db19-139">hello Azure admin roles control hello ability toomap an Azure subscription tooan AD tenant.</span></span>

<span data-ttu-id="2db19-140">Obtener más información acerca de los roles de administrador de Azure de hello en el artículo hello [cómo tooadd o cambiar la cuenta de administrador, Administrador de servicios y Coadministrador de Azure][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="2db19-140">Find out more about hello Azure admin roles in hello article [How tooadd or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="2db19-141">Roles de la aplicación</span><span class="sxs-lookup"><span data-stu-id="2db19-141">Application roles</span></span>

<span data-ttu-id="2db19-142">roles de aplicación Hola controlan toodevices de acceso de la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="2db19-142">hello application roles control access toodevices in your preconfigured solution.</span></span>

<span data-ttu-id="2db19-143">Hay dos roles definidos y una función implícita definida en una aplicación aprovisionada:</span><span class="sxs-lookup"><span data-stu-id="2db19-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="2db19-144">**Administrador:** tiene control total tooadd, administrar, quite los dispositivos y modificar la configuración.</span><span class="sxs-lookup"><span data-stu-id="2db19-144">**Admin:** Has full control tooadd, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="2db19-145">**ReadOnly:** puede ver dispositivos, reglas, acciones, trabajos y telemetría.</span><span class="sxs-lookup"><span data-stu-id="2db19-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="2db19-146">Puede encontrar permisos Hola asignan el rol de tooeach en hello [RolePermissions.cs] [ lnk-resource-cs] archivo de código fuente.</span><span class="sxs-lookup"><span data-stu-id="2db19-146">You can find hello permissions assigned tooeach role in hello [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="2db19-147">Cambio de roles de aplicación para un usuario</span><span class="sxs-lookup"><span data-stu-id="2db19-147">Changing application roles for a user</span></span>

<span data-ttu-id="2db19-148">Puede usar Hola siguiendo el procedimiento toomake un usuario en el Administrador de la solución preconfigurada de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2db19-148">You can use hello following procedure toomake a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="2db19-149">Debe ser un rol de toochange AAD administrador global para un usuario:</span><span class="sxs-lookup"><span data-stu-id="2db19-149">You must be an AAD global administrator toochange roles for a user:</span></span>

1. <span data-ttu-id="2db19-150">Vaya toohello [portal de Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="2db19-150">Go toohello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="2db19-151">Seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2db19-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="2db19-152">Asegúrese de que está usando directorio Hola elegido en azureiotsuite.com al aprovisionar la solución.</span><span class="sxs-lookup"><span data-stu-id="2db19-152">Make sure you are using hello directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="2db19-153">Si tiene varios directorios asociados a su suscripción, puede cambiar entre ellos si hace clic en el nombre de su cuenta en hello superior derecha del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="2db19-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at hello top-right of hello portal.</span></span>
4. <span data-ttu-id="2db19-154">Haga clic en **Aplicaciones empresariales** y en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2db19-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="2db19-155">Muestre **Todas las aplicaciones** con **Cualquier** estado.</span><span class="sxs-lookup"><span data-stu-id="2db19-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="2db19-156">A continuación, busque una aplicación con el nombre de la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="2db19-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="2db19-157">Haga clic en el nombre de Hola de aplicación Hola que coincida con el nombre de la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="2db19-157">Click hello name of hello application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="2db19-158">Haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2db19-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="2db19-159">Seleccione usuario Hola desea tooswitch roles.</span><span class="sxs-lookup"><span data-stu-id="2db19-159">Select hello user you want tooswitch roles.</span></span>
8. <span data-ttu-id="2db19-160">Haga clic en **asignar** y seleccione Hola rol (como **administración**) le gustaría tooassign toohello usuario, haga clic en la marca de verificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2db19-160">Click **Assign** and select hello role (such as **Admin**) you'd like tooassign toohello user, click hello check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="2db19-161">P+F</span><span class="sxs-lookup"><span data-stu-id="2db19-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="2db19-162">Soy un administrador de servicios y me gustaría que la asignación de directorio de hello toochange entre mi suscripción y un inquilino AAD específico.</span><span class="sxs-lookup"><span data-stu-id="2db19-162">I'm a service administrator and I'd like toochange hello directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="2db19-163">¿Cómo completo esta tarea?</span><span class="sxs-lookup"><span data-stu-id="2db19-163">How do I complete this task?</span></span>

1. <span data-ttu-id="2db19-164">Vaya toohello [portal de Azure clásico][lnk-classic-portal], haga clic en **configuración** en lista de hello de servicios en el lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2db19-164">Go toohello [Azure classic portal][lnk-classic-portal], click **Settings** in hello list of services on hello left-hand side.</span></span>
2. <span data-ttu-id="2db19-165">Seleccione la suscripción de Hola que desea que la asignación de directorio de hello toochange a.</span><span class="sxs-lookup"><span data-stu-id="2db19-165">Select hello subscription you'd like toochange hello directory mapping to.</span></span>
3. <span data-ttu-id="2db19-166">Haga clic en **Editar directorio**.</span><span class="sxs-lookup"><span data-stu-id="2db19-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="2db19-167">Seleccione hello **Directory** le gustaría toouse en la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="2db19-167">Select hello **Directory** you would like toouse in hello dropdown.</span></span> <span data-ttu-id="2db19-168">Haga clic en la flecha hacia adelante Hola.</span><span class="sxs-lookup"><span data-stu-id="2db19-168">Click hello forward arrow.</span></span>
5. <span data-ttu-id="2db19-169">Confirmar la asignación de directorio de Hola y afectados coadministradores.</span><span class="sxs-lookup"><span data-stu-id="2db19-169">Confirm hello directory mapping and affected co-administrators.</span></span> <span data-ttu-id="2db19-170">Si va a mover de otro directorio, se quitan todos los Hola coadministradores de directorio original Hola.</span><span class="sxs-lookup"><span data-stu-id="2db19-170">If you are moving from another directory, all hello co-administrators from hello original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="2db19-171">Soy un usuario o miembro del dominio en el inquilino de AAD de Hola y he creado una solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="2db19-171">I'm a domain user/member on hello AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="2db19-172">¿Cómo se asigna un rol en mi aplicación?</span><span class="sxs-lookup"><span data-stu-id="2db19-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="2db19-173">Solicitar un toomake administrador global que un administrador global en hello AAD de inquilinos y, a continuación, asigna roles toousers.</span><span class="sxs-lookup"><span data-stu-id="2db19-173">Ask a global administrator toomake you a global administrator on hello AAD tenant and then assign roles toousers yourself.</span></span> <span data-ttu-id="2db19-174">O bien, pida un tooassign administrador global es un rol directamente.</span><span class="sxs-lookup"><span data-stu-id="2db19-174">Alternatively, ask a global administrator tooassign you a role directly.</span></span> <span data-ttu-id="2db19-175">Si desea que el inquilino de AAD de hello toochange en que se ha implementado la solución preconfigurada, vea la siguiente pregunta de Hola.</span><span class="sxs-lookup"><span data-stu-id="2db19-175">If you'd like toochange hello AAD tenant your preconfigured solution has been deployed to, see hello next question.</span></span>

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="2db19-176">¿Cómo se puede cambiar el inquilino de AAD Hola a que mi solución preconfigurada de supervisión y la aplicación se asignan?</span><span class="sxs-lookup"><span data-stu-id="2db19-176">How do I switch hello AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="2db19-177">Puede ejecutar una implementación en la nube desde <https://github.com/Azure/azure-iot-remote-monitoring> e implementar de nuevo con un inquilino de ADD recién creado.</span><span class="sxs-lookup"><span data-stu-id="2db19-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="2db19-178">Dado que son, de forma predeterminada, un administrador global cuando se crea un inquilino de AAD, que tiene permisos tooadd usuarios y asigna roles a los usuarios de toothose.</span><span class="sxs-lookup"><span data-stu-id="2db19-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions tooadd users and assign roles toothose users.</span></span>

1. <span data-ttu-id="2db19-179">Crear un directorio AAD en hello [portal de Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="2db19-179">Create an AAD directory in hello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="2db19-180">Vaya demasiado<https://github.com/Azure/azure-iot-remote-monitoring>.</span><span class="sxs-lookup"><span data-stu-id="2db19-180">Go too<https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="2db19-181">Ejecute `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (por ejemplo, `build.cmd cloud debug myRMSolution`)</span><span class="sxs-lookup"><span data-stu-id="2db19-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="2db19-182">Cuando se le pida, establezca hello **tenantid** toobe el inquilino recién creado en lugar de su inquilino anterior.</span><span class="sxs-lookup"><span data-stu-id="2db19-182">When prompted, set hello **tenantid** toobe your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="2db19-183">Desea toochange un administrador de servicios o Coadministrador cuando inicia sesión con una cuenta organizativa</span><span class="sxs-lookup"><span data-stu-id="2db19-183">I want toochange a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="2db19-184">Vea el artículo de soporte técnico de hello [cambiar el Administrador de servicios y Coadministrador cuando inicia sesión con una cuenta organizativa][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="2db19-184">See hello support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="2db19-185">¿Por qué veo este error?</span><span class="sxs-lookup"><span data-stu-id="2db19-185">Why am I seeing this error?</span></span> <span data-ttu-id="2db19-186">"Su cuenta no tiene toocreate de los permisos adecuados de hello una solución.</span><span class="sxs-lookup"><span data-stu-id="2db19-186">"Your account does not have hello proper permissions toocreate a solution.</span></span> <span data-ttu-id="2db19-187">Póngase en contacto con el administrador de cuentas o inténtelo con otra cuenta."</span><span class="sxs-lookup"><span data-stu-id="2db19-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="2db19-188">Mire Hola siguiente diagrama para obtener instrucciones:</span><span class="sxs-lookup"><span data-stu-id="2db19-188">Look at hello following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="2db19-189">Si continúa el error de hello toosee después de validar un administrador global de inquilino de AAD de Hola y Coadministrador de suscripción de hello, pida al administrador de cuenta quitar usuario hello y volver a asignar los permisos necesarios en este orden.</span><span class="sxs-lookup"><span data-stu-id="2db19-189">If you continue toosee hello error after validating you are a global administrator on hello AAD tenant and a co-administrator on hello subscription, have your account administrator remove hello user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="2db19-190">En primer lugar, agregar usuario hello como administrador global y, a continuación, agregar el usuario como Coadministrador en hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2db19-190">First, add hello user as a global administrator and then add user as a co-administrator on hello Azure subscription.</span></span> <span data-ttu-id="2db19-191">Si los problemas persisten, póngase en contacto con [Ayuda y soporte técnico][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="2db19-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="2db19-192">¿Por qué veo este error cuando tengo una suscripción de Azure?</span><span class="sxs-lookup"><span data-stu-id="2db19-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="2db19-193">"Una suscripción de Azure es necesario toocreate preconfigurado y soluciones.</span><span class="sxs-lookup"><span data-stu-id="2db19-193">"An Azure subscription is required toocreate pre-configured solutions.</span></span> <span data-ttu-id="2db19-194">Puede crear una cuenta de evaluación gratuita en pocos minutos".</span><span class="sxs-lookup"><span data-stu-id="2db19-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="2db19-195">Si está seguro de que tiene una suscripción de Azure, validar la asignación de su suscripción de inquilinos de Hola e inquilino correcto de hello está seleccionado en la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="2db19-195">If you're certain you have an Azure subscription, validate hello tenant mapping for your subscription and ensure hello correct tenant is selected in hello dropdown.</span></span> <span data-ttu-id="2db19-196">Si ha validado Hola deseado inquilino es correcto, siga Hola anterior diagrama y validar la asignación de Hola de su suscripción y este inquilino AAD.</span><span class="sxs-lookup"><span data-stu-id="2db19-196">If you’ve validated hello desired tenant is correct, follow hello preceding diagram and validate hello mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2db19-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2db19-197">Next steps</span></span>
<span data-ttu-id="2db19-198">toocontinue de aprendizaje sobre los conjuntos de IoT, vea cómo puede [personalizar una solución preconfigurada][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="2db19-198">toocontinue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

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

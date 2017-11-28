---
title: roles de Control de acceso basado en roles personalizados aaaCreate y asignar toointernal y los usuarios externos de Azure | Documentos de Microsoft
description: Asignar roles personalizados de RBAC creados con PowerShell y la CLI para usuarios internos y externos
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="7865c-103">Introducción al control de acceso basado en roles</span><span class="sxs-lookup"><span data-stu-id="7865c-103">Intro on role-based access control</span></span>

<span data-ttu-id="7865c-104">Control de acceso basado en roles es una característica sola portal Azure permitir a los propietarios de Hola de una suscripción tooassign roles granulares tooother quienes pueden administrar ámbitos de recurso específico en su entorno.</span><span class="sxs-lookup"><span data-stu-id="7865c-104">Role-based access control is an Azure portal only feature allowing hello owners of a subscription tooassign granular roles tooother users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="7865c-105">RBAC permite una mejor administración de seguridad para las organizaciones grandes y para PYMES trabajar con colaboradores externos, proveedores o autónomos que necesitan tener acceso a recursos de toospecific en su entorno, pero no necesariamente toda la infraestructura de toohello o cualquier ámbitos relacionados con la facturación.</span><span class="sxs-lookup"><span data-stu-id="7865c-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access toospecific resources in your environment but not necessarily toohello entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="7865c-106">RBAC ofrece flexibilidad de Hola de propietario de una suscripción de Azure administrada por la cuenta de administrador de hello (rol de administrador de servicio en un nivel de suscripción) y haber varios toowork usuarios invitados en Hola misma suscripción pero sin cualquier administrativas derechos para él.</span><span class="sxs-lookup"><span data-stu-id="7865c-106">RBAC allows hello flexibility of owning one Azure subscription managed by hello administrator account (service administrator role at a subscription level) and have multiple users invited toowork under hello same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="7865c-107">Desde una perspectiva de facturación y administración, característica RBAC Hola demuestra toobe una opción eficaz administración y tiempo para el uso de Azure en distintos escenarios.</span><span class="sxs-lookup"><span data-stu-id="7865c-107">From a management and billing perspective, hello RBAC feature proves toobe a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7865c-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7865c-108">Prerequisites</span></span>
<span data-ttu-id="7865c-109">El uso de RBAC en hello entorno de Azure requiere:</span><span class="sxs-lookup"><span data-stu-id="7865c-109">Using RBAC in hello Azure environment requires:</span></span>

* <span data-ttu-id="7865c-110">Tener una independiente de suscripción de Azure toohello usuario asignado como propietario (rol de suscripción)</span><span class="sxs-lookup"><span data-stu-id="7865c-110">Having a standalone Azure subscription assigned toohello user as owner (subscription role)</span></span>
* <span data-ttu-id="7865c-111">Tiene el rol de propietario de Hola de hello suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="7865c-111">Have hello Owner role of hello Azure subscription</span></span>
* <span data-ttu-id="7865c-112">Tener acceso toohello [portal de Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="7865c-112">Have access toohello [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="7865c-113">Asegúrese de que hello toohave después de proveedores de recursos registrado para la suscripción de usuario de hello: **Microsoft.Authorization**.</span><span class="sxs-lookup"><span data-stu-id="7865c-113">Make sure toohave hello following Resource Providers registered for hello user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="7865c-114">Para obtener más información sobre cómo tooregister Hola proveedores de recursos, consulte [proveedores del Administrador de recursos, regiones, versiones de API y esquemas](/azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="7865c-114">For more information on how tooregister hello resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7865c-115">Las suscripciones de Office 365 o licencias de Azure Active Directory (por ejemplo: obtener acceso a Active Directory tooAzure) aprovisionado desde Hola Office 365 portal no calidad usar RBAC.</span><span class="sxs-lookup"><span data-stu-id="7865c-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access tooAzure Active Directory) provisioned from hello O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="7865c-116">Uso de RBAC</span><span class="sxs-lookup"><span data-stu-id="7865c-116">How can RBAC be used</span></span>
<span data-ttu-id="7865c-117">RBAC puede aplicarse en tres ámbitos diferentes de Azure.</span><span class="sxs-lookup"><span data-stu-id="7865c-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="7865c-118">De hello mayor ámbito toohello más baja, son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="7865c-118">From hello highest scope toohello lowest one, they are as follows:</span></span>

* <span data-ttu-id="7865c-119">Suscripción (más alto)</span><span class="sxs-lookup"><span data-stu-id="7865c-119">Subscription (highest)</span></span>
* <span data-ttu-id="7865c-120">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="7865c-120">Resource group</span></span>
* <span data-ttu-id="7865c-121">Ámbito de recursos (Hola menor nivel de acceso oferta permisos destino tooan ámbito de recursos individuales de Azure)</span><span class="sxs-lookup"><span data-stu-id="7865c-121">Resource scope (hello lowest access level offering targeted permissions tooan individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a><span data-ttu-id="7865c-122">Asignar roles RBAC en el ámbito de la suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="7865c-122">Assign RBAC roles at hello subscription scope</span></span>
<span data-ttu-id="7865c-123">Hay dos ejemplos comunes (entre otros) en los que se utiliza RBAC:</span><span class="sxs-lookup"><span data-stu-id="7865c-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="7865c-124">Tener usuarios externos de organizaciones de hello (que no forma parte del inquilino de Azure Active Directory del usuario del Administrador de hello) invitó toomanage determinados recursos o suscripción todo Hola</span><span class="sxs-lookup"><span data-stu-id="7865c-124">Having external users from hello organizations (not part of hello admin user's Azure Active Directory tenant) invited toomanage certain resources or hello whole subscription</span></span>
* <span data-ttu-id="7865c-125">Trabajar con los usuarios dentro de la organización de hello (forman parte del inquilino de Azure Active Directory del usuario de hello), pero parte de los distintos equipos o grupos que necesiten acceso granular cualquier toohello suscripción completa o grupos de recursos de toocertain o el recurso ámbitos Hola entorno de</span><span class="sxs-lookup"><span data-stu-id="7865c-125">Working with users inside hello organization (they are part of hello user's Azure Active Directory tenant) but part of different teams or groups which need granular access either toohello whole subscription or toocertain resource groups or resource scopes in hello environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="7865c-126">Conceder acceso en el nivel de suscripción para un usuario fuera de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7865c-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="7865c-127">Solo se pueden conceder roles RBAC **propietarios** de suscripción de hello, por tanto, el usuario de administrador de hello debe haber iniciado con un nombre de usuario que tiene este rol asignado previamente o creó Hola suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="7865c-127">RBAC roles can be granted only by **Owners** of hello subscription therefore hello admin user must be logged with a username which has this role pre-assigned or has created hello Azure subscription.</span></span>

<span data-ttu-id="7865c-128">De hello portal de Azure, después de iniciar sesión como administrador, seleccione "Suscripciones" y seleccione Hola habían deseado uno.</span><span class="sxs-lookup"><span data-stu-id="7865c-128">From hello Azure portal, after you sign-in as admin, select “Subscriptions” and chose hello desired one.</span></span>
<span data-ttu-id="7865c-129">![hoja de suscripción en el portal de Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) de forma predeterminada, si ha adquirido el usuario de administrador de Hola Hola suscripción de Azure, usuario Hola se mostrará como **Administrador de la cuenta**, que se va a rol de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="7865c-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if hello admin user has purchased hello Azure subscription, hello user will show up as **Account Admin**, this being hello subscription role.</span></span> <span data-ttu-id="7865c-130">Para obtener más detalles sobre las funciones de suscripción de Azure de hello, consulte [agregar o cambiar roles de administrador de Azure que administran la suscripción de Hola o servicios](/billing/billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="7865c-130">For more details on hello Azure subscription roles, see [Add or change Azure administrator roles that manage hello subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="7865c-131">En este ejemplo, Hola usuario "alflanigan@outlook.com" es hello **propietario** de hello "Gratuita" suscripción en hello AAD inquilinos "Default inquilino de Azure".</span><span class="sxs-lookup"><span data-stu-id="7865c-131">In this example, hello user "alflanigan@outlook.com" is hello **Owner** of hello "Free Trial" subscription in hello AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="7865c-132">Puesto que este usuario es el creador de Hola de hello suscripción de Azure con hello inicial Account de Microsoft "Outlook" (Microsoft Account = Outlook, etc. en vivo) será el nombre de dominio predeterminado de Hola para todos los demás usuarios que agregó en este inquilino **"@alflaniganuoutlook.onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="7865c-132">Since this user is hello creator of hello Azure subscription with hello initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) hello default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="7865c-133">De forma predeterminada, sintaxis de Hola de nuevo dominio de hello está formado por que reúnan Hola nombre de usuario y nombre de dominio del usuario de Hola que creó el inquilino de Hola y Agregar extensión de hello **". onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="7865c-133">By design, hello syntax of hello new domain is formed by putting together hello username and domain name of hello user who created hello tenant and adding hello extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="7865c-134">Además, los usuarios pueden iniciar sesión con un nombre de dominio personalizado en el inquilino de hello después de agregar y comprobar de nuevo inquilino de Hola.</span><span class="sxs-lookup"><span data-stu-id="7865c-134">Furthermore, users can sign-in with a custom domain name in hello tenant after adding and verifying it for hello new tenant.</span></span> <span data-ttu-id="7865c-135">Para obtener más detalles sobre cómo tooverify un nombre de dominio personalizado en un inquilino de Azure Active Directory, vea [agregar un directorio de tooyour de nombre de dominio personalizado](/active-directory/active-directory-add-domain).</span><span class="sxs-lookup"><span data-stu-id="7865c-135">For more details on how tooverify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name tooyour directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="7865c-136">En este ejemplo, el directorio de Hola "inquilino predeterminado Azure" contiene solo los usuarios con el nombre de dominio de Hola "@alflanigan.onmicrosoft.com".</span><span class="sxs-lookup"><span data-stu-id="7865c-136">In this example, hello "Default tenant Azure" directory contains only users with hello domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="7865c-137">Después de seleccionar la suscripción de hello, debe hacer clic en el usuario de administrador de hello **Control de acceso (IAM)** y, a continuación, **agregar un nuevo rol**.</span><span class="sxs-lookup"><span data-stu-id="7865c-137">After selecting hello subscription, hello admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![Característica de control de acceso IAM en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![Agregar un nuevo usuario en la característica de control de acceso IAM en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="7865c-140">Hola siguiente paso es tooselect Hola rol toobe asignado y usuario de Hola que se asignará el rol RBAC Hola a.</span><span class="sxs-lookup"><span data-stu-id="7865c-140">hello next step is tooselect hello role toobe assigned and hello user whom hello RBAC role will be assigned to.</span></span> <span data-ttu-id="7865c-141">Hola **rol** usuario de administrador de Hola de menú desplegable ve solo Hola RBAC funciones integradas que están disponibles en Azure.</span><span class="sxs-lookup"><span data-stu-id="7865c-141">In hello **Role** dropdown menu hello admin user sees only hello built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="7865c-142">Para obtener explicaciones detalladas de cada rol y sus ámbitos asignables, consulte [Roles integrados en el control de acceso basado en roles de Azure](/active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="7865c-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="7865c-143">usuario de administrador de Hello, a continuación, debe tooadd dirección de correo electrónico de Hola de usuario externo Hola.</span><span class="sxs-lookup"><span data-stu-id="7865c-143">hello admin user then needs tooadd hello email address of hello external user.</span></span> <span data-ttu-id="7865c-144">Hola espera comportamiento es Hola usuario externo toonot aparecen en hello existente inquilino.</span><span class="sxs-lookup"><span data-stu-id="7865c-144">hello expected behavior is for hello external user toonot show up in hello existing tenant.</span></span> <span data-ttu-id="7865c-145">Una vez se ha invitado usuario externo hello, estarán visible en **suscripciones > Control de acceso (IAM)** con todos los usuarios actuales de Hola que están asignados actualmente a un rol de RBAC en hello ámbito de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="7865c-145">After hello external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all hello current users which are currently assigned an RBAC role at hello Subscription scope.</span></span>





![Agregar permisos toonew RBAC rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![Lista de roles RBAC en el nivel de suscripción](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="7865c-148">usuario Hola "chessercarlton@gmail.com" se ha invitado toobe una **propietario** para suscripción de "Prueba gratuita" hello.</span><span class="sxs-lookup"><span data-stu-id="7865c-148">hello user "chessercarlton@gmail.com" has been invited toobe an **Owner** for hello “Free Trial” subscription.</span></span> <span data-ttu-id="7865c-149">Después de enviar la invitación de hello, usuario externo Hola recibirá una confirmación por correo electrónico con un vínculo de activación.</span><span class="sxs-lookup"><span data-stu-id="7865c-149">After sending hello invitation, hello external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="7865c-150">![invitación por correo electrónico para el rol de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="7865c-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="7865c-151">Que se va a organización toohello externo, Hola nuevo usuario no tiene los atributos existentes en el directorio de "Default inquilino de Azure" Hola.</span><span class="sxs-lookup"><span data-stu-id="7865c-151">Being external toohello organization, hello new user does not have any existing attributes in hello "Default tenant Azure" directory.</span></span> <span data-ttu-id="7865c-152">Se creará una vez que concede al usuario externo de hello toobe de consentimiento que se registran en el directorio Hola que está asociado a la suscripción de Hola que se ha asignado un rol para.</span><span class="sxs-lookup"><span data-stu-id="7865c-152">They will be created after hello external user has given consent toobe recorded in hello directory which is associated with hello subscription which he has been assigned a role to.</span></span>





![Mensaje de invitación por correo electrónico para el rol de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="7865c-154">usuario externo Hello muestra de Hola inquilino de Azure Active Directory de ahora en adelante como usuario externo y se puede ver en hello portal de Azure y en el portal clásico de Hola.</span><span class="sxs-lookup"><span data-stu-id="7865c-154">hello external user shows in hello Azure Active Directory tenant from now on as external user and this can be viewed both in hello Azure portal and in hello classic portal.</span></span>





![Hoja de usuarios de Azure Active Directory en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![Hoja de usuarios de Azure Active Directory en el Portal de Azure clásico](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="7865c-157">Hola **usuarios** vista en ambos usuarios externos de portales Hola puede ser reconocida por:</span><span class="sxs-lookup"><span data-stu-id="7865c-157">In hello **Users** view in both portals hello external users can be recognized by:</span></span>

* <span data-ttu-id="7865c-158">tipo de icono diferente de Hola Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7865c-158">hello different icon type in hello Azure portal</span></span>
* <span data-ttu-id="7865c-159">Hola diferente subcontratación punto en el portal clásico de Hola</span><span class="sxs-lookup"><span data-stu-id="7865c-159">hello different sourcing point in hello classic portal</span></span>

<span data-ttu-id="7865c-160">Sin embargo, conceder **propietario** o **colaborador** usuario externo de acceso tooan en hello **suscripción** ámbito, no permite que el directorio del usuario de administrador de hello acceso toohello, a menos que hello **administrador Global** lo permite.</span><span class="sxs-lookup"><span data-stu-id="7865c-160">However, granting **Owner** or **Contributor** access tooan external user at hello **Subscription** scope, does not allow hello access toohello admin user's directory, unless hello **Global Admin** allows it.</span></span> <span data-ttu-id="7865c-161">En Propiedades del usuario hello, Hola **usuario tipo** que tiene dos parámetros comunes, **miembro** y **invitado** pueden identificarse.</span><span class="sxs-lookup"><span data-stu-id="7865c-161">In hello user proprieties,  hello **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="7865c-162">Un miembro es un usuario que está registrado en el directorio de hello mientras un invitado es un directorio de toohello de usuario invitado desde un origen externo.</span><span class="sxs-lookup"><span data-stu-id="7865c-162">A member is a user which is registered in hello directory while a guest is a user invited toohello directory from an external source.</span></span> <span data-ttu-id="7865c-163">Para más información, consulte [¿Cómo agregan los administradores de Azure Active Directory usuarios de colaboración B2B?](/active-directory/active-directory-b2b-admin-add-users)</span><span class="sxs-lookup"><span data-stu-id="7865c-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="7865c-164">Asegúrese de que, después de escribir las credenciales de hello en el portal de hello, usuario externo Hola selecciona directorio correcto de hello toosign en.</span><span class="sxs-lookup"><span data-stu-id="7865c-164">Make sure that after entering hello credentials in hello portal, hello external user selects hello correct directory toosign-in to.</span></span> <span data-ttu-id="7865c-165">Hello mismo usuario puede tener acceso toomultiple directorios y puede seleccionar cualquiera de ellas haciendo clic en el nombre de usuario de hello en el lado derecho superior de Hola Hola portal de Azure y, a continuación, elija directorio adecuado de hello en lista de desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="7865c-165">hello same user can have access toomultiple directories and can select either one of  them by clicking hello username in hello top right-hand side in hello Azure portal and then choose hello appropriate directory from hello dropdown list.</span></span>

<span data-ttu-id="7865c-166">Al que se va a un invitado en el directorio de hello, usuario externo Hola puede administrar todos los recursos para hello suscripción de Azure, pero no puede obtener acceso a directorio Hola.</span><span class="sxs-lookup"><span data-stu-id="7865c-166">While being a guest in hello directory, hello external user can manage all resources for hello Azure subscription, but can't access hello directory.</span></span>





![portal de Azure active directory acceso restringido tooazure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="7865c-168">Azure Active Directory y una suscripción de Azure no tienen una relación de primario-secundario como tienen otros recursos de Azure (por ejemplo: las máquinas virtuales, las redes virtuales, las aplicaciones web, el almacenamiento, etc.) en una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="7865c-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="7865c-169">Todos Hola este último se crea, administra y factura en una suscripción de Azure, mientras que una suscripción de Azure es toomanage usado Hola acceso tooan directorio de Azure.</span><span class="sxs-lookup"><span data-stu-id="7865c-169">All hello latter is created, managed and billed under an Azure subscription while an Azure subscription is used toomanage hello access tooan Azure directory.</span></span> <span data-ttu-id="7865c-170">Para obtener más información, consulte [suscripción de Azure cómo está relacionado tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span><span class="sxs-lookup"><span data-stu-id="7865c-170">For more details, see [How an Azure subscription is related tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="7865c-171">Todas las funciones RBAC de hello integrados, **propietario** y **colaborador** ofrecen acceso a la administración completa tooall recursos en entorno de hello, Hola diferencia es que no se puede crear un colaborador y delete nueva Funciones RBAC.</span><span class="sxs-lookup"><span data-stu-id="7865c-171">From all hello built-in RBAC roles, **Owner** and **Contributor** offer full management access tooall resources in hello environment, hello difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="7865c-172">Hello otras funciones integradas, como **colaborador de la máquina Virtual** ofrecen acceso a la administración completa únicamente los recursos de toohello indicados por el nombre de hello, independientemente de hello **grupo de recursos** se están creando a.</span><span class="sxs-lookup"><span data-stu-id="7865c-172">hello other built-in roles like **Virtual Machine Contributor** offer full management access only toohello resources indicated by hello name, regardless of hello **Resource Group** they are being created into.</span></span>

<span data-ttu-id="7865c-173">Rol Hola RBAC integrado asignación de **colaborador de la máquina Virtual** en un nivel de suscripción, significa que ese rol de Hola Hola asignados al usuario:</span><span class="sxs-lookup"><span data-stu-id="7865c-173">Assigning hello built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that hello user assigned hello role:</span></span>

* <span data-ttu-id="7865c-174">Puede ver todas las máquinas virtuales independientemente de sus implementación hello y fecha de grupos de recursos que forman parte de</span><span class="sxs-lookup"><span data-stu-id="7865c-174">Can view all virtual machines regardless their deployment date and hello resource groups they are part of</span></span>
* <span data-ttu-id="7865c-175">Tiene máquinas virtuales de administración completa acceso toohello de suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="7865c-175">Has full management access toohello virtual machines in hello subscription</span></span>
* <span data-ttu-id="7865c-176">No se puede ver otros tipos de recursos de suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="7865c-176">Can't view any other resource types in hello subscription</span></span>
* <span data-ttu-id="7865c-177">No puede realizar ningún cambio desde la perspectiva de facturación.</span><span class="sxs-lookup"><span data-stu-id="7865c-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="7865c-178">Que se va a una característica única portal Azure de RBAC, no concede portal clásico de toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="7865c-178">RBAC being an Azure portal only feature, it doesn't grant access toohello classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a><span data-ttu-id="7865c-179">Asignar a un usuario externo de RBAC rol tooan integrado</span><span class="sxs-lookup"><span data-stu-id="7865c-179">Assign a built-in RBAC role tooan external user</span></span>
<span data-ttu-id="7865c-180">Para un escenario diferente en esta prueba, Hola usuario externo "alflanigan@gmail.com" se agrega como un **colaborador de la máquina Virtual**.</span><span class="sxs-lookup"><span data-stu-id="7865c-180">For a different scenario in this test, hello external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![Rol integrado de colaborador de la máquina virtual](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="7865c-182">el comportamiento normal de este usuario externo a este rol integrada de Hello es toosee y administrar solo las máquinas virtuales y su adyacentes Administrador de recursos solo recursos necesario al implementar.</span><span class="sxs-lookup"><span data-stu-id="7865c-182">hello normal behavior for this external user with this built-in role is toosee and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="7865c-183">De forma predeterminada, estos roles limitados proporcionan acceso solo tootheir de recursos correspondiente creados en hello portal de Azure, a pesar de todo algunos todavía se pueden implementar en el portal de clásico de hello (por ejemplo: máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="7865c-183">By design, these limited roles offer access only tootheir correspondent resources created in hello Azure portal, regardless some can still be deployed in hello classic portal as well (for example: virtual machines).</span></span>





![Información general sobre el rol de colaborador de la máquina virtual en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a><span data-ttu-id="7865c-185">Conceder acceso en un nivel de suscripción de un usuario en hello mismo directorio</span><span class="sxs-lookup"><span data-stu-id="7865c-185">Grant access at a subscription level for a user in hello same directory</span></span>
<span data-ttu-id="7865c-186">flujo del proceso de Hello es idéntico tooadding un usuario externo, tanto de hello perspectiva concediendo Hola RBAC el rol Administrador, así como usuario Hola se concede el rol de acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="7865c-186">hello process flow is identical tooadding an external user, both from hello admin perspective granting hello RBAC role as well as hello user being granted access toohello role.</span></span> <span data-ttu-id="7865c-187">Hola diferencia es que el usuario invitado de hello no recibirán las invitaciones de correo electrónico ya que todos los ámbitos de recursos de hello dentro de suscripción de hello estarán disponibles en el panel de hello tras iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="7865c-187">hello difference here is that hello invited user will not receive any email invitations as all hello resource scopes within hello subscription will be available in hello dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a><span data-ttu-id="7865c-188">Asignar roles RBAC en el ámbito de grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="7865c-188">Assign RBAC roles at hello resource group scope</span></span>
<span data-ttu-id="7865c-189">Asignar un rol de RBAC en una **grupo de recursos** ámbito tiene un proceso idéntico para la asignación de rol de hello en nivel de suscripción de hello, para ambos tipos de usuarios: internos o externos (parte de hello mismo directorio).</span><span class="sxs-lookup"><span data-stu-id="7865c-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning hello role at hello subscription level, for both types of users - either external or internal (part of hello same directory).</span></span> <span data-ttu-id="7865c-190">Hola a los usuarios que se asignan roles RBAC hello es toosee en su entorno solo el grupo de recursos de hello les ha asignado acceso de hello **grupos de recursos** icono Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7865c-190">hello users which are assigned hello RBAC role is toosee in their environment only hello resource group they have been assigned access from hello **Resource Groups** icon in hello Azure portal.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-scope"></a><span data-ttu-id="7865c-191">Asignar roles RBAC en el ámbito de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="7865c-191">Assign RBAC roles at hello resource scope</span></span>
<span data-ttu-id="7865c-192">Asignar un rol RBAC en un ámbito de recursos en Azure tiene un proceso idéntico para la asignación de rol de hello en nivel de suscripción de Hola o en el nivel de grupo de recursos de hello, siguiente Hola mismo flujo de trabajo para ambos escenarios.</span><span class="sxs-lookup"><span data-stu-id="7865c-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning hello role at hello subscription level or at hello resource group level, following hello same workflow for both scenarios.</span></span> <span data-ttu-id="7865c-193">Una vez más, los usuarios de Hola que se asignan roles RBAC Hola pueden ver únicamente los elementos de Hola que les ha asignado acceso a cualquier hello en **todos los recursos** ficha o directamente en su panel.</span><span class="sxs-lookup"><span data-stu-id="7865c-193">Again, hello users which are assigned hello RBAC role can see only hello items that they have been assigned access to, either in hello **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="7865c-194">Es un aspecto importante de RBAC tanto en el ámbito de grupo de recursos o ámbito de recursos para el directorio correcto de hello usuarios toomake seguro toosign de toohello.</span><span class="sxs-lookup"><span data-stu-id="7865c-194">An important aspect for RBAC both at resource group scope or resource scope is for hello users toomake sure toosign-in toohello correct directory.</span></span>





![Inicio de sesión en un directorio en Azure Portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="7865c-196">Asignación de roles de RBAC en un grupo de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7865c-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="7865c-197">Todos los escenarios de hello mediante RBAC en tres ámbitos diferentes hello en los privilegios de Hola de oferta de Azure de administrar, implementar y administrar diversos recursos como un usuario asignado sin Hola de necesitan de la administración de una suscripción personal.</span><span class="sxs-lookup"><span data-stu-id="7865c-197">All hello scenarios using RBAC at hello three different scopes in Azure offer hello privilege of managing, deploying and administering various resources as an assigned user without hello need of managing a personal subscription.</span></span> <span data-ttu-id="7865c-198">Se asigna el rol RBAC de hello sin tener en cuenta para una suscripción, el grupo de recursos o el ámbito de recursos, todos los recursos de hello creados más adelante los usuarios de hello asignado se facturan en hello una suscripción de Azure donde los usuarios de hello tienen acceso a.</span><span class="sxs-lookup"><span data-stu-id="7865c-198">Regardless hello RBAC role is assigned for a subscription, resource group or resource scope, all hello resources created further on by hello assigned users are billed under hello one Azure subscription where hello users have access to.</span></span> <span data-ttu-id="7865c-199">De esta manera, hello los usuarios que tienen permisos de administrador para esa suscripción de Azure completo de facturación tiene información general completa en el consumo de hello, sin tener en cuenta que va a administrar recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7865c-199">This way, hello users who have billing administrator permissions for that entire Azure subscription has a complete overview on hello consumption, regardless who is managing hello resources.</span></span>

<span data-ttu-id="7865c-200">Para las organizaciones grandes, se pueden aplicar funciones RBAC en hello igual en grupos de Azure Active Directory teniendo en cuenta la perspectiva de hello ese usuario de administrador de hello desea acceso granular de toogrant Hola para equipos o departamentos completos, no individualmente para cada usuario, por lo tanto teniendo en cuenta, como mucho tiempo y la administración eficaz opción.</span><span class="sxs-lookup"><span data-stu-id="7865c-200">For larger organizations, RBAC roles can be applied in hello same way for Azure Active Directory groups considering hello perspective that hello admin user wants toogrant hello granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="7865c-201">tooillustrate este ejemplo, hello **colaborador** rol se ha agregado tooone de grupos de hello en el inquilino de hello en nivel de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="7865c-201">tooillustrate this example, hello **Contributor** role has been added tooone of hello groups in hello tenant at hello subscription level.</span></span>





![Agregar rol de RBAC para grupos de AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="7865c-203">Estos grupos son grupos de seguridad que se aprovisionan y administran únicamente dentro de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7865c-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a><span data-ttu-id="7865c-204">Crear un tooopen compatibilidad personalizada de RBAC rol solicitudes mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="7865c-204">Create a custom RBAC role tooopen support requests using PowerShell</span></span>
<span data-ttu-id="7865c-205">Hola integrada RBAC las funciones que están disponibles en Azure Asegúrese de determinados niveles de permiso basados en los recursos disponibles en el entorno de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="7865c-205">hello built-in RBAC roles which are available in Azure ensure certain permission levels based on hello available resources in hello environment.</span></span> <span data-ttu-id="7865c-206">Sin embargo, si ninguno de estos roles se ajustan a las necesidades del usuario del Administrador de hello, hay acceso de toolimit de opción de hello aún más mediante la creación de roles personalizados de RBAC.</span><span class="sxs-lookup"><span data-stu-id="7865c-206">However, if none of these roles suit hello admin user's needs, there is hello option toolimit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="7865c-207">Crear roles personalizados de RBAC requiere tootake un rol integrado, modificarlo y, a continuación, importarlo en el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="7865c-207">Creating custom RBAC roles requires tootake one built-in role, edit it and then import it back in hello environment.</span></span> <span data-ttu-id="7865c-208">descarga de Hola y la carga de rol de Hola se administran mediante PowerShell o CLI.</span><span class="sxs-lookup"><span data-stu-id="7865c-208">hello download and upload of hello role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="7865c-209">Es importante toounderstand Hola requisitos previos de creación de una función personalizada que pueden conceder acceso granular en nivel de suscripción de Hola y también permiten Hola invitado usuario Hola flexibilidad de abrir solicitudes de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="7865c-209">It is important toounderstand hello prerequisites of creating a custom role which can grant granular access at hello subscription level and also allow hello invited user hello flexibility of opening support requests.</span></span>

<span data-ttu-id="7865c-210">Para este rol integradas de ejemplo Hola **lector** que permite a los usuarios acceso tooview todos los recursos de hello ámbitos pero no tooedit o crear nuevos ha sido personalizado tooallow Hola Hola opción de usuario de las solicitudes de soporte técnico de apertura.</span><span class="sxs-lookup"><span data-stu-id="7865c-210">For this example hello built-in role **Reader** which allows users access tooview all hello resource scopes but not tooedit them or create new ones has been customized tooallow hello user hello option of opening support requests.</span></span>

<span data-ttu-id="7865c-211">Hola la primera acción de exportación de hello **lector** rol necesidades toobe completado en PowerShell se ejecutaron con permisos elevados como administrador.</span><span class="sxs-lookup"><span data-stu-id="7865c-211">hello first action of exporting hello **Reader** role needs toobe completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Captura de pantalla de PowerShell para el rol Lector de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="7865c-213">A continuación, debe tooextract plantilla JSON Hola de rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="7865c-213">Then you need tooextract hello JSON template of hello role.</span></span>





![Plantilla JSON para el rol personalizado Lector de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="7865c-215">Un rol de RBAC típico se compone de tres secciones principales, **Actions**, **NotActions** y **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="7865c-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="7865c-216">Hola **acción** sección se enumeran todas las operaciones permitidas para este rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="7865c-216">In hello **Action** section are listed all hello permitted operations for this role.</span></span> <span data-ttu-id="7865c-217">Es importante toounderstand que se asigna cada acción desde un proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="7865c-217">It's important toounderstand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="7865c-218">En este caso, para crear Hola de incidencias de soporte técnico **Microsoft.Support** debe aparecer el proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="7865c-218">In this case, for creating support tickets hello **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="7865c-219">toobe puede toosee Hola a todos los proveedores de recursos disponibles y registrados en su suscripción, puede usar PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7865c-219">toobe able toosee all hello resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="7865c-220">Además, puede comprobar para hello todos Hola disponible PowerShell cmdlets toomanage Hola proveedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="7865c-220">Additionally, you can check for hello all hello available PowerShell cmdlets toomanage hello resource providers.</span></span>
    <span data-ttu-id="7865c-221">![Captura de pantalla de PowerShell para la administración de proveedores de recursos](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="7865c-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="7865c-222">toorestrict todos Hola acciones para un rol determinado de RBAC, recursos proveedores aparecen en la sección de hello **NotActions**.</span><span class="sxs-lookup"><span data-stu-id="7865c-222">toorestrict all hello actions for a particular RBAC role, resource providers are listed under hello section **NotActions**.</span></span>
<span data-ttu-id="7865c-223">Por último, es obligatorio que ese rol RBAC hello contiene suscripción explícita Hola identificadores que se utiliza.</span><span class="sxs-lookup"><span data-stu-id="7865c-223">Last, it's mandatory that hello RBAC role contains hello explicit subscription IDs where it is used.</span></span> <span data-ttu-id="7865c-224">Hello Id. de suscripción aparecen en hello **AssignableScopes**, en caso contrario no se permitirán rol de hello tooimport en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="7865c-224">hello subscription IDs are listed under hello **AssignableScopes**, otherwise you will not be allowed tooimport hello role in your subscription.</span></span>

<span data-ttu-id="7865c-225">Después de crear y personalizar Hola RBAC rol, debe toobe entorno de hello atrás importados.</span><span class="sxs-lookup"><span data-stu-id="7865c-225">After creating and customizing hello RBAC role, it needs toobe imported back hello environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="7865c-226">En este ejemplo, nombre personalizado de Hola para este rol RBAC es "Reader soporte vales nivel de acceso" Permitir Hola usuario tooview todo en suscripción de Hola y también las solicitudes de soporte técnico de tooopen.</span><span class="sxs-lookup"><span data-stu-id="7865c-226">In this example, hello custom name for this RBAC role is "Reader support tickets access level" allowing hello user tooview everything in hello subscription and also tooopen support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="7865c-227">son Hello solo dos funciones RBAC integradas que permiten acción Hola de apertura de solicitudes de soporte técnico **propietario** y **colaborador**.</span><span class="sxs-lookup"><span data-stu-id="7865c-227">hello only two built-in RBAC roles allowing hello action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="7865c-228">Para una solicitud de soporte de usuario toobe tooopen capaz de debe asignarse un rol RBAC solo en el ámbito de la suscripción de hello, ya que todas las solicitudes de soporte técnico se crean en función de una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="7865c-228">For a user toobe able tooopen support requests, he must be assigned an RBAC role only at hello subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="7865c-229">Este nuevo rol de seguridad se ha asignado el usuario tooan de hello mismo directorio.</span><span class="sxs-lookup"><span data-stu-id="7865c-229">This new custom role has been assigned tooan user from hello same directory.</span></span>





![captura de pantalla de roles personalizados de RBAC importó Hola portal de Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![captura de pantalla de asignación personalizada importada RBAC rol toouser Hola mismo directorio](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![Captura de pantalla de los permisos de un rol importado personalizado de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="7865c-233">ejemplo de Hola ha sido aún más detallada tooemphasize Hola límites de este rol RBAC personalizado como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="7865c-233">hello example has been further detailed tooemphasize hello limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="7865c-234">Puede crear nuevas solicitudes de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="7865c-234">Can create new support requests</span></span>
* <span data-ttu-id="7865c-235">No puede crear nuevos ámbitos de recursos (por ejemplo: máquinas virtuales)</span><span class="sxs-lookup"><span data-stu-id="7865c-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="7865c-236">No puede crear nuevos grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="7865c-236">Can't create new resource groups</span></span>





![Captura de pantalla de un rol personalizado de RBAC que puede crear solicitudes de soporte técnico](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![captura de pantalla de funciones RBAC personalizado no se puede toocreate máquinas virtuales](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![captura de pantalla de funciones RBAC personalizado no se puede toocreate RGs nueva](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a><span data-ttu-id="7865c-240">Crear un tooopen compatibilidad personalizada de RBAC rol solicitudes mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="7865c-240">Create a custom RBAC role tooopen support requests using Azure CLI</span></span>
<span data-ttu-id="7865c-241">La ejecución en un equipo Mac y sin necesidad de acceso tooPowerShell, CLI de Azure es Hola forma toogo.</span><span class="sxs-lookup"><span data-stu-id="7865c-241">Running on a Mac and without having access tooPowerShell, Azure CLI is hello way toogo.</span></span>

<span data-ttu-id="7865c-242">Hola pasos toocreate un rol personalizado son Hola igual, con excepción de hello único que usan CLI rol hello no se pueden descargar en una plantilla JSON, pero puede verse en hello CLI.</span><span class="sxs-lookup"><span data-stu-id="7865c-242">hello steps toocreate a custom role are hello same, with hello sole exception that using CLI hello role can't be downloaded in a JSON template, but it can be viewed in hello CLI.</span></span>

<span data-ttu-id="7865c-243">En este ejemplo he elegido rol integrado de Hola de **lector de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="7865c-243">For this example I have chosen hello built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![Captura de pantalla de la CLI que muestra un rol de lector de copia de seguridad](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="7865c-245">Editar rol hello en Visual Studio después de copiar propiedades de hello en una plantilla JSON, Hola **Microsoft.Support** proveedor de recursos se ha agregado en hello **acciones** secciones para que puedan abrir este usuario solicitudes de soporte técnico mientras continúa toobe un lector para almacenes de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="7865c-245">Editing hello role in Visual Studio after copying hello proprieties in a JSON template, hello **Microsoft.Support** resource provider has been added in hello **Actions** sections so that this user can open support requests while continuing toobe a reader for hello backup vaults.</span></span> <span data-ttu-id="7865c-246">Nuevo es Id. de suscripción de hello tooadd necesarios donde se usará este rol en hello **AssignableScopes** sección.</span><span class="sxs-lookup"><span data-stu-id="7865c-246">Again it is necessary tooadd hello subscription ID where this role will be used in hello **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![Captura de pantalla de la CLI con la importación de un rol personalizado de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="7865c-248">nuevo rol de Hello ahora está disponible en hello portal de Azure y proceso de assignation Hola Hola mismo como en ejemplos anteriores Hola.</span><span class="sxs-lookup"><span data-stu-id="7865c-248">hello new role is now available in hello Azure portal and hello assignation process is hello same as in hello previous examples.</span></span>





![Captura de pantalla de Azure Portal de un rol personalizado de RBAC creado con la CLI 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="7865c-250">A partir de hello 2017 de compilación más reciente, Hola Shell en la nube de Azure está generalmente disponible.</span><span class="sxs-lookup"><span data-stu-id="7865c-250">As of hello latest Build 2017, hello Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="7865c-251">Shell de nube de Azure es un complemento tooIDE y Hola Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7865c-251">Azure Cloud Shell is a complement tooIDE and hello Azure Portal.</span></span> <span data-ttu-id="7865c-252">Con este servicio, tiene un shell basado en explorador, autenticado y hospedado en Azure, que puede usar en lugar de la CLI instalada en su equipo.</span><span class="sxs-lookup"><span data-stu-id="7865c-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)

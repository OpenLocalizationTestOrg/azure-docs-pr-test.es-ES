---
title: las aplicaciones aaaHow aparecen en el panel de acceso de hello | Documentos de Microsoft
description: "Solucionar problemas de por qué aparece una aplicación Hola Panel de acceso"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a><span data-ttu-id="0e964-103">Cómo aparecen las aplicaciones en el panel de acceso de Hola</span><span class="sxs-lookup"><span data-stu-id="0e964-103">How applications appear on hello access panel</span></span>

<span data-ttu-id="0e964-104">Hola Panel de acceso es un portal basado en web que permite a los usuarios con un trabajo o cuenta educativa en aplicaciones de Azure Active Directory (Azure AD) tooview y de inicio en la nube que Hola Administrador de Azure AD le haya concedido acceso a.</span><span class="sxs-lookup"><span data-stu-id="0e964-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="0e964-105">Estas aplicaciones se configuran en nombre de usuario de hello en el portal de Azure AD Hola.</span><span class="sxs-lookup"><span data-stu-id="0e964-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="0e964-106">Hola, administrador puede aprovisionar directamente usuario de toohello la aplicación Hola o un grupo de tooa que un usuario forma parte de lo que en la aplicación hello que aparecen en el Panel de acceso del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e964-106">hello admin can provision hello application toohello user directly or tooa group a user is part of resulting in hello application appearing on hello user’s Access Panel.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="0e964-107">General emite toocheck primero</span><span class="sxs-lookup"><span data-stu-id="0e964-107">General issues toocheck first</span></span>

-   <span data-ttu-id="0e964-108">Si se acaba de quitar una aplicación de un usuario o grupo Hola usuario es miembro de, toosign de entrada y salida vuelva a intentarlo en el Panel de acceso del usuario de hello después de unos toosee minutos si se quita la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0e964-108">If an application was just removed from a user or group hello user is a member of, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is removed.</span></span>

-   <span data-ttu-id="0e964-109">Si se acaba de quitar una licencia a un usuario o grupo de usuario de hello es que un miembro de este puede tardar mucho tiempo, según el tamaño de Hola y la complejidad del grupo de Hola para toobe cambios realizado.</span><span class="sxs-lookup"><span data-stu-id="0e964-109">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="0e964-110">Permitir un tiempo adicional antes de iniciar sesión en el Panel de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e964-110">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="0e964-111">Problemas relacionados tooassigning aplicaciones toousers</span><span class="sxs-lookup"><span data-stu-id="0e964-111">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="0e964-112">Un usuario puede estar viendo una aplicación en su Panel de acceso porque le asignase previamente tooit.</span><span class="sxs-lookup"><span data-stu-id="0e964-112">A user may be seeing an application on their Access Panel because they had been previously assigned tooit.</span></span> <span data-ttu-id="0e964-113">A continuación se muestran algunas maneras toocheck:</span><span class="sxs-lookup"><span data-stu-id="0e964-113">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="0e964-114">Comprobar si un usuario se ha asignado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="0e964-114">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="0e964-115">Comprobar si un usuario está sometido a una licencia relacionados con la aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="0e964-115">Check if a user is under a license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="0e964-116">Comprobar si un usuario se ha asignado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="0e964-116">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="0e964-117">toocheck si se asigna a un usuario toohello aplicación, siga Hola pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0e964-117">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="0e964-118">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="0e964-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0e964-119">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="0e964-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0e964-120">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="0e964-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0e964-121">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0e964-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0e964-122">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0e964-122">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="0e964-123">**Búsqueda** como nombre de Hola de aplicación hello en cuestión.</span><span class="sxs-lookup"><span data-stu-id="0e964-123">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="0e964-124">Haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0e964-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="0e964-125">Compruebe toosee si el usuario se le asigna la aplicación toohello.</span><span class="sxs-lookup"><span data-stu-id="0e964-125">Check toosee if your user is assigned toohello application.</span></span>

  * <span data-ttu-id="0e964-126">Si desea que tooremove Hola usuario de la aplicación hello, **haga clic en la fila de hello** del usuario de Hola y seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="0e964-126">If you want tooremove hello user from hello application, **click hello row** of hello user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="0e964-127">Comprobar si un usuario está sometido a una licencia relacionados con la aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="0e964-127">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="0e964-128">toocheck un usuario había asignado licencias, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="0e964-128">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="0e964-129">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="0e964-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0e964-130">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="0e964-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0e964-131">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="0e964-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0e964-132">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e964-132">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="0e964-133">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0e964-133">click **All users**.</span></span>

6.  <span data-ttu-id="0e964-134">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="0e964-134">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="0e964-135">Haga clic en **licencias** toosee qué usuario de hello licencias actualmente tiene asignada.</span><span class="sxs-lookup"><span data-stu-id="0e964-135">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

   * <span data-ttu-id="0e964-136">Si se asigna la licencia de Office tooan Esto activar tooappear de las aplicaciones de Office de primera entidad de usuario de Hola Hola Panel de acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="0e964-136">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="0e964-137">Problemas relacionados tooassigning aplicaciones toogroups</span><span class="sxs-lookup"><span data-stu-id="0e964-137">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="0e964-138">Un usuario puede estar viendo una aplicación en su Panel de acceso ya que forman parte de un grupo que se ha asignado la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="0e964-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="0e964-139">A continuación se muestran algunas maneras toocheck:</span><span class="sxs-lookup"><span data-stu-id="0e964-139">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="0e964-140">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="0e964-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="0e964-141">Comprobar si un usuario es miembro de un grupo asignado tooa licencia</span><span class="sxs-lookup"><span data-stu-id="0e964-141">Check if a user is a member of a group assigned tooa license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="0e964-142">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="0e964-142">Check a user’s group memberships</span></span>

<span data-ttu-id="0e964-143">toocheck pertenencia de un grupo, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="0e964-143">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="0e964-144">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="0e964-144">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0e964-145">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="0e964-145">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0e964-146">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="0e964-146">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0e964-147">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e964-147">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="0e964-148">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0e964-148">click **All users**.</span></span>

6.  <span data-ttu-id="0e964-149">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="0e964-149">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="0e964-150">Haga clic en **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="0e964-150">click **Groups.**</span></span>

8.  <span data-ttu-id="0e964-151">Compruebe toosee si el usuario es parte de una aplicación de toohello de grupo asignado.</span><span class="sxs-lookup"><span data-stu-id="0e964-151">Check toosee if your user is part of a Group assigned toohello application.</span></span>

   * <span data-ttu-id="0e964-152">Si desea que tooremove Hola usuario del grupo de hello, **haga clic en la fila de hello** del grupo de Hola y seleccione Eliminar.</span><span class="sxs-lookup"><span data-stu-id="0e964-152">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a><span data-ttu-id="0e964-153">Comprobar si un usuario es miembro de un grupo asignado tooa licencia</span><span class="sxs-lookup"><span data-stu-id="0e964-153">Check if a user is a member of a group assigned tooa license</span></span>

1.  <span data-ttu-id="0e964-154">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="0e964-154">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0e964-155">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="0e964-155">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0e964-156">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="0e964-156">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0e964-157">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e964-157">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="0e964-158">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0e964-158">click **All users**.</span></span>

6.  <span data-ttu-id="0e964-159">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="0e964-159">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="0e964-160">Haga clic en **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="0e964-160">click **Groups.**</span></span>

8.  <span data-ttu-id="0e964-161">Haga clic en la fila de Hola de un grupo específico.</span><span class="sxs-lookup"><span data-stu-id="0e964-161">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="0e964-162">Haga clic en **licencias** toosee qué grupo de licencias Hola asignó tooit.</span><span class="sxs-lookup"><span data-stu-id="0e964-162">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

  * <span data-ttu-id="0e964-163">Si se asigna el grupo de hello licencia de Office tooan en que esto, puede habilitar determinada tooappear de las aplicaciones de Office de primera entidad Hola Panel de acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="0e964-163">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="0e964-164">Si estos pasos no Hola resolver el problema de Hola</span><span class="sxs-lookup"><span data-stu-id="0e964-164">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="0e964-165">Abra una incidencia de soporte técnico con hello siguiente información si está disponible:</span><span class="sxs-lookup"><span data-stu-id="0e964-165">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="0e964-166">Id. de error de correlación</span><span class="sxs-lookup"><span data-stu-id="0e964-166">Correlation error ID</span></span>

-   <span data-ttu-id="0e964-167">UPN (dirección de correo electrónico del usuario)</span><span class="sxs-lookup"><span data-stu-id="0e964-167">UPN (user email address)</span></span>

-   <span data-ttu-id="0e964-168">Id. de inquilino</span><span class="sxs-lookup"><span data-stu-id="0e964-168">Tenant ID</span></span>

-   <span data-ttu-id="0e964-169">Tipo de explorador</span><span class="sxs-lookup"><span data-stu-id="0e964-169">Browser type</span></span>

-   <span data-ttu-id="0e964-170">Zona horaria y hora/período de tiempo durante el que se produce el error</span><span class="sxs-lookup"><span data-stu-id="0e964-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="0e964-171">Seguimientos de Fiddler</span><span class="sxs-lookup"><span data-stu-id="0e964-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e964-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e964-172">Next steps</span></span>
[<span data-ttu-id="0e964-173">Administración de aplicaciones con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e964-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)

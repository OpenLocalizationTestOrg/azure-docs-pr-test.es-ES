---
title: "Cómo aparecen las aplicaciones en el panel de acceso | Microsoft Docs"
description: "Solucionar por qué una aplicación no aparece en el panel de acceso"
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
ms.openlocfilehash: f8ccf2cf66b49940bc7f2b9f4764020efc04838e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-applications-appear-on-the-access-panel"></a><span data-ttu-id="765b8-103">Cómo aparecen las aplicaciones en el panel de acceso</span><span class="sxs-lookup"><span data-stu-id="765b8-103">How applications appear on the access panel</span></span>

<span data-ttu-id="765b8-104">El panel de acceso es un portal basado en web que permite que un usuario con una cuenta profesional o educativa de Azure Active Directory (Azure AD) vea e inicie las aplicaciones basadas en la nube a las que el administrador de Azure AD le ha concedido acceso.</span><span class="sxs-lookup"><span data-stu-id="765b8-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="765b8-105">Estas aplicaciones se configuran en nombre del usuario en el portal de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="765b8-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="765b8-106">El administrador puede aprovisionar la aplicación para el usuario directamente o para un grupo del que el usuario forma parte con lo cual la aplicación aparecerá en el panel de acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="765b8-106">The admin can provision the application to the user directly or to a group a user is part of resulting in the application appearing on the user’s Access Panel.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="765b8-107">Problemas generales para comprobar primero</span><span class="sxs-lookup"><span data-stu-id="765b8-107">General issues to check first</span></span>

-   <span data-ttu-id="765b8-108">Si se acaba de quitar una aplicación a un usuario o a un grupo al que este pertenece, intente volver a iniciar y cerrar sesión en el panel de acceso del usuario después de unos minutos para ver si la aplicación se ha quitado.</span><span class="sxs-lookup"><span data-stu-id="765b8-108">If an application was just removed from a user or group the user is a member of, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is removed.</span></span>

-   <span data-ttu-id="765b8-109">Si se acaba de quitar una licencia de un usuario o grupo del que el usuario es miembro, los cambios pueden tardar tiempo, en función del tamaño y la complejidad del grupo.</span><span class="sxs-lookup"><span data-stu-id="765b8-109">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="765b8-110">Espere un poco más de tiempo antes de iniciar sesión en el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="765b8-110">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="765b8-111">Problemas relacionados con la asignación de aplicaciones a los usuarios</span><span class="sxs-lookup"><span data-stu-id="765b8-111">Problems related to assigning applications to users</span></span>

<span data-ttu-id="765b8-112">Un usuario puede ver una aplicación en su panel de acceso si ya se le había asignado previamente a él.</span><span class="sxs-lookup"><span data-stu-id="765b8-112">A user may be seeing an application on their Access Panel because they had been previously assigned to it.</span></span> <span data-ttu-id="765b8-113">A continuación se muestran algunas maneras de comprobarlo:</span><span class="sxs-lookup"><span data-stu-id="765b8-113">Below are some ways to check:</span></span>

-   [<span data-ttu-id="765b8-114">Comprobar si un usuario está asignado a la aplicación</span><span class="sxs-lookup"><span data-stu-id="765b8-114">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="765b8-115">Comprobar si un usuario posee una licencia relacionada con la aplicación</span><span class="sxs-lookup"><span data-stu-id="765b8-115">Check if a user is under a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="765b8-116">Comprobar si un usuario está asignado a la aplicación</span><span class="sxs-lookup"><span data-stu-id="765b8-116">Check if a user is assigned to the application</span></span>

<span data-ttu-id="765b8-117">Para comprobar si un usuario está asignado a la aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="765b8-117">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="765b8-118">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="765b8-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="765b8-119">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="765b8-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="765b8-120">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="765b8-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="765b8-121">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="765b8-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="765b8-122">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="765b8-122">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="765b8-123">**Busque** el nombre de la aplicación en cuestión.</span><span class="sxs-lookup"><span data-stu-id="765b8-123">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="765b8-124">Haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="765b8-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="765b8-125">Compruebe si el usuario está asignado a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="765b8-125">Check to see if your user is assigned to the application.</span></span>

  * <span data-ttu-id="765b8-126">Si desea quitar el usuario de la aplicación, **haga clic en la fila** del usuario y seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="765b8-126">If you want to remove the user from the application, **click the row** of the user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="765b8-127">Comprobar si un usuario posee una licencia relacionada con la aplicación</span><span class="sxs-lookup"><span data-stu-id="765b8-127">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="765b8-128">Para comprobar las licencias asignadas de un usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="765b8-128">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="765b8-129">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="765b8-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="765b8-130">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="765b8-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="765b8-131">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="765b8-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="765b8-132">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="765b8-132">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="765b8-133">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="765b8-133">click **All users**.</span></span>

6.  <span data-ttu-id="765b8-134">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="765b8-134">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="765b8-135">Haga clic en **Licencias** para ver qué licencias tiene asignadas actualmente el usuario.</span><span class="sxs-lookup"><span data-stu-id="765b8-135">click **Licenses** to see which licenses the user currently has assigned.</span></span>

   * <span data-ttu-id="765b8-136">Si el usuario está asignado a una licencia de Office, esto permitirá que las aplicaciones de Office aparezcan en el panel de acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="765b8-136">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="765b8-137">Problemas relacionados con la asignación de aplicaciones a grupos</span><span class="sxs-lookup"><span data-stu-id="765b8-137">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="765b8-138">Puede que un usuario vea una aplicación en su Panel de acceso porque forme parte de un grupo al que se ha asignado esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="765b8-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="765b8-139">A continuación se muestran algunas maneras de comprobarlo:</span><span class="sxs-lookup"><span data-stu-id="765b8-139">Below are some ways to check:</span></span>

-   [<span data-ttu-id="765b8-140">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="765b8-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="765b8-141">Comprobar si un usuario es miembro de un grupo asignado a una licencia</span><span class="sxs-lookup"><span data-stu-id="765b8-141">Check if a user is a member of a group assigned to a license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="765b8-142">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="765b8-142">Check a user’s group memberships</span></span>

<span data-ttu-id="765b8-143">Para comprobar la pertenencia de un grupo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="765b8-143">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="765b8-144">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="765b8-144">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="765b8-145">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="765b8-145">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="765b8-146">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="765b8-146">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="765b8-147">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="765b8-147">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="765b8-148">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="765b8-148">click **All users**.</span></span>

6.  <span data-ttu-id="765b8-149">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="765b8-149">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="765b8-150">Haga clic en **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="765b8-150">click **Groups.**</span></span>

8.  <span data-ttu-id="765b8-151">Compruebe si el usuario forma parte de un grupo al que se ha asignado la aplicación.</span><span class="sxs-lookup"><span data-stu-id="765b8-151">Check to see if your user is part of a Group assigned to the application.</span></span>

   * <span data-ttu-id="765b8-152">Si desea quitar el usuario del grupo, **haga clic en la fila** del grupo y seleccione Eliminar.</span><span class="sxs-lookup"><span data-stu-id="765b8-152">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-to-a-license"></a><span data-ttu-id="765b8-153">Comprobar si un usuario es miembro de un grupo asignado a una licencia</span><span class="sxs-lookup"><span data-stu-id="765b8-153">Check if a user is a member of a group assigned to a license</span></span>

1.  <span data-ttu-id="765b8-154">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="765b8-154">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="765b8-155">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="765b8-155">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="765b8-156">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="765b8-156">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="765b8-157">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="765b8-157">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="765b8-158">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="765b8-158">click **All users**.</span></span>

6.  <span data-ttu-id="765b8-159">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="765b8-159">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="765b8-160">Haga clic en **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="765b8-160">click **Groups.**</span></span>

8.  <span data-ttu-id="765b8-161">Haga clic en la fila de un grupo específico.</span><span class="sxs-lookup"><span data-stu-id="765b8-161">click the row of a specific group.</span></span>

9.  <span data-ttu-id="765b8-162">Haga clic en **Licencias** para ver qué licencias tiene asignadas el grupo.</span><span class="sxs-lookup"><span data-stu-id="765b8-162">click **Licenses** to see which licenses the group has assigned to it.</span></span>

  * <span data-ttu-id="765b8-163">Si el grupo está asignado a una licencia de Office, esto permitirá que determinadas aplicaciones de Office aparezcan en el panel de acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="765b8-163">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="765b8-164">Si después de seguir estos pasos, el problema no se ha resuelto,</span><span class="sxs-lookup"><span data-stu-id="765b8-164">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="765b8-165">abra una incidencia de soporte técnico con la información siguiente si está disponible:</span><span class="sxs-lookup"><span data-stu-id="765b8-165">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="765b8-166">Id. de error de correlación</span><span class="sxs-lookup"><span data-stu-id="765b8-166">Correlation error ID</span></span>

-   <span data-ttu-id="765b8-167">UPN (dirección de correo electrónico del usuario)</span><span class="sxs-lookup"><span data-stu-id="765b8-167">UPN (user email address)</span></span>

-   <span data-ttu-id="765b8-168">Id. de inquilino</span><span class="sxs-lookup"><span data-stu-id="765b8-168">Tenant ID</span></span>

-   <span data-ttu-id="765b8-169">Tipo de explorador</span><span class="sxs-lookup"><span data-stu-id="765b8-169">Browser type</span></span>

-   <span data-ttu-id="765b8-170">Zona horaria y hora/período de tiempo durante el que se produce el error</span><span class="sxs-lookup"><span data-stu-id="765b8-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="765b8-171">Seguimientos de Fiddler</span><span class="sxs-lookup"><span data-stu-id="765b8-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="765b8-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="765b8-172">Next steps</span></span>
[<span data-ttu-id="765b8-173">Administración de aplicaciones con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="765b8-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)

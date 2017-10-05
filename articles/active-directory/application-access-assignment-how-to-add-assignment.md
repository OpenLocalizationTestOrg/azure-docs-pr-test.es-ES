---
title: "Asignación de usuarios y grupos a una aplicación | Microsoft Docs"
description: "Asignar usuarios a la aplicación para conceder acceso"
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
ms.openlocfilehash: 61536612e0dd5102b8f5e911c350826846f5ed77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-and-groups-to-an-application"></a><span data-ttu-id="d8e62-103">Asignación de usuarios y grupos a una aplicación</span><span class="sxs-lookup"><span data-stu-id="d8e62-103">How to assign users and groups to an application</span></span>

<span data-ttu-id="d8e62-104">Antes de que los usuarios puedan hacer cualquiera de las siguientes acciones para una aplicación específica, debe primero **asignarles a la aplicación** para concederles acceso:</span><span class="sxs-lookup"><span data-stu-id="d8e62-104">Before your users can do any of the below for a specific application, you need to first **assign them to the application** to grant them access:</span></span>

-   <span data-ttu-id="d8e62-105">Acceso a una aplicación mediante la **navegación directa a la dirección URL de la aplicación** (también conocido como inicio de sesión iniciado por el proveedor de servicios).</span><span class="sxs-lookup"><span data-stu-id="d8e62-105">Access an application by **navigating to the application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="d8e62-106">Acceso a una aplicación mediante la **dirección URL de acceso de usuarios** en la página **Propiedades** de una aplicación (también conocido como inicio de sesión iniciado por un proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="d8e62-106">Access an application by using the **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="d8e62-107">Vea como aparece una aplicación en su [panel de acceso a las aplicaciones](https://myapps.microsoft.com/) o aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="d8e62-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="d8e62-108">Vea como aparece una aplicación en el [iniciador de aplicaciones de Office 365](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span><span class="sxs-lookup"><span data-stu-id="d8e62-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-to-assign-applications-with-azure-active-directory"></a><span data-ttu-id="d8e62-109">Métodos de asignación de aplicaciones con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8e62-109">Methods to assign applications with Azure Active Directory</span></span> 

<span data-ttu-id="d8e62-110">Hay 3 formas de asignar aplicaciones con Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="d8e62-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="d8e62-111">Asignación de un usuario directamente a una aplicación como administrador</span><span class="sxs-lookup"><span data-stu-id="d8e62-111">Assign a user directly to an application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="d8e62-112">Asignación de un grupo directamente a una aplicación como administrador</span><span class="sxs-lookup"><span data-stu-id="d8e62-112">Assign a group directly to an application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="d8e62-113">Habilitar el acceso de autoservicio a las aplicaciones para permitir a los usuarios buscar sus propias aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d8e62-113">Enable self-service application access to allow users to find their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="d8e62-114">Asignación de un usuario directamente como administrador</span><span class="sxs-lookup"><span data-stu-id="d8e62-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="d8e62-115">Para asignar uno o varios usuarios a una aplicación directamente, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d8e62-115">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="d8e62-116">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d8e62-117">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="d8e62-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d8e62-118">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d8e62-119">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8e62-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d8e62-120">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d8e62-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="d8e62-121">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="d8e62-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="d8e62-122">Seleccione la aplicación que desea asignar a un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="d8e62-122">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="d8e62-123">Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8e62-123">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d8e62-124">Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-124">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="d8e62-125">Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-125">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="d8e62-126">Escriba el **nombre completo** o la **dirección de correo electrónico** del usuario al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-126">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="d8e62-127">Mantenga el puntero sobre el **usuario** en la lista para que aparezca una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-127">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="d8e62-128">Haga clic en la casilla situada junto a la foto o el logotipo del perfil del usuario para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-128">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="d8e62-129">**Opcional:** si desea **agregar más de un usuario**, escriba otro **nombre completo** o **dirección de correo electrónico** en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-129">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="d8e62-130">Cuando haya terminado de seleccionar usuarios, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8e62-130">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="d8e62-131">**Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="d8e62-131">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="d8e62-132">Haga clic en el botón **Asignar** para asignar la aplicación a los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="d8e62-132">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="d8e62-133">Tras un breve período de tiempo, los usuarios seleccionados podrán iniciar estas aplicaciones mediante los métodos descritos en la sección de descripción de la solución.</span><span class="sxs-lookup"><span data-stu-id="d8e62-133">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="d8e62-134">Asignación de un grupo directamente a una aplicación como administrador</span><span class="sxs-lookup"><span data-stu-id="d8e62-134">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="d8e62-135">Para asignar uno o varios grupos a una aplicación directamente, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d8e62-135">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="d8e62-136">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d8e62-137">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="d8e62-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d8e62-138">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d8e62-139">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8e62-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d8e62-140">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d8e62-140">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="d8e62-141">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="d8e62-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="d8e62-142">Seleccione la aplicación que desea asignar a un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="d8e62-142">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="d8e62-143">Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8e62-143">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d8e62-144">Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-144">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="d8e62-145">Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-145">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="d8e62-146">Escriba el **nombre completo** del grupo al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-146">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="d8e62-147">Mantenga el puntero sobre el **grupo** en la lista para que aparezca una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-147">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="d8e62-148">Haga clic en la casilla situada junto a la foto o el logotipo del perfil del grupo para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-148">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="d8e62-149">**Opcional**: si desea **agregar más de un grupo**, escriba otro **nombre de grupo completo** o en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese grupo a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-149">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="d8e62-150">Cuando haya terminado de seleccionar grupos, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8e62-150">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="d8e62-151">**Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los grupos que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="d8e62-151">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="d8e62-152">Haga clic en el botón **Asignar** para asignar la aplicación a los grupos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="d8e62-152">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="d8e62-153">Tras un breve período de tiempo, los usuarios de los grupos seleccionados podrán iniciar estas aplicaciones mediante los métodos descritos en la sección de descripción de la solución.</span><span class="sxs-lookup"><span data-stu-id="d8e62-153">After a short period of time, the users within the groups you have selected be able to launch these applications using the methods described in the solution description section.</span></span> <span data-ttu-id="d8e62-154">Si se trata de grupos dinámicos, puede que haya algo de retardo de procesamiento adicional en estas asignaciones hasta que aparezcan para los usuarios dentro de estos grupos asignados.</span><span class="sxs-lookup"><span data-stu-id="d8e62-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="d8e62-155">Habilitar el acceso de autoservicio a las aplicaciones para permitir a los usuarios buscar sus propias aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d8e62-155">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="d8e62-156">El acceso de autoservicio a las aplicaciones es una excelente manera de permitir a los usuarios detectar automáticamente aplicaciones y, si lo desea, permitir que el grupo de negocios apruebe el acceso a esas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d8e62-156">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="d8e62-157">Puede permitir que el grupo de negocios administre las credenciales asignadas a esos usuarios para que puedan realizar un inicio de sesión único con contraseña en las aplicaciones directamente desde sus paneles de acceso.</span><span class="sxs-lookup"><span data-stu-id="d8e62-157">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="d8e62-158">Para habilitar el acceso de autoservicio a las aplicaciones, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d8e62-158">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="d8e62-159">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d8e62-160">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="d8e62-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d8e62-161">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d8e62-162">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8e62-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d8e62-163">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d8e62-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="d8e62-164">Si no ve que la aplicación que desea aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="d8e62-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="d8e62-165">Seleccione la aplicación en la que desea habilitar el acceso de autoservicio de la lista.</span><span class="sxs-lookup"><span data-stu-id="d8e62-165">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="d8e62-166">Cuando se cargue la aplicación, haga clic en **Autoservicio** en el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8e62-166">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d8e62-167">Para habilitar el acceso de autoservicio a las aplicaciones para esta aplicación, establezca la opción **¿Quiere permitir que los usuarios soliciten acceso a esta aplicación?** en **Sí.**</span><span class="sxs-lookup"><span data-stu-id="d8e62-167">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="d8e62-168">A continuación, seleccione el grupo al que se deben agregar los usuarios que solicitan acceso a esta aplicación, haga clic en el selector situado junto a la etiqueta **¿A qué grupo se deberían agregar los usuarios asignados?** y seleccione un grupo.</span><span class="sxs-lookup"><span data-stu-id="d8e62-168">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="d8e62-169">**Opcional:** si desea requerir la aprobación de la empresa antes de permitir el acceso a los usuarios, establezca la opción **¿Quiere requerir una aprobación para conceder acceso a esta aplicación?** en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-169">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="d8e62-170">**Opcional: para las aplicaciones que solo utilizan el inicio de sesión único con contraseña,** si desea permitir que los aprobadores de la empresa especifiquen las contraseñas que se envían a esta aplicación para los usuarios aprobados, establezca la opción **¿Quiere permitir que los aprobadores establezcan las contraseñas de los usuarios de esta aplicación?** en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="d8e62-170">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="d8e62-171">**Opcional:** para especificar los aprobadores de la empresa que tienen permiso para aprobar el acceso a esta aplicación, haga clic en el selector situado junto a la etiqueta **¿Quién tiene permiso para aprobar el acceso a esta aplicación?** para seleccionar hasta 10 aprobadores individuales de la empresa.</span><span class="sxs-lookup"><span data-stu-id="d8e62-171">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="d8e62-172">No se admiten grupos.</span><span class="sxs-lookup"><span data-stu-id="d8e62-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="d8e62-173">**Opcional:** **para las aplicaciones que exponen roles**, si desea asignar usuarios aprobados de autoservicio a un rol, haga clic en el selector situado junto a la etiqueta **¿A qué rol deben asignarse los usuarios de esta aplicación?** para seleccionar el rol al que se deben asignar estos usuarios.</span><span class="sxs-lookup"><span data-stu-id="d8e62-173">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="d8e62-174">Haga clic en el botón **Guardar** de la parte superior de la hoja para terminar.</span><span class="sxs-lookup"><span data-stu-id="d8e62-174">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="d8e62-175">Cuando se haya completado la configuración de la aplicación de autoservicio, los usuarios pueden navegar a sus [paneles de acceso a las aplicaciones](https://myapps.microsoft.com/) y hacer clic en el botón **+ Agregar** para buscar las aplicaciones para las que se ha habilitado el acceso de autoservicio.</span><span class="sxs-lookup"><span data-stu-id="d8e62-175">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="d8e62-176">Los aprobadores de la empresa pueden también ver una notificación en sus [paneles de acceso a las aplicaciones](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="d8e62-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="d8e62-177">Puede habilitar un correo electrónico que les informa cuando un usuario ha solicitado el acceso a una aplicación que requiere su aprobación.</span><span class="sxs-lookup"><span data-stu-id="d8e62-177">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="d8e62-178">Estas aprobaciones admiten flujos de trabajo de aprobación única, lo que significa que si especifica varios aprobadores, cualquier aprobador individual puede aprobar el acceso a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8e62-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8e62-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d8e62-179">Next steps</span></span>
[<span data-ttu-id="d8e62-180">Proporcionar un inicio de sesión único a las aplicaciones con el proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="d8e62-180">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

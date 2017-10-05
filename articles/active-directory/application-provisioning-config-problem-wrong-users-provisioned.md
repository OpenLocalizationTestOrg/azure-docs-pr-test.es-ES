---
title: "Aprovisionamiento de un conjunto de usuarios incorrecto en una aplicación de la galería de Azure AD | Microsoft Docs"
description: "Obtenga información para averiguar por qué se está aprovisionando un conjunto de usuarios para una aplicación diferente del esperado."
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
ms.openlocfilehash: 85b533584c8ec15a23be32e20db7de583fced6a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-to-an-azure-ad-gallery-application"></a><span data-ttu-id="2b7ec-103">Aprovisionamiento de un conjunto de usuarios incorrecto en una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b7ec-103">Wrong set of users are being provisioned to an Azure AD Gallery application</span></span>

<span data-ttu-id="2b7ec-104">La selección de los usuarios que se aprovisionan para la aplicación se basa principalmente en los usuarios y los grupos que se han **asignado** a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-104">Which users are provisioned to the app is primarily driven by which users and groups have been **assigned** to the application.</span></span>

<span data-ttu-id="2b7ec-105">Use los siguientes recursos para obtener información sobre cómo comprobar qué usuarios y grupos se han asignado a una aplicación en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-105">Use the resources below to learn how to check which users and groups have been assigned to an application within Azure Active Directory.</span></span>

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="2b7ec-106">Asignación de un usuario directamente como administrador</span><span class="sxs-lookup"><span data-stu-id="2b7ec-106">Assign a user directly as an administrator</span></span>

<span data-ttu-id="2b7ec-107">Para asignar uno o varios usuarios a una aplicación directamente, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2b7ec-107">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="2b7ec-108">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2b7ec-109">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b7ec-110">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b7ec-111">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b7ec-112">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-112">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="2b7ec-113">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="2b7ec-113">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="2b7ec-114">Seleccione la aplicación que desea asignar a un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-114">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="2b7ec-115">Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-115">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2b7ec-116">Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-116">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="2b7ec-117">Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-117">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="2b7ec-118">Escriba el **nombre completo** o la **dirección de correo electrónico** del usuario al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-118">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="2b7ec-119">Mantenga el puntero sobre el **usuario** en la lista para que aparezca una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-119">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="2b7ec-120">Haga clic en la casilla situada junto a la foto o el logotipo del perfil del usuario para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-120">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="2b7ec-121">**Opcional:** si desea **agregar más de un usuario**, escriba otro **nombre completo** o **dirección de correo electrónico** en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-121">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="2b7ec-122">Cuando haya terminado de seleccionar usuarios, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-122">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="2b7ec-123">**Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-123">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="2b7ec-124">Haga clic en el botón **Asignar** para asignar la aplicación a los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-124">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="2b7ec-125">Si el aprovisionamiento está configurado y ya se está ejecutando para una aplicación, los nuevos usuarios deben aprovisionarse en una aplicación en aproximadamente 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-125">If provisioning is configured and already running for an app, new users should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="2b7ec-126">Compruebe los **registros de auditoría** para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-126">Check the **Audit Logs** for details.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="2b7ec-127">Asignación de un grupo directamente a una aplicación como administrador</span><span class="sxs-lookup"><span data-stu-id="2b7ec-127">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="2b7ec-128">Para asignar uno o varios grupos a una aplicación directamente, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2b7ec-128">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="2b7ec-129">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2b7ec-130">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2b7ec-131">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2b7ec-132">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2b7ec-133">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-133">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="2b7ec-134">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="2b7ec-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="2b7ec-135">Seleccione la aplicación que desea asignar a un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-135">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="2b7ec-136">Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-136">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2b7ec-137">Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-137">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="2b7ec-138">Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-138">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="2b7ec-139">Escriba el **nombre completo** del grupo al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-139">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="2b7ec-140">Mantenga el puntero sobre el **grupo** en la lista para que aparezca una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-140">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="2b7ec-141">Haga clic en la casilla situada junto a la foto o el logotipo del perfil del grupo para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-141">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="2b7ec-142">**Opcional**: si desea **agregar más de un grupo**, escriba otro **nombre de grupo completo** o en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese grupo a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-142">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="2b7ec-143">Cuando haya terminado de seleccionar grupos, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-143">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="2b7ec-144">**Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los grupos que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-144">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="2b7ec-145">Haga clic en el botón **Asignar** para asignar la aplicación a los grupos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-145">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="2b7ec-146">Si el aprovisionamiento está configurado y ya se está ejecutando para una aplicación, los nuevos usuarios contenidos en el grupo deben aprovisionarse en una aplicación en aproximadamente 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-146">If provisioning is configured and already running for an app, new users contained within the group should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="2b7ec-147">Compruebe los **registros de auditoría** para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-147">Check the **Audit Logs** for details.</span></span>

>[!IMPORTANT]
><span data-ttu-id="2b7ec-148">Aprovisionamiento del nombre del grupo y los detalles del grupo, además de los miembros, si se admite para algunas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-148">Provisioning of the group name and group details, in addition to the members, if supported for some applications.</span></span> <span data-ttu-id="2b7ec-149">Puede habilitar o deshabilitar esta funcionalidad habilitando o deshabilitando la **Asignación** para los objetos de grupo que se muestran en la pestaña **Aprovisionamiento**.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-149">You can enable or disable this functionality by enabling or disabling the **Mapping** for group objects shown in the **Provisioning** tab.</span></span> 
>
>

<span data-ttu-id="2b7ec-150">Si están habilitados los grupos de aprovisionamiento, asegúrese de revisar las asignaciones de atributos para asegurarse de que se utiliza un campo apropiado para el "identificador coincidente".</span><span class="sxs-lookup"><span data-stu-id="2b7ec-150">If provisioning groups is enabled, be sure to review the attribute mappings to ensure an appropriate field is being used for the “matching ID”.</span></span> <span data-ttu-id="2b7ec-151">Esto puede ser el nombre para mostrar o el alias de correo electrónico, ya que el grupo y sus miembros no se han aprovisionado si la propiedad coincidente está vacía o no se rellenado para un grupo en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b7ec-151">This can be the display name or email alias, as the group and its members not be provisioned if the matching property is empty or not populated for a group in Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b7ec-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2b7ec-152">Next steps</span></span>
[<span data-ttu-id="2b7ec-153">Automatización del aprovisionamiento y desaprovisionamiento de usuarios para aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b7ec-153">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

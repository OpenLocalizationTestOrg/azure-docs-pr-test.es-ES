---
title: "aplicación de la Galería de tooan aprovisionado Azure AD que se aaaWrong conjunto de usuarios | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toofind out ¿por qué se va un conjunto diferente de los usuarios aprovisionados tooan aplicación a los que esperaba"
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
ms.openlocfilehash: adb90b12a53fb3160ce2b73b2559df92b283438e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a><span data-ttu-id="c3c93-103">Un conjunto de usuarios erróneo se están aprovisionados tooan Azure AD Galería aplicación</span><span class="sxs-lookup"><span data-stu-id="c3c93-103">Wrong set of users are being provisioned tooan Azure AD Gallery application</span></span>

<span data-ttu-id="c3c93-104">Qué usuarios son aprovisionados toohello aplicación se basa principalmente en qué usuarios y grupos que han sido **asignado** toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="c3c93-104">Which users are provisioned toohello app is primarily driven by which users and groups have been **assigned** toohello application.</span></span>

<span data-ttu-id="c3c93-105">Usar recursos de hello situados por debajo de toolearn cómo toocheck qué usuarios y grupos se han asignado tooan aplicación en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c3c93-105">Use hello resources below toolearn how toocheck which users and groups have been assigned tooan application within Azure Active Directory.</span></span>

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="c3c93-106">Asignación de un usuario directamente como administrador</span><span class="sxs-lookup"><span data-stu-id="c3c93-106">Assign a user directly as an administrator</span></span>

<span data-ttu-id="c3c93-107">tooassign uno o más usuarios tooan application directamente, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="c3c93-107">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="c3c93-108">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="c3c93-108">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c3c93-109">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="c3c93-109">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c3c93-110">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="c3c93-110">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c3c93-111">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c3c93-111">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c3c93-112">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c3c93-112">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="c3c93-113">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="c3c93-113">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c3c93-114">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="c3c93-114">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="c3c93-115">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c3c93-115">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c3c93-116">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="c3c93-116">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="c3c93-117">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="c3c93-117">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="c3c93-118">Tipo de hello **nombre completo** o **dirección de correo electrónico** del usuario de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="c3c93-118">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="c3c93-119">Mantenga el mouse sobre hello **usuario** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="c3c93-119">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="c3c93-120">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla toohello del siguiente usuario su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="c3c93-120">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="c3c93-121">**Opcional:** si lo desea demasiado**agregar más de un usuario**, tipo de otro **nombre completo** o **dirección de correo electrónico** en hello **buscar por nombre o dirección de correo electrónico** cuadro de búsqueda y haga clic en hello casilla tooadd este usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="c3c93-121">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="c3c93-122">Cuando haya terminado de seleccionar usuarios, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="c3c93-122">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="c3c93-123">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** hoja tooselect un rol tooassign toohello usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="c3c93-123">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="c3c93-124">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="c3c93-124">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="c3c93-125">Si se configura el aprovisionamiento y ya está ejecutando para una aplicación, los nuevos usuarios deben ser aplicación tooan aprovisionado en aproximadamente 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="c3c93-125">If provisioning is configured and already running for an app, new users should be provisioned tooan application in approximately 10 minutes.</span></span> <span data-ttu-id="c3c93-126">Comprobar hello **los registros de auditoría** para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="c3c93-126">Check hello **Audit Logs** for details.</span></span>

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a><span data-ttu-id="c3c93-127">Asignar un grupo directamente tooan aplicación como administrador</span><span class="sxs-lookup"><span data-stu-id="c3c93-127">Assign a group directly tooan application as an administrator</span></span>

<span data-ttu-id="c3c93-128">tooassign uno o más grupos de aplicación de tooan directamente, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="c3c93-128">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="c3c93-129">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="c3c93-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c3c93-130">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="c3c93-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c3c93-131">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="c3c93-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c3c93-132">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c3c93-132">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c3c93-133">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c3c93-133">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="c3c93-134">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="c3c93-134">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c3c93-135">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="c3c93-135">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="c3c93-136">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c3c93-136">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c3c93-137">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="c3c93-137">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="c3c93-138">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="c3c93-138">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="c3c93-139">Tipo de hello **nombre de grupo completa** del grupo de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="c3c93-139">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="c3c93-140">Mantenga el mouse sobre hello **grupo** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="c3c93-140">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="c3c93-141">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla siguiente toohello del grupo su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="c3c93-141">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="c3c93-142">**Opcional:** si lo desea demasiado**agregar más de un grupo**, tipo de otro **nombre de grupo completa** en hello **buscar por nombre o dirección de correo** cuadro de búsqueda, y haga clic en hello casilla tooadd este grupo toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="c3c93-142">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="c3c93-143">Cuando haya terminado la selección de grupos, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="c3c93-143">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="c3c93-144">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** grupos hoja tooselect una toohello tooassign de rol que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="c3c93-144">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="c3c93-145">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello grupos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="c3c93-145">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="c3c93-146">Si el aprovisionamiento es configurado y ya se está ejecutando para una aplicación, nuevos usuarios incluidos en el grupo de hello deben ser tooan aprovisionado en aproximadamente 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="c3c93-146">If provisioning is configured and already running for an app, new users contained within hello group should be provisioned tooan application in approximately 10 minutes.</span></span> <span data-ttu-id="c3c93-147">Comprobar hello **los registros de auditoría** para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="c3c93-147">Check hello **Audit Logs** for details.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c3c93-148">Aprovisionamiento de Hola nombre del grupo y del grupo de detalles, en los miembros de suma toohello, si admiten para algunas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c3c93-148">Provisioning of hello group name and group details, in addition toohello members, if supported for some applications.</span></span> <span data-ttu-id="c3c93-149">Puede habilitar o deshabilitar esta funcionalidad habilitando o deshabilitando hello **asignación** para los objetos de grupo se muestra en hello **Provisioning** ficha.</span><span class="sxs-lookup"><span data-stu-id="c3c93-149">You can enable or disable this functionality by enabling or disabling hello **Mapping** for group objects shown in hello **Provisioning** tab.</span></span> 
>
>

<span data-ttu-id="c3c93-150">Si está habilitado el aprovisionamiento de grupos, asegúrese de tooreview Hola atributo asignaciones tooensure un campo correspondiente se utiliza para saludo "Id. de búsqueda de coincidencias".</span><span class="sxs-lookup"><span data-stu-id="c3c93-150">If provisioning groups is enabled, be sure tooreview hello attribute mappings tooensure an appropriate field is being used for hello “matching ID”.</span></span> <span data-ttu-id="c3c93-151">Esto puede ser el nombre para mostrar hello o correo electrónico alias, como hello grupo y sus miembros no se aprovisionan si ninguna propiedad coincidente con hello está vacía o no rellena para un grupo en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3c93-151">This can be hello display name or email alias, as hello group and its members not be provisioned if hello matching property is empty or not populated for a group in Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3c93-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c3c93-152">Next steps</span></span>
[<span data-ttu-id="c3c93-153">Automatizar el aprovisionamiento de usuarios y desaprovisionamiento tooSaaS aplicaciones con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3c93-153">Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

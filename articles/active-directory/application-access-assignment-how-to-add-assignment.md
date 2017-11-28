---
title: "aplicación del tooan de usuarios y grupos de tooassign aaaHow | Documentos de Microsoft"
description: "Asignar a los usuarios acceso a la aplicación toohello toogrant"
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
ms.openlocfilehash: e039a26e4b8f88ad747354859f1071b8f74b6789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-and-groups-tooan-application"></a><span data-ttu-id="6296a-103">¿Cómo tooassign a los usuarios y grupos de una aplicación tooan</span><span class="sxs-lookup"><span data-stu-id="6296a-103">How tooassign users and groups tooan application</span></span>

<span data-ttu-id="6296a-104">Antes de que los usuarios pueden realizar cualquiera de Hola a continuación para una aplicación específica, debe toofirst **asignarlos aplicación toohello** toogrant acceso:</span><span class="sxs-lookup"><span data-stu-id="6296a-104">Before your users can do any of hello below for a specific application, you need toofirst **assign them toohello application** toogrant them access:</span></span>

-   <span data-ttu-id="6296a-105">Acceso a una aplicación por **navegar directamente por dirección URL de la aplicación toohello** (también conocido como iniciado en SP inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="6296a-105">Access an application by **navigating toohello application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="6296a-106">Acceso a una aplicación mediante el uso de hello **dirección URL de acceso de usuario** en una aplicación **propiedades** página (también conocido como iniciado por IDP inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="6296a-106">Access an application by using hello **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="6296a-107">Vea como aparece una aplicación en su [panel de acceso a las aplicaciones](https://myapps.microsoft.com/) o aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="6296a-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="6296a-108">Vea como aparece una aplicación en el [iniciador de aplicaciones de Office 365](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span><span class="sxs-lookup"><span data-stu-id="6296a-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-tooassign-applications-with-azure-active-directory"></a><span data-ttu-id="6296a-109">Aplicaciones de tooassign de métodos con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6296a-109">Methods tooassign applications with Azure Active Directory</span></span> 

<span data-ttu-id="6296a-110">Hay 3 formas de asignar aplicaciones con Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="6296a-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="6296a-111">Asignar un usuario directamente tooan aplicación como administrador</span><span class="sxs-lookup"><span data-stu-id="6296a-111">Assign a user directly tooan application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="6296a-112">Asignar un grupo directamente tooan aplicación como administrador</span><span class="sxs-lookup"><span data-stu-id="6296a-112">Assign a group directly tooan application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="6296a-113">Habilitar aplicación self-service acceso tooallow usuarios toofind sus propias aplicaciones</span><span class="sxs-lookup"><span data-stu-id="6296a-113">Enable self-service application access tooallow users toofind their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="6296a-114">Asignación de un usuario directamente como administrador</span><span class="sxs-lookup"><span data-stu-id="6296a-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="6296a-115">tooassign uno o más usuarios tooan application directamente, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="6296a-115">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="6296a-116">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="6296a-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="6296a-117">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="6296a-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6296a-118">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="6296a-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6296a-119">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6296a-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6296a-120">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6296a-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="6296a-121">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="6296a-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="6296a-122">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="6296a-122">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="6296a-123">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6296a-123">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="6296a-124">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="6296a-124">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="6296a-125">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="6296a-125">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="6296a-126">Tipo de hello **nombre completo** o **dirección de correo electrónico** del usuario de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="6296a-126">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="6296a-127">Mantenga el mouse sobre hello **usuario** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="6296a-127">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="6296a-128">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla toohello del siguiente usuario su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="6296a-128">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="6296a-129">**Opcional:** si lo desea demasiado**agregar más de un usuario**, tipo de otro **nombre completo** o **dirección de correo electrónico** en hello **buscar por nombre o dirección de correo electrónico** cuadro de búsqueda y haga clic en hello casilla tooadd este usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="6296a-129">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="6296a-130">Cuando haya terminado de seleccionar usuarios, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="6296a-130">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="6296a-131">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** hoja tooselect un rol tooassign toohello usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="6296a-131">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="6296a-132">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="6296a-132">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="6296a-133">Tras un breve período de tiempo, los usuarios de Hola que seleccionó ser capaz de toolaunch dichas aplicaciones usan Hola métodos descritos en la sección de descripción de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="6296a-133">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a><span data-ttu-id="6296a-134">Asignar un grupo directamente tooan aplicación como administrador</span><span class="sxs-lookup"><span data-stu-id="6296a-134">Assign a group directly tooan application as an administrator</span></span>

<span data-ttu-id="6296a-135">tooassign uno o más grupos de aplicación de tooan directamente, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="6296a-135">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="6296a-136">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="6296a-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="6296a-137">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="6296a-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6296a-138">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="6296a-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6296a-139">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6296a-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6296a-140">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6296a-140">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="6296a-141">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="6296a-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="6296a-142">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="6296a-142">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="6296a-143">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6296a-143">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="6296a-144">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="6296a-144">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="6296a-145">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="6296a-145">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="6296a-146">Tipo de hello **nombre de grupo completa** del grupo de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="6296a-146">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="6296a-147">Mantenga el mouse sobre hello **grupo** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="6296a-147">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="6296a-148">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla siguiente toohello del grupo su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="6296a-148">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="6296a-149">**Opcional:** si lo desea demasiado**agregar más de un grupo**, tipo de otro **nombre de grupo completa** en hello **buscar por nombre o dirección de correo** cuadro de búsqueda, y haga clic en hello casilla tooadd este grupo toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="6296a-149">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="6296a-150">Cuando haya terminado la selección de grupos, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="6296a-150">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="6296a-151">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** grupos hoja tooselect una toohello tooassign de rol que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="6296a-151">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="6296a-152">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello grupos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="6296a-152">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="6296a-153">Tras un breve período de tiempo, los usuarios de hello dentro de grupos de Hola que seleccionó ser capaz de toolaunch dichas aplicaciones usan Hola métodos descritos en la sección de descripción de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="6296a-153">After a short period of time, hello users within hello groups you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span> <span data-ttu-id="6296a-154">Si se trata de grupos dinámicos, puede que haya algo de retardo de procesamiento adicional en estas asignaciones hasta que aparezcan para los usuarios dentro de estos grupos asignados.</span><span class="sxs-lookup"><span data-stu-id="6296a-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="6296a-155">Habilitar aplicación self-service acceso tooallow usuarios toofind sus propias aplicaciones</span><span class="sxs-lookup"><span data-stu-id="6296a-155">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="6296a-156">Acceso a la aplicación de autoservicio es una tooself de los usuarios de manera estupenda tooallow-detectar las aplicaciones, si lo desea permitir el acceso de tooapprove de grupo de negocios de hello toothose aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6296a-156">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="6296a-157">Puede permitir credenciales de Hola de hello business grupo toomanage asignan a usuarios toothose para derecho de inicio de sesión único en aplicaciones de contraseña de sus paneles de acceso.</span><span class="sxs-lookup"><span data-stu-id="6296a-157">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="6296a-158">aplicación de tooan de acceso de tooenable aplicación self-service, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="6296a-158">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="6296a-159">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="6296a-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="6296a-160">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="6296a-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6296a-161">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="6296a-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6296a-162">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6296a-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6296a-163">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6296a-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="6296a-164">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="6296a-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="6296a-165">Seleccionar aplicación hello desea tooenable acceso de autoservicio toofrom Hola lista.</span><span class="sxs-lookup"><span data-stu-id="6296a-165">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="6296a-166">Una vez que se carga la aplicación hello, haga clic en **self-service** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6296a-166">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="6296a-167">tooenable acceso a la aplicación de autoservicio para esta aplicación, activar hello **permitir que los usuarios de aplicación de toorequest access toothis?** alternar demasiado**sí.**</span><span class="sxs-lookup"><span data-stu-id="6296a-167">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="6296a-168">A continuación, tooselect Hola grupo toowhich los usuarios que solicitan acceso toothis aplicación debe agregarse, haga clic en siguiente toohello etiqueta de selector de hello **toowhich grupo debería asignar se agregan usuarios?** y seleccione un grupo.</span><span class="sxs-lookup"><span data-stu-id="6296a-168">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="6296a-169">**Opcional:** si desea que toorequire la aprobación de un negocio antes de que los usuarios tienen permiso de acceso, establezca hello **requieren aprobación antes de conceder acceso toothis aplicación?** alternar demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="6296a-169">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="6296a-170">**Opcional: para aplicaciones que utilizan la contraseña de inicio de sesión único en solo,** si desea que tooallow esas contraseñas hello toospecify de aprobadores empresariales que se envían toothis aplicación para los usuarios aprobados, establezca hello **permitir aprobadores tooset ¿contraseñas de usuario para esta aplicación?**  alternar demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="6296a-170">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="6296a-171">**Opcional:** toospecify Hola business aprobadores se permiten la aplicación de toothis de tooapprove access, haga clic en siguiente toohello etiqueta de selector de hello **que se permite la aplicación de tooapprove access toothis?** tooselect seguridad too10 aprobadores de negocios individuales.</span><span class="sxs-lookup"><span data-stu-id="6296a-171">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="6296a-172">No se admiten grupos.</span><span class="sxs-lookup"><span data-stu-id="6296a-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="6296a-173">**Opcional:** **para las aplicaciones que exponen funciones**, si desea que el rol de tooa de tooassign usuarios aprobados de autoservicio, haga clic en hello selector siguiente toohello **toowhich rol deben asignarse a los usuarios en este ¿aplicación?**  tooselect Hola rol toowhich se deben asignar estos usuarios.</span><span class="sxs-lookup"><span data-stu-id="6296a-173">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="6296a-174">Haga clic en hello **guardar** situado en la parte superior de Hola de hello hoja toofinish.</span><span class="sxs-lookup"><span data-stu-id="6296a-174">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="6296a-175">Cuando se haya completado la configuración de la aplicación de autoservicio, los usuarios pueden navegar tootheir [Panel de acceso de la aplicación](https://myapps.microsoft.com/) y haga clic en hello **+ agregar** botón toofind Hola aplicaciones toowhich ha habilitado Acceso de autoservicio.</span><span class="sxs-lookup"><span data-stu-id="6296a-175">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="6296a-176">Los aprobadores de la empresa pueden también ver una notificación en sus [paneles de acceso a las aplicaciones](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="6296a-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="6296a-177">Puede habilitar un correo electrónico que les informa de cuándo un usuario ha solicitado la aplicación de tooan de acceso que requiere su aprobación.</span><span class="sxs-lookup"><span data-stu-id="6296a-177">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="6296a-178">Estas aprobaciones admiten flujos de trabajo de aprobación única, lo que significa que si especifica varios aprobadores, cualquier aprobador único posible aplicación de aprobador access toohello.</span><span class="sxs-lookup"><span data-stu-id="6296a-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6296a-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6296a-179">Next steps</span></span>
[<span data-ttu-id="6296a-180">Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="6296a-180">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

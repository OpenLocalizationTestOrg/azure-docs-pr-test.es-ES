---
title: "aaaHow tooconfigure contraseña inicio de sesión único para una aplicación de la Galería de Azure AD | Documentos de Microsoft"
description: "Cómo tooconfigure una aplicación para proteger basada en contraseña de inicio de sesión único cuando ya se incluye en hello Galería de aplicaciones de Azure AD"
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
ms.openlocfilehash: 7a93bff119b477d946368686fc2d9006ca2722a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="3bedd-103">¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación de la Galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3bedd-103">How tooconfigure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="3bedd-104">Cuando se agrega una aplicación de hello [Galería de aplicaciones de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), tiene la opción de Hola de cómo desea que su toosign a los usuarios de aplicación de toothat.</span><span class="sxs-lookup"><span data-stu-id="3bedd-104">When you add an application from hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have hello choice of how you want your users toosign in toothat application.</span></span> <span data-ttu-id="3bedd-105">Puede configurar esta opción en cualquier momento seleccionando hello **Single Sign-on** elemento de navegación en una aplicación empresarial de hello [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3bedd-105">You can configure this choice at any time by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="3bedd-106">Uno de tooyou disponible de métodos de inicio de sesión único de hello es hello [basado en contraseña Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opción.</span><span class="sxs-lookup"><span data-stu-id="3bedd-106">One of hello single sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="3bedd-107">Se trata de una excelente manera de tooget a integrar aplicaciones en Azure AD rápidamente y le permite:</span><span class="sxs-lookup"><span data-stu-id="3bedd-107">This is a great way tooget started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="3bedd-108">Habilitar **inicio de sesión único para los usuarios** por almacenar de forma segura y reproducir los nombres de usuario y contraseñas de aplicación hello ha integrado con Azure AD</span><span class="sxs-lookup"><span data-stu-id="3bedd-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="3bedd-109">**Compatibilidad con aplicaciones que requieren varios campos de inicio de sesión** para aplicaciones que requieren algo más que simplemente username y password campos toosign en</span><span class="sxs-lookup"><span data-stu-id="3bedd-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="3bedd-110">**Personalizar las etiquetas de hello** Hola username y password de campos de entrada, los usuarios verán en hello [Panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) cuando escriban sus credenciales</span><span class="sxs-lookup"><span data-stu-id="3bedd-110">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="3bedd-111">Permitir la **usuarios** tooprovide sus propios nombres de usuario y contraseñas para cuentas de aplicación existente que está escribiendo en manualmente en hello [Panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="3bedd-111">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="3bedd-112">Permitir que un **miembro del grupo de negocios de hello** contraseñas y nombres de usuario de hello toospecify asignan tooa usuario mediante hello [autoservicio acceso a la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) característica</span><span class="sxs-lookup"><span data-stu-id="3bedd-112">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="3bedd-113">Permitir que un **administrador** toospecify Hola nombres y contraseñas asignadas tooa usuario mediante las credenciales de actualización de hello característica cuando [asignar una aplicación de usuario tooan](#assign-a-user-to-an-application-directly)</span><span class="sxs-lookup"><span data-stu-id="3bedd-113">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="3bedd-114">Permitir que un **administrador** toospecify Hola compartido username o la contraseña utilizada por un grupo de personas mediante las credenciales de actualización de hello característica cuando [asignar una aplicación de tooan de grupo](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="3bedd-114">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="3bedd-115">A continuación se describe cómo habilitar [basado en contraseña Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan aplicación que ya está en hello [Galería de aplicaciones de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="3bedd-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan application that is already in hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="3bedd-116">Introducción a los pasos necesarios</span><span class="sxs-lookup"><span data-stu-id="3bedd-116">Overview of steps required</span></span>
<span data-ttu-id="3bedd-117">una aplicación desde la Galería de Azure AD de hello tooconfigure debe:</span><span class="sxs-lookup"><span data-stu-id="3bedd-117">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="3bedd-118">Agregar una aplicación de la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="3bedd-118">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="3bedd-119">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="3bedd-119">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="3bedd-120">Asignar Hola aplicación tooa usuario o un grupo</span><span class="sxs-lookup"><span data-stu-id="3bedd-120">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="3bedd-121">Asignar una aplicación de usuario tooan directamente</span><span class="sxs-lookup"><span data-stu-id="3bedd-121">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="3bedd-122">Asignar a un grupo de tooa aplicación directamente</span><span class="sxs-lookup"><span data-stu-id="3bedd-122">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="3bedd-123">Agregar una aplicación de la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="3bedd-123">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="3bedd-124">tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="3bedd-124">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="3bedd-125">Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="3bedd-125">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="3bedd-126">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="3bedd-126">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3bedd-127">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3bedd-127">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3bedd-128">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3bedd-128">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3bedd-129">Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja</span><span class="sxs-lookup"><span data-stu-id="3bedd-129">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="3bedd-130">Hola **escriba un nombre** cuadro de texto de hello **agregar a partir de la Galería de hello** sección, escriba un nombre Hola de aplicación hello</span><span class="sxs-lookup"><span data-stu-id="3bedd-130">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="3bedd-131">Seleccionar aplicación hello tooconfigure que desee para el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="3bedd-131">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="3bedd-132">Antes de agregar la aplicación hello, puede cambiar su nombre de hello **nombre** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3bedd-132">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="3bedd-133">Haga clic en **agregar** button, aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="3bedd-133">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="3bedd-134">Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="3bedd-134">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="3bedd-135">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="3bedd-135">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="3bedd-136">tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="3bedd-136">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="3bedd-137">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="3bedd-137">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3bedd-138">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="3bedd-138">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3bedd-139">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3bedd-139">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3bedd-140">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3bedd-140">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3bedd-141">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3bedd-141">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3bedd-142">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="3bedd-142">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3bedd-143">Seleccione la aplicación hello desea tooconfigure inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="3bedd-143">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="3bedd-144">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3bedd-144">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3bedd-145">Modo de hello seleccione **sesión basada en contraseña.**</span><span class="sxs-lookup"><span data-stu-id="3bedd-145">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="3bedd-146">[Asignar usuarios de aplicación de toohello](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="3bedd-146">[Assign users toohello application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="3bedd-147">Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="3bedd-147">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="3bedd-148">En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.</span><span class="sxs-lookup"><span data-stu-id="3bedd-148">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="3bedd-149">Asignar una aplicación de usuario tooan directamente</span><span class="sxs-lookup"><span data-stu-id="3bedd-149">Assign a user tooan application directly</span></span>

<span data-ttu-id="3bedd-150">tooassign uno o más usuarios tooan application directamente, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="3bedd-150">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="3bedd-151">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="3bedd-151">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3bedd-152">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="3bedd-152">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3bedd-153">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3bedd-153">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3bedd-154">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3bedd-154">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3bedd-155">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3bedd-155">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3bedd-156">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="3bedd-156">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3bedd-157">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="3bedd-157">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="3bedd-158">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3bedd-158">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3bedd-159">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="3bedd-159">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="3bedd-160">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="3bedd-160">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="3bedd-161">Tipo de hello **nombre completo** o **dirección de correo electrónico** del usuario de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="3bedd-161">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="3bedd-162">Mantenga el mouse sobre hello **usuario** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="3bedd-162">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="3bedd-163">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla toohello del siguiente usuario su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="3bedd-163">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="3bedd-164">**Opcional:** si lo desea demasiado**agregar más de un usuario**, tipo de otro **nombre completo** o **dirección de correo electrónico** en hello **buscar por nombre o dirección de correo electrónico** cuadro de búsqueda y haga clic en hello casilla tooadd este usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="3bedd-164">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="3bedd-165">Cuando haya terminado de seleccionar usuarios, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="3bedd-165">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="3bedd-166">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** hoja tooselect un rol tooassign toohello usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="3bedd-166">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="3bedd-167">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="3bedd-167">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="3bedd-168">Asignar a un grupo de tooa aplicación directamente</span><span class="sxs-lookup"><span data-stu-id="3bedd-168">Assign an application tooa group directly</span></span>

<span data-ttu-id="3bedd-169">tooassign uno o más grupos de aplicación de tooan directamente, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="3bedd-169">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="3bedd-170">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="3bedd-170">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3bedd-171">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="3bedd-171">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3bedd-172">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3bedd-172">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3bedd-173">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3bedd-173">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3bedd-174">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3bedd-174">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3bedd-175">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="3bedd-175">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3bedd-176">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="3bedd-176">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="3bedd-177">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="3bedd-177">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3bedd-178">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="3bedd-178">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="3bedd-179">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="3bedd-179">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="3bedd-180">Tipo de hello **nombre de grupo completa** del grupo de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="3bedd-180">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="3bedd-181">Mantenga el mouse sobre hello **grupo** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="3bedd-181">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="3bedd-182">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla siguiente toohello del grupo su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="3bedd-182">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="3bedd-183">**Opcional:** si lo desea demasiado**agregar más de un grupo**, tipo de otro **nombre de grupo completa** en hello **buscar por nombre o dirección de correo** cuadro de búsqueda, y haga clic en hello casilla tooadd este grupo toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="3bedd-183">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="3bedd-184">Cuando haya terminado la selección de grupos, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="3bedd-184">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="3bedd-185">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** grupos hoja tooselect una toohello tooassign de rol que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="3bedd-185">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="3bedd-186">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello grupos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="3bedd-186">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="3bedd-187">Después de un breve período, los usuarios de Hola que seleccionó ser capaz de toolaunch estas aplicaciones en Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3bedd-187">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bedd-188">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3bedd-188">Next steps</span></span>
[<span data-ttu-id="3bedd-189">Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="3bedd-189">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

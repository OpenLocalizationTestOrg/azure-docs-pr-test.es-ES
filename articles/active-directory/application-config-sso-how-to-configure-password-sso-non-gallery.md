---
title: "aaaHow tooconfigure contraseña inicio de sesión único para una galería no applicationn | Documentos de Microsoft"
description: "Cómo tooconfigure una aplicación no galería personalizada para proteger basada en contraseña de inicio de sesión único cuando no se encuentra en hello Galería de aplicaciones de Azure AD"
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="ccf74-103">¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación no Galería</span><span class="sxs-lookup"><span data-stu-id="ccf74-103">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="ccf74-104">Además opciones toohello encuentra Galería de aplicaciones de hello Azure AD, también tiene Hola opción tooadd una **aplicación no gallery** cuando aplicación Hola que desea no aparece.</span><span class="sxs-lookup"><span data-stu-id="ccf74-104">In addition toohello choices found within hello Azure AD Application Gallery, you also have hello option tooadd a **non-gallery application** when hello application you want is not listed there.</span></span> <span data-ttu-id="ccf74-105">Con esta capacidad, puede agregar todas las aplicaciones que ya existe en su organización, o cualquier aplicación de terceros que puedan usar desde un proveedor que ya no forma parte del programa Hola a [Galería de aplicaciones de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="ccf74-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="ccf74-106">Una vez que agregue una aplicación no galería, puede configurar solo inicio de sesión método hello esta aplicación utiliza seleccionando hello **Single Sign-on** elemento de navegación en una aplicación empresarial de hello [Portal de Azure ](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ccf74-106">Once you add a non-gallery application, you can then configure hello Single sign-on method this application uses by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="ccf74-107">Uno de hello Single Sign-on métodos disponible tooyou es hello [basado en contraseña Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opción.</span><span class="sxs-lookup"><span data-stu-id="ccf74-107">One of hello Single Sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="ccf74-108">Con hello **agregar una aplicación de la Galería no** experiencia, puede integrar cualquier aplicación que representa un nombre de usuario basado en HTML y la contraseña de entrada de campo, incluso si no está en nuestro conjunto de aplicaciones previamente integradas.</span><span class="sxs-lookup"><span data-stu-id="ccf74-108">With hello **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="ccf74-109">Esto funciona de manera de Hello es una página de barrido de tecnología que forma parte del programa Hola a extensión del Panel de acceso que nos permite tooauto-se detectan los campos de entrada de nombre de usuario y contraseña, almacene de forma segura para la instancia de la aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="ccf74-109">hello way this works is by a page scraping technology that is part of hello Access Panel extension that allows us tooauto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="ccf74-110">A continuación, reproduzca de forma segura nombres de usuario y campos de toothose las contraseñas cuando un usuario navega toothat aplicación en el panel de acceso de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="ccf74-110">Then securely replay usernames and passwords toothose fields when a user navigates toothat application on hello application access panel.</span></span>

<span data-ttu-id="ccf74-111">Se trata de una excelente manera de tooget a integrar rápidamente cualquier tipo de aplicación en Azure AD y le permite:</span><span class="sxs-lookup"><span data-stu-id="ccf74-111">This is a great way tooget started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="ccf74-112">Integrar **cualquier aplicación de Hola a todos** con el inquilino de Azure AD, siempre y cuando se representa un campo de entrada de usuario y la contraseña HTML</span><span class="sxs-lookup"><span data-stu-id="ccf74-112">Integrate **any application in hello world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="ccf74-113">Habilitar **inicio de sesión único para los usuarios** por almacenar de forma segura y reproducir los nombres de usuario y contraseñas de aplicación hello ha integrado con Azure AD</span><span class="sxs-lookup"><span data-stu-id="ccf74-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="ccf74-114">**La detección automática de entrada** campos para cualquier aplicación y le permiten toomanually detectar esos campos mediante Hola extensión de explorador del Panel de acceso, en caso de que la detección automática no encontrarlos</span><span class="sxs-lookup"><span data-stu-id="ccf74-114">**Auto-detect input** fields for any application and allow you toomanually detect those fields using hello Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="ccf74-115">**Compatibilidad con aplicaciones que requieren varios campos de inicio de sesión** para aplicaciones que requieren algo más que simplemente username y password campos toosign en</span><span class="sxs-lookup"><span data-stu-id="ccf74-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="ccf74-116">**Personalizar las etiquetas de hello** Hola username y password de campos de entrada, los usuarios verán en hello [Panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) cuando escriban sus credenciales</span><span class="sxs-lookup"><span data-stu-id="ccf74-116">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="ccf74-117">Permitir la **usuarios** tooprovide sus propios nombres de usuario y contraseñas para cuentas de aplicación existente que está escribiendo en manualmente en hello [Panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="ccf74-117">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="ccf74-118">Permitir que un **miembro del grupo de negocios de hello** contraseñas y nombres de usuario de hello toospecify asignan tooa usuario mediante hello [autoservicio acceso a la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) característica</span><span class="sxs-lookup"><span data-stu-id="ccf74-118">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="ccf74-119">Permitir que un **administrador** toospecify Hola nombres y contraseñas asignadas tooa usuario mediante las credenciales de actualización de hello característica cuando [asignar una aplicación de usuario tooan](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="ccf74-119">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="ccf74-120">Permitir que un **administrador** toospecify Hola compartido username o la contraseña utilizada por un grupo de personas mediante las credenciales de actualización de hello característica cuando [asignar una aplicación de tooan de grupo](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="ccf74-120">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="ccf74-121">A continuación se describe cómo habilitar [basado en contraseña Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) aplicación tooany agregar utilizando hello **agregar una aplicación de la Galería no** experimentar.</span><span class="sxs-lookup"><span data-stu-id="ccf74-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany application that you add using hello **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="ccf74-122">Introducción a los pasos necesarios</span><span class="sxs-lookup"><span data-stu-id="ccf74-122">Overview of steps required</span></span>

<span data-ttu-id="ccf74-123">una aplicación desde la Galería de Azure AD de hello tooconfigure debe:</span><span class="sxs-lookup"><span data-stu-id="ccf74-123">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="ccf74-124">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="ccf74-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="ccf74-125">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="ccf74-125">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="ccf74-126">Asignar Hola aplicación tooa usuario o un grupo</span><span class="sxs-lookup"><span data-stu-id="ccf74-126">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="ccf74-127">Asignar una aplicación de usuario tooan directamente</span><span class="sxs-lookup"><span data-stu-id="ccf74-127">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="ccf74-128">Asignar a un grupo de tooa aplicación directamente</span><span class="sxs-lookup"><span data-stu-id="ccf74-128">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="ccf74-129">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="ccf74-129">Add a non-gallery application</span></span>

<span data-ttu-id="ccf74-130">tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="ccf74-130">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="ccf74-131">Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="ccf74-131">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="ccf74-132">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="ccf74-132">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ccf74-133">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="ccf74-133">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ccf74-134">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ccf74-134">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ccf74-135">Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja</span><span class="sxs-lookup"><span data-stu-id="ccf74-135">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="ccf74-136">Haga clic en **Aplicación situada fuera de la galería**.</span><span class="sxs-lookup"><span data-stu-id="ccf74-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="ccf74-137">Escriba el nombre de saludo de la aplicación Hola **nombre** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="ccf74-137">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="ccf74-138">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ccf74-138">Select **Add.**</span></span>

<span data-ttu-id="ccf74-139">Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="ccf74-139">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="ccf74-140">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="ccf74-140">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="ccf74-141">tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="ccf74-141">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="ccf74-142">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="ccf74-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ccf74-143">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="ccf74-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ccf74-144">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="ccf74-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ccf74-145">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ccf74-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ccf74-146">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ccf74-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="ccf74-147">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="ccf74-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ccf74-148">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ccf74-148">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="ccf74-149">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="ccf74-149">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ccf74-150">Modo de hello seleccione **sesión basada en contraseña.**</span><span class="sxs-lookup"><span data-stu-id="ccf74-150">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="ccf74-151">Escriba hello **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="ccf74-151">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="ccf74-152">Se trata de dirección URL de Hola donde los usuarios escribir su toosign en nombre de usuario y contraseña a.</span><span class="sxs-lookup"><span data-stu-id="ccf74-152">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="ccf74-153">Asegúrese de que está visible en la dirección URL de Hola Hola campos inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ccf74-153">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="ccf74-154">Asignar a usuarios de aplicación de toohello.</span><span class="sxs-lookup"><span data-stu-id="ccf74-154">Assign users toohello application.</span></span>

11. <span data-ttu-id="ccf74-155">Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="ccf74-155">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="ccf74-156">En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.</span><span class="sxs-lookup"><span data-stu-id="ccf74-156">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="ccf74-157">Asignar una aplicación de usuario tooan directamente</span><span class="sxs-lookup"><span data-stu-id="ccf74-157">Assign a user tooan application directly</span></span>

<span data-ttu-id="ccf74-158">tooassign uno o más usuarios tooan application directamente, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="ccf74-158">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="ccf74-159">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="ccf74-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="ccf74-160">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="ccf74-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ccf74-161">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="ccf74-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ccf74-162">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ccf74-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ccf74-163">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ccf74-163">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="ccf74-164">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="ccf74-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ccf74-165">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="ccf74-165">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="ccf74-166">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="ccf74-166">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ccf74-167">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="ccf74-167">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="ccf74-168">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="ccf74-168">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="ccf74-169">Tipo de hello **nombre completo** o **dirección de correo electrónico** del usuario de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="ccf74-169">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="ccf74-170">Mantenga el mouse sobre hello **usuario** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="ccf74-170">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="ccf74-171">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla toohello del siguiente usuario su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="ccf74-171">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="ccf74-172">**Opcional:** si lo desea demasiado**agregar más de un usuario**, tipo de otro **nombre completo** o **dirección de correo electrónico** en hello **buscar por nombre o dirección de correo electrónico** cuadro de búsqueda y haga clic en hello casilla tooadd este usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="ccf74-172">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="ccf74-173">Cuando haya terminado de seleccionar usuarios, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="ccf74-173">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="ccf74-174">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** hoja tooselect un rol tooassign toohello usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="ccf74-174">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="ccf74-175">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="ccf74-175">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="ccf74-176">Asignar a un grupo de tooa aplicación directamente</span><span class="sxs-lookup"><span data-stu-id="ccf74-176">Assign an application tooa group directly</span></span>

<span data-ttu-id="ccf74-177">tooassign uno o más grupos de aplicación de tooan directamente, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="ccf74-177">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="ccf74-178">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="ccf74-178">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="ccf74-179">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="ccf74-179">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ccf74-180">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="ccf74-180">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ccf74-181">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ccf74-181">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ccf74-182">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ccf74-182">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="ccf74-183">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="ccf74-183">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="ccf74-184">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="ccf74-184">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="ccf74-185">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="ccf74-185">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ccf74-186">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="ccf74-186">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="ccf74-187">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="ccf74-187">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="ccf74-188">Tipo de hello **nombre de grupo completa** del grupo de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="ccf74-188">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="ccf74-189">Mantenga el mouse sobre hello **grupo** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="ccf74-189">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="ccf74-190">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla siguiente toohello del grupo su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="ccf74-190">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="ccf74-191">**Opcional:** si lo desea demasiado**agregar más de un grupo**, tipo de otro **nombre de grupo completa** en hello **buscar por nombre o dirección de correo** cuadro de búsqueda, y haga clic en hello casilla tooadd este grupo toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="ccf74-191">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="ccf74-192">Cuando haya terminado la selección de grupos, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="ccf74-192">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="ccf74-193">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** grupos hoja tooselect una toohello tooassign de rol que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="ccf74-193">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="ccf74-194">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello grupos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="ccf74-194">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="ccf74-195">Después de un breve período, los usuarios de Hola que seleccionó ser capaz de toolaunch estas aplicaciones en Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ccf74-195">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccf74-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ccf74-196">Next steps</span></span>
[<span data-ttu-id="ccf74-197">Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="ccf74-197">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

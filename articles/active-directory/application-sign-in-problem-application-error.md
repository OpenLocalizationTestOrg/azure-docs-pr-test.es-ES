---
title: "aaaError en la página de la aplicación después de iniciar sesión | Documentos de Microsoft"
description: "Cómo tooresolve problemas con Azure AD iniciar sesión cuando la propia aplicación Hola emite un error"
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
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="d433c-103">Error en la página de aplicación después de iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="d433c-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="d433c-104">En este escenario, Azure AD ha iniciado sesión el usuario de hello en pero aplicación hello muestra un error no permitir el inicio de sesión de hello usuario toosuccessfully finalizar hello en flujo.</span><span class="sxs-lookup"><span data-stu-id="d433c-104">In this scenario, Azure AD has signed hello user in, but hello application is displaying an error not allowing hello user toosuccessfully finish hello sign in flow.</span></span> <span data-ttu-id="d433c-105">En este escenario, aplicación hello no acepta problema de respuesta de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d433c-105">In this scenario, hello application is not accepting hello response issue by Azure AD.</span></span>

<span data-ttu-id="d433c-106">Hay algunos motivos posibles por qué aplicación hello no aceptó la respuesta de Hola de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d433c-106">There are some possible reasons why hello application didn’t accept hello response from Azure AD.</span></span> <span data-ttu-id="d433c-107">Si el error de hello en la aplicación hello no es lo suficientemente claro tooknow ¿qué es, a continuación, falta de respuesta de hello:</span><span class="sxs-lookup"><span data-stu-id="d433c-107">If hello error in hello application is not clear enough tooknow what is missing in hello response, then:</span></span>

-   <span data-ttu-id="d433c-108">Si aplicación hello Galería hello Azure AD, compruebe ha seguido todos los pasos de hello en el artículo hello [cómo toodebug basado en SAML single sign-on tooapplications en Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="d433c-108">If hello application is hello Azure AD Gallery, verify you have followed all hello steps in hello article [How toodebug SAML-based single sign-on tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="d433c-109">Utilice una herramienta como [Fiddler](http://www.telerik.com/fiddler) toocapture SAML solicitud, respuesta de SAML y el token SAML.</span><span class="sxs-lookup"><span data-stu-id="d433c-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) toocapture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="d433c-110">Compartir respuesta de SAML de hello con hello aplicación proveedor tooknow novedades que faltan.</span><span class="sxs-lookup"><span data-stu-id="d433c-110">Share hello SAML response with hello application vendor tooknow what is missing.</span></span>

## <a name="missing-attributes-in-hello-saml-response"></a><span data-ttu-id="d433c-111">Atributos que faltan en hello respuesta de SAML</span><span class="sxs-lookup"><span data-stu-id="d433c-111">Missing attributes in hello SAML response</span></span>

<span data-ttu-id="d433c-112">tooadd un atributo en toobe de configuración de Azure AD Hola enviado como respuesta de hello Azure AD, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="d433c-112">tooadd an attribute in hello Azure AD configuration toobe sent in hello Azure AD response, follow hello steps below:</span></span>

1.  <span data-ttu-id="d433c-113">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="d433c-113">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d433c-114">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="d433c-114">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d433c-115">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="d433c-115">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d433c-116">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d433c-116">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d433c-117">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d433c-117">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="d433c-118">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="d433c-118">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d433c-119">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d433c-119">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d433c-120">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d433c-120">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d433c-121">Haga clic en **ver y editar atributos de todos los demás usuarios en** hello **atributos de usuario** Hola de sección tooedit atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="d433c-121">click **View and edit all other user attributes under** hello **User Attributes** section tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="d433c-122">tooadd un atributo:</span><span class="sxs-lookup"><span data-stu-id="d433c-122">tooadd an attribute:</span></span>

   * <span data-ttu-id="d433c-123">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="d433c-123">click **Add attribute**.</span></span> <span data-ttu-id="d433c-124">Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="d433c-124">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   * <span data-ttu-id="d433c-125">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d433c-125">Click **Save.**</span></span> <span data-ttu-id="d433c-126">Verá el nuevo atributo de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="d433c-126">You see hello new attribute in hello table.</span></span>

9.  <span data-ttu-id="d433c-127">Guardar configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="d433c-127">Save hello configuration.</span></span>

<span data-ttu-id="d433c-128">Próxima vez Hola usuario inicia sesión en la aplicación toohello, Azure AD Enviar nuevo atributo de Hola Hola respuesta de SAML.</span><span class="sxs-lookup"><span data-stu-id="d433c-128">Next time hello user signs in toohello application, Azure AD send hello new attribute in hello SAML response.</span></span>

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="d433c-129">aplicación Hello espera un valor de identificador de usuario diferente o un formato</span><span class="sxs-lookup"><span data-stu-id="d433c-129">hello application expects a different User Identifier value or format</span></span>

<span data-ttu-id="d433c-130">Hello aplicación de inicio de sesión toohello error porque Hola respuesta de SAML no encuentra los atributos, como los roles o porque la aplicación hello espera un formato diferente para el atributo de EntityID Hola.</span><span class="sxs-lookup"><span data-stu-id="d433c-130">hello sign-in toohello application is failing because hello SAML response is missing attributes such as roles or because hello application is expecting a different format for hello EntityID attribute.</span></span>

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a><span data-ttu-id="d433c-131">Agregue un atributo en la configuración de la aplicación hello Azure AD:</span><span class="sxs-lookup"><span data-stu-id="d433c-131">Add an attribute in hello Azure AD application configuration:</span></span>

<span data-ttu-id="d433c-132">Hola toochange valor de identificador de usuario, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d433c-132">toochange hello User Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="d433c-133">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="d433c-133">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d433c-134">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="d433c-134">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d433c-135">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="d433c-135">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d433c-136">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d433c-136">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d433c-137">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d433c-137">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="d433c-138">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="d433c-138">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d433c-139">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d433c-139">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d433c-140">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d433c-140">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d433c-141">En hello **atributos de usuario**, seleccione Hola identificador único para los usuarios en hello **identificador de usuario** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="d433c-141">Under hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="d433c-142">Cambiar el formato de EntityID (Identificador de usuario)</span><span class="sxs-lookup"><span data-stu-id="d433c-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="d433c-143">Si la aplicación hello espera otro formato para el atributo de EntityID Hola.</span><span class="sxs-lookup"><span data-stu-id="d433c-143">If hello application expects another format for hello EntityID attribute.</span></span> <span data-ttu-id="d433c-144">A continuación, no será formato de tooselect capaz de hello EntityID (identificador de usuario) que Azure AD envía toohello aplicación en respuesta Hola después de la autenticación de usuario.</span><span class="sxs-lookup"><span data-stu-id="d433c-144">Then, you won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="d433c-145">Azure formato AD seleccione Hola Hola NameID atributo (identificador de usuario) en función de valor de hello seleccionado u Hola formato solicitado por la aplicación hello en hello AuthRequest de SAML.</span><span class="sxs-lookup"><span data-stu-id="d433c-145">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="d433c-146">Para obtener más información, visite el artículo de hello [protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) en hello sección NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="d433c-146">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a><span data-ttu-id="d433c-147">aplicación Hello espera un método de firma diferente para hello respuesta de SAML</span><span class="sxs-lookup"><span data-stu-id="d433c-147">hello application expects a different signature method for hello SAML response</span></span>

<span data-ttu-id="d433c-148">toochange ¿qué partes del token SAML de hello están firmados digitalmente por Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d433c-148">toochange what parts of hello SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="d433c-149">Siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="d433c-149">Follow hello steps below:</span></span>

1.  <span data-ttu-id="d433c-150">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="d433c-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d433c-151">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="d433c-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d433c-152">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="d433c-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d433c-153">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d433c-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d433c-154">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d433c-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d433c-155">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="d433c-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d433c-156">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d433c-156">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d433c-157">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d433c-157">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d433c-158">Haga clic en **Mostrar configuración de firma de certificado avanzada** en hello **el certificado de firma de SAML** sección.</span><span class="sxs-lookup"><span data-stu-id="d433c-158">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="d433c-159">Seleccione Hola adecuado **opción firma** esperado por la aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="d433c-159">Select hello appropriate **Signing Option** expected by hello application:</span></span>

  * <span data-ttu-id="d433c-160">Firmar respuesta SAML</span><span class="sxs-lookup"><span data-stu-id="d433c-160">Sign SAML response</span></span>

  * <span data-ttu-id="d433c-161">Firmar respuesta y aserción SAML</span><span class="sxs-lookup"><span data-stu-id="d433c-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="d433c-162">Firmar aserción SAML</span><span class="sxs-lookup"><span data-stu-id="d433c-162">Sign SAML assertion</span></span>

<span data-ttu-id="d433c-163">Próxima vez Hola usuario inicia sesión en la aplicación toohello, inicio de sesión de Azure AD Hola parte de respuesta SAML de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="d433c-163">Next time hello user signs in toohello application, Azure AD sign hello part of hello SAML response selected.</span></span>

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a><span data-ttu-id="d433c-164">aplicación Hello espera Hola firma toobe algoritmo SHA-1</span><span class="sxs-lookup"><span data-stu-id="d433c-164">hello application expects hello signing algorithm toobe SHA-1</span></span>

<span data-ttu-id="d433c-165">De forma predeterminada, Azure AD firma de token SAML de hello mediante Hola mayoría algoritmo de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d433c-165">By default, Azure AD signs hello SAML token using hello most security algorithm.</span></span> <span data-ttu-id="d433c-166">No se recomienda cambiar el algoritmo de inicio de sesión de hello tooSHA-1, a menos que requiera la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d433c-166">Changing hello sign algorithm tooSHA-1 is not recommended unless required by hello application.</span></span>

<span data-ttu-id="d433c-167">toochange Hola algoritmo de firma, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="d433c-167">toochange hello signing algorithm, follow hello steps below:</span></span>

1.  <span data-ttu-id="d433c-168">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="d433c-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d433c-169">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="d433c-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d433c-170">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="d433c-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d433c-171">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d433c-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d433c-172">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d433c-172">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="d433c-173">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="d433c-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d433c-174">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d433c-174">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d433c-175">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d433c-175">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d433c-176">Haga clic en **Mostrar configuración de firma de certificado avanzada** en hello **el certificado de firma de SAML** sección.</span><span class="sxs-lookup"><span data-stu-id="d433c-176">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="d433c-177">Seleccione SHA-1, Hola **algoritmo de firma**.</span><span class="sxs-lookup"><span data-stu-id="d433c-177">Select SHA-1, in hello **Signing Algorithm**.</span></span>

<span data-ttu-id="d433c-178">Próxima vez Hola usuario inicia sesión en la aplicación toohello, inicio de sesión de Azure AD Hola token SAML utilizando el algoritmo SHA-1.</span><span class="sxs-lookup"><span data-stu-id="d433c-178">Next time hello user signs in toohello application, Azure AD sign hello SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d433c-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d433c-179">Next steps</span></span>
[<span data-ttu-id="d433c-180">¿Cómo toodebug basado en SAML single sign-on tooapplications en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d433c-180">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)

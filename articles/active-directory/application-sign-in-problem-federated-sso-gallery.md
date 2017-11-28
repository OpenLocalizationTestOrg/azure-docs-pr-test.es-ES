---
title: "aaaProblems iniciar sesión en la aplicación de la Galería de tooa configurado para federado inicio de sesión único | Documentos de Microsoft"
description: "Guía de errores específicos de hello al iniciar sesión en una aplicación que se ha configurado para basado en SAML federado inicio de sesión único con Azure AD"
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
ms.openlocfilehash: ba20a4904860cf063967029cad33fb80f16e4956
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="f6d4f-103">Problemas para iniciar sesión en la aplicación de la Galería de tooa configurada para un inicio de sesión único federado</span><span class="sxs-lookup"><span data-stu-id="f6d4f-103">Problems signing in tooa gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="f6d4f-104">tootroubleshoot su problema, necesita tooverify configuración de la aplicación hello en Azure AD como sigue:</span><span class="sxs-lookup"><span data-stu-id="f6d4f-104">tootroubleshoot your problem, you need tooverify hello application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="f6d4f-105">Ha seguido todos los pasos de configuración de Hola para hello aplicación de la Galería de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-105">You have followed all hello configuration steps for hello Azure AD gallery application.</span></span>

-   <span data-ttu-id="f6d4f-106">Identificador Hello y dirección URL de respuesta que se configura en AAD coinciden únicamente valores esperados en la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="f6d4f-106">hello Identifier and Reply URL configured in AAD match they expected values in hello application</span></span>

-   <span data-ttu-id="f6d4f-107">Que haya asignado a los usuarios de aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="f6d4f-107">You have assigned users toohello application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="f6d4f-108">No se encontró la aplicación en el directorio</span><span class="sxs-lookup"><span data-stu-id="f6d4f-108">Application not found in directory</span></span>

<span data-ttu-id="f6d4f-109">*AADSTS70001 de error: No se encontró la aplicación con el identificador 'https://contoso.com' en el directorio de hello*.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in hello directory*.</span></span>

<span data-ttu-id="f6d4f-110">**Causa posible**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-110">**Possible cause**</span></span>

<span data-ttu-id="f6d4f-111">atributo de emisor de Hola se envía desde Hola aplicación tooAzure AD en la solicitud SAML de hello no coincide con el valor de identificador hello configurado en la aplicación hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-111">hello Issuer attribute sends from hello application tooAzure AD in hello SAML request doesn’t match hello Identifier value configured in hello application Azure AD.</span></span>

<span data-ttu-id="f6d4f-112">**Resolución**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-112">**Resolution**</span></span>

<span data-ttu-id="f6d4f-113">Asegúrese de que ese atributo de emisor de hello en solicitud SAML de Hola que coincidentes Hola valor de identificador configurado en Azure AD:</span><span class="sxs-lookup"><span data-stu-id="f6d4f-113">Ensure that hello Issuer attribute in hello SAML request it’s matching hello Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="f6d4f-114">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-114">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f6d4f-115">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-115">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f6d4f-116">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-116">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f6d4f-117">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-117">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f6d4f-118">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-118">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="f6d4f-119">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-119">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="f6d4f-120">Seleccione la aplicación hello desea tooconfigure inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="f6d4f-120">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="f6d4f-121">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-121">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f6d4f-122">Vaya demasiado**dominio y las direcciones URL** sección.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-122">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="f6d4f-123">Compruebe que Hola el valor en hello identificador cuadro de texto es que coincida con el valor de hello para el valor de identificador de hello muestra error Hola.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-123">Verify that hello value in hello Identifier textbox is matching hello value for hello identifier value displayed in hello error.</span></span>

<span data-ttu-id="f6d4f-124">Después de que ha actualizado el valor de identificador hello en Azure AD y su valor de hello coincidente envía por la aplicación hello en solicitud SAML de hello, debe ser capaz de toosign en toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-124">After you have updated hello Identifier value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a><span data-ttu-id="f6d4f-125">dirección de respuesta de Hello no coincide con direcciones de respuesta de hello configuradas para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-125">hello reply address does not match hello reply addresses configured for hello application.</span></span>

<span data-ttu-id="f6d4f-126">*Error AADSTS50011: dirección de respuesta de hello 'https://contoso.com' no coincide con direcciones de respuesta de hello configuradas para la aplicación hello*</span><span class="sxs-lookup"><span data-stu-id="f6d4f-126">*Error AADSTS50011: hello reply address ‘https://contoso.com’ does not match hello reply addresses configured for hello application*</span></span>

<span data-ttu-id="f6d4f-127">**Causa posible**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-127">**Possible cause**</span></span>

<span data-ttu-id="f6d4f-128">Hola AssertionConsumerServiceURL valor en la solicitud SAML de hello no coincide con valor de dirección URL de respuesta de Hola o un modelo configurado en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-128">hello AssertionConsumerServiceURL value in hello SAML request doesn't match hello Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="f6d4f-129">Hola AssertionConsumerServiceURL valor en la solicitud SAML de hello es dirección URL de hello consulte Error Hola.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-129">hello AssertionConsumerServiceURL value in hello SAML request is hello URL you see in hello error.</span></span>

<span data-ttu-id="f6d4f-130">**Resolución**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-130">**Resolution**</span></span>

<span data-ttu-id="f6d4f-131">Asegúrese de ese valor de AssertionConsumerServiceURL hello en solicitud SAML de hello su coincidencia Hola valor de dirección URL de respuesta configurado en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-131">Ensure that hello AssertionConsumerServiceURL value in hello SAML request it's matching hello Reply URL value configured in Azure AD.</span></span>

1.  <span data-ttu-id="f6d4f-132">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-132">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f6d4f-133">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-133">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f6d4f-134">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-134">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f6d4f-135">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-135">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f6d4f-136">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-136">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="f6d4f-137">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-137">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="f6d4f-138">Seleccione la aplicación hello desea tooconfigure inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="f6d4f-138">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="f6d4f-139">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-139">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f6d4f-140">Vaya demasiado**dominio y las direcciones URL** sección.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-140">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="f6d4f-141">Compruebe o actualice el valor de Hola Hola valor AssertionConsumerServiceURL en la solicitud SAML de Hola de Hola de toomatch de cuadro de texto dirección URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-141">Verify or update hello value in hello Reply URL textbox toomatch hello AssertionConsumerServiceURL value in hello SAML request.</span></span>  
    * <span data-ttu-id="f6d4f-142">Si no ve el cuadro de texto de dirección URL de respuesta de hello, seleccione hello **mostrar avanzadas de configuración de direcciones URL** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-142">If you don't see hello Reply URL textbox, select hello **Show advanced URL settings** checkbox.</span></span>

<span data-ttu-id="f6d4f-143">Una vez que ha actualizado el valor de dirección URL de respuesta de hello en Azure AD y tiene que coincide con el valor de hello envía por la aplicación hello en hello solicitud SAML, debe ser capaz de toosign en toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-143">After you have updated hello Reply URL value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="f6d4f-144">Usuario no asignado a un rol</span><span class="sxs-lookup"><span data-stu-id="f6d4f-144">User not assigned a role</span></span>

<span data-ttu-id="f6d4f-145">*Error AADSTS50105: Hola firmado en el usuario 'brian@contoso.com' no está asignado el rol de tooa para la aplicación hello*.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-145">*Error AADSTS50105: hello signed in user 'brian@contoso.com' is not assigned tooa role for hello application*.</span></span>

<span data-ttu-id="f6d4f-146">**Causa posible**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-146">**Possible cause**</span></span>

<span data-ttu-id="f6d4f-147">usuario Hello no se ha concedido acceso toohello aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-147">hello user has not been granted access toohello application in Azure AD.</span></span>

<span data-ttu-id="f6d4f-148">**Resolución**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-148">**Resolution**</span></span>

<span data-ttu-id="f6d4f-149">tooassign uno o más usuarios tooan application directamente, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="f6d4f-149">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="f6d4f-150">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f6d4f-151">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f6d4f-152">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f6d4f-153">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f6d4f-154">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="f6d4f-155">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="f6d4f-156">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-156">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="f6d4f-157">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-157">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f6d4f-158">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-158">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="f6d4f-159">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-159">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="f6d4f-160">Tipo de hello **nombre completo** o **dirección de correo electrónico** del usuario de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-160">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="f6d4f-161">Mantenga el mouse sobre hello **usuario** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-161">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="f6d4f-162">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla toohello del siguiente usuario su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-162">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="f6d4f-163">**Opcional:** si lo desea demasiado**agregar más de un usuario**, tipo de otro **nombre completo** o **dirección de correo electrónico** en hello **buscar por nombre o dirección de correo electrónico** cuadro de búsqueda y haga clic en hello casilla tooadd este usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-163">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="f6d4f-164">Cuando haya terminado de seleccionar usuarios, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-164">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="f6d4f-165">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** hoja tooselect un rol tooassign toohello usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-165">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="f6d4f-166">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-166">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="f6d4f-167">Tras un breve período de tiempo, los usuarios de Hola que seleccionó ser capaz de toolaunch dichas aplicaciones usan Hola métodos descritos en la sección de descripción de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-167">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="f6d4f-168">No es una solicitud SAML válida</span><span class="sxs-lookup"><span data-stu-id="f6d4f-168">Not a valid SAML Request</span></span>

<span data-ttu-id="f6d4f-169">*Error AADSTS75005: solicitud de hello no es un mensaje de protocolo de Saml2 válido.*</span><span class="sxs-lookup"><span data-stu-id="f6d4f-169">*Error AADSTS75005: hello request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="f6d4f-170">**Causa posible**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-170">**Possible cause**</span></span>

<span data-ttu-id="f6d4f-171">Azure AD no es compatible con hello SAML enviado por la aplicación hello para el inicio de sesión único de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-171">Azure AD doesn’t support hello SAML Request sent by hello application for Single Sign-on.</span></span> <span data-ttu-id="f6d4f-172">Algunos de los problemas más comunes son:</span><span class="sxs-lookup"><span data-stu-id="f6d4f-172">Some common issues are:</span></span>

-   <span data-ttu-id="f6d4f-173">Faltan campos obligatorios en la solicitud SAML de Hola</span><span class="sxs-lookup"><span data-stu-id="f6d4f-173">Missing required fields in hello SAML request</span></span>

-   <span data-ttu-id="f6d4f-174">Método codificado de la solicitud SAML</span><span class="sxs-lookup"><span data-stu-id="f6d4f-174">SAML request encoded method</span></span>

<span data-ttu-id="f6d4f-175">**Resolución**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-175">**Resolution**</span></span>

1.  <span data-ttu-id="f6d4f-176">Capture la solicitud SAML.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-176">Capture SAML request.</span></span> <span data-ttu-id="f6d4f-177">Siga el tutorial de hello [cómo toodebug basado en SAML single sign-on tooapplications en Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn cómo solicitar toocapture Hola SAML.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-177">follow hello tutorial [How toodebug SAML-based single sign-on tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn how toocapture hello SAML request.</span></span>

2.  <span data-ttu-id="f6d4f-178">Póngase en contacto con el proveedor de la aplicación hello y recurso compartido:</span><span class="sxs-lookup"><span data-stu-id="f6d4f-178">Contact hello application vendor and share:</span></span>

   -   <span data-ttu-id="f6d4f-179">La solicitud SAML</span><span class="sxs-lookup"><span data-stu-id="f6d4f-179">SAML request</span></span>

   -   [<span data-ttu-id="f6d4f-180">Los requisitos del protocolo SAML de inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6d4f-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="f6d4f-181">Debe validar admiten la implementación de Azure AD SAML hello para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-181">They should validate they support hello Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="f6d4f-182">Ningún recurso en la lista requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="f6d4f-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="f6d4f-183">*Aplicación de cliente de AADSTS65005:hello de error ha solicitado acceso tooresource ' 00000002-0000-0000-c000-000000000000'. Error en esta solicitud porque Hola de cliente no especifica este recurso en su lista de requiredResourceAccess*.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-183">*Error AADSTS65005:hello client application has requested access tooresource '00000002-0000-0000-c000-000000000000'. This request has failed because hello client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="f6d4f-184">**Causa posible**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-184">**Possible cause**</span></span>

<span data-ttu-id="f6d4f-185">objeto de la aplicación Hello está dañado.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-185">hello application object is corrupted.</span></span>

<span data-ttu-id="f6d4f-186">**Resolución: opción 1**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-186">**Resolution: option 1**</span></span>

<span data-ttu-id="f6d4f-187">problema de hello toosolve, agregue el valor de identificador único de hello en configuración de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-187">toosolve hello problem, add hello unique Identifier value in hello Azure AD configuration.</span></span> <span data-ttu-id="f6d4f-188">tooadd un valor de identificador, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="f6d4f-188">tooadd a Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="f6d4f-189">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-189">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f6d4f-190">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-190">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f6d4f-191">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-191">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f6d4f-192">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-192">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f6d4f-193">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-193">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="f6d4f-194">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-194">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="f6d4f-195">Seleccionar aplicación hello ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-195">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="f6d4f-196">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="f6d4f-196">Once hello application loads, click on hello **Single sign-on** from hello application’s left hand navigation menu</span></span>

8.  <span data-ttu-id="f6d4f-197">En hello **dominio y la dirección URL** sección, compruebe en hello **mostrar avanzadas de configuración de la URL**.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-197">Under hello **Domain and URL** section, check on hello **Show advanced URL settings**.</span></span>

9.  <span data-ttu-id="f6d4f-198">Hola **identificador** cuadro de texto escriba un identificador único para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-198">in hello **Identifier** textbox type a unique identifier for hello application.</span></span>

10. <span data-ttu-id="f6d4f-199">**Guardar** configuración Hola.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-199">**Save** hello configuration.</span></span>


<span data-ttu-id="f6d4f-200">**Resolución: opción 2**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-200">**Resolution option 2**</span></span>

<span data-ttu-id="f6d4f-201">Si la opción 1 anteriormente no funcionaron para usted, intente quitar aplicación hello del directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-201">If option 1 above did not work for you, try removing hello application from hello directory.</span></span> <span data-ttu-id="f6d4f-202">A continuación, agregar y volver a configurar aplicación hello, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="f6d4f-202">Then, add and reconfigure hello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="f6d4f-203">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-203">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f6d4f-204">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-204">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f6d4f-205">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-205">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f6d4f-206">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-206">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f6d4f-207">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-207">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="f6d4f-208">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-208">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="f6d4f-209">Seleccione la aplicación hello desea tooconfigure inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="f6d4f-209">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="f6d4f-210">Haga clic en **eliminar** en hello superior izquierda de la aplicación hello **Introducción** hoja.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-210">Click **Delete** at hello top-left of hello application **Overview** blade.</span></span>

8.  <span data-ttu-id="f6d4f-211">Actualizar Azure AD y agregar la aplicación hello de galería de Azure AD de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-211">Refresh Azure AD and Add hello application from hello Azure AD gallery.</span></span> <span data-ttu-id="f6d4f-212">A continuación, Configure la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="f6d4f-212">Then, Configure hello application</span></span>

<span data-ttu-id="f6d4f-213"><span id="_Hlk477190176" class="anchor"></span>Después de volver a configurar la aplicación hello, debe ser capaz de toosign en toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-213"><span id="_Hlk477190176" class="anchor"></span>After reconfiguring hello application, you should be able toosign in toohello application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="f6d4f-214">Certificado o clave no configurados</span><span class="sxs-lookup"><span data-stu-id="f6d4f-214">Certificate or key not configured</span></span>

<span data-ttu-id="f6d4f-215">*Error AADSTS50003: No hay configurada ninguna clave de firma.*</span><span class="sxs-lookup"><span data-stu-id="f6d4f-215">*Error AADSTS50003: No signing key configured.*</span></span>

<span data-ttu-id="f6d4f-216">**Causa posible**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-216">**Possible cause**</span></span>

<span data-ttu-id="f6d4f-217">objeto de aplicación Hola está dañado y Azure AD no reconoce el certificado de hello configurado para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-217">hello application object is corrupted and Azure AD doesn’t recognize hello certificate configured for hello application.</span></span>

<span data-ttu-id="f6d4f-218">**Resolución**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-218">**Resolution**</span></span>

<span data-ttu-id="f6d4f-219">toodelete y cree un nuevo certificado, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="f6d4f-219">toodelete and create a new certificate, follow hello steps below:</span></span>

1.  <span data-ttu-id="f6d4f-220">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-220">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f6d4f-221">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-221">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f6d4f-222">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-222">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f6d4f-223">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-223">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f6d4f-224">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-224">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="f6d4f-225">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="f6d4f-225">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="f6d4f-226">Seleccione la aplicación hello desea tooconfigure inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="f6d4f-226">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="f6d4f-227">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-227">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f6d4f-228">Haga clic en **crear un nuevo certificado** en hello **SAML certificado de firma** sección.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-228">click **Create new certificate** under hello **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="f6d4f-229">Seleccione la fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-229">Select Expiration date.</span></span> <span data-ttu-id="f6d4f-230">A continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-230">Then, click **Save.**</span></span>

10. <span data-ttu-id="f6d4f-231">Comprobar **activar el nuevo certificado** certificados de active toooverride Hola.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-231">Check **Make new certificate active** toooverride hello active certificate.</span></span> <span data-ttu-id="f6d4f-232">A continuación, haga clic en **guardar** princip Hola de hoja de Hola y acepte el certificado de sustitución de tooactivate Hola.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-232">Then, click **Save** at hello top of hello blade and accept tooactivate hello rollover certificate.</span></span>

11. <span data-ttu-id="f6d4f-233">En hello **el certificado de firma de SAML** sección, haga clic en **quitar** tooremove hello **Unused** certificado.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-233">Under hello **SAML Signing Certificate** section, click **remove** tooremove hello **Unused** certificate.</span></span>

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="f6d4f-234">Problema al personalizar las notificaciones SAML de hello envía tooan aplicación</span><span class="sxs-lookup"><span data-stu-id="f6d4f-234">Problem when customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="f6d4f-235">toolearn cómo toocustomize Hola SAML atributo notificaciones envían tooyour aplicación, consulte [notificaciones de asignación en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="f6d4f-235">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6d4f-236">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f6d4f-236">Next steps</span></span>
[<span data-ttu-id="f6d4f-237">¿Cómo toodebug basado en SAML single sign-on tooapplications en Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6d4f-237">How toodebug SAML-based single sign-on tooapplications in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)

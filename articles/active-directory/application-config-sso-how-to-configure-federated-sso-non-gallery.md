---
title: "aaaHow tooconfigure federado inicio de sesión único para una aplicación no Galería | Documentos de Microsoft"
description: "¿Cómo tooconfigure federado inicio de sesión único para una aplicación no galería personalizada que desee toointegrate con Azure AD"
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
ms.openlocfilehash: f4a37cb500c075d0ce917ad8f13411f2ce208c56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="becb5-103">¿Cómo tooconfigure federado inicio de sesión único para una aplicación no Galería</span><span class="sxs-lookup"><span data-stu-id="becb5-103">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="becb5-104">una aplicación no Galería tooconfigure, necesita toohave Azure AD premium y aplicación hello es compatible con SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="becb5-104">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="becb5-105">Para más información acerca de las versiones de Azure AD, visite [Precios de Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="becb5-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="becb5-106">Introducción a los pasos necesarios</span><span class="sxs-lookup"><span data-stu-id="becb5-106">Overview of steps required</span></span>
<span data-ttu-id="becb5-107">A continuación se muestra una introducción de alto nivel de hello pasos necesarios tooconfigure federado inicio de sesión único para una galería-no (p. ej., personalizado) aplicación.</span><span class="sxs-lookup"><span data-stu-id="becb5-107">Below is a high level overview of hello steps required tooconfigure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="becb5-108">Configurar valores de metadatos de la aplicación hello en Azure AD (inicio de sesión en la dirección URL de respuesta de dirección URL, identificador)</span><span class="sxs-lookup"><span data-stu-id="becb5-108">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="becb5-109">Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="becb5-109">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="becb5-110">Recuperación de los metadatos y el certificado de Azure AD</span><span class="sxs-lookup"><span data-stu-id="becb5-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="becb5-111">Configurar los valores de metadatos de Azure AD de la aplicación hello (inicio de sesión en la dirección URL, emisor, dirección URL de cierre de sesión y certificado)</span><span class="sxs-lookup"><span data-stu-id="becb5-111">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="becb5-112">Asignar a usuarios de aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="becb5-112">Assign users toohello application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-toonon-gallery-applications"></a><span data-ttu-id="becb5-113">Configuración de aplicaciones único inicio de sesión toonon-Galería</span><span class="sxs-lookup"><span data-stu-id="becb5-113">Configuring single sign-on toonon-gallery applications</span></span>

<span data-ttu-id="becb5-114">tooconfigure inicio de sesión único para una aplicación que no está en la Galería de Azure AD de hello, siga Hola pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="becb5-114">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="becb5-115">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="becb5-115">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="becb5-116">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="becb5-116">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="becb5-117">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="becb5-117">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="becb5-118">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="becb5-118">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="becb5-119">Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja.</span><span class="sxs-lookup"><span data-stu-id="becb5-119">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="becb5-120">Haga clic en **aplicación gallery no** en hello **agregar su propia aplicación** sección</span><span class="sxs-lookup"><span data-stu-id="becb5-120">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="becb5-121">Escriba el nombre de Hola de aplicación Hola Hola **nombre** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="becb5-121">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="becb5-122">Haga clic en **agregar** button, aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="becb5-122">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="becb5-123">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="becb5-123">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="becb5-124">Seleccione **sesión basado en SAML** en hello **modo** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="becb5-124">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="becb5-125">Especifique los valores de hello necesario en **dominio y las direcciones URL.**</span><span class="sxs-lookup"><span data-stu-id="becb5-125">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="becb5-126">Deberá obtener estos valores del proveedor de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="becb5-126">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="becb5-127">aplicación de hello tooconfigure como SSO iniciado por IdP, escriba Hola dirección URL de respuesta y Hola identificador.</span><span class="sxs-lookup"><span data-stu-id="becb5-127">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2. <span data-ttu-id="becb5-128">**Opcional:** Hola de aplicación de hello tooconfigure como SSO iniciado por el SP, inicio de sesión en la dirección URL es un valor necesario.</span><span class="sxs-lookup"><span data-stu-id="becb5-128">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="becb5-129">Hola **atributos de usuario**, seleccione Hola identificador único para los usuarios en hello **identificador de usuario** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="becb5-129">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="becb5-130">**Opcional:** haga clic en **ver y editar todos los demás atributos de usuario** tooedit Hola atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="becb5-130">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="becb5-131">tooadd un atributo:</span><span class="sxs-lookup"><span data-stu-id="becb5-131">tooadd an attribute:</span></span>

   1. <span data-ttu-id="becb5-132">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="becb5-132">click **Add attribute**.</span></span> <span data-ttu-id="becb5-133">Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="becb5-133">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="becb5-134">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="becb5-134">Click **Save.**</span></span> <span data-ttu-id="becb5-135">Verá el nuevo atributo de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="becb5-135">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="becb5-136">Haga clic en **configurar &lt;nombre de la aplicación&gt;**  tooaccess documentación sobre cómo tooconfigure inicio de sesión único en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="becb5-136">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="becb5-137">Además, tiene las direcciones URL de Azure AD y certificados necesarios para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="becb5-137">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

15. [<span data-ttu-id="becb5-138">Asignar a usuarios de aplicación de toohello.</span><span class="sxs-lookup"><span data-stu-id="becb5-138">Assign users toohello application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="becb5-139">Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="becb5-139">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="becb5-140">tooselect Hola identificador de usuario o agregar atributos de usuario, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="becb5-140">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="becb5-141">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="becb5-141">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="becb5-142">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="becb5-142">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="becb5-143">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="becb5-143">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="becb5-144">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="becb5-144">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="becb5-145">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="becb5-145">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="becb5-146">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="becb5-146">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="becb5-147">Seleccionar aplicación hello ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="becb5-147">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="becb5-148">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="becb5-148">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="becb5-149">En hello **atributos de usuario** Hola de sección, seleccione un identificador único para los usuarios en hello **identificador de usuario** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="becb5-149">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="becb5-150">Hello opción seleccionada debe toomatch Hola esperado valor en hello aplicación tooauthenticate Hola del usuario.</span><span class="sxs-lookup"><span data-stu-id="becb5-150">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

 ><span data-ttu-id="becb5-151">[! Tenga en cuenta} Azure AD Seleccionar formato de hello para el atributo de NameID hello (identificador de usuario) en función de valor de hello seleccionado u Hola formato solicitado por la aplicación hello en hello AuthRequest de SAML.</span><span class="sxs-lookup"><span data-stu-id="becb5-151">[!NOTE} Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="becb5-152">Para obtener más información, visite el artículo de hello [protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) en hello sección NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="becb5-152">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="becb5-153">atributos de usuario de tooadd, haga clic en **ver y editar todos los demás atributos de usuario** tooedit Hola atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="becb5-153">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="becb5-154">tooadd un atributo:</span><span class="sxs-lookup"><span data-stu-id="becb5-154">tooadd an attribute:</span></span>

   1. <span data-ttu-id="becb5-155">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="becb5-155">click **Add attribute**.</span></span> <span data-ttu-id="becb5-156">Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="becb5-156">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="becb5-157">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="becb5-157">Click **Save.**</span></span> <span data-ttu-id="becb5-158">Verá el nuevo atributo de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="becb5-158">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="becb5-159">Descargar los metadatos de Azure AD de Hola o certificado</span><span class="sxs-lookup"><span data-stu-id="becb5-159">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="becb5-160">metadatos de la aplicación hello toodownload o certificado de Azure AD, siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="becb5-160">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="becb5-161">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="becb5-161">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="becb5-162">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="becb5-162">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="becb5-163">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="becb5-163">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="becb5-164">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="becb5-164">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="becb5-165">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="becb5-165">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="becb5-166">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="becb5-166">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="becb5-167">Seleccionar aplicación hello ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="becb5-167">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="becb5-168">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="becb5-168">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="becb5-169">Vaya demasiado**el certificado de firma de SAML** sección, a continuación, haga clic en **descargar** valor de la columna.</span><span class="sxs-lookup"><span data-stu-id="becb5-169">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="becb5-170">Dependiendo de qué aplicación hello es necesario configurar el inicio de sesión único, vea cualquier toodownload de opción Hola Hola Metadata XML u Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="becb5-170">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="becb5-171">Azure AD no proporciona la dirección URL tooget Hola metadatos.</span><span class="sxs-lookup"><span data-stu-id="becb5-171">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="becb5-172">solo se pueden recuperar metadatos de Hola como un archivo XML.</span><span class="sxs-lookup"><span data-stu-id="becb5-172">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="becb5-173">Asignar a usuarios de aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="becb5-173">Assign users toohello application</span></span>

<span data-ttu-id="becb5-174">tooassign uno o más usuarios tooan application directamente, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="becb5-174">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="becb5-175">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="becb5-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="becb5-176">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="becb5-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="becb5-177">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="becb5-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="becb5-178">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="becb5-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="becb5-179">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="becb5-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="becb5-180">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="becb5-180">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="becb5-181">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="becb5-181">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="becb5-182">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="becb5-182">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="becb5-183">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="becb5-183">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="becb5-184">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="becb5-184">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="becb5-185">Tipo de hello **nombre completo** o **dirección de correo electrónico** del usuario de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="becb5-185">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="becb5-186">Mantenga el mouse sobre hello **usuario** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="becb5-186">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="becb5-187">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla toohello del siguiente usuario su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="becb5-187">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="becb5-188">**Opcional:** si lo desea demasiado**agregar más de un usuario**, tipo de otro **nombre completo** o **dirección de correo electrónico** en hello **buscar por nombre o dirección de correo electrónico** cuadro de búsqueda y haga clic en hello casilla tooadd este usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="becb5-188">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="becb5-189">Cuando haya terminado de seleccionar usuarios, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="becb5-189">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="becb5-190">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** hoja tooselect un rol tooassign toohello usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="becb5-190">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="becb5-191">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="becb5-191">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="becb5-192">Tras un breve período de tiempo, los usuarios de Hola que seleccionó ser capaz de toolaunch dichas aplicaciones usan Hola métodos descritos en la sección de descripción de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="becb5-192">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="becb5-193">Personalizar las notificaciones SAML de hello envía tooan aplicación</span><span class="sxs-lookup"><span data-stu-id="becb5-193">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="becb5-194">toolearn cómo toocustomize Hola SAML atributo notificaciones envían tooyour aplicación, consulte [notificaciones de asignación en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="becb5-194">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="becb5-195">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="becb5-195">Next steps</span></span>
[<span data-ttu-id="becb5-196">Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="becb5-196">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

---
title: "un inicio de sesión único para una aplicación de la Galería de Azure AD federado aaaHow tooconfigure | Documentos de Microsoft"
description: "Un inicio de sesión único para una existente Galería de Azure AD aplicación y utilice tutoriales tooget a trabajar rápidamente cómo federado tooconfigure"
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
ms.openlocfilehash: a93de021fddd253e4fe663c221b822d12625fd54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="42101-103">¿Cómo tooconfigure federado inicio de sesión único para una aplicación de la Galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="42101-103">How tooconfigure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="42101-104">Todas las aplicaciones en la Galería de hello Azure AD habilitado con capacidad de inicio de sesión único de empresa tiene un tutorial paso a paso disponible.</span><span class="sxs-lookup"><span data-stu-id="42101-104">All applications in hello Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="42101-105">Puede tener acceso a hello [lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para obtener instrucciones detalladas paso a paso.</span><span class="sxs-lookup"><span data-stu-id="42101-105">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="42101-106">Introducción a los pasos necesarios</span><span class="sxs-lookup"><span data-stu-id="42101-106">Overview of steps required</span></span>
<span data-ttu-id="42101-107">una aplicación desde la Galería de Azure AD de hello tooconfigure debe:</span><span class="sxs-lookup"><span data-stu-id="42101-107">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="42101-108">Agregar una aplicación de la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="42101-108">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="42101-109">Configurar valores de metadatos de la aplicación hello en Azure AD (inicio de sesión en la dirección URL de respuesta de dirección URL, identificador)</span><span class="sxs-lookup"><span data-stu-id="42101-109">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="42101-110">Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="42101-110">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="42101-111">Recuperación de los metadatos y el certificado de Azure AD</span><span class="sxs-lookup"><span data-stu-id="42101-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="42101-112">Configurar los valores de metadatos de Azure AD de la aplicación hello (inicio de sesión en la dirección URL, emisor, dirección URL de cierre de sesión y certificado)</span><span class="sxs-lookup"><span data-stu-id="42101-112">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="42101-113">Asignar a usuarios de aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="42101-113">Assign users toohello application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="42101-114">Agregar una aplicación de la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="42101-114">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="42101-115">tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="42101-115">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="42101-116">Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="42101-116">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="42101-117">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="42101-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="42101-118">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="42101-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="42101-119">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="42101-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="42101-120">Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja.</span><span class="sxs-lookup"><span data-stu-id="42101-120">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="42101-121">Hola **escriba un nombre** cuadro de texto de hello **agregar a partir de la Galería de hello** sección, escriba un nombre de aplicación hello como Hola.</span><span class="sxs-lookup"><span data-stu-id="42101-121">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="42101-122">Seleccionar aplicación hello tooconfigure que desee para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="42101-122">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="42101-123">Antes de agregar la aplicación hello, puede cambiar su nombre de hello **nombre** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="42101-123">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="42101-124">Haga clic en **agregar** button, aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="42101-124">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="42101-125">Tras un breve período de tiempo, es que la hoja de configuración de la aplicación pueda toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="42101-125">After a short period of time, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="42101-126">Configurar inicio de sesión único para una aplicación desde la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="42101-126">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="42101-127">tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="42101-127">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="42101-128">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="42101-128">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="42101-129">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="42101-129">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="42101-130">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="42101-130">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="42101-131">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="42101-131">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="42101-132">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="42101-132">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="42101-133">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="42101-133">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="42101-134">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="42101-134">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="42101-135">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="42101-135">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="42101-136">Seleccione **sesión basado en SAML** de hello **modo** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="42101-136">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="42101-137">Especifique los valores de hello necesario en **dominio y las direcciones URL.**</span><span class="sxs-lookup"><span data-stu-id="42101-137">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="42101-138">Deberá obtener estos valores del proveedor de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="42101-138">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="42101-139">aplicación de hello tooconfigure como SSO iniciado por el SP, Hola inicio de sesión en la dirección URL es un valor necesario.</span><span class="sxs-lookup"><span data-stu-id="42101-139">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="42101-140">En algunas aplicaciones, Hola identificador también es un valor obligatorio.</span><span class="sxs-lookup"><span data-stu-id="42101-140">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="42101-141">aplicación de hello tooconfigure como SSO iniciado por IdP, Hola dirección URL de respuesta es un valor necesario.</span><span class="sxs-lookup"><span data-stu-id="42101-141">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="42101-142">En algunas aplicaciones, Hola identificador también es un valor obligatorio.</span><span class="sxs-lookup"><span data-stu-id="42101-142">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="42101-143">**Opcional:** haga clic en **mostrar avanzadas de configuración de direcciones URL** si desea que los valores no sean necesarios de hello toosee.</span><span class="sxs-lookup"><span data-stu-id="42101-143">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="42101-144">Hola **atributos de usuario**, seleccione Hola identificador único para los usuarios en hello **identificador de usuario** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="42101-144">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="42101-145">**Opcional:** haga clic en **ver y editar todos los demás atributos de usuario** tooedit Hola atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="42101-145">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

  <span data-ttu-id="42101-146">tooadd un atributo:</span><span class="sxs-lookup"><span data-stu-id="42101-146">tooadd an attribute:</span></span>
   
   1. <span data-ttu-id="42101-147">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="42101-147">click **Add attribute**.</span></span> <span data-ttu-id="42101-148">Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="42101-148">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   1. <span data-ttu-id="42101-149">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="42101-149">Click **Save.**</span></span> <span data-ttu-id="42101-150">Verá el nuevo atributo de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="42101-150">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="42101-151">Haga clic en **configurar &lt;nombre de la aplicación&gt;**  tooaccess documentación sobre cómo tooconfigure inicio de sesión único en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="42101-151">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="42101-152">Además, tendrá las direcciones URL de metadatos de Hola y requiere un certificado toosetup SSO con la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="42101-152">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="42101-153">Haga clic en **guardar** configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="42101-153">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="42101-154">Asignar a usuarios de aplicación de toohello.</span><span class="sxs-lookup"><span data-stu-id="42101-154">Assign users toohello application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="42101-155">Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="42101-155">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="42101-156">tooselect Hola identificador de usuario o agregar atributos de usuario, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="42101-156">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="42101-157">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="42101-157">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="42101-158">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="42101-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="42101-159">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="42101-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="42101-160">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="42101-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="42101-161">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="42101-161">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="42101-162">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="42101-162">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="42101-163">Seleccionar aplicación hello ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="42101-163">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="42101-164">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="42101-164">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="42101-165">En hello **atributos de usuario** Hola de sección, seleccione un identificador único para los usuarios en hello **identificador de usuario** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="42101-165">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="42101-166">Hello opción seleccionada debe toomatch Hola esperado valor en hello aplicación tooauthenticate Hola del usuario.</span><span class="sxs-lookup"><span data-stu-id="42101-166">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="42101-167">Azure formato AD seleccione Hola Hola NameID atributo (identificador de usuario) en función de valor de hello seleccionado u Hola formato solicitado por la aplicación hello en hello AuthRequest de SAML.</span><span class="sxs-lookup"><span data-stu-id="42101-167">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="42101-168">Para obtener más información, visite el artículo de hello [protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) en hello sección NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="42101-168">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="42101-169">atributos de usuario de tooadd, haga clic en **ver y editar todos los demás atributos de usuario** tooedit Hola atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="42101-169">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="42101-170">tooadd un atributo:</span><span class="sxs-lookup"><span data-stu-id="42101-170">tooadd an attribute:</span></span>
  
   1. <span data-ttu-id="42101-171">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="42101-171">click **Add attribute**.</span></span> <span data-ttu-id="42101-172">Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="42101-172">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="42101-173">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="42101-173">Click **Save**.</span></span> <span data-ttu-id="42101-174">Verá el nuevo atributo de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="42101-174">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="42101-175">Descargar los metadatos de Azure AD de Hola o certificado</span><span class="sxs-lookup"><span data-stu-id="42101-175">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="42101-176">metadatos de la aplicación hello toodownload o certificado de Azure AD, siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="42101-176">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="42101-177">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="42101-177">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="42101-178">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="42101-178">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="42101-179">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="42101-179">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="42101-180">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="42101-180">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="42101-181">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="42101-181">click **All Applications** tooview a list of all your applications.</span></span>

  *  <span data-ttu-id="42101-182">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="42101-182">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications**.</span></span>

6.  <span data-ttu-id="42101-183">Seleccionar aplicación hello ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="42101-183">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="42101-184">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="42101-184">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="42101-185">Vaya demasiado**el certificado de firma de SAML** sección, a continuación, haga clic en **descargar** valor de la columna.</span><span class="sxs-lookup"><span data-stu-id="42101-185">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="42101-186">Dependiendo de qué aplicación hello es necesario configurar el inicio de sesión único, vea cualquier toodownload de opción Hola Hola Metadata XML u Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="42101-186">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="42101-187">Azure AD no proporciona la dirección URL tooget Hola metadatos.</span><span class="sxs-lookup"><span data-stu-id="42101-187">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="42101-188">solo se pueden recuperar metadatos de Hola como un archivo XML.</span><span class="sxs-lookup"><span data-stu-id="42101-188">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="42101-189">Asignar a usuarios de aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="42101-189">Assign users toohello application</span></span>

<span data-ttu-id="42101-190">tooassign uno o más usuarios tooan application directamente, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="42101-190">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="42101-191">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="42101-191">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="42101-192">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="42101-192">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="42101-193">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="42101-193">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="42101-194">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="42101-194">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="42101-195">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="42101-195">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="42101-196">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="42101-196">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="42101-197">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="42101-197">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="42101-198">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="42101-198">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="42101-199">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="42101-199">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="42101-200">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="42101-200">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="42101-201">Tipo de hello **nombre completo** o **dirección de correo electrónico** del usuario de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="42101-201">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="42101-202">Mantenga el mouse sobre hello **usuario** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="42101-202">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="42101-203">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla toohello del siguiente usuario su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="42101-203">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="42101-204">**Opcional:** si lo desea demasiado**agregar más de un usuario**, tipo de otro **nombre completo** o **dirección de correo electrónico** en hello **buscar por nombre o dirección de correo electrónico** cuadro de búsqueda y haga clic en hello casilla tooadd este usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="42101-204">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="42101-205">Cuando haya terminado de seleccionar usuarios, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="42101-205">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="42101-206">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** hoja tooselect un rol tooassign toohello usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="42101-206">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="42101-207">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="42101-207">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="42101-208">Tras un breve período de tiempo, los usuarios de Hola que seleccionó ser capaz de toolaunch dichas aplicaciones usan Hola métodos descritos en la sección de descripción de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="42101-208">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="42101-209">Personalizar las notificaciones SAML de hello envía tooan aplicación</span><span class="sxs-lookup"><span data-stu-id="42101-209">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="42101-210">toolearn cómo toocustomize Hola SAML atributo notificaciones envían tooyour aplicación, consulte [notificaciones de asignación en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="42101-210">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42101-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="42101-211">Next steps</span></span>
[<span data-ttu-id="42101-212">Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="42101-212">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)




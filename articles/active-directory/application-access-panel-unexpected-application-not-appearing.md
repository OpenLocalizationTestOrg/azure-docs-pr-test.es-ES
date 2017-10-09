---
title: "aplicación aaaAn asignado no aparece en el panel de acceso de hello | Documentos de Microsoft"
description: "Solucionar problemas de por qué una aplicación no aparece en el Panel de acceso de Hola"
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
ms.reviwer: japere
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a><span data-ttu-id="1202c-103">Una aplicación asignada no aparece en el panel de acceso de Hola</span><span class="sxs-lookup"><span data-stu-id="1202c-103">An assigned application is not appearing on hello access panel</span></span>

<span data-ttu-id="1202c-104">Hola Panel de acceso es un portal basado en web que permite a los usuarios con un trabajo o cuenta educativa en aplicaciones de Azure Active Directory (Azure AD) tooview y de inicio en la nube que Hola Administrador de Azure AD le haya concedido acceso a.</span><span class="sxs-lookup"><span data-stu-id="1202c-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="1202c-105">Estas aplicaciones se configuran en nombre de usuario de hello en el portal de Azure AD Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="1202c-106">aplicación Hello debe configurarse correctamente y asignado toohello usuario o un grupo de usuario de hello es miembro de la aplicación de hello toosee Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1202c-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="1202c-107">tipo Hello de aplicaciones posible que un usuario esté viendo se dividen en hello siguientes categorías:</span><span class="sxs-lookup"><span data-stu-id="1202c-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="1202c-108">Aplicaciones de Office 365</span><span class="sxs-lookup"><span data-stu-id="1202c-108">Office 365 Applications</span></span>

-   <span data-ttu-id="1202c-109">Aplicaciones de Microsoft y de terceros configuradas con SSO basado en federación</span><span class="sxs-lookup"><span data-stu-id="1202c-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="1202c-110">Aplicaciones de SSO basado en contraseña</span><span class="sxs-lookup"><span data-stu-id="1202c-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="1202c-111">Aplicaciones con soluciones SSO existentes</span><span class="sxs-lookup"><span data-stu-id="1202c-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="1202c-112">General emite toocheck primero</span><span class="sxs-lookup"><span data-stu-id="1202c-112">General issues toocheck first</span></span>

-   <span data-ttu-id="1202c-113">Si una aplicación se acaba de agregar usuario tooa, toosign de entrada y salida vuelva a intentarlo en el Panel de acceso del usuario de hello después de unos toosee minutos si se agrega la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-113">If an application was just added tooa user, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is added.</span></span>

-   <span data-ttu-id="1202c-114">Si se acaba de quitar una licencia a un usuario o grupo de usuario de hello es que un miembro de este puede tardar mucho tiempo, según el tamaño de Hola y la complejidad del grupo de Hola para toobe cambios realizado.</span><span class="sxs-lookup"><span data-stu-id="1202c-114">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="1202c-115">Permitir un tiempo adicional antes de iniciar sesión en el Panel de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-115">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooapplication-configuration"></a><span data-ttu-id="1202c-116">Configuración de tooapplication relacionados de problemas</span><span class="sxs-lookup"><span data-stu-id="1202c-116">Problems related tooapplication configuration</span></span>

<span data-ttu-id="1202c-117">Puede que una aplicación no aparezca en el panel de acceso de un usuario porque no está configurada correctamente.</span><span class="sxs-lookup"><span data-stu-id="1202c-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="1202c-118">A continuación se muestran algunas maneras que se puede solucionar problemas de configuración de tooapplication relacionados de problemas:</span><span class="sxs-lookup"><span data-stu-id="1202c-118">Below are some ways you can troubleshoot issues related tooapplication configuration:</span></span>

-   [<span data-ttu-id="1202c-119">¿Cómo tooconfigure federado inicio de sesión único para una aplicación de la Galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1202c-119">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="1202c-120">¿Cómo tooconfigure federado inicio de sesión único para una aplicación no Galería</span><span class="sxs-lookup"><span data-stu-id="1202c-120">How tooconfigure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="1202c-121">¿Cómo tooconfigure una contraseña única aplicación de inicio de sesión para una aplicación de la Galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1202c-121">How tooconfigure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="1202c-122">¿Cómo tooconfigure una contraseña única aplicación de inicio de sesión para una aplicación no Galería</span><span class="sxs-lookup"><span data-stu-id="1202c-122">How tooconfigure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="1202c-123">¿Cómo tooconfigure federado inicio de sesión único para una aplicación de la Galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1202c-123">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="1202c-124">Todas las aplicaciones de la Galería de Azure AD Hola habilitado con capacidad de Enterprise Single Sign-On tiene un tutorial paso a paso disponible.</span><span class="sxs-lookup"><span data-stu-id="1202c-124">All applications in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="1202c-125">Puede tener acceso a hello [lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para obtener instrucciones paso a paso detallados.</span><span class="sxs-lookup"><span data-stu-id="1202c-125">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="1202c-126">una aplicación desde la Galería de Azure AD de hello tooconfigure debe:</span><span class="sxs-lookup"><span data-stu-id="1202c-126">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="1202c-127">Agregar una aplicación de la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="1202c-127">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="1202c-128">Configurar valores de metadatos de la aplicación hello en Azure AD (inicio de sesión en la dirección URL de respuesta de dirección URL, identificador)</span><span class="sxs-lookup"><span data-stu-id="1202c-128">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="1202c-129">Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="1202c-129">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="1202c-130">Recuperación de los metadatos y el certificado de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1202c-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="1202c-131">Configurar los valores de metadatos de Azure AD de la aplicación hello (inicio de sesión en la dirección URL, emisor, dirección URL de cierre de sesión y certificado)</span><span class="sxs-lookup"><span data-stu-id="1202c-131">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="1202c-132">Agregar una aplicación de la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="1202c-132">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="1202c-133">tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="1202c-133">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-134">Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="1202c-134">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="1202c-135">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-135">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-136">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-136">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-137">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1202c-137">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1202c-138">Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja.</span><span class="sxs-lookup"><span data-stu-id="1202c-138">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="1202c-139">Hola **escriba un nombre** cuadro de texto de hello **agregar a partir de la Galería de hello** sección, escriba un nombre de aplicación hello como Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-139">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="1202c-140">Seleccionar aplicación hello tooconfigure que desee para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1202c-140">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="1202c-141">Antes de agregar la aplicación hello, puede cambiar su nombre de hello **nombre** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="1202c-141">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="1202c-142">Haga clic en **agregar** button, aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1202c-142">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="1202c-143">Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-143">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="1202c-144">Configurar inicio de sesión único para una aplicación desde la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="1202c-144">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="1202c-145">tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="1202c-145">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-146">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="1202c-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1202c-147">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-148">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-149">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1202c-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1202c-150">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1202c-150">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1202c-151">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="1202c-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1202c-152">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1202c-152">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="1202c-153">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1202c-154">Seleccione **sesión basado en SAML** de hello **modo** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="1202c-154">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="1202c-155">Especifique los valores de hello necesario en **dominio y las direcciones URL.**</span><span class="sxs-lookup"><span data-stu-id="1202c-155">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="1202c-156">Deberá obtener estos valores del proveedor de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-156">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="1202c-157">aplicación de hello tooconfigure como SSO iniciado por el SP, Hola inicio de sesión en la dirección URL es un valor necesario.</span><span class="sxs-lookup"><span data-stu-id="1202c-157">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="1202c-158">En algunas aplicaciones, Hola identificador también es un valor obligatorio.</span><span class="sxs-lookup"><span data-stu-id="1202c-158">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="1202c-159">aplicación de hello tooconfigure como SSO iniciado por IdP, Hola dirección URL de respuesta es un valor necesario.</span><span class="sxs-lookup"><span data-stu-id="1202c-159">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="1202c-160">En algunas aplicaciones, Hola identificador también es un valor obligatorio.</span><span class="sxs-lookup"><span data-stu-id="1202c-160">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="1202c-161">**Opcional:** haga clic en **mostrar avanzadas de configuración de direcciones URL** si desea que los valores no sean necesarios de hello toosee.</span><span class="sxs-lookup"><span data-stu-id="1202c-161">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="1202c-162">Hola **atributos de usuario**, seleccione Hola identificador único para los usuarios en hello **identificador de usuario** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="1202c-162">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="1202c-163">**Opcional:** haga clic en **ver y editar todos los demás atributos de usuario** tooedit Hola atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="1202c-163">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="1202c-164">tooadd un atributo:</span><span class="sxs-lookup"><span data-stu-id="1202c-164">tooadd an attribute:</span></span>

   1. <span data-ttu-id="1202c-165">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="1202c-165">click **Add attribute**.</span></span> <span data-ttu-id="1202c-166">Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-166">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="1202c-167">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1202c-167">click **Save.**</span></span> <span data-ttu-id="1202c-168">Verá el nuevo atributo de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-168">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="1202c-169">Haga clic en **configurar &lt;nombre de la aplicación&gt;**  tooaccess documentación sobre cómo tooconfigure inicio de sesión único en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-169">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="1202c-170">Además, tendrá las direcciones URL de metadatos de Hola y requiere un certificado toosetup SSO con la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-170">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="1202c-171">Haga clic en **guardar** configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-171">click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="1202c-172">Asignar a usuarios de aplicación de toohello.</span><span class="sxs-lookup"><span data-stu-id="1202c-172">Assign users toohello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="1202c-173">Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="1202c-173">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="1202c-174">tooselect Hola identificador de usuario o agregar atributos de usuario, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="1202c-174">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-175">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="1202c-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1202c-176">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-177">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-178">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1202c-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1202c-179">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1202c-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1202c-180">Si no ve la aplicación hello desea tooshow aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="1202c-180">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1202c-181">Seleccionar aplicación hello ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1202c-181">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="1202c-182">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-182">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1202c-183">En hello **atributos de usuario** Hola de sección, seleccione un identificador único para los usuarios en hello **identificador de usuario** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="1202c-183">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="1202c-184">Hello opción seleccionada debe toomatch Hola esperado valor en hello aplicación tooauthenticate Hola del usuario.</span><span class="sxs-lookup"><span data-stu-id="1202c-184">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="1202c-185">Azure formato AD seleccione Hola Hola NameID atributo (identificador de usuario) en función de valor de hello seleccionado u Hola formato solicitado por la aplicación hello en hello AuthRequest de SAML.</span><span class="sxs-lookup"><span data-stu-id="1202c-185">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="1202c-186">Para obtener más información, visite el artículo de hello [protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) en hello sección NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="1202c-186">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="1202c-187">atributos de usuario de tooadd, haga clic en **ver y editar todos los demás atributos de usuario** tooedit Hola atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="1202c-187">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="1202c-188">tooadd un atributo:</span><span class="sxs-lookup"><span data-stu-id="1202c-188">tooadd an attribute:</span></span>

   1. <span data-ttu-id="1202c-189">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="1202c-189">click **Add attribute**.</span></span> <span data-ttu-id="1202c-190">Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-190">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="1202c-191">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1202c-191">click **Save.**</span></span> <span data-ttu-id="1202c-192">Verá el nuevo atributo de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-192">You will see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="1202c-193">Descargar los metadatos de Azure AD de Hola o certificado</span><span class="sxs-lookup"><span data-stu-id="1202c-193">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="1202c-194">metadatos de la aplicación hello toodownload o certificado de Azure AD, siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="1202c-194">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-195">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="1202c-195">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1202c-196">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-196">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-197">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-197">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-198">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1202c-198">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1202c-199">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1202c-199">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1202c-200">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="1202c-200">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1202c-201">Seleccionar aplicación hello ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1202c-201">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="1202c-202">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-202">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1202c-203">Vaya demasiado**el certificado de firma de SAML** sección, a continuación, haga clic en **descargar** valor de la columna.</span><span class="sxs-lookup"><span data-stu-id="1202c-203">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="1202c-204">Dependiendo de qué aplicación hello es necesario configurar el inicio de sesión único, vea cualquier toodownload de opción Hola Hola Metadata XML u Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="1202c-204">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="1202c-205">Azure AD no proporciona la dirección URL tooget Hola metadatos.</span><span class="sxs-lookup"><span data-stu-id="1202c-205">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="1202c-206">solo se pueden recuperar metadatos de Hola como un archivo XML.</span><span class="sxs-lookup"><span data-stu-id="1202c-206">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="1202c-207">¿Cómo tooconfigure federado inicio de sesión único para una aplicación no Galería</span><span class="sxs-lookup"><span data-stu-id="1202c-207">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="1202c-208">una aplicación no Galería tooconfigure, necesita toohave Azure AD premium y aplicación hello es compatible con SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="1202c-208">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="1202c-209">Para más información acerca de las versiones de Azure AD, visite [Precios de Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="1202c-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="1202c-210">Configurar valores de metadatos de la aplicación hello en Azure AD (inicio de sesión en la dirección URL de respuesta de dirección URL, identificador)</span><span class="sxs-lookup"><span data-stu-id="1202c-210">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="1202c-211">Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="1202c-211">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="1202c-212">Recuperación de los metadatos y el certificado de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1202c-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="1202c-213">Configurar los valores de metadatos de Azure AD de la aplicación hello (inicio de sesión en la dirección URL, emisor, dirección URL de cierre de sesión y certificado)</span><span class="sxs-lookup"><span data-stu-id="1202c-213">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="1202c-214">Configurar valores de metadatos de la aplicación hello en Azure AD (inicio de sesión en la dirección URL de respuesta de dirección URL, identificador)</span><span class="sxs-lookup"><span data-stu-id="1202c-214">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="1202c-215">tooconfigure inicio de sesión único para una aplicación que no está en la Galería de Azure AD de hello, siga Hola pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1202c-215">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-216">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="1202c-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1202c-217">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-218">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-219">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1202c-219">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1202c-220">Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja.</span><span class="sxs-lookup"><span data-stu-id="1202c-220">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="1202c-221">Haga clic en **aplicación gallery no** en hello **agregar su propia aplicación** sección.</span><span class="sxs-lookup"><span data-stu-id="1202c-221">click **Non-gallery application** in hello **Add your own app** section.</span></span>

7.  <span data-ttu-id="1202c-222">Escriba el nombre de Hola de aplicación Hola Hola **nombre** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="1202c-222">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="1202c-223">Haga clic en **agregar** button, aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1202c-223">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="1202c-224">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-224">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="1202c-225">Seleccione **sesión basado en SAML** en hello **modo** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="1202c-225">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="1202c-226">Especifique los valores de hello necesario en **dominio y las direcciones URL.**</span><span class="sxs-lookup"><span data-stu-id="1202c-226">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="1202c-227">Deberá obtener estos valores del proveedor de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-227">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="1202c-228">aplicación de hello tooconfigure como SSO iniciado por IdP, escriba Hola dirección URL de respuesta y Hola identificador.</span><span class="sxs-lookup"><span data-stu-id="1202c-228">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2.  <span data-ttu-id="1202c-229">**Opcional:** Hola de aplicación de hello tooconfigure como SSO iniciado por el SP, inicio de sesión en la dirección URL es un valor necesario.</span><span class="sxs-lookup"><span data-stu-id="1202c-229">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="1202c-230">Hola **atributos de usuario**, seleccione Hola identificador único para los usuarios en hello **identificador de usuario** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="1202c-230">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="1202c-231">**Opcional:** haga clic en **ver y editar todos los demás atributos de usuario** tooedit Hola atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="1202c-231">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="1202c-232">tooadd un atributo:</span><span class="sxs-lookup"><span data-stu-id="1202c-232">tooadd an attribute:</span></span>

   1. <span data-ttu-id="1202c-233">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="1202c-233">click **Add attribute**.</span></span> <span data-ttu-id="1202c-234">Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-234">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="1202c-235">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1202c-235">Click **Save.**</span></span> <span data-ttu-id="1202c-236">Verá el nuevo atributo de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-236">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="1202c-237">Haga clic en **configurar &lt;nombre de la aplicación&gt;**  tooaccess documentación sobre cómo tooconfigure inicio de sesión único en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-237">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="1202c-238">Además, tiene las direcciones URL de Azure AD y certificados necesarios para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-238">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="1202c-239">Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="1202c-239">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="1202c-240">tooselect Hola identificador de usuario o agregar atributos de usuario, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="1202c-240">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-241">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="1202c-241">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1202c-242">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-242">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-243">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-243">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-244">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1202c-244">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1202c-245">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1202c-245">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="1202c-246">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="1202c-246">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1202c-247">Seleccionar aplicación hello ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1202c-247">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="1202c-248">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-248">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1202c-249">En hello **atributos de usuario** Hola de sección, seleccione un identificador único para los usuarios en hello **identificador de usuario** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="1202c-249">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="1202c-250">Hello opción seleccionada debe toomatch Hola esperado valor en hello aplicación tooauthenticate Hola del usuario.</span><span class="sxs-lookup"><span data-stu-id="1202c-250">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="1202c-251">Azure formato AD seleccione Hola Hola NameID atributo (identificador de usuario) en función de valor de hello seleccionado u Hola formato solicitado por la aplicación hello en hello AuthRequest de SAML.</span><span class="sxs-lookup"><span data-stu-id="1202c-251">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="1202c-252">Para obtener más información, visite el artículo de hello [protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) en hello sección NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="1202c-252">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="1202c-253">atributos de usuario de tooadd, haga clic en **ver y editar todos los demás atributos de usuario** tooedit Hola atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="1202c-253">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="1202c-254">tooadd un atributo:</span><span class="sxs-lookup"><span data-stu-id="1202c-254">tooadd an attribute:</span></span>

   1. <span data-ttu-id="1202c-255">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="1202c-255">click **Add attribute**.</span></span> <span data-ttu-id="1202c-256">Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-256">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="1202c-257">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1202c-257">Click **Save.**</span></span> <span data-ttu-id="1202c-258">Verá el nuevo atributo de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-258">You see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="1202c-259">Descargar los metadatos de Azure AD de Hola o certificado</span><span class="sxs-lookup"><span data-stu-id="1202c-259">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="1202c-260">metadatos de la aplicación hello toodownload o certificado de Azure AD, siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="1202c-260">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-261">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="1202c-261">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1202c-262">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-262">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-263">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-263">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-264">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1202c-264">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1202c-265">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1202c-265">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="1202c-266">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="1202c-266">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1202c-267">Seleccionar aplicación hello ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1202c-267">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="1202c-268">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-268">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1202c-269">Vaya demasiado**el certificado de firma de SAML** sección, a continuación, haga clic en **descargar** valor de la columna.</span><span class="sxs-lookup"><span data-stu-id="1202c-269">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="1202c-270">Dependiendo de qué aplicación hello es necesario configurar el inicio de sesión único, vea cualquier toodownload de opción Hola Hola Metadata XML u Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="1202c-270">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="1202c-271">Azure AD no proporciona la dirección URL tooget Hola metadatos.</span><span class="sxs-lookup"><span data-stu-id="1202c-271">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="1202c-272">solo se pueden recuperar metadatos de Hola como un archivo XML.</span><span class="sxs-lookup"><span data-stu-id="1202c-272">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="1202c-273">¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación de la Galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1202c-273">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="1202c-274">una aplicación desde la Galería de Azure AD de hello tooconfigure debe:</span><span class="sxs-lookup"><span data-stu-id="1202c-274">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="1202c-275">Agregar una aplicación de la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="1202c-275">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="1202c-276">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="1202c-276">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="1202c-277">Agregar una aplicación de la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="1202c-277">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="1202c-278">tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="1202c-278">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-279">Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="1202c-279">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="1202c-280">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-280">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-281">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-281">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-282">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1202c-282">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1202c-283">Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja.</span><span class="sxs-lookup"><span data-stu-id="1202c-283">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="1202c-284">Hola **escriba un nombre** cuadro de texto de hello **agregar a partir de la Galería de hello** sección, escriba un nombre de aplicación hello como Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-284">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="1202c-285">Seleccionar aplicación hello tooconfigure que desee para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1202c-285">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="1202c-286">Antes de agregar la aplicación hello, puede cambiar su nombre de hello **nombre** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="1202c-286">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="1202c-287">Haga clic en **agregar** button, aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1202c-287">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="1202c-288">Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-288">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="1202c-289">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="1202c-289">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="1202c-290">tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="1202c-290">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-291">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="1202c-291">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1202c-292">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-292">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-293">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-293">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-294">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1202c-294">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1202c-295">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1202c-295">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="1202c-296">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="1202c-296">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1202c-297">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1202c-297">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="1202c-298">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-298">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1202c-299">Modo de hello seleccione **sesión basada en contraseña.**</span><span class="sxs-lookup"><span data-stu-id="1202c-299">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="1202c-300">[Asignar usuarios de aplicación de toohello](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="1202c-300">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="1202c-301">Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-301">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="1202c-302">En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.</span><span class="sxs-lookup"><span data-stu-id="1202c-302">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="1202c-303">¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación no Galería</span><span class="sxs-lookup"><span data-stu-id="1202c-303">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="1202c-304">una aplicación desde la Galería de Azure AD de hello tooconfigure debe:</span><span class="sxs-lookup"><span data-stu-id="1202c-304">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="1202c-305">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="1202c-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="1202c-306">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="1202c-306">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="1202c-307">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="1202c-307">Add a non-gallery application</span></span>

<span data-ttu-id="1202c-308">tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="1202c-308">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-309">Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="1202c-309">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="1202c-310">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-310">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-311">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-311">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-312">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1202c-312">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1202c-313">Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja.</span><span class="sxs-lookup"><span data-stu-id="1202c-313">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="1202c-314">Haga clic en **Aplicación situada fuera de la galería**.</span><span class="sxs-lookup"><span data-stu-id="1202c-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="1202c-315">Escriba el nombre de saludo de la aplicación Hola **nombre** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="1202c-315">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="1202c-316">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1202c-316">Select **Add.**</span></span>

<span data-ttu-id="1202c-317">Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-317">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="1202c-318">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="1202c-318">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="1202c-319">tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="1202c-319">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-320">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="1202c-320">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1202c-321">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-321">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-322">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-322">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-323">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1202c-323">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1202c-324">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1202c-324">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="1202c-325">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="1202c-325">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1202c-326">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1202c-326">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="1202c-327">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-327">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1202c-328">Modo de hello seleccione **sesión basada en contraseña.**</span><span class="sxs-lookup"><span data-stu-id="1202c-328">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="1202c-329">Escriba hello **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="1202c-329">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="1202c-330">Se trata de dirección URL de Hola donde los usuarios escribir su toosign en nombre de usuario y contraseña a.</span><span class="sxs-lookup"><span data-stu-id="1202c-330">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="1202c-331">Asegúrese de que está visible en la dirección URL de Hola Hola campos inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="1202c-331">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="1202c-332">[Asignar usuarios de aplicación de toohello](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="1202c-332">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="1202c-333">Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-333">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="1202c-334">En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.</span><span class="sxs-lookup"><span data-stu-id="1202c-334">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="1202c-335">Problemas relacionados tooassigning aplicaciones toousers</span><span class="sxs-lookup"><span data-stu-id="1202c-335">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="1202c-336">Un usuario puede no esté viendo una aplicación en su Panel de acceso porque no se les asignan toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="1202c-336">A user may not be seeing an application on their Access Panel because they are not assigned toohello application.</span></span> <span data-ttu-id="1202c-337">A continuación se muestran algunas maneras toocheck:</span><span class="sxs-lookup"><span data-stu-id="1202c-337">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="1202c-338">Comprobar si un usuario se ha asignado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="1202c-338">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="1202c-339">¿Cómo tooassign directamente una aplicación de tooan de usuario</span><span class="sxs-lookup"><span data-stu-id="1202c-339">How tooassign a user tooan application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="1202c-340">Compruebe si un usuario se haya asignado tooa licencia relacionados con la aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="1202c-340">Check if a user is assigned tooa license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="1202c-341">¿Cómo tooassign un usuario de tooa de licencia</span><span class="sxs-lookup"><span data-stu-id="1202c-341">How tooassign a license tooa user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="1202c-342">Comprobar si un usuario se ha asignado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="1202c-342">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="1202c-343">toocheck si se asigna a un usuario toohello aplicación, siga Hola pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1202c-343">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-344">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="1202c-344">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1202c-345">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-345">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-346">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-346">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-347">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1202c-347">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1202c-348">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1202c-348">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="1202c-349">**Búsqueda** como nombre de Hola de aplicación hello en cuestión.</span><span class="sxs-lookup"><span data-stu-id="1202c-349">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="1202c-350">Haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1202c-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="1202c-351">Compruebe toosee si el usuario se le asigna la aplicación toohello.</span><span class="sxs-lookup"><span data-stu-id="1202c-351">Check toosee if your user is assigned toohello application.</span></span>

   * <span data-ttu-id="1202c-352">Si no siga los pasos de hello en "cómo tooassign una aplicación de usuario tooan directamente" toodo para.</span><span class="sxs-lookup"><span data-stu-id="1202c-352">If not follow hello steps in “How tooassign a user tooan application directly” toodo so.</span></span>

### <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="1202c-353">¿Cómo tooassign directamente una aplicación de tooan de usuario</span><span class="sxs-lookup"><span data-stu-id="1202c-353">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="1202c-354">tooassign uno o más usuarios tooan application directamente, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="1202c-354">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-355">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global**.</span><span class="sxs-lookup"><span data-stu-id="1202c-355">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="1202c-356">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-356">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-357">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-357">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-358">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1202c-358">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1202c-359">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1202c-359">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1202c-360">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="1202c-360">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1202c-361">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="1202c-361">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="1202c-362">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-362">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1202c-363">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="1202c-363">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="1202c-364">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="1202c-364">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="1202c-365">Tipo de hello **nombre completo** o **dirección de correo electrónico** del usuario de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="1202c-365">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="1202c-366">Mantenga el mouse sobre hello **usuario** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="1202c-366">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="1202c-367">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla toohello del siguiente usuario su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="1202c-367">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="1202c-368">**Opcional:** si lo desea demasiado**agregar más de un usuario**, tipo de otro **nombre completo** o **dirección de correo electrónico** en hello **buscar por nombre o dirección de correo electrónico** cuadro de búsqueda y haga clic en hello casilla tooadd este usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="1202c-368">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="1202c-369">Cuando haya terminado de seleccionar usuarios, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="1202c-369">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="1202c-370">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** hoja tooselect un rol tooassign toohello usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="1202c-370">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="1202c-371">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="1202c-371">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="1202c-372">Después de un breve período, los usuarios de Hola que seleccionó ser capaz de toolaunch estas aplicaciones en Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1202c-372">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="1202c-373">Comprobar si un usuario está sometido a una licencia relacionados con la aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="1202c-373">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="1202c-374">toocheck un usuario había asignado licencias, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="1202c-374">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-375">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="1202c-375">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1202c-376">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-376">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-377">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-377">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-378">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-378">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1202c-379">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1202c-379">click **All users**.</span></span>

6.  <span data-ttu-id="1202c-380">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1202c-380">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1202c-381">Haga clic en **licencias** toosee qué usuario de hello licencias actualmente tiene asignada.</span><span class="sxs-lookup"><span data-stu-id="1202c-381">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

  * <span data-ttu-id="1202c-382">Si se asigna la licencia de Office tooan Esto activar tooappear de las aplicaciones de Office de primera entidad de usuario de Hola Hola Panel de acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="1202c-382">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-user-a-license"></a><span data-ttu-id="1202c-383">¿Cómo tooassign un usuario una licencia</span><span class="sxs-lookup"><span data-stu-id="1202c-383">How tooassign a user a license</span></span> 

<span data-ttu-id="1202c-384">tooassign un usuario tooa de licencias, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="1202c-384">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-385">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="1202c-385">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1202c-386">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-386">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-387">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-387">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-388">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-388">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1202c-389">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1202c-389">click **All users**.</span></span>

6.  <span data-ttu-id="1202c-390">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1202c-390">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1202c-391">Haga clic en **licencias** toosee qué usuario de hello licencias actualmente tiene asignada.</span><span class="sxs-lookup"><span data-stu-id="1202c-391">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="1202c-392">Haga clic en hello **asignar** botón.</span><span class="sxs-lookup"><span data-stu-id="1202c-392">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="1202c-393">Seleccione **uno o más productos** en lista de Hola de productos disponibles.</span><span class="sxs-lookup"><span data-stu-id="1202c-393">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="1202c-394">**Opcional** haga clic en hello **opciones de asignación** elemento toogranularly asignar productos.</span><span class="sxs-lookup"><span data-stu-id="1202c-394">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="1202c-395">Cuando haya finalizado este procedimiento, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1202c-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="1202c-396">Haga clic en hello **asignar** botón tooassign estos usuario toothis de licencias.</span><span class="sxs-lookup"><span data-stu-id="1202c-396">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="1202c-397">Problemas relacionados tooassigning aplicaciones toogroups</span><span class="sxs-lookup"><span data-stu-id="1202c-397">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="1202c-398">Un usuario puede estar viendo una aplicación en su Panel de acceso ya que forman parte de un grupo que se ha asignado la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="1202c-399">A continuación se muestran algunas maneras toocheck:</span><span class="sxs-lookup"><span data-stu-id="1202c-399">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="1202c-400">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="1202c-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="1202c-401">¿Cómo tooassign una tooa de aplicación de grupo directamente</span><span class="sxs-lookup"><span data-stu-id="1202c-401">How tooassign an application tooa group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="1202c-402">Comprobar si un usuario forma parte del grupo asignado licencias tooa</span><span class="sxs-lookup"><span data-stu-id="1202c-402">Check if a user is part of group assigned tooa license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="1202c-403">¿Cómo tooassign un grupo de tooa de licencias</span><span class="sxs-lookup"><span data-stu-id="1202c-403">How tooassign a license tooa group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="1202c-404">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="1202c-404">Check a user’s group memberships</span></span>

<span data-ttu-id="1202c-405">toocheck pertenencia de un grupo, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="1202c-405">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-406">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="1202c-406">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1202c-407">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-407">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-408">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-408">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-409">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-409">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1202c-410">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1202c-410">click **All users**.</span></span>

6.  <span data-ttu-id="1202c-411">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1202c-411">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1202c-412">Haga clic en **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="1202c-412">click **Groups**.</span></span>

8.  <span data-ttu-id="1202c-413">Compruebe toosee si el usuario es parte de una aplicación de toohello de grupo asignado.</span><span class="sxs-lookup"><span data-stu-id="1202c-413">Check toosee if your user is part of a Group assigned toohello application.</span></span>

  * <span data-ttu-id="1202c-414">Si desea que tooremove Hola usuario del grupo de hello, **haga clic en la fila de hello** del grupo de Hola y seleccione Eliminar.</span><span class="sxs-lookup"><span data-stu-id="1202c-414">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="how-tooassign-an-application-tooa-group-directly"></a><span data-ttu-id="1202c-415">¿Cómo tooassign una tooa de aplicación de grupo directamente</span><span class="sxs-lookup"><span data-stu-id="1202c-415">How tooassign an application tooa group directly</span></span>

<span data-ttu-id="1202c-416">tooassign uno o más grupos de aplicación de tooan directamente, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="1202c-416">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-417">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global**.</span><span class="sxs-lookup"><span data-stu-id="1202c-417">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="1202c-418">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-418">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-419">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-419">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-420">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1202c-420">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1202c-421">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1202c-421">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1202c-422">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="1202c-422">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1202c-423">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="1202c-423">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="1202c-424">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1202c-424">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1202c-425">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="1202c-425">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="1202c-426">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="1202c-426">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="1202c-427">Tipo de hello **nombre de grupo completa** del grupo de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="1202c-427">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="1202c-428">Mantenga el mouse sobre hello **grupo** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="1202c-428">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="1202c-429">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla siguiente toohello del grupo su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="1202c-429">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="1202c-430">**Opcional:** si lo desea demasiado**agregar más de un grupo**, tipo de otro **nombre de grupo completa** en hello **buscar por nombre o dirección de correo** cuadro de búsqueda, y haga clic en hello casilla tooadd este grupo toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="1202c-430">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="1202c-431">Cuando haya terminado la selección de grupos, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="1202c-431">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="1202c-432">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** grupos hoja tooselect una toohello tooassign de rol que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="1202c-432">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="1202c-433">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello grupos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="1202c-433">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="1202c-434">Después de un breve período, los usuarios de Hola que seleccionó ser capaz de toolaunch estas aplicaciones en Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1202c-434">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a><span data-ttu-id="1202c-435">Comprobar si un usuario forma parte del grupo asignado licencias tooa</span><span class="sxs-lookup"><span data-stu-id="1202c-435">Check if a user is part of group assigned tooa license</span></span>

1.  <span data-ttu-id="1202c-436">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="1202c-436">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1202c-437">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-437">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-438">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-438">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-439">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-439">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1202c-440">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1202c-440">click **All users**.</span></span>

6.  <span data-ttu-id="1202c-441">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1202c-441">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1202c-442">Haga clic en **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="1202c-442">click **Groups**.</span></span>

8.  <span data-ttu-id="1202c-443">Haga clic en la fila de Hola de un grupo específico.</span><span class="sxs-lookup"><span data-stu-id="1202c-443">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="1202c-444">Haga clic en **licencias** toosee qué grupo de licencias Hola asignó tooit.</span><span class="sxs-lookup"><span data-stu-id="1202c-444">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

   * <span data-ttu-id="1202c-445">Si se asigna el grupo de hello licencia de Office tooan en que esto, puede habilitar determinada tooappear de las aplicaciones de Office de primera entidad Hola Panel de acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="1202c-445">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-license-tooa-group"></a><span data-ttu-id="1202c-446">¿Cómo tooassign un grupo de tooa de licencias</span><span class="sxs-lookup"><span data-stu-id="1202c-446">How tooassign a license tooa group</span></span>

<span data-ttu-id="1202c-447">tooassign un grupo de tooa licencias, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="1202c-447">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="1202c-448">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="1202c-448">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1202c-449">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-449">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1202c-450">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1202c-450">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1202c-451">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-451">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1202c-452">Haga clic en **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="1202c-452">click **All groups**.</span></span>

6.  <span data-ttu-id="1202c-453">**Búsqueda** para grupo de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1202c-453">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1202c-454">Haga clic en **licencias** toosee qué grupo de licencias Hola actualmente tiene asignada.</span><span class="sxs-lookup"><span data-stu-id="1202c-454">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="1202c-455">Haga clic en hello **asignar** botón.</span><span class="sxs-lookup"><span data-stu-id="1202c-455">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="1202c-456">Seleccione **uno o más productos** en lista de Hola de productos disponibles.</span><span class="sxs-lookup"><span data-stu-id="1202c-456">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="1202c-457">**Opcional** haga clic en hello **opciones de asignación** elemento toogranularly asignar productos.</span><span class="sxs-lookup"><span data-stu-id="1202c-457">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="1202c-458">Cuando haya finalizado este procedimiento, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1202c-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="1202c-459">Haga clic en hello **asignar** botón tooassign estos toothis de grupo de licencias.</span><span class="sxs-lookup"><span data-stu-id="1202c-459">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="1202c-460">Esto puede tardar mucho tiempo, en función de hello tamaño y la complejidad del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1202c-460">This may take a long time, depending on hello size and complexity of hello group.</span></span>

>[!NOTE]
><span data-ttu-id="1202c-461">toodo esto con mayor rapidez, considere la posibilidad de temporalmente asignar una licencia toohello usuario directamente.</span><span class="sxs-lookup"><span data-stu-id="1202c-461">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="1202c-462">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1202c-462">Next steps</span></span>
[<span data-ttu-id="1202c-463">Agregar nuevos usuarios tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1202c-463">Add new users tooAzure Active Directory</span></span>](active-directory-users-create-azure-portal.md)


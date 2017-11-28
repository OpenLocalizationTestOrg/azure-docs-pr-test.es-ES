---
title: "aplicaciones de SaaS aaaConfigure para la colaboración B2B de Azure Active Directory | Documentos de Microsoft"
description: "Ejemplos de código y PowerShell para la colaboración B2B de Azure Active Directory"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="e7afa-103">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e7afa-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="e7afa-104">La colaboración de B2B de Azure Active Directory (Azure AD) funciona con la mayoría de las aplicaciones que se integran con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7afa-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="e7afa-105">En esta sección, se proporcionan las instrucciones necesarias para configurar varias aplicaciones populares de SAS para usarlas con B2B de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7afa-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="e7afa-106">Antes de examinar las instrucciones específicas de la aplicación, estas son algunas reglas generales:</span><span class="sxs-lookup"><span data-stu-id="e7afa-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="e7afa-107">Para la mayoría de las aplicaciones de hello, el programa de instalación de usuario debe toohappen manualmente.</span><span class="sxs-lookup"><span data-stu-id="e7afa-107">For most of hello apps, user setup needs toohappen manually.</span></span> <span data-ttu-id="e7afa-108">Es decir, los usuarios deben crearse manualmente en la aplicación hello así.</span><span class="sxs-lookup"><span data-stu-id="e7afa-108">That is, users must be created manually in hello app as well.</span></span>

* <span data-ttu-id="e7afa-109">Para las aplicaciones que admiten la instalación automática, por ejemplo, Dropbox, invitaciones independientes se crean desde las aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7afa-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from hello apps.</span></span> <span data-ttu-id="e7afa-110">Los usuarios debe ser seguro tooaccept cada invitación.</span><span class="sxs-lookup"><span data-stu-id="e7afa-110">Users must be sure tooaccept each invitation.</span></span>

* <span data-ttu-id="e7afa-111">En atributos de usuario de hello, toomitigate los problemas con el disco de perfil de usuario con sufijo (UPD) de usuarios invitados, establezca siempre **identificador de usuario** demasiado**user.mail**.</span><span class="sxs-lookup"><span data-stu-id="e7afa-111">In hello user attributes, toomitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** too**user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="e7afa-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="e7afa-112">Dropbox Business</span></span>

<span data-ttu-id="e7afa-113">tooenable toosign de los usuarios con su cuenta de organización, debe configurar manualmente Business Dropbox toouse Azure AD como proveedor de identidades de lenguaje de marcado de aserción de seguridad (SAML).</span><span class="sxs-lookup"><span data-stu-id="e7afa-113">tooenable users toosign in using their organization account, you must manually configure Dropbox Business toouse Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="e7afa-114">Por lo tanto, si Dropbox empresariales no ha sido configurado toodo no se puede solicitar o toosign de usuarios en el uso de Azure AD de otra manera.</span><span class="sxs-lookup"><span data-stu-id="e7afa-114">If Dropbox Business has not been configured toodo so, it cannot prompt or otherwise allow users toosign in using Azure AD.</span></span>

1. <span data-ttu-id="e7afa-115">aplicación de negocio de Dropbox tooadd hello en Azure AD, seleccione **aplicaciones empresariales** en Hola panel izquierdo y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="e7afa-115">tooadd hello Dropbox Business app into Azure AD, select **Enterprise applications** in hello left pane, and then click **Add**.</span></span>

  ![botón de "Agregar" Hello en la página de aplicaciones de empresa de Hola](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="e7afa-117">Hola **agregar una aplicación** ventana, escriba **dropbox** en Hola cuadro de búsqueda y, a continuación, seleccione **Dropbox para empresas** en la lista de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7afa-117">In hello **Add an application** window, enter **dropbox** in hello search box, and then select **Dropbox for Business** in hello results list.</span></span>

  ![Busque "dropbox" en hello agregar una página de aplicación](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="e7afa-119">En hello **inicio de sesión único** página, seleccione **inicio de sesión único** en Hola panel izquierdo y, a continuación, escriba **user.mail** en hello **identificador de usuario** cuadro.</span><span class="sxs-lookup"><span data-stu-id="e7afa-119">On hello **Single sign-on** page, select **Single sign-on** in hello left pane, and then enter **user.mail** in hello **User Identifier** box.</span></span> <span data-ttu-id="e7afa-120">(de manera predeterminada se establece como UPN).</span><span class="sxs-lookup"><span data-stu-id="e7afa-120">(It's set as UPN by default.)</span></span>

  ![Configurar inicio de sesión único para la aplicación hello](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="e7afa-122">toodownload Hola certificado toouse para la configuración de la lista desplegable, seleccione **configurar DropBox**y, a continuación, seleccione **SAML único inicio de sesión en dirección URL del servicio** en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7afa-122">toodownload hello certificate toouse for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in hello list.</span></span>

  ![Descargando certificado de hello para la configuración de Dropbox](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="e7afa-124">Inicio de sesión tooDropbox con hello sesión dirección URL de hello **inicio de sesión único** página.</span><span class="sxs-lookup"><span data-stu-id="e7afa-124">Sign in tooDropbox with hello sign-on URL from hello **Single sign-on** page.</span></span>

  ![página de Hello en el inicio de sesión de Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="e7afa-126">En el menú de hello, seleccione **consola de administración de**.</span><span class="sxs-lookup"><span data-stu-id="e7afa-126">On hello menu, select **Admin Console**.</span></span>

  ![vínculo de "Consola de administración" de Hello en el menú de Dropbox de Hola](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="e7afa-128">Hola **autenticación** cuadro de diálogo, seleccione **más**, cargar el certificado de hello y, a continuación, en hello **iniciar sesión en la dirección URL** cuadro, escriba la dirección URL de hello el inicio de sesión único SAML.</span><span class="sxs-lookup"><span data-stu-id="e7afa-128">In hello **Authentication** dialog box, select **More**, upload hello certificate and then, in hello **Sign in URL** box, enter hello SAML single sign-on URL.</span></span>

  ![Hola vínculo "Más" en el cuadro de diálogo de autenticación de hello contraído](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Hola "Inicio de sesión en URL" Hola expande el cuadro de diálogo de autenticación](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="e7afa-131">el programa de instalación automática de usuarios tooconfigure Hola portal de Azure, seleccione **Provisioning** en hello panel izquierdo, seleccione **automática** en hello **modo de aprovisionamiento** cuadro y, a continuación, seleccione **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="e7afa-131">tooconfigure automatic user setup in hello Azure portal, select **Provisioning** in hello left pane, select **Automatic** in hello **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Configurar el aprovisionamiento automático de usuarios en hello portal de Azure](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="e7afa-133">Después de que los usuarios invitados o miembro se han configurado en la aplicación de Dropbox hello, que reciben una invitación de independiente de Dropbox.</span><span class="sxs-lookup"><span data-stu-id="e7afa-133">After guest or member users have been set up in hello Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="e7afa-134">toouse inicio de sesión único en Dropbox, los invitados deben Aceptar invitación Hola haciendo clic en un vínculo en ella.</span><span class="sxs-lookup"><span data-stu-id="e7afa-134">toouse Dropbox single sign-on, invitees must accept hello invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="e7afa-135">Box</span><span class="sxs-lookup"><span data-stu-id="e7afa-135">Box</span></span>
<span data-ttu-id="e7afa-136">Puede permitir a los usuarios tooauthenticate cuadro invitado a los usuarios con su cuenta de Azure AD utilizando federación basada en hello protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="e7afa-136">You can enable users tooauthenticate Box guest users with their Azure AD account by using federation that's based on hello SAML protocol.</span></span> <span data-ttu-id="e7afa-137">En este procedimiento, se carga tooBox.com de metadatos.</span><span class="sxs-lookup"><span data-stu-id="e7afa-137">In this procedure, you upload metadata tooBox.com.</span></span>

1. <span data-ttu-id="e7afa-138">Agregar aplicación de cuadro de hello de aplicaciones empresariales de Hola.</span><span class="sxs-lookup"><span data-stu-id="e7afa-138">Add hello Box app from hello enterprise apps.</span></span>

2. <span data-ttu-id="e7afa-139">Configurar inicio de sesión único de hello siguiente orden:</span><span class="sxs-lookup"><span data-stu-id="e7afa-139">Configure single sign-on in hello following order:</span></span>

  ![Configuración del inicio de sesión único de Box](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="e7afa-141">a.</span><span class="sxs-lookup"><span data-stu-id="e7afa-141">a.</span></span> <span data-ttu-id="e7afa-142">Hola **dirección URL de inicio de sesión** cuadro, asegúrese que dirección URL de inicio de sesión de Hola está establecida correctamente para cuadro Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7afa-142">In hello **Sign on URL** box, ensure that hello sign-on URL is set appropriately for Box in hello Azure portal.</span></span> <span data-ttu-id="e7afa-143">Esta dirección URL es Hola de su inquilino de Box.com.</span><span class="sxs-lookup"><span data-stu-id="e7afa-143">This URL is hello URL of your Box.com tenant.</span></span> <span data-ttu-id="e7afa-144">Debe seguir la convención de nomenclatura de hello *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="e7afa-144">It should follow hello naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="e7afa-145">Hola **identificador** no se aplica toothis aplicación, pero sigue apareciendo como un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="e7afa-145">hello **Identifier** does not apply toothis app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="e7afa-146">b.</span><span class="sxs-lookup"><span data-stu-id="e7afa-146">b.</span></span> <span data-ttu-id="e7afa-147">Hola **identificador de usuario** cuadro, escriba **user.mail** (para SSO para las cuentas de invitado).</span><span class="sxs-lookup"><span data-stu-id="e7afa-147">In hello **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="e7afa-148">c.</span><span class="sxs-lookup"><span data-stu-id="e7afa-148">c.</span></span> <span data-ttu-id="e7afa-149">En **Certificado de firma de SAML**, haga clic en **Crear nuevo certificado**.</span><span class="sxs-lookup"><span data-stu-id="e7afa-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="e7afa-150">d.</span><span class="sxs-lookup"><span data-stu-id="e7afa-150">d.</span></span> <span data-ttu-id="e7afa-151">toobegin configurar su toouse de inquilino de Box.com Azure AD como proveedor de identidades, Descargar archivo de metadatos de hello y, a continuación, guárdelo tooyour la unidad local.</span><span class="sxs-lookup"><span data-stu-id="e7afa-151">toobegin configuring your Box.com tenant toouse Azure AD as an identity provider, download hello metadata file and then save it tooyour local drive.</span></span>

 <span data-ttu-id="e7afa-152">e.</span><span class="sxs-lookup"><span data-stu-id="e7afa-152">e.</span></span> <span data-ttu-id="e7afa-153">Reenviar Hola metadatos archivo toohello cuadro equipo de soporte técnico, que configura el inicio de sesión único automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e7afa-153">Forward hello metadata file toohello Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="e7afa-154">Para la instalación de usuario automático de Azure AD, en el panel izquierdo de hello, seleccione **Provisioning**y, a continuación, seleccione **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="e7afa-154">For Azure AD automatic user setup, in hello left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Autorizar el cuadro de herramientas de Azure AD tooconnect](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="e7afa-156">Al igual que los invitados de Dropbox, los invitados cuadro deben canjear su invitación de aplicación del cuadro de hello.</span><span class="sxs-lookup"><span data-stu-id="e7afa-156">Like Dropbox invitees, Box invitees must redeem their invitation from hello Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7afa-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e7afa-157">Next steps</span></span>

<span data-ttu-id="e7afa-158">Vea Hola siguientes artículos en la colaboración B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="e7afa-158">See hello following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="e7afa-159">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="e7afa-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="e7afa-160">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e7afa-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="e7afa-161">Agregar un rol de tooa de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e7afa-161">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="e7afa-162">Delegación de las invitaciones de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e7afa-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="e7afa-163">Grupos dinámicos y colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e7afa-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="e7afa-164">Código de colaboración B2B y ejemplos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7afa-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="e7afa-165">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e7afa-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="e7afa-166">Asignación de notificaciones de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e7afa-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="e7afa-167">Uso compartido externo de Office 365</span><span class="sxs-lookup"><span data-stu-id="e7afa-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="e7afa-168">Limitaciones actuales de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="e7afa-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)

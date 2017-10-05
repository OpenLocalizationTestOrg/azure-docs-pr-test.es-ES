---
title: "Configuración de aplicaciones de SaaS para la colaboración B2B de Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: 149a493f7b369415f0a2726dd6a576f0195c13d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="a6571-103">Configuración de aplicaciones de SaaS para la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="a6571-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="a6571-104">La colaboración de B2B de Azure Active Directory (Azure AD) funciona con la mayoría de las aplicaciones que se integran con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6571-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="a6571-105">En esta sección, se proporcionan las instrucciones necesarias para configurar varias aplicaciones populares de SAS para usarlas con B2B de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6571-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="a6571-106">Antes de examinar las instrucciones específicas de la aplicación, estas son algunas reglas generales:</span><span class="sxs-lookup"><span data-stu-id="a6571-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="a6571-107">En la mayoría de las aplicaciones, la instalación del usuario se debe realizar de forma manual.</span><span class="sxs-lookup"><span data-stu-id="a6571-107">For most of the apps, user setup needs to happen manually.</span></span> <span data-ttu-id="a6571-108">Es decir, los usuarios deben crearse de forma manual también en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a6571-108">That is, users must be created manually in the app as well.</span></span>

* <span data-ttu-id="a6571-109">En el caso de las aplicaciones que admiten la instalación automática, como Dropbox, se crean invitaciones independientes desde las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a6571-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from the apps.</span></span> <span data-ttu-id="a6571-110">Los usuarios debe asegurarse de aceptar cada invitación.</span><span class="sxs-lookup"><span data-stu-id="a6571-110">Users must be sure to accept each invitation.</span></span>

* <span data-ttu-id="a6571-111">En los atributos del usuario, para mitigar cualquier problema de alteración del disco de perfil de usuario (UPD) en usuarios invitados, en **Identificador de usuario**, seleccione siempre **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="a6571-111">In the user attributes, to mitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** to **user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="a6571-112">Dropbox Business</span><span class="sxs-lookup"><span data-stu-id="a6571-112">Dropbox Business</span></span>

<span data-ttu-id="a6571-113">Para permitir que los usuarios inicien sesión con su cuenta de organización, es preciso configurar manualmente Dropbox Business para que use Azure AD como proveedor de identidades del lenguaje de marcado de aserción de seguridad (SAML).</span><span class="sxs-lookup"><span data-stu-id="a6571-113">To enable users to sign in using their organization account, you must manually configure Dropbox Business to use Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="a6571-114">Si Dropbox Business no se ha configurado para ello, no puede solicitar o, en caso contrario, permitir a los usuarios que inicien sesión con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6571-114">If Dropbox Business has not been configured to do so, it cannot prompt or otherwise allow users to sign in using Azure AD.</span></span>

1. <span data-ttu-id="a6571-115">Para agregar la aplicación Dropbox Business a Azure AD, seleccione **Aplicaciones empresariales** en el panel izquierdo y, después, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a6571-115">To add the Dropbox Business app into Azure AD, select **Enterprise applications** in the left pane, and then click **Add**.</span></span>

  ![El botón "Agregar" de la página Aplicaciones empresariales](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="a6571-117">En la ventana **Agregar una aplicación**, escriba **dropbox** en el cuadro de búsqueda y seleccione **Dropbox for Business** en la lista de resultados.</span><span class="sxs-lookup"><span data-stu-id="a6571-117">In the **Add an application** window, enter **dropbox** in the search box, and then select **Dropbox for Business** in the results list.</span></span>

  ![Busque "dropbox" en la página Agregar una aplicación](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="a6571-119">En la página **Inicio de sesión único**, seleccione **Inicio de sesión único** en el panel izquierdo y, después, escriba **user.mail** en el cuando **Identificador de usuario**</span><span class="sxs-lookup"><span data-stu-id="a6571-119">On the **Single sign-on** page, select **Single sign-on** in the left pane, and then enter **user.mail** in the **User Identifier** box.</span></span> <span data-ttu-id="a6571-120">(de manera predeterminada se establece como UPN).</span><span class="sxs-lookup"><span data-stu-id="a6571-120">(It's set as UPN by default.)</span></span>

  ![Configuración del inicio de sesión único para la aplicación](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="a6571-122">Para descargar el certificado que se va a usar para la configuración de Dropbox, seleccione **Configurar DropBox**y, después, seleccione **SAML Single Sign On Service URL** (URL del servicio de inicio de sesión único de SAML) en la lista.</span><span class="sxs-lookup"><span data-stu-id="a6571-122">To download the certificate to use for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in the list.</span></span>

  ![Descarga del certificado para la configuración de Dropbox](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="a6571-124">Inicie sesión en Dropbox con la URL de inicio de sesión desde la página **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a6571-124">Sign in to Dropbox with the sign-on URL from the **Single sign-on** page.</span></span>

  ![La página de inicio de sesión de Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="a6571-126">En el menú, seleccione **Admin Console** (Consola de administración).</span><span class="sxs-lookup"><span data-stu-id="a6571-126">On the menu, select **Admin Console**.</span></span>

  ![El vínculo "Admin Console" (Consola de administración) en el menú de Dropbox](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="a6571-128">En el cuadro de diálogo **Authentication** (Autenticación), seleccione **More** (Más), cargue el certificado y, después, en el cuadro **Sign in URL** (URL de inicio de sesión), escriba la URL de inicio de sesión único de SAML.</span><span class="sxs-lookup"><span data-stu-id="a6571-128">In the **Authentication** dialog box, select **More**, upload the certificate and then, in the **Sign in URL** box, enter the SAML single sign-on URL.</span></span>

  ![El vínculo "More" (Más) en el cuadro de diálogo Authentication (Autenticación) contraído](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![El vínculo "Sign in URL" (URL de inicio de sesión) en el cuadro de diálogo Authentication (Autenticación) expandido](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="a6571-131">Para configurar la instalación automática del usuario en Azure Portal, seleccione **Aprovisionamiento** en el panel izquierdo, después **Automático** en el cuadro **Modo de aprovisionamiento** y, finalmente, seleccione **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="a6571-131">To configure automatic user setup in the Azure portal, select **Provisioning** in the left pane, select **Automatic** in the **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Configuración del aprovisionamiento automático de usuarios en Azure Portal](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="a6571-133">Una vez que los usuarios miembros o invitados se hayan configurado en la aplicación de Dropbox, reciben una invitación independiente de Dropbox.</span><span class="sxs-lookup"><span data-stu-id="a6571-133">After guest or member users have been set up in the Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="a6571-134">Para usar el inicio de sesión único de Dropbox, los invitados deben aceptar dicha invitación haciendo clic en un vínculo de ella.</span><span class="sxs-lookup"><span data-stu-id="a6571-134">To use Dropbox single sign-on, invitees must accept the invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="a6571-135">Box</span><span class="sxs-lookup"><span data-stu-id="a6571-135">Box</span></span>
<span data-ttu-id="a6571-136">Puede permitir que los usuarios autentiquen usuarios invitados de Box con su cuenta de Azure AD mediante el uso de una federación basada en el protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="a6571-136">You can enable users to authenticate Box guest users with their Azure AD account by using federation that's based on the SAML protocol.</span></span> <span data-ttu-id="a6571-137">En este procedimiento, se cargan metadatos en Box.com.</span><span class="sxs-lookup"><span data-stu-id="a6571-137">In this procedure, you upload metadata to Box.com.</span></span>

1. <span data-ttu-id="a6571-138">Agregue la aplicación Box desde las aplicaciones empresariales.</span><span class="sxs-lookup"><span data-stu-id="a6571-138">Add the Box app from the enterprise apps.</span></span>

2. <span data-ttu-id="a6571-139">Configure el inicio de sesión único en el orden siguiente:</span><span class="sxs-lookup"><span data-stu-id="a6571-139">Configure single sign-on in the following order:</span></span>

  ![Configuración del inicio de sesión único de Box](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="a6571-141">a.</span><span class="sxs-lookup"><span data-stu-id="a6571-141">a.</span></span> <span data-ttu-id="a6571-142">En el cuadro **URL de inicio de sesión**, asegúrese de que la dirección URL de inicio de sesión se ha establecido correctamente para Box en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a6571-142">In the **Sign on URL** box, ensure that the sign-on URL is set appropriately for Box in the Azure portal.</span></span> <span data-ttu-id="a6571-143">Esta es la dirección URL de su inquilino de Box.com.</span><span class="sxs-lookup"><span data-stu-id="a6571-143">This URL is the URL of your Box.com tenant.</span></span> <span data-ttu-id="a6571-144">Debe seguir la convención de nomenclatura *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="a6571-144">It should follow the naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="a6571-145">**Identificador** no se aplica a esta aplicación, pero sigue apareciendo como campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="a6571-145">The **Identifier** does not apply to this app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="a6571-146">b.</span><span class="sxs-lookup"><span data-stu-id="a6571-146">b.</span></span> <span data-ttu-id="a6571-147">En el cuadro **Identificador de usuario**, escriba **user.mail** (para el SSO de las cuentas de invitado).</span><span class="sxs-lookup"><span data-stu-id="a6571-147">In the **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="a6571-148">c.</span><span class="sxs-lookup"><span data-stu-id="a6571-148">c.</span></span> <span data-ttu-id="a6571-149">En **Certificado de firma de SAML**, haga clic en **Crear nuevo certificado**.</span><span class="sxs-lookup"><span data-stu-id="a6571-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="a6571-150">d.</span><span class="sxs-lookup"><span data-stu-id="a6571-150">d.</span></span> <span data-ttu-id="a6571-151">Para empezar a configurar el inquilino de Box.com para que use Azure AD como proveedor de identidades, descargue el archivo de metadatos y guárdelo en una unidad local.</span><span class="sxs-lookup"><span data-stu-id="a6571-151">To begin configuring your Box.com tenant to use Azure AD as an identity provider, download the metadata file and then save it to your local drive.</span></span>

 <span data-ttu-id="a6571-152">e.</span><span class="sxs-lookup"><span data-stu-id="a6571-152">e.</span></span> <span data-ttu-id="a6571-153">Reenvíe el archivo de metadatos al equipo de soporte técnico de Box para que configuren el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a6571-153">Forward the metadata file to the Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="a6571-154">Para la instalación automática de usuarios de Azure AD, en el panel izquierdo, seleccione **Aprovisionamiento**y, después, **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="a6571-154">For Azure AD automatic user setup, in the left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Autorizar a Azure AD para conectarse a Box](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="a6571-156">Los invitados de Box deben canjear su invitación desde la aplicación de Box tal como lo hacen los de Dropbox.</span><span class="sxs-lookup"><span data-stu-id="a6571-156">Like Dropbox invitees, Box invitees must redeem their invitation from the Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6571-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a6571-157">Next steps</span></span>

<span data-ttu-id="a6571-158">Consulte los siguientes artículos sobre la colaboración de B2B de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="a6571-158">See the following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="a6571-159">¿Qué es la colaboración B2B de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="a6571-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="a6571-160">Propiedades de usuario de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="a6571-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="a6571-161">Incorporación de usuarios de colaboración B2B a un rol</span><span class="sxs-lookup"><span data-stu-id="a6571-161">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="a6571-162">Delegación de las invitaciones de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="a6571-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="a6571-163">Grupos dinámicos y colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="a6571-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="a6571-164">Código de colaboración B2B y ejemplos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6571-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="a6571-165">Tokens de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="a6571-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="a6571-166">Asignación de notificaciones de usuario de colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="a6571-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="a6571-167">Uso compartido externo de Office 365</span><span class="sxs-lookup"><span data-stu-id="a6571-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="a6571-168">Limitaciones actuales de la colaboración B2B</span><span class="sxs-lookup"><span data-stu-id="a6571-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)

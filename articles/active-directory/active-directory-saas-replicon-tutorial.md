---
title: "Tutorial: Integración de Azure Active Directory con Replicon | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse Replicon con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="d57b7-103">Tutorial: Integración de Azure Active Directory con Replicon</span><span class="sxs-lookup"><span data-stu-id="d57b7-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="d57b7-104">objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y Replicon.</span><span class="sxs-lookup"><span data-stu-id="d57b7-104">hello objective of this tutorial is tooshow hello integration of Azure and Replicon.</span></span> <span data-ttu-id="d57b7-105">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d57b7-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="d57b7-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="d57b7-106">A valid Azure subscription</span></span>
* <span data-ttu-id="d57b7-107">Un inquilino de Replicon</span><span class="sxs-lookup"><span data-stu-id="d57b7-107">A Replicon tenant</span></span>

<span data-ttu-id="d57b7-108">Después de completar este tutorial, los usuarios de hello Azure AD que haya asignado tooReplicon será toosingle capaz de inicio de sesión en la aplicación hello en el sitio de empresa de Replicon (servicio iniciado por el proveedor inicio de sesión), o mediante hello [Introducción toohello acceso Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d57b7-108">After completing this tutorial, hello Azure AD users you have assigned tooReplicon will be able toosingle sign into hello application at your Replicon company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="d57b7-109">escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d57b7-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="d57b7-110">Habilitar la integración de aplicación Hola para Replicon</span><span class="sxs-lookup"><span data-stu-id="d57b7-110">Enabling hello application integration for Replicon</span></span>
2. <span data-ttu-id="d57b7-111">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="d57b7-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="d57b7-112">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="d57b7-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="d57b7-113">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="d57b7-113">Assigning users</span></span>

<span data-ttu-id="d57b7-114">![Escenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="d57b7-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-replicon"></a><span data-ttu-id="d57b7-115">Habilitar la integración de aplicación Hola para Replicon</span><span class="sxs-lookup"><span data-stu-id="d57b7-115">Enable hello application integration for Replicon</span></span>
<span data-ttu-id="d57b7-116">objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para Replicon.</span><span class="sxs-lookup"><span data-stu-id="d57b7-116">hello objective of this section is toooutline how tooenable hello application integration for Replicon.</span></span>

<span data-ttu-id="d57b7-117">**integración de aplicaciones de hello tooenable para Replicon, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d57b7-117">**tooenable hello application integration for Replicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="d57b7-118">Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d57b7-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="d57b7-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d57b7-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="d57b7-120">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="d57b7-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="d57b7-121">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="d57b7-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="d57b7-122">![Aplicaciones](./media/active-directory-saas-replicon-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="d57b7-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="d57b7-123">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="d57b7-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="d57b7-124">![Agregar aplicaciones](./media/active-directory-saas-replicon-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="d57b7-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="d57b7-125">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="d57b7-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="d57b7-126">![Agregar una aplicación de la galería](./media/active-directory-saas-replicon-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="d57b7-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="d57b7-127">Hola **cuadro de búsqueda**, tipo **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="d57b7-127">In hello **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="d57b7-128">![Galería de aplicaciones](./media/active-directory-saas-replicon-tutorial/IC777799.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="d57b7-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="d57b7-129">En el panel de resultados de hello, seleccione **Replicon**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d57b7-129">In hello results pane, select **Replicon**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="d57b7-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="d57b7-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="d57b7-131">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="d57b7-131">Configure single sign-on</span></span>

<span data-ttu-id="d57b7-132">objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooReplicon con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="d57b7-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooReplicon with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="d57b7-133">**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d57b7-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="d57b7-134">En el portal de Azure clásico en Hola Hola **Replicon** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d57b7-134">In hello Azure classic portal, on hello **Replicon** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="d57b7-135">![Configurar inicio de sesión único](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="d57b7-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="d57b7-136">En hello **¿cómo desea que los usuarios toosign en tooReplicon** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d57b7-136">On hello **How would you like users toosign on tooReplicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="d57b7-137">![Configurar inicio de sesión único](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="d57b7-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="d57b7-138">En hello **configurar URL de aplicación** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="d57b7-138">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="d57b7-139">![Configurar dirección URL de la aplicación](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="d57b7-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="d57b7-140">Hola **Replicon inicio de sesión en la URL** cuadro de texto, escriba la dirección URL de inquilino de Replicon (p. ej.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="d57b7-140">In hello **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="d57b7-141">Hola **dirección URL de respuesta de Replicon** cuadro de texto, escriba su Replicon **AssertionConsumerService** dirección URL (p. ej.: *https://global.replicon.com/! / saml2/empresa/sso/post*).</span><span class="sxs-lookup"><span data-stu-id="d57b7-141">In hello **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="d57b7-142">Puede obtener dirección URL de Hola de hello metadatos de Replicon en: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.</span><span class="sxs-lookup"><span data-stu-id="d57b7-142">You can get hello URL from hello Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="d57b7-143">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d57b7-143">Click **Next**.</span></span>

4. <span data-ttu-id="d57b7-144">En hello **configurar inicio de sesión único en Replicon** page, toodownload sus metadatos, haga clic en **descargar metadatos**y, a continuación, guarde los metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d57b7-144">On hello **Configure single sign-on at Replicon** page, toodownload your metadata, click **Download metadata**, and then save hello metadata on your computer.</span></span>
   
    <span data-ttu-id="d57b7-145">![Configurar inicio de sesión único](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="d57b7-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="d57b7-146">En otra ventana del explorador web, inicie sesión en como administrador en el sitio de Replicon de la compañía.</span><span class="sxs-lookup"><span data-stu-id="d57b7-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="d57b7-147">tooconfigure SAML 2.0, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d57b7-147">tooconfigure SAML 2.0, perform hello following steps:</span></span>
   
    <span data-ttu-id="d57b7-148">![Habilitar la autenticación SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "Habilitar la autenticación SAML")</span><span class="sxs-lookup"><span data-stu-id="d57b7-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="d57b7-149">Hola toodisplay **EnableSAML Authentication2** cuadro de diálogo, anexar Hola después de dirección URL de tooyour, después de la clave de su empresa: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="d57b7-149">toodisplay hello **EnableSAML Authentication2** dialog, append hello following tooyour URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="d57b7-150">siguiente Hello muestra esquema Hola de dirección URL completa de hello:</span><span class="sxs-lookup"><span data-stu-id="d57b7-150">hello following shows hello schema of hello complete URL:</span></span>  
   <span data-ttu-id="d57b7-151">**https://na2.replicon.com/\<SuClaveCompañía\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="d57b7-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="d57b7-152">Haga clic en hello  **+**  tooexpand hello **v20Configuration** sección.</span><span class="sxs-lookup"><span data-stu-id="d57b7-152">Click hello **+** tooexpand hello **v20Configuration** section.</span></span>
   3. <span data-ttu-id="d57b7-153">Haga clic en hello  **+**  tooexpand hello **metaDataConfiguration** sección.</span><span class="sxs-lookup"><span data-stu-id="d57b7-153">Click hello **+** tooexpand hello **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="d57b7-154">Haga clic en **Elegir archivo**, tooselect su archivo XML de metadatos de proveedor de identidad y haga clic en **enviar**.</span><span class="sxs-lookup"><span data-stu-id="d57b7-154">Click **Choose File**, tooselect your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="d57b7-155">En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d57b7-155">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="d57b7-156">![Configurar inicio de sesión único](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="d57b7-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="d57b7-157">Configurar aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="d57b7-157">Configure user provisioning</span></span>

<span data-ttu-id="d57b7-158">En orden tooenable toolog de los usuarios de Azure AD en Replicon, se les deben aprovisionar en Replicon.</span><span class="sxs-lookup"><span data-stu-id="d57b7-158">In order tooenable Azure AD users toolog into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="d57b7-159">En caso de hello de Replicon, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="d57b7-159">In hello case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="d57b7-160">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d57b7-160">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="d57b7-161">En una ventana del explorador web, inicie sesión en como administrador en el sitio de Replicon de la compañía.</span><span class="sxs-lookup"><span data-stu-id="d57b7-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="d57b7-162">Vaya demasiado**administración \> usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d57b7-162">Go too**Administration \> Users**.</span></span>
   
    <span data-ttu-id="d57b7-163">![Usuarios](./media/active-directory-saas-replicon-tutorial/IC777806.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="d57b7-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="d57b7-164">Haga clic en **+Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="d57b7-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="d57b7-165">![Agregar usuario](./media/active-directory-saas-replicon-tutorial/IC777807.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="d57b7-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="d57b7-166">Hola **perfil de usuario** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d57b7-166">In hello **User Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="d57b7-167">![Perfil de usuario](./media/active-directory-saas-replicon-tutorial/IC777808.png "Perfil de usuario")</span><span class="sxs-lookup"><span data-stu-id="d57b7-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="d57b7-168">Hola **nombre de inicio de sesión** cuadro de texto, hello Azure AD de tipo dirección de correo electrónico del usuario de hello Azure AD que desee tooprovision.</span><span class="sxs-lookup"><span data-stu-id="d57b7-168">In hello **Login Name** textbox, type hello Azure AD email address of hello Azure AD user you want tooprovision.</span></span>
  2. <span data-ttu-id="d57b7-169">En **Tipo de autenticación,** seleccione **SSO**.</span><span class="sxs-lookup"><span data-stu-id="d57b7-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="d57b7-170">Hola **departamento** cuadro de texto, escriba el departamento del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="d57b7-170">In hello **Department** textbox, type hello user’s department.</span></span>
  4. <span data-ttu-id="d57b7-171">En **Tipo de empleado**, seleccione **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="d57b7-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="d57b7-172">Haga clic en **Guardar perfil de usuario**.</span><span class="sxs-lookup"><span data-stu-id="d57b7-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="d57b7-173">Puede usar cualquier otra Replicon usuario cuenta herramienta de creación o las API proporcionadas por Replicon tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="d57b7-173">You can use any other Replicon user account creation tools or APIs provided by Replicon tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="d57b7-174">Asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="d57b7-174">Assign users</span></span>
<span data-ttu-id="d57b7-175">tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.</span><span class="sxs-lookup"><span data-stu-id="d57b7-175">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="d57b7-176">**tooassign tooReplicon de los usuarios, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d57b7-176">**tooassign users tooReplicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="d57b7-177">Hola portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="d57b7-177">In hello Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="d57b7-178">En hello **Replicon** página de integración de aplicaciones, haga clic en **asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d57b7-178">On hello **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="d57b7-179">![Asignar usuarios](./media/active-directory-saas-replicon-tutorial/IC777809.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="d57b7-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="d57b7-180">Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.</span><span class="sxs-lookup"><span data-stu-id="d57b7-180">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="d57b7-181">![Sí](./media/active-directory-saas-replicon-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="d57b7-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="d57b7-182">Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d57b7-182">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="d57b7-183">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d57b7-183">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


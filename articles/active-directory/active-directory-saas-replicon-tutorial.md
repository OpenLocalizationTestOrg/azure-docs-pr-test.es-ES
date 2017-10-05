---
title: "Tutorial: Integración de Azure Active Directory con Replicon | Microsoft Docs"
description: "Aprenda cómo usar Replicon con Azure Active Directory para habilitar el inicio de sesión único, el aprovisionamiento automatizado, etc."
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
ms.openlocfilehash: 2aeeceb61191962b62892b8409218684f76c6fa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="e583e-103">Tutorial: Integración de Azure Active Directory con Replicon</span><span class="sxs-lookup"><span data-stu-id="e583e-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="e583e-104">El objetivo de este tutorial es mostrar la integración de Azure y Replicon.</span><span class="sxs-lookup"><span data-stu-id="e583e-104">The objective of this tutorial is to show the integration of Azure and Replicon.</span></span> <span data-ttu-id="e583e-105">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e583e-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="e583e-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="e583e-106">A valid Azure subscription</span></span>
* <span data-ttu-id="e583e-107">Un inquilino de Replicon</span><span class="sxs-lookup"><span data-stu-id="e583e-107">A Replicon tenant</span></span>

<span data-ttu-id="e583e-108">Después de completar este tutorial, los usuarios de Azure AD que ha asignado a Replicon podrán realizar un inicio de sesión único en la aplicación en el sitio de la compañía Replicon (inicio de sesión iniciado por el proveedor de servicios) o con la [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e583e-108">After completing this tutorial, the Azure AD users you have assigned to Replicon will be able to single sign into the application at your Replicon company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="e583e-109">La situación descrita en este tutorial consta de los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e583e-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="e583e-110">Habilitación de la integración de aplicaciones para Replicon</span><span class="sxs-lookup"><span data-stu-id="e583e-110">Enabling the application integration for Replicon</span></span>
2. <span data-ttu-id="e583e-111">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="e583e-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="e583e-112">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="e583e-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="e583e-113">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="e583e-113">Assigning users</span></span>

<span data-ttu-id="e583e-114">![Escenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="e583e-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-replicon"></a><span data-ttu-id="e583e-115">Habilitación de la integración de aplicaciones para Replicon</span><span class="sxs-lookup"><span data-stu-id="e583e-115">Enable the application integration for Replicon</span></span>
<span data-ttu-id="e583e-116">El objetivo de esta sección es describir cómo habilitar la integración de aplicaciones para Replicon.</span><span class="sxs-lookup"><span data-stu-id="e583e-116">The objective of this section is to outline how to enable the application integration for Replicon.</span></span>

<span data-ttu-id="e583e-117">**Siga estos pasos con el fin de habilitar la integración de aplicaciones para Replicon:**</span><span class="sxs-lookup"><span data-stu-id="e583e-117">**To enable the application integration for Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="e583e-118">En el panel de navegación izquierdo del Portal de Azure clásico, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e583e-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="e583e-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="e583e-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="e583e-120">En la lista **Directory**, seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="e583e-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e583e-121">Para abrir la vista de aplicaciones, haga clic en **Applications**, en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="e583e-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="e583e-122">![Aplicaciones](./media/active-directory-saas-replicon-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="e583e-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="e583e-123">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="e583e-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="e583e-124">![Agregar aplicaciones](./media/active-directory-saas-replicon-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="e583e-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="e583e-125">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="e583e-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="e583e-126">![Agregar una aplicación de la galería](./media/active-directory-saas-replicon-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="e583e-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="e583e-127">En el **cuadro de búsqueda**, escriba **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="e583e-127">In the **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="e583e-128">![Galería de aplicaciones](./media/active-directory-saas-replicon-tutorial/IC777799.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="e583e-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="e583e-129">En el panel de resultados, seleccione **Replicon** y haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e583e-129">In the results pane, select **Replicon**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="e583e-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="e583e-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="e583e-131">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="e583e-131">Configure single sign-on</span></span>

<span data-ttu-id="e583e-132">El objetivo de esta sección es describir cómo habilitar usuarios para que se autentiquen en Replicon con su cuenta de Azure AD a través de la federación basada en el protocolo SAML.</span><span class="sxs-lookup"><span data-stu-id="e583e-132">The objective of this section is to outline how to enable users to authenticate to Replicon with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="e583e-133">**Siga estos pasos para configurar el inicio de sesión único:**</span><span class="sxs-lookup"><span data-stu-id="e583e-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="e583e-134">En el Portal de Azure clásico, en la página de integración de aplicaciones de **Replicon**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e583e-134">In the Azure classic portal, on the **Replicon** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="e583e-135">![Configurar inicio de sesión único](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="e583e-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="e583e-136">En la página **¿Cómo desea que los usuarios inicien sesión en Replicon?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e583e-136">On the **How would you like users to sign on to Replicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="e583e-137">![Configurar inicio de sesión único](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="e583e-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="e583e-138">En la página **Configurar dirección URL de la aplicación** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e583e-138">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="e583e-139">![Configurar dirección URL de la aplicación](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="e583e-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="e583e-140">En el cuadro de texto **URL de inicio de sesión de Replicon**, escriba la dirección URL del inquilino de Replicon (p. ej.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="e583e-140">In the **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="e583e-141">En el cuadro de texto **URL de inicio de sesión de Replicon**, escriba la dirección URL **AssertionConsumerService** de Replicon (p. ej.: *https://global.replicon.com/!/saml2/company/sso/post*).</span><span class="sxs-lookup"><span data-stu-id="e583e-141">In the **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="e583e-142">Puede obtener la dirección URL de los metadatos de Replicon en: **https://global.replicon.com/!/saml2/\<SuClaveCompañía\>**.</span><span class="sxs-lookup"><span data-stu-id="e583e-142">You can get the URL from the Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="e583e-143">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e583e-143">Click **Next**.</span></span>

4. <span data-ttu-id="e583e-144">En la página **Configurar inicio de sesión único en Replicon**, para descargar los metadatos, haga clic en **Descargar metadatos** y guarde los metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e583e-144">On the **Configure single sign-on at Replicon** page, to download your metadata, click **Download metadata**, and then save the metadata on your computer.</span></span>
   
    <span data-ttu-id="e583e-145">![Configurar inicio de sesión único](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="e583e-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="e583e-146">En otra ventana del explorador web, inicie sesión en como administrador en el sitio de Replicon de la compañía.</span><span class="sxs-lookup"><span data-stu-id="e583e-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="e583e-147">Lleve a cabo los siguientes pasos para configurar SAML 2.0:</span><span class="sxs-lookup"><span data-stu-id="e583e-147">To configure SAML 2.0, perform the following steps:</span></span>
   
    <span data-ttu-id="e583e-148">![Habilitar la autenticación SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "Habilitar la autenticación SAML")</span><span class="sxs-lookup"><span data-stu-id="e583e-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="e583e-149">Para mostrar el cuadro de diálogo **EnableSAMLAuthentication2**, anexe la siguiente cadena a la dirección URL, después de la clave de la empresa: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**.</span><span class="sxs-lookup"><span data-stu-id="e583e-149">To display the **EnableSAML Authentication2** dialog, append the following to your URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="e583e-150">Lo siguiente muestra el esquema de la dirección URL completa:</span><span class="sxs-lookup"><span data-stu-id="e583e-150">The following shows the schema of the complete URL:</span></span>  
   <span data-ttu-id="e583e-151">**https://na2.replicon.com/\<SuClaveCompañía\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="e583e-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="e583e-152">Haga clic en **+** para expandir la sección **v20Configuration**.</span><span class="sxs-lookup"><span data-stu-id="e583e-152">Click the **+** to expand the **v20Configuration** section.</span></span>
   3. <span data-ttu-id="e583e-153">Haga clic en **+** para expandir la sección **metaDataConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="e583e-153">Click the **+** to expand the **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="e583e-154">Haga clic en **Elegir archivo** para seleccionar el archivo XML de metadatos del proveedor de identidades y haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="e583e-154">Click **Choose File**, to select your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="e583e-155">En el Portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único y haga clic en **Completar** para cerrar el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e583e-155">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="e583e-156">![Configurar inicio de sesión único](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="e583e-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="e583e-157">Configurar aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="e583e-157">Configure user provisioning</span></span>

<span data-ttu-id="e583e-158">Para permitir que los usuarios de Azure AD inicien sesión en Replicon, deben aprovisionarse en Replicon.</span><span class="sxs-lookup"><span data-stu-id="e583e-158">In order to enable Azure AD users to log into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="e583e-159">En el caso de Replicon, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="e583e-159">In the case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="e583e-160">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="e583e-160">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="e583e-161">En una ventana del explorador web, inicie sesión en como administrador en el sitio de Replicon de la compañía.</span><span class="sxs-lookup"><span data-stu-id="e583e-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="e583e-162">Vaya a **Administración \> Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e583e-162">Go to **Administration \> Users**.</span></span>
   
    <span data-ttu-id="e583e-163">![Usuarios](./media/active-directory-saas-replicon-tutorial/IC777806.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="e583e-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="e583e-164">Haga clic en **+Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="e583e-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="e583e-165">![Agregar usuario](./media/active-directory-saas-replicon-tutorial/IC777807.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="e583e-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="e583e-166">En la sección **Perfil de usuario** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e583e-166">In the **User Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e583e-167">![Perfil de usuario](./media/active-directory-saas-replicon-tutorial/IC777808.png "Perfil de usuario")</span><span class="sxs-lookup"><span data-stu-id="e583e-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="e583e-168">En el cuadro de texto **Nombre de inicio de sesión** , escriba la dirección de correo electrónico del usuario de Azure AD que quiera aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="e583e-168">In the **Login Name** textbox, type the Azure AD email address of the Azure AD user you want to provision.</span></span>
  2. <span data-ttu-id="e583e-169">En **Tipo de autenticación,** seleccione **SSO**.</span><span class="sxs-lookup"><span data-stu-id="e583e-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="e583e-170">En el cuadro de texto **Departamento** , escriba el departamento del usuario.</span><span class="sxs-lookup"><span data-stu-id="e583e-170">In the **Department** textbox, type the user’s department.</span></span>
  4. <span data-ttu-id="e583e-171">En **Tipo de empleado**, seleccione **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="e583e-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="e583e-172">Haga clic en **Guardar perfil de usuario**.</span><span class="sxs-lookup"><span data-stu-id="e583e-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="e583e-173">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Replicon que proporcione Replicon para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="e583e-173">You can use any other Replicon user account creation tools or APIs provided by Replicon to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="e583e-174">Asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="e583e-174">Assign users</span></span>
<span data-ttu-id="e583e-175">Para probar la configuración, debe conceder acceso a los usuarios de Azure AD a los que quiere permitir el uso de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="e583e-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="e583e-176">**Para asignar usuarios a Replicon, lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="e583e-176">**To assign users to Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="e583e-177">En el Portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="e583e-177">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="e583e-178">En la página de integración de aplicaciones de **Replicon**, haga clic en **Asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e583e-178">On the **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="e583e-179">![Asignar usuarios](./media/active-directory-saas-replicon-tutorial/IC777809.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="e583e-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="e583e-180">Seleccione su usuario de prueba, haga clic en **Asignar** y en **Sí** para confirmar la asignación.</span><span class="sxs-lookup"><span data-stu-id="e583e-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="e583e-181">![Sí](./media/active-directory-saas-replicon-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="e583e-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="e583e-182">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e583e-182">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="e583e-183">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e583e-183">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


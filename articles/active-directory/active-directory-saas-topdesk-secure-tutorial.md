---
title: "Tutorial: integración de Azure Active Directory con TOPdesk - Secure | Microsoft Docs"
description: "Aprenda cómo usar TOPdesk - Secure con Azure Active Directory para habilitar el inicio de sesión único, el aprovisionamiento automatizado, etc."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 28f0542dbe87bb34c83a7852db7c3a9fef055ce9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="d18e3-103">Tutorial: integración de Azure Active Directory con TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="d18e3-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="d18e3-104">El objetivo de este tutorial es mostrar la integración de Azure y TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="d18e3-104">The objective of this tutorial is to show the integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="d18e3-105">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d18e3-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="d18e3-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="d18e3-106">A valid Azure subscription</span></span>
* <span data-ttu-id="d18e3-107">Una suscripción habilitada para el inicio de sesión único en TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="d18e3-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="d18e3-108">Después de completar este tutorial, los usuarios de Azure AD que ha asignado a TOPdesk - Secure podrán realizar un inicio de sesión único en la aplicación en el sitio de la compañía de TOPdesk - Secure (inicio de sesión iniciado por el proveedor de servicios) o con la [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d18e3-108">After completing this tutorial, the Azure AD users you have assigned to TOPdesk - Secure will be able to single sign into the application at your TOPdesk - Secure company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="d18e3-109">La situación descrita en este tutorial consta de los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d18e3-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="d18e3-110">Habilitación de la integración de aplicaciones para TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="d18e3-110">Enabling the application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="d18e3-111">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="d18e3-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="d18e3-112">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="d18e3-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="d18e3-113">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="d18e3-113">Assigning users</span></span>

<span data-ttu-id="d18e3-114">![Escenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="d18e3-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-topdesk---secure"></a><span data-ttu-id="d18e3-115">Habilitación de la integración de aplicaciones para TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="d18e3-115">Enabling the application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="d18e3-116">El objetivo de esta sección es describir cómo habilitar la integración de las aplicaciones para TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="d18e3-116">The objective of this section is to outline how to enable the application integration for TOPdesk - Secure.</span></span>

### <a name="to-enable-the-application-integration-for-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="d18e3-117">Siga estos pasos para habilitar la integración de aplicaciones para TOPdesk - Secure:</span><span class="sxs-lookup"><span data-stu-id="d18e3-117">To enable the application integration for TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="d18e3-118">En el panel de navegación izquierdo del Portal de Azure clásico, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="d18e3-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d18e3-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="d18e3-120">En la lista **Directory**, seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="d18e3-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="d18e3-121">Para abrir la vista de aplicaciones, haga clic en **Applications**, en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="d18e3-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="d18e3-122">![Aplicaciones](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="d18e3-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="d18e3-123">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="d18e3-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="d18e3-124">![Agregar aplicaciones](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="d18e3-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="d18e3-125">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="d18e3-126">![Agregar una aplicación de la galería](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="d18e3-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="d18e3-127">En el **cuadro de búsqueda**, escriba **TOPdesk - Secure**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-127">In the **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="d18e3-128">![Galería de aplicaciones](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="d18e3-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="d18e3-129">En el panel de resultados, seleccione **TOPdesk - Secure** y, luego, haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d18e3-129">In the results pane, select **TOPdesk - Secure**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="d18e3-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span><span class="sxs-lookup"><span data-stu-id="d18e3-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="d18e3-131">Configuración del inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="d18e3-131">Configuring single sign-on</span></span>
<span data-ttu-id="d18e3-132">El objetivo de esta sección es describir cómo se habilita la autenticación de los usuarios en TOPdesk - Secure con su cuenta de Azure AD usando el protocolo SAML basado en la federación.</span><span class="sxs-lookup"><span data-stu-id="d18e3-132">The objective of this section is to outline how to enable users to authenticate to TOPdesk - Secure with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="d18e3-133">La configuración del inicio de sesión único para TOPdesk - Secure requiere cargar un archivo de icono de logotipo.</span><span class="sxs-lookup"><span data-stu-id="d18e3-133">Configuring single sign-on for TOPdesk - Secure requires you to upload a logo icon file.</span></span> <span data-ttu-id="d18e3-134">Para obtener el archivo de icono, póngase en contacto con el equipo de soporte técnico de TOPdesk.</span><span class="sxs-lookup"><span data-stu-id="d18e3-134">To get the icon file, contact the TOPdesk support team.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="d18e3-135">Siga estos pasos para configurar el inicio de sesión único:</span><span class="sxs-lookup"><span data-stu-id="d18e3-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="d18e3-136">Inicie sesión en su sitio de la compañía de **TOPdesk - Secure** como administrador.</span><span class="sxs-lookup"><span data-stu-id="d18e3-136">Sign on to your **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="d18e3-137">En el menú **TOPdesk**, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-137">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="d18e3-138">![Configuración](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="d18e3-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="d18e3-139">Haga clic en **Login Settings**(Configuración de inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="d18e3-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="d18e3-140">![Configuración de inicio de sesión](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Configuración de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="d18e3-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="d18e3-141">Expanda el menú **Login Settings** (Configuración de inicio de sesión) y luego haga clic en **General**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-141">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="d18e3-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="d18e3-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="d18e3-143">En la sección **Secure** (Seguro) de la sección de configuración **SAML login** (Inicio de sesión SAML), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d18e3-143">In the **Secure** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="d18e3-144">![Configuración técnica](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Configuración técnica")</span><span class="sxs-lookup"><span data-stu-id="d18e3-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="d18e3-145">a.</span><span class="sxs-lookup"><span data-stu-id="d18e3-145">a.</span></span> <span data-ttu-id="d18e3-146">Haga clic en **Download** (Descargar) para descargar el archivo de metadatos público y luego guárdelo localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d18e3-146">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="d18e3-147">b.</span><span class="sxs-lookup"><span data-stu-id="d18e3-147">b.</span></span> <span data-ttu-id="d18e3-148">Abra el archivo de metadatos y luego busque el nodo **AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="d18e3-148">Open the metadata file, and then locate the **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="d18e3-149">![Servicio de consumidor de aserciones](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Servicio de consumidor de aserciones")</span><span class="sxs-lookup"><span data-stu-id="d18e3-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="d18e3-150">c.</span><span class="sxs-lookup"><span data-stu-id="d18e3-150">c.</span></span> <span data-ttu-id="d18e3-151">Copie el valor **AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="d18e3-151">Copy the **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="d18e3-152">Necesitará el valor de la sección **Configurar dirección URL de la aplicación** más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d18e3-152">You will need the value in the **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="d18e3-153">En otra ventana del explorador web, inicie sesión en su **Portal de Azure clásico** como administrador.</span><span class="sxs-lookup"><span data-stu-id="d18e3-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="d18e3-154">En el **TOPdesk - Secure** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** para abrir el ** configurar inicio de sesión único ** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d18e3-154">On the **TOPdesk - Secure** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="d18e3-155">![Configurar inicio de sesión único](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="d18e3-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="d18e3-156">En la página **¿Cómo desea que los usuarios inicien sesión en TOPdesk - Secure?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y, después, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-156">On the **How would you like users to sign on to TOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="d18e3-157">![Configurar inicio de sesión único](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="d18e3-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="d18e3-158">En la página **Configurar dirección URL de la aplicación** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d18e3-158">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="d18e3-159">![Configurar dirección URL de la aplicación](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="d18e3-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="d18e3-160">a.</span><span class="sxs-lookup"><span data-stu-id="d18e3-160">a.</span></span> <span data-ttu-id="d18e3-161">En el cuadro de texto **URL de inicio de sesión de TOPdesk - Secure**, escriba la dirección URL que utilizan los usuarios para iniciar sesión en su aplicación TOPdesk - Secure (por ejemplo, "*https://qssolutions.topdesk.net*").</span><span class="sxs-lookup"><span data-stu-id="d18e3-161">In the **TOPdesk - Secure Sign On URL** textbox, type the URL used by your users to sign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="d18e3-162">b.</span><span class="sxs-lookup"><span data-stu-id="d18e3-162">b.</span></span> <span data-ttu-id="d18e3-163">En el cuadro de texto **URL de respuesta de TOPdesk – Secure**, pegue la **dirección URL de AssertionConsumerService de TOPdesk - Public** (por ejemplo, "*https://qssolutions.topdesk.net/tas/public/login/saml*").</span><span class="sxs-lookup"><span data-stu-id="d18e3-163">In the **TOPdesk – Public Reply URL** textbox, paste the **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="d18e3-164">c.</span><span class="sxs-lookup"><span data-stu-id="d18e3-164">c.</span></span> <span data-ttu-id="d18e3-165">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-165">Click **Next**.</span></span>

10. <span data-ttu-id="d18e3-166">En la página **Configurar inicio de sesión único en TOPdesk - Secure**, para descargar su archivo de metadatos, haga clic en **Descargar metadatos** y luego guarde el archivo localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d18e3-166">On the **Configure single sign-on at TOPdesk - Secure** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
    
    <span data-ttu-id="d18e3-167">![Configurar inicio de sesión único](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="d18e3-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="d18e3-168">Lleve a cabo los siguientes pasos para crear un archivo de certificado:</span><span class="sxs-lookup"><span data-stu-id="d18e3-168">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="d18e3-169">![Certificado](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificado")</span><span class="sxs-lookup"><span data-stu-id="d18e3-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="d18e3-170">a.</span><span class="sxs-lookup"><span data-stu-id="d18e3-170">a.</span></span> <span data-ttu-id="d18e3-171">Abra el archivo de metadatos descargado.</span><span class="sxs-lookup"><span data-stu-id="d18e3-171">Open the downloaded metadata file.</span></span>
    <span data-ttu-id="d18e3-172">b.</span><span class="sxs-lookup"><span data-stu-id="d18e3-172">b.</span></span> <span data-ttu-id="d18e3-173">Expanda el nodo **RoleDescriptor** cuyo **xsi:type** es **fed:ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-173">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="d18e3-174">c.</span><span class="sxs-lookup"><span data-stu-id="d18e3-174">c.</span></span> <span data-ttu-id="d18e3-175">Copie el valor del nodo **X509Certificate** .</span><span class="sxs-lookup"><span data-stu-id="d18e3-175">Copy the value of the **X509Certificate** node.</span></span>
    <span data-ttu-id="d18e3-176">d.</span><span class="sxs-lookup"><span data-stu-id="d18e3-176">d.</span></span> <span data-ttu-id="d18e3-177">Guarde el valor de **X509Certificate** copiado localmente en el equipo en un archivo.</span><span class="sxs-lookup"><span data-stu-id="d18e3-177">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="d18e3-178">En el sitio de la compañía de TOPdesk - Secure, en el menú **TOPdesk**, haga clic en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="d18e3-178">On your TOPdesk - Secure company site, in the **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="d18e3-179">![Configuración](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="d18e3-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="d18e3-180">Haga clic en **Login Settings**(Configuración de inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="d18e3-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="d18e3-181">![Configuración de inicio de sesión](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Configuración de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="d18e3-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="d18e3-182">Expanda el menú **Login Settings** (Configuración de inicio de sesión) y luego haga clic en **General**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-182">Expand the **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="d18e3-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="d18e3-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="d18e3-184">En la sección **Public** (Público), haga clic en **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="d18e3-184">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="d18e3-185">![Agregar](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Agregar")</span><span class="sxs-lookup"><span data-stu-id="d18e3-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="d18e3-186">En la página de diálogo del **SAML configuration assistant** (Asistente de configuración de SAML), realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d18e3-186">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="d18e3-187">![Asistente para configuración de SAML](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "Asistente de configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="d18e3-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="d18e3-188">a.</span><span class="sxs-lookup"><span data-stu-id="d18e3-188">a.</span></span> <span data-ttu-id="d18e3-189">Para cargar el archivo de metadatos que ha descargado en **Federation Metadata** (Metadatos de federación), haga clic en **Browse** (Examinar).</span><span class="sxs-lookup"><span data-stu-id="d18e3-189">To upload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="d18e3-190">b.</span><span class="sxs-lookup"><span data-stu-id="d18e3-190">b.</span></span> <span data-ttu-id="d18e3-191">Para cargar el archivo del certificado, en **Certificate (RSA)** (Certificado [RSA]), haga clic en **Browse** (Examinar).</span><span class="sxs-lookup"><span data-stu-id="d18e3-191">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="d18e3-192">c.</span><span class="sxs-lookup"><span data-stu-id="d18e3-192">c.</span></span> <span data-ttu-id="d18e3-193">Para cargar el archivo de logotipo que obtuvo del equipo de soporte técnico de TOPdesk, en **Logo icon** (Icono de logotipo), haga clic en **Browse** (Examinar).</span><span class="sxs-lookup"><span data-stu-id="d18e3-193">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="d18e3-194">d.</span><span class="sxs-lookup"><span data-stu-id="d18e3-194">d.</span></span> <span data-ttu-id="d18e3-195">En el cuadro de texto **User name attribute** (Atributo de nombre de usuario), escriba **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-195">In the **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="d18e3-196">e.</span><span class="sxs-lookup"><span data-stu-id="d18e3-196">e.</span></span> <span data-ttu-id="d18e3-197">En el cuadro de texto **Display name** (Nombre para mostrar), escriba un nombre para su configuración.</span><span class="sxs-lookup"><span data-stu-id="d18e3-197">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="d18e3-198">f.</span><span class="sxs-lookup"><span data-stu-id="d18e3-198">f.</span></span> <span data-ttu-id="d18e3-199">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-199">Click **Save**.</span></span>

17. <span data-ttu-id="d18e3-200">En el Portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único y haga clic en **Completar** para cerrar el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-200">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="d18e3-201">![Configurar inicio de sesión único](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="d18e3-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="d18e3-202">Configuración del aprovisionamiento de usuario</span><span class="sxs-lookup"><span data-stu-id="d18e3-202">Configuring user provisioning</span></span>
<span data-ttu-id="d18e3-203">Para permitir que los usuarios de Azure AD inicien sesión en TOPdesk - Secure, deben aprovisionarse en TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="d18e3-203">In order to enable Azure AD users to log into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="d18e3-204">En el caso de TOPdesk - Secure, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="d18e3-204">In the case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="d18e3-205">Siga estos pasos para configurar el aprovisionamiento de usuario:</span><span class="sxs-lookup"><span data-stu-id="d18e3-205">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="d18e3-206">Inicie sesión en su sitio de la compañía de **TOPdesk - Secure** como administrador.</span><span class="sxs-lookup"><span data-stu-id="d18e3-206">Sign on to your **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="d18e3-207">En el menú de la parte superior, haga clic en **TOPdesk \> New \> Support Files \> Operator** (TOPdesk > Nuevo > Archivos de soporte > Operador).</span><span class="sxs-lookup"><span data-stu-id="d18e3-207">In the menu on the top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="d18e3-208">![Operador](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operador")</span><span class="sxs-lookup"><span data-stu-id="d18e3-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="d18e3-209">En el cuadro de diálogo **Nuevo operador** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d18e3-209">On the **New Operator** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="d18e3-210">![New operador](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "Nuevo operador")</span><span class="sxs-lookup"><span data-stu-id="d18e3-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="d18e3-211">a.</span><span class="sxs-lookup"><span data-stu-id="d18e3-211">a.</span></span> <span data-ttu-id="d18e3-212">Haga clic en la pestaña General.</span><span class="sxs-lookup"><span data-stu-id="d18e3-212">Click the General tab.</span></span>
   
    <span data-ttu-id="d18e3-213">b.</span><span class="sxs-lookup"><span data-stu-id="d18e3-213">b.</span></span> <span data-ttu-id="d18e3-214">En el cuadro de texto **Apellido** de la sección **General**, escriba los apellidos de una cuenta válida de Azure Active Directory que desee aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="d18e3-214">In the **Surname** textbox of the **General** section, type the last name of a valid Azure Active Directory account you want to provision.</span></span>
   
    <span data-ttu-id="d18e3-215">c.</span><span class="sxs-lookup"><span data-stu-id="d18e3-215">c.</span></span> <span data-ttu-id="d18e3-216">Seleccione un **sitio** para la cuenta en la sección **Location** (Ubicación).</span><span class="sxs-lookup"><span data-stu-id="d18e3-216">Select a **Site** for the account in the **Location** section.</span></span>
   
    <span data-ttu-id="d18e3-217">d.</span><span class="sxs-lookup"><span data-stu-id="d18e3-217">d.</span></span> <span data-ttu-id="d18e3-218">En el cuadro de texto **Login Name** (Nombre de inicio de sesión) de la sección **TOPdesk Login** (Inicio de sesión de TOPdesk), escriba el nombre de inicio de sesión del usuario.</span><span class="sxs-lookup"><span data-stu-id="d18e3-218">In the **Login Name** textbox of the **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="d18e3-219">e.</span><span class="sxs-lookup"><span data-stu-id="d18e3-219">e.</span></span> <span data-ttu-id="d18e3-220">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="d18e3-221">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de TOPdesk - Secure ofrecida por TOPdesk - Secure para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="d18e3-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="d18e3-222">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="d18e3-222">Assigning users</span></span>
<span data-ttu-id="d18e3-223">Para probar la configuración, debe conceder acceso a los usuarios de Azure AD a los que quiere permitir el uso de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="d18e3-223">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="d18e3-224">Para asignar usuarios a TOPdesk - Secure, lleve a cabo los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d18e3-224">To assign users to TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="d18e3-225">En el Portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="d18e3-225">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="d18e3-226">En el ** TOPdesk - Secure ** página de integración de aplicaciones, haga clic en **asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d18e3-226">On the **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="d18e3-227">![Asignar usuarios](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="d18e3-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="d18e3-228">Seleccione su usuario de prueba, haga clic en **Asignar** y en **Sí** para confirmar la asignación.</span><span class="sxs-lookup"><span data-stu-id="d18e3-228">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="d18e3-229">![Sí](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="d18e3-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="d18e3-230">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d18e3-230">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="d18e3-231">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d18e3-231">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


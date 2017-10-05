---
title: "Tutorial: Integración de Azure Active Directory con Canvas Lms | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Canvas Lms."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 2212b7a81b66d1afd1aa78d1487b07b6d7b84129
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="5732b-103">Tutorial: integración de Azure Active Directory con Canvas Lms</span><span class="sxs-lookup"><span data-stu-id="5732b-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="5732b-104">En este tutorial, aprenderá a integrar Canvas con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5732b-104">In this tutorial, you learn how to integrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5732b-105">Integrar Canvas con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="5732b-105">Integrating Canvas with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5732b-106">En Azure AD se puede controlar quién tiene acceso a Canvas.</span><span class="sxs-lookup"><span data-stu-id="5732b-106">You can control in Azure AD who has access to Canvas</span></span>
- <span data-ttu-id="5732b-107">Puede permitir que los usuarios inicien sesión automáticamente en Canvas (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5732b-107">You can enable your users to automatically get signed-on to Canvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5732b-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5732b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5732b-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5732b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5732b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5732b-110">Prerequisites</span></span>

<span data-ttu-id="5732b-111">Para configurar la integración de Azure AD con Canvas, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="5732b-111">To configure Azure AD integration with Canvas, you need the following items:</span></span>

- <span data-ttu-id="5732b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5732b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5732b-113">Una suscripción habilitada para el inicio de sesión único en Canvas</span><span class="sxs-lookup"><span data-stu-id="5732b-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5732b-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="5732b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5732b-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="5732b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5732b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5732b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5732b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5732b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5732b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="5732b-118">Scenario description</span></span>
<span data-ttu-id="5732b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="5732b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5732b-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="5732b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5732b-121">Adición de Canvas desde la galería</span><span class="sxs-lookup"><span data-stu-id="5732b-121">Adding Canvas from the gallery</span></span>
2. <span data-ttu-id="5732b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5732b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-the-gallery"></a><span data-ttu-id="5732b-123">Adición de Canvas desde la galería</span><span class="sxs-lookup"><span data-stu-id="5732b-123">Adding Canvas from the gallery</span></span>
<span data-ttu-id="5732b-124">Para configurar la integración de Canvas en Azure AD, deberá agregar Canvas desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="5732b-124">To configure the integration of Canvas into Azure AD, you need to add Canvas from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5732b-125">**Para agregar Canvas desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="5732b-125">**To add Canvas from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5732b-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5732b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5732b-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="5732b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5732b-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5732b-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="5732b-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5732b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="5732b-133">En el cuadro de búsqueda, escriba **Canvas**.</span><span class="sxs-lookup"><span data-stu-id="5732b-133">In the search box, type **Canvas**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="5732b-135">En el panel de resultados, seleccione **Canvas** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5732b-135">In the results panel, select **Canvas**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5732b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5732b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5732b-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Canvas con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5732b-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5732b-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Canvas para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5732b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Canvas is to a user in Azure AD.</span></span> <span data-ttu-id="5732b-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Canvas.</span><span class="sxs-lookup"><span data-stu-id="5732b-140">In other words, a link relationship between an Azure AD user and the related user in Canvas needs to be established.</span></span>

<span data-ttu-id="5732b-141">Para establecer la relación de vínculo, en Canvas, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="5732b-141">In Canvas, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5732b-142">Para configurar y probar el inicio de sesión único de Azure AD con Canvas, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="5732b-142">To configure and test Azure AD single sign-on with Canvas, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5732b-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="5732b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5732b-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5732b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5732b-145">**[Creación de un usuario de prueba de Canvas](#creating-a-canvas-test-user)**: para tener un homólogo de Britta Simon en Canvas que esté vinculado a la representación de Azure AD de usuario.</span><span class="sxs-lookup"><span data-stu-id="5732b-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - to have a counterpart of Britta Simon in Canvas that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5732b-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5732b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5732b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="5732b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5732b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5732b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5732b-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Canvas.</span><span class="sxs-lookup"><span data-stu-id="5732b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="5732b-150">**Para configurar el inicio de sesión único de Azure AD con Canvas, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="5732b-150">**To configure Azure AD single sign-on with Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="5732b-151">En Azure Portal, en la página de integración de la aplicación **Canvas**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="5732b-151">In the Azure portal, on the **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="5732b-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="5732b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="5732b-155">En la sección **Dominio y direcciones URL de Canvas**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5732b-155">On the **Canvas Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="5732b-157">a.</span><span class="sxs-lookup"><span data-stu-id="5732b-157">a.</span></span> <span data-ttu-id="5732b-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenant-name>.instructure.com`.</span><span class="sxs-lookup"><span data-stu-id="5732b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="5732b-159">b.</span><span class="sxs-lookup"><span data-stu-id="5732b-159">b.</span></span> <span data-ttu-id="5732b-160">En el cuadro de texto **Identificador**, escriba el valor con el siguiente patrón: `https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="5732b-160">In the **Identifier** textbox, type the value using the following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5732b-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="5732b-161">These values are not real.</span></span> <span data-ttu-id="5732b-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="5732b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5732b-163">Póngase en contacto con el [equipo de soporte de cliente de Canvas](https://community.canvaslms.com/community/help) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="5732b-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) to get these values.</span></span> 
 
4. <span data-ttu-id="5732b-164">En la sección **Certificado de firma de SAML**, copie el valor de **HUELLA DIGITAL** certificado.</span><span class="sxs-lookup"><span data-stu-id="5732b-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="5732b-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="5732b-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5732b-168">En la sección **Configuración de Canvas**, haga clic en **Configurar Canvas** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="5732b-168">On the **Canvas Configuration** section, click **Configure Canvas** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5732b-169">Copie la **dirección URL cambiada de la contraseña, la dirección URL de cierre de sesión, el identificador de entidad de SAML y la dirección URL del servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="5732b-169">Copy the **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="5732b-171">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Canvas.</span><span class="sxs-lookup"><span data-stu-id="5732b-171">In a different web browser window, log in to your Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="5732b-172">Vaya a **Cursos \> Cuentas administradas \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="5732b-172">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="5732b-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="5732b-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="5732b-174">En el panel de navegación izquierdo, seleccione **Authentication** (Autenticación) y, después, haga clic en **Add New SAML Config** (Agregar nueva configuración de SAML).</span><span class="sxs-lookup"><span data-stu-id="5732b-174">In the navigation pane on the left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="5732b-175">![Autenticación](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Autenticación")</span><span class="sxs-lookup"><span data-stu-id="5732b-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="5732b-176">En la página Curent Integration (integración actual) realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="5732b-176">On the Current Integration page, perform the following steps:</span></span>
   
    <span data-ttu-id="5732b-177">![Integración actual](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Integración actual")</span><span class="sxs-lookup"><span data-stu-id="5732b-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="5732b-178">a.</span><span class="sxs-lookup"><span data-stu-id="5732b-178">a.</span></span> <span data-ttu-id="5732b-179">En el cuadro de texto **IdP Entity ID** (Id. de entidad IdP), pegue el valor de **SAML Entity ID** (Identificador de entidad de SAML) que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5732b-179">In **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5732b-180">b.</span><span class="sxs-lookup"><span data-stu-id="5732b-180">b.</span></span> <span data-ttu-id="5732b-181">En el cuadro de texto **URL de inicio de sesión**, pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5732b-181">In **Log On URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="5732b-182">c.</span><span class="sxs-lookup"><span data-stu-id="5732b-182">c.</span></span> <span data-ttu-id="5732b-183">En el cuadro de texto **URL de cierre de sesión**, pegue el valor de **Sign-Out URL** (Dirección URL de cierre de sesión) que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5732b-183">In **Log Out URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5732b-184">d.</span><span class="sxs-lookup"><span data-stu-id="5732b-184">d.</span></span> <span data-ttu-id="5732b-185">En el cuadro de texto **Change Password Link** (Cambiar vínculo de contraseña), pegue el valor de **Cambiar dirección URL de contraseña** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5732b-185">In **Change Password Link** textbox, paste the value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="5732b-186">e.</span><span class="sxs-lookup"><span data-stu-id="5732b-186">e.</span></span> <span data-ttu-id="5732b-187">En el cuadro de texto **Certificate Fingerprint** (Huella digital de certificado), pegue el valor de **Huella digital** del certificado que haya copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5732b-187">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="5732b-188">f.</span><span class="sxs-lookup"><span data-stu-id="5732b-188">f.</span></span> <span data-ttu-id="5732b-189">En la lista **Atributo de inicio de sesión**, seleccione **NameID**.</span><span class="sxs-lookup"><span data-stu-id="5732b-189">From the **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="5732b-190">g.</span><span class="sxs-lookup"><span data-stu-id="5732b-190">g.</span></span> <span data-ttu-id="5732b-191">En la lista **Formato de identificador**, seleccione **emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="5732b-191">From the **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="5732b-192">h.</span><span class="sxs-lookup"><span data-stu-id="5732b-192">h.</span></span> <span data-ttu-id="5732b-193">Haga clic en **Guardar configuración de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="5732b-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="5732b-194">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5732b-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5732b-195">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="5732b-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5732b-196">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5732b-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5732b-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5732b-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="5732b-198">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5732b-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="5732b-200">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="5732b-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5732b-201">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5732b-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5732b-203">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5732b-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5732b-205">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5732b-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5732b-207">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="5732b-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5732b-209">a.</span><span class="sxs-lookup"><span data-stu-id="5732b-209">a.</span></span> <span data-ttu-id="5732b-210">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5732b-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5732b-211">b.</span><span class="sxs-lookup"><span data-stu-id="5732b-211">b.</span></span> <span data-ttu-id="5732b-212">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5732b-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5732b-213">c.</span><span class="sxs-lookup"><span data-stu-id="5732b-213">c.</span></span> <span data-ttu-id="5732b-214">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="5732b-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5732b-215">d.</span><span class="sxs-lookup"><span data-stu-id="5732b-215">d.</span></span> <span data-ttu-id="5732b-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5732b-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="5732b-217">Creación de un usuario de prueba de Canvas</span><span class="sxs-lookup"><span data-stu-id="5732b-217">Creating a Canvas test user</span></span>

<span data-ttu-id="5732b-218">Para permitir que los usuarios de Azure AD inicien sesión en Canvas, tienen que aprovisionarse en Canvas.</span><span class="sxs-lookup"><span data-stu-id="5732b-218">To enable Azure AD users to log in to Canvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="5732b-219">En el caso de Canvas, el aprovisionamiento de usuario es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="5732b-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="5732b-220">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="5732b-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="5732b-221">Inicie sesión en su inquilino de **Canvas** .</span><span class="sxs-lookup"><span data-stu-id="5732b-221">Log in to your **Canvas** tenant.</span></span>

2. <span data-ttu-id="5732b-222">Vaya a **Cursos \> Cuentas administradas \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="5732b-222">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="5732b-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="5732b-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="5732b-224">Haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5732b-224">Click **Users**.</span></span>
   
   <span data-ttu-id="5732b-225">![Usuarios](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="5732b-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="5732b-226">Haga clic en **Add New User**(Agregar nuevo usuario).</span><span class="sxs-lookup"><span data-stu-id="5732b-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="5732b-227">![Usuarios](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="5732b-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="5732b-228">En la página de diálogo Agregar nuevo usuario, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5732b-228">On the Add a New User dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="5732b-229">![Agregar usuario](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="5732b-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="5732b-230">a.</span><span class="sxs-lookup"><span data-stu-id="5732b-230">a.</span></span> <span data-ttu-id="5732b-231">En el cuadro de texto **Nombre completo**, escriba el nombre de usuario, por ejemplo, **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5732b-231">In the **Full Name** textbox, enter the name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="5732b-232">b.</span><span class="sxs-lookup"><span data-stu-id="5732b-232">b.</span></span> <span data-ttu-id="5732b-233">En el cuadro de texto **E-mail** (Correo electrónico), escriba el correo electrónico del usuario con el siguiente formato **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="5732b-233">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="5732b-234">c.</span><span class="sxs-lookup"><span data-stu-id="5732b-234">c.</span></span> <span data-ttu-id="5732b-235">En el cuadro de texto **Login** (Inicio de sesión), escriba la dirección de correo electrónico de Azure AD del usuario **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="5732b-235">In the **Login** textbox, enter the user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="5732b-236">d.</span><span class="sxs-lookup"><span data-stu-id="5732b-236">d.</span></span> <span data-ttu-id="5732b-237">Seleccione **Email the user about this account creation**(Enviar correo electrónico al usuario sobre la creación de esta cuenta).</span><span class="sxs-lookup"><span data-stu-id="5732b-237">Select **Email the user about this account creation**.</span></span>

   <span data-ttu-id="5732b-238">e.</span><span class="sxs-lookup"><span data-stu-id="5732b-238">e.</span></span> <span data-ttu-id="5732b-239">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="5732b-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="5732b-240">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Canvas ofrecida por Canvas para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="5732b-240">You can use any other Canvas user account creation tools or APIs provided by Canvas to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5732b-241">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5732b-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5732b-242">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Canvas.</span><span class="sxs-lookup"><span data-stu-id="5732b-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Canvas.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="5732b-244">**Para asignar Britta Simon a Canvas, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="5732b-244">**To assign Britta Simon to Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="5732b-245">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5732b-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="5732b-247">En la lista de aplicaciones, seleccione **Canvas**.</span><span class="sxs-lookup"><span data-stu-id="5732b-247">In the applications list, select **Canvas**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="5732b-249">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5732b-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="5732b-251">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5732b-251">Click **Add** button.</span></span> <span data-ttu-id="5732b-252">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5732b-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="5732b-254">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="5732b-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5732b-255">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5732b-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5732b-256">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="5732b-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5732b-257">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="5732b-257">Testing single sign-on</span></span>

<span data-ttu-id="5732b-258">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="5732b-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5732b-259">Al hacer clic en el icono de Canvas en el panel de acceso, debería iniciar sesión automáticamente en su aplicación de Canvas.</span><span class="sxs-lookup"><span data-stu-id="5732b-259">When you click the Canvas tile in the Access Panel, you should get automatically signed-on to your Canvas application.</span></span>
<span data-ttu-id="5732b-260">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5732b-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5732b-261">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="5732b-261">Additional resources</span></span>

* [<span data-ttu-id="5732b-262">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5732b-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5732b-263">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5732b-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png


---
title: "Tutorial: Integración de Azure Active Directory con Aha! | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Aha!."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7723864b2e1ab2d5b69d86f0fa18416b9d3f9aa3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="ac930-104">Tutorial: Integración de Azure Active Directory con Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="ac930-105">En este tutorial, aprenderá a integrar Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-105">In this tutorial, you learn how to integrate Aha!</span></span> <span data-ttu-id="ac930-106">con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ac930-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ac930-107">Integración de Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-107">Integrating Aha!</span></span> <span data-ttu-id="ac930-108">La integración de Aha! con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ac930-108">with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ac930-109">En Azure AD se puede controlar quién tiene acceso a Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-109">You can control in Azure AD who has access to Aha!</span></span>
- <span data-ttu-id="ac930-110">Puede permitir a los usuarios iniciar sesión automáticamente en Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-110">You can enable your users to automatically get signed-on to Aha!</span></span> <span data-ttu-id="ac930-111">(inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac930-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ac930-112">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ac930-112">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ac930-113">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ac930-113">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac930-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ac930-114">Prerequisites</span></span>

<span data-ttu-id="ac930-115">Para configurar la integración de Azure AD con Aha!, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ac930-115">To configure Azure AD integration with Aha!, you need the following items:</span></span>

- <span data-ttu-id="ac930-116">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac930-116">An Azure AD subscription</span></span>
- <span data-ttu-id="ac930-117">Una</span><span class="sxs-lookup"><span data-stu-id="ac930-117">An Aha!</span></span> <span data-ttu-id="ac930-118">suscripción habilitada para inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="ac930-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ac930-119">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ac930-119">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ac930-120">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ac930-120">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ac930-121">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ac930-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ac930-122">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ac930-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ac930-123">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ac930-123">Scenario description</span></span>
<span data-ttu-id="ac930-124">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ac930-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ac930-125">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="ac930-125">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ac930-126">Adición de Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-126">Adding Aha!</span></span> <span data-ttu-id="ac930-127">desde la galería</span><span class="sxs-lookup"><span data-stu-id="ac930-127">from the gallery</span></span>
2. <span data-ttu-id="ac930-128">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac930-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-the-gallery"></a><span data-ttu-id="ac930-129">Adición de Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-129">Adding Aha!</span></span> <span data-ttu-id="ac930-130">desde la galería</span><span class="sxs-lookup"><span data-stu-id="ac930-130">from the gallery</span></span>
<span data-ttu-id="ac930-131">Para configurar la integración de Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-131">To configure the integration of Aha!</span></span> <span data-ttu-id="ac930-132">en Azure AD, tiene que agregar Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-132">into Azure AD, you need to add Aha!</span></span> <span data-ttu-id="ac930-133">desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="ac930-133">from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ac930-134">**Para agregar Aha! desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ac930-134">**To add Aha! from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ac930-135">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ac930-135">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ac930-137">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ac930-137">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ac930-138">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ac930-138">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="ac930-140">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ac930-140">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="ac930-142">En el cuadro de búsqueda, escriba **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="ac930-142">In the search box, type **Aha!**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="ac930-144">En el panel de resultados, seleccione **Aha!** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ac930-144">In the results panel, select **Aha!**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ac930-146">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac930-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ac930-147">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="ac930-148">en función de un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ac930-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ac930-149">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-149">For single sign-on to work, Azure AD needs to know what the counterpart user in Aha!</span></span> <span data-ttu-id="ac930-150">que es un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac930-150">is to a user in Azure AD.</span></span> <span data-ttu-id="ac930-151">Es decir, la relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-151">In other words, a link relationship between an Azure AD user and the related user in Aha!</span></span> <span data-ttu-id="ac930-152">debe establecerse.</span><span class="sxs-lookup"><span data-stu-id="ac930-152">needs to be established.</span></span>

<span data-ttu-id="ac930-153">Para establecer la relación de vínculo, en Aha!, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="ac930-153">In Aha!, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ac930-154">Para configurar y probar el inicio de sesión único de Azure AD con Aha!, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ac930-154">To configure and test Azure AD single sign-on with Aha!, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ac930-155">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="ac930-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ac930-156">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ac930-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ac930-157">**[Creación de un usuario de prueba de Aha!](#creating-an-aha-test-user)** : para tener un equivalente de Britta Simon en Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - to have a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="ac930-158">que esté vinculado a la representación de Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="ac930-158">that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ac930-159">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac930-159">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ac930-160">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ac930-160">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ac930-161">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac930-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ac930-162">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la</span><span class="sxs-lookup"><span data-stu-id="ac930-162">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="ac930-163">aplicación Aha!.</span><span class="sxs-lookup"><span data-stu-id="ac930-163">application.</span></span>

<span data-ttu-id="ac930-164">**Para configurar el inicio de sesión único de Azure AD con Aha!, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ac930-164">**To configure Azure AD single sign-on with Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="ac930-165">En Azure Portal, en la página de integración de aplicaciones **Aha!**,</span><span class="sxs-lookup"><span data-stu-id="ac930-165">In the Azure portal, on the **Aha!**</span></span> <span data-ttu-id="ac930-166">haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ac930-166">application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="ac930-168">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ac930-168">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="ac930-170">En la sección  **Dominio y direcciones URL de Aha!**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ac930-170">On the **Aha! Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="ac930-172">a.</span><span class="sxs-lookup"><span data-stu-id="ac930-172">a.</span></span> <span data-ttu-id="ac930-173">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.aha.io/session/new`.</span><span class="sxs-lookup"><span data-stu-id="ac930-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="ac930-174">b.</span><span class="sxs-lookup"><span data-stu-id="ac930-174">b.</span></span> <span data-ttu-id="ac930-175">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="ac930-175">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ac930-176">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="ac930-176">These values are not real.</span></span> <span data-ttu-id="ac930-177">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ac930-177">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ac930-178">Póngase en contacto con el [equipo de soporte técnico de Aha! ](https://www.aha.io/company/contact) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="ac930-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="ac930-179">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ac930-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="ac930-181">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="ac930-181">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ac930-183">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-183">In a different web browser window, log in to your Aha!</span></span> <span data-ttu-id="ac930-184">como administrador.</span><span class="sxs-lookup"><span data-stu-id="ac930-184">company site as an administrator.</span></span>

7. <span data-ttu-id="ac930-185">En el menú de la parte superior, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="ac930-185">In the menu on the top, click **Settings**.</span></span>

    <span data-ttu-id="ac930-186">![Configuración](./media/active-directory-saas-aha-tutorial/IC798950.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="ac930-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="ac930-187">Haga clic en **Cuenta**.</span><span class="sxs-lookup"><span data-stu-id="ac930-187">Click **Account**.</span></span>
   
    <span data-ttu-id="ac930-188">![Perfil](./media/active-directory-saas-aha-tutorial/IC798951.png "Perfil")</span><span class="sxs-lookup"><span data-stu-id="ac930-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="ac930-189">Haga clic en **Seguridad e inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ac930-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="ac930-190">![Seguridad e inicio de sesión único](./media/active-directory-saas-aha-tutorial/IC798952.png "Seguridad e inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="ac930-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="ac930-191">En la sección **Inicio de sesión único**, en **Proveedor de identidades**, seleccione **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="ac930-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="ac930-192">![Seguridad e inicio de sesión único](./media/active-directory-saas-aha-tutorial/IC798953.png "Seguridad e inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="ac930-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="ac930-193">Siga estos pasos en la página de configuración **Inicio de sesión único** :</span><span class="sxs-lookup"><span data-stu-id="ac930-193">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
    
    <span data-ttu-id="ac930-194">![Inicio de sesión único](./media/active-directory-saas-aha-tutorial/IC798954.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="ac930-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="ac930-195">a.</span><span class="sxs-lookup"><span data-stu-id="ac930-195">a.</span></span> <span data-ttu-id="ac930-196">En el cuadro de texto **Name** (Nombre), escriba el nombre de la configuración.</span><span class="sxs-lookup"><span data-stu-id="ac930-196">In the **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="ac930-197">b.</span><span class="sxs-lookup"><span data-stu-id="ac930-197">b.</span></span> <span data-ttu-id="ac930-198">En **Configurar con**, seleccione **Archivo de metadatos**.</span><span class="sxs-lookup"><span data-stu-id="ac930-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="ac930-199">c.</span><span class="sxs-lookup"><span data-stu-id="ac930-199">c.</span></span> <span data-ttu-id="ac930-200">Para cargar el archivo de metadatos descargado, haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="ac930-200">To upload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="ac930-201">d.</span><span class="sxs-lookup"><span data-stu-id="ac930-201">d.</span></span> <span data-ttu-id="ac930-202">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="ac930-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="ac930-203">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ac930-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ac930-204">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ac930-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ac930-205">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ac930-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ac930-206">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac930-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="ac930-207">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ac930-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="ac930-209">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="ac930-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ac930-210">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ac930-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ac930-212">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ac930-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ac930-214">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ac930-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ac930-216">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="ac930-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ac930-218">a.</span><span class="sxs-lookup"><span data-stu-id="ac930-218">a.</span></span> <span data-ttu-id="ac930-219">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ac930-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ac930-220">b.</span><span class="sxs-lookup"><span data-stu-id="ac930-220">b.</span></span> <span data-ttu-id="ac930-221">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ac930-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ac930-222">c.</span><span class="sxs-lookup"><span data-stu-id="ac930-222">c.</span></span> <span data-ttu-id="ac930-223">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ac930-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ac930-224">d.</span><span class="sxs-lookup"><span data-stu-id="ac930-224">d.</span></span> <span data-ttu-id="ac930-225">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ac930-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="ac930-226">Creación de un</span><span class="sxs-lookup"><span data-stu-id="ac930-226">Creating an Aha!</span></span> <span data-ttu-id="ac930-227">usuario de prueba de Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-227">test user</span></span>

<span data-ttu-id="ac930-228">Para permitir que los usuarios de Azure AD inicien sesión en Aha!, tienen que aprovisionarse en Aha!.</span><span class="sxs-lookup"><span data-stu-id="ac930-228">To enable Azure AD users to log in to Aha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="ac930-229">En el caso de Aha!, el aprovisionamiento es una tarea automatizada.</span><span class="sxs-lookup"><span data-stu-id="ac930-229">In the case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="ac930-230">No hay ningún elemento de acción para usted.</span><span class="sxs-lookup"><span data-stu-id="ac930-230">There is no action item for you.</span></span>

<span data-ttu-id="ac930-231">Los usuarios se crean automáticamente si es necesario durante el primer intento de inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ac930-231">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="ac930-232">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-232">You can use any other Aha!</span></span> <span data-ttu-id="ac930-233">que proporcione Aha!</span><span class="sxs-lookup"><span data-stu-id="ac930-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="ac930-234">para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="ac930-234">to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ac930-235">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac930-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ac930-236">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Aha!.</span><span class="sxs-lookup"><span data-stu-id="ac930-236">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Aha!.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="ac930-238">**Para asignar el usuario Britta Simon a Aha!, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="ac930-238">**To assign Britta Simon to Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="ac930-239">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ac930-239">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ac930-241">En la lista de aplicaciones, seleccione **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="ac930-241">In the applications list, select **Aha!**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="ac930-243">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ac930-243">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="ac930-245">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ac930-245">Click **Add** button.</span></span> <span data-ttu-id="ac930-246">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ac930-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="ac930-248">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="ac930-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ac930-249">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ac930-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ac930-250">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ac930-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ac930-251">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="ac930-251">Testing single sign-on</span></span>

<span data-ttu-id="ac930-252">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ac930-252">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="ac930-253">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ac930-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ac930-254">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ac930-254">Additional resources</span></span>

* [<span data-ttu-id="ac930-255">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac930-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ac930-256">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ac930-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png


---
title: "Tutorial: Integración de Azure Active Directory con BGS Online | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y BGS Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4fd6b29b-1b46-4fd1-9f5e-16b1c9d892cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: d1abd3f8e2980e03fc092613183a261880fbce38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bgs-online"></a><span data-ttu-id="23122-103">Tutorial: Integración de Azure Active Directory con BGS Online</span><span class="sxs-lookup"><span data-stu-id="23122-103">Tutorial: Azure Active Directory integration with BGS Online</span></span>

<span data-ttu-id="23122-104">En este tutorial, obtendrá información sobre cómo integrar BGS Online con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="23122-104">In this tutorial, you learn how to integrate BGS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="23122-105">Integrar BGS Online con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="23122-105">Integrating BGS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="23122-106">Puede controlar en Azure AD quién tiene acceso a BGS Online.</span><span class="sxs-lookup"><span data-stu-id="23122-106">You can control in Azure AD who has access to BGS Online</span></span>
- <span data-ttu-id="23122-107">Puede permitir que los usuarios inicien sesión automáticamente en BGS Online (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23122-107">You can enable your users to automatically get signed-on to BGS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="23122-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="23122-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="23122-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="23122-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23122-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="23122-110">Prerequisites</span></span>

<span data-ttu-id="23122-111">Para configurar la integración de Azure AD con BGS Online, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="23122-111">To configure Azure AD integration with BGS Online, you need the following items:</span></span>

- <span data-ttu-id="23122-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="23122-112">An Azure AD subscription</span></span>
- <span data-ttu-id="23122-113">Una suscripción habilitada para el inicio de sesión único en BGS Online</span><span class="sxs-lookup"><span data-stu-id="23122-113">A BGS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="23122-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="23122-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="23122-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="23122-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="23122-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="23122-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="23122-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="23122-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="23122-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="23122-118">Scenario description</span></span>
<span data-ttu-id="23122-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="23122-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="23122-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="23122-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="23122-121">Adición de BGS Online desde la galería</span><span class="sxs-lookup"><span data-stu-id="23122-121">Adding BGS Online from the gallery</span></span>
2. <span data-ttu-id="23122-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="23122-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bgs-online-from-the-gallery"></a><span data-ttu-id="23122-123">Adición de BGS Online desde la galería</span><span class="sxs-lookup"><span data-stu-id="23122-123">Adding BGS Online from the gallery</span></span>
<span data-ttu-id="23122-124">Para configurar la integración de BGS Online en Azure AD, deberá agregar BGS Online desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="23122-124">To configure the integration of BGS Online into Azure AD, you need to add BGS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="23122-125">**Para agregar BGS Online desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="23122-125">**To add BGS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="23122-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="23122-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="23122-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="23122-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="23122-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="23122-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="23122-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23122-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="23122-133">En el cuadro de búsqueda, escriba **BGS Online**.</span><span class="sxs-lookup"><span data-stu-id="23122-133">In the search box, type **BGS Online**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_search.png)

5. <span data-ttu-id="23122-135">En el panel de resultados, seleccione **BGS Online** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="23122-135">In the results panel, select **BGS Online**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="23122-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="23122-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="23122-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con BGS Online con un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="23122-138">In this section, you configure and test Azure AD single sign-on with BGS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="23122-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de BGS Online para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23122-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BGS Online is to a user in Azure AD.</span></span> <span data-ttu-id="23122-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de BGS Online.</span><span class="sxs-lookup"><span data-stu-id="23122-140">In other words, a link relationship between an Azure AD user and the related user in BGS Online needs to be established.</span></span>

<span data-ttu-id="23122-141">Para establecer la relación de vínculo, en BGS Online, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="23122-141">In BGS Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="23122-142">Para configurar y probar el inicio de sesión único de Azure AD con BGS Online, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="23122-142">To configure and test Azure AD single sign-on with BGS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="23122-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="23122-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="23122-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="23122-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="23122-145">**[Creación de un usuario de prueba de BGS Online](#creating-a-bgs-online-test-user)**: para tener un homólogo de Britta Simon en BGS Online que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23122-145">**[Creating a BGS Online test user](#creating-a-bgs-online-test-user)** - to have a counterpart of Britta Simon in BGS Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="23122-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23122-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="23122-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="23122-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="23122-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="23122-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="23122-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo en la aplicación BGS Online.</span><span class="sxs-lookup"><span data-stu-id="23122-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BGS Online application.</span></span>

<span data-ttu-id="23122-150">**Para configurar el inicio de sesión único de Azure AD con BGS Online, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="23122-150">**To configure Azure AD single sign-on with BGS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="23122-151">En Azure Portal, en la página de integración de la aplicación **BGS Online**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="23122-151">In the Azure portal, on the **BGS Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="23122-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="23122-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_samlbase.png)

3. <span data-ttu-id="23122-155">En la sección **Dominio y direcciones URL de BGS Online**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="23122-155">On the **BGS Online Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_url.png)

    <span data-ttu-id="23122-157">a.</span><span class="sxs-lookup"><span data-stu-id="23122-157">a.</span></span> <span data-ttu-id="23122-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="23122-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="23122-159">En el entorno de producción, use este patrón`https://<company name>.millwardbrown.report`</span><span class="sxs-lookup"><span data-stu-id="23122-159">For production environment, use this pattern `https://<company name>.millwardbrown.report`</span></span> 

    <span data-ttu-id="23122-160">En el entorno de prueba, use este patrón`https://millwardbrown.marketingtracker.nl/mt5/`</span><span class="sxs-lookup"><span data-stu-id="23122-160">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/`</span></span>

    <span data-ttu-id="23122-161">b.</span><span class="sxs-lookup"><span data-stu-id="23122-161">b.</span></span> <span data-ttu-id="23122-162">En el cuadro de texto **URL de respuesta** , escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="23122-162">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    
    <span data-ttu-id="23122-163">En el entorno de producción, use este patrón`https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="23122-163">For production environment, use this pattern `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span></span> 
      
    <span data-ttu-id="23122-164">En el entorno de prueba, use este patrón`https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="23122-164">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="23122-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="23122-165">These values are not real.</span></span> <span data-ttu-id="23122-166">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="23122-166">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="23122-167">Póngase en contacto con el [equipo de soporte técnico de BGS Online](mailTo:bgsdashboardteam@millwardbrown.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="23122-167">Contact [BGS Online support team](mailTo:bgsdashboardteam@millwardbrown.com) to get these values.</span></span>
 

4. <span data-ttu-id="23122-168">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="23122-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_certificate.png) 

5. <span data-ttu-id="23122-170">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="23122-170">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bgsonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="23122-172">En la sección **Configuración de BGS Online**, haga clic en **Configurar BGS Online** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="23122-172">On the **BGS Online Configuration** section, click **Configure BGS Online** to open **Configure sign-on** window.</span></span> <span data-ttu-id="23122-173">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="23122-173">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_configure.png) 

7. <span data-ttu-id="23122-175">Para configurar el inicio de sesión único en **BGS Online**, es preciso enviar los datos descargados de **XML de metadatos**, **SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** al [equipo de soporte técnico de BGS Online](mailto:bgsdashboardteam@millwardbrown.com).</span><span class="sxs-lookup"><span data-stu-id="23122-175">To configure single sign-on on **BGS Online** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com).</span></span> 


> [!TIP]
> <span data-ttu-id="23122-176">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="23122-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="23122-177">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="23122-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="23122-178">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="23122-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="23122-179">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="23122-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="23122-180">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="23122-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="23122-182">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="23122-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="23122-183">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="23122-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="23122-185">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="23122-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="23122-187">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="23122-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="23122-189">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="23122-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="23122-191">a.</span><span class="sxs-lookup"><span data-stu-id="23122-191">a.</span></span> <span data-ttu-id="23122-192">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="23122-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="23122-193">b.</span><span class="sxs-lookup"><span data-stu-id="23122-193">b.</span></span> <span data-ttu-id="23122-194">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="23122-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="23122-195">c.</span><span class="sxs-lookup"><span data-stu-id="23122-195">c.</span></span> <span data-ttu-id="23122-196">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="23122-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="23122-197">d.</span><span class="sxs-lookup"><span data-stu-id="23122-197">d.</span></span> <span data-ttu-id="23122-198">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="23122-198">Click **Create**.</span></span>
 
### <a name="creating-a-bgs-online-test-user"></a><span data-ttu-id="23122-199">Creación de un usuario de prueba de BGS Online</span><span class="sxs-lookup"><span data-stu-id="23122-199">Creating a BGS Online test user</span></span>

<span data-ttu-id="23122-200">En esta sección, creará un usuario llamado Britta Simon en BGS Online.</span><span class="sxs-lookup"><span data-stu-id="23122-200">In this section, you create a user called Britta Simon in BGS Online.</span></span> <span data-ttu-id="23122-201">Trabaje con el [equipo de soporte técnico de BGS Online](mailto:bgsdashboardteam@millwardbrown.com) para agregar los usuarios a la plataforma de BGS Online.</span><span class="sxs-lookup"><span data-stu-id="23122-201">Work with [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com) to add the users in the BGS Online platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="23122-202">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="23122-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="23122-203">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a BGS Online.</span><span class="sxs-lookup"><span data-stu-id="23122-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BGS Online.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="23122-205">**Para asignar a Britta Simon a BGS Online, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="23122-205">**To assign Britta Simon to BGS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="23122-206">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="23122-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="23122-208">En la lista de aplicaciones. seleccione **BGS Online**.</span><span class="sxs-lookup"><span data-stu-id="23122-208">In the applications list, select **BGS Online**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_app.png) 

3. <span data-ttu-id="23122-210">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="23122-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="23122-212">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="23122-212">Click **Add** button.</span></span> <span data-ttu-id="23122-213">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="23122-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="23122-215">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="23122-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="23122-216">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="23122-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="23122-217">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="23122-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="23122-218">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="23122-218">Testing single sign-on</span></span>

<span data-ttu-id="23122-219">En esta sección, probará la configuración de SSO de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="23122-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="23122-220">Al hacer clic en el icono de BGS Online en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación BGS Online.</span><span class="sxs-lookup"><span data-stu-id="23122-220">When you click the BGS Online tile in the Access Panel, you should get automatically signed-on to your BGS Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="23122-221">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="23122-221">Additional resources</span></span>

* [<span data-ttu-id="23122-222">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="23122-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="23122-223">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="23122-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_203.png


---
title: "Tutorial: Integración de Azure Active Directory con QuickHelp | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y QuickHelp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 1c72b0ddee636090129dab7a5c7ec6ffd452434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="8148e-103">Tutorial: Integración de Azure Active Directory con QuickHelp</span><span class="sxs-lookup"><span data-stu-id="8148e-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="8148e-104">En este tutorial, obtendrá información sobre cómo integrar QuickHelp con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8148e-104">In this tutorial, you learn how to integrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8148e-105">Integrar QuickHelp con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8148e-105">Integrating QuickHelp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8148e-106">Puede controlar en Azure AD quién tiene acceso a QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="8148e-106">You can control in Azure AD who has access to QuickHelp</span></span>
- <span data-ttu-id="8148e-107">Puede permitir que los usuarios inicien sesión automáticamente en QuickHelp (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8148e-107">You can enable your users to automatically get signed-on to QuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8148e-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8148e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8148e-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8148e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8148e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8148e-110">Prerequisites</span></span>

<span data-ttu-id="8148e-111">Para configurar la integración de Azure AD con QuickHelp, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8148e-111">To configure Azure AD integration with QuickHelp, you need the following items:</span></span>

- <span data-ttu-id="8148e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8148e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8148e-113">Una suscripción habilitada para el inicio de sesión único en QuickHelp</span><span class="sxs-lookup"><span data-stu-id="8148e-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8148e-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8148e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8148e-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8148e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8148e-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8148e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8148e-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8148e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8148e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8148e-118">Scenario description</span></span>
<span data-ttu-id="8148e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8148e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8148e-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="8148e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8148e-121">Agregar QuickHelp desde la galería</span><span class="sxs-lookup"><span data-stu-id="8148e-121">Adding QuickHelp from the gallery</span></span>
2. <span data-ttu-id="8148e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8148e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-the-gallery"></a><span data-ttu-id="8148e-123">Agregar QuickHelp desde la galería</span><span class="sxs-lookup"><span data-stu-id="8148e-123">Adding QuickHelp from the gallery</span></span>
<span data-ttu-id="8148e-124">Para configurar la integración de QuickHelp en Azure AD, deberá agregar QuickHelp desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="8148e-124">To configure the integration of QuickHelp into Azure AD, you need to add QuickHelp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8148e-125">**Para agregar QuickHelp desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="8148e-125">**To add QuickHelp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8148e-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8148e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8148e-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8148e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8148e-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8148e-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8148e-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8148e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8148e-133">En el cuadro de búsqueda, escriba **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="8148e-133">In the search box, type **QuickHelp**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="8148e-135">En el panel de resultados, seleccione **QuickHelp** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8148e-135">In the results panel, select **QuickHelp**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8148e-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8148e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8148e-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con QuickHelp con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8148e-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8148e-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de QuickHelp para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8148e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp is to a user in Azure AD.</span></span> <span data-ttu-id="8148e-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="8148e-140">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="8148e-141">Para establecer la relación de vínculo, en QuickHelp, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="8148e-141">In QuickHelp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8148e-142">Para configurar y probar el inicio de sesión único de Azure AD con QuickHelp, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8148e-142">To configure and test Azure AD single sign-on with QuickHelp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8148e-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="8148e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8148e-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8148e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8148e-145">**[Creación de un usuario de prueba de QuickHelp](#creating-a-quickhelp-test-user)**: para tener un homólogo de Britta Simon en QuickHelp vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8148e-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - to have a counterpart of Britta Simon in QuickHelp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8148e-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8148e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8148e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8148e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8148e-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8148e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8148e-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="8148e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="8148e-150">**Para configurar el inicio de sesión único de Azure AD con QuickHelp, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="8148e-150">**To configure Azure AD single sign-on with QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="8148e-151">En Azure Portal, en la página de integración de la aplicación **QuickHelp**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8148e-151">In the Azure portal, on the **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8148e-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8148e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="8148e-155">En la sección **Dominio y direcciones URL de QuickHelp**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8148e-155">On the **QuickHelp Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="8148e-157">a.</span><span class="sxs-lookup"><span data-stu-id="8148e-157">a.</span></span> <span data-ttu-id="8148e-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://quickhelp.com/<instancename>/#/Login`.</span><span class="sxs-lookup"><span data-stu-id="8148e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="8148e-159">b.</span><span class="sxs-lookup"><span data-stu-id="8148e-159">b.</span></span> <span data-ttu-id="8148e-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="8148e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8148e-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="8148e-161">These values are not real.</span></span> <span data-ttu-id="8148e-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="8148e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8148e-163">Póngase en contacto con el [equipo de soporte de cliente de QuickHelp](https://support.quickhelp.com/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="8148e-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="8148e-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8148e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="8148e-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8148e-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="8148e-168">Inicie sesión en el sitio de la empresa de QuickHelp como administrador.</span><span class="sxs-lookup"><span data-stu-id="8148e-168">Sign-on to your QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="8148e-169">En el menú de la parte superior, haga clic en **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="8148e-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Configurar inicio de sesión único][21]

8. <span data-ttu-id="8148e-171">En el menú **Administrador de QuickHelp**, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="8148e-171">In the **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Configurar inicio de sesión único][22]

9. <span data-ttu-id="8148e-173">Haga clic en **Configuración de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="8148e-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="8148e-174">En la página **Configuración de autenticación** , realice los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="8148e-174">On the **Authentication Settings** page, perform the following steps</span></span>
   
    ![Configurar inicio de sesión único][23]
   
    <span data-ttu-id="8148e-176">a.</span><span class="sxs-lookup"><span data-stu-id="8148e-176">a.</span></span> <span data-ttu-id="8148e-177">En **Tipo de SSO**, seleccione **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="8148e-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="8148e-178">b.</span><span class="sxs-lookup"><span data-stu-id="8148e-178">b.</span></span> <span data-ttu-id="8148e-179">Para cargar el archivo de metadatos de Azure descargado, haga clic en **Examinar**, vaya hasta el archivo y, luego, haga clic en **Cargar metadatos**.</span><span class="sxs-lookup"><span data-stu-id="8148e-179">To upload your downloaded Azure metadata file, click **Browse**, navigate to the file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="8148e-180">c.</span><span class="sxs-lookup"><span data-stu-id="8148e-180">c.</span></span> <span data-ttu-id="8148e-181">En el cuadro de texto **Correo electrónico**, escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="8148e-181">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="8148e-182">d.</span><span class="sxs-lookup"><span data-stu-id="8148e-182">d.</span></span> <span data-ttu-id="8148e-183">En el cuadro de texto **Nombre**, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="8148e-183">In the **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="8148e-184">e.</span><span class="sxs-lookup"><span data-stu-id="8148e-184">e.</span></span> <span data-ttu-id="8148e-185">En el cuadro de texto **Apellido**, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="8148e-185">In the **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="8148e-186">f.</span><span class="sxs-lookup"><span data-stu-id="8148e-186">f.</span></span> <span data-ttu-id="8148e-187">En la **Barra de acciones**, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="8148e-187">In the **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8148e-188">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8148e-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8148e-189">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="8148e-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8148e-190">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8148e-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8148e-191">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8148e-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="8148e-192">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8148e-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8148e-194">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="8148e-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8148e-195">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8148e-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8148e-197">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8148e-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8148e-199">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8148e-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8148e-201">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="8148e-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8148e-203">a.</span><span class="sxs-lookup"><span data-stu-id="8148e-203">a.</span></span> <span data-ttu-id="8148e-204">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8148e-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8148e-205">b.</span><span class="sxs-lookup"><span data-stu-id="8148e-205">b.</span></span> <span data-ttu-id="8148e-206">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8148e-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8148e-207">c.</span><span class="sxs-lookup"><span data-stu-id="8148e-207">c.</span></span> <span data-ttu-id="8148e-208">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8148e-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8148e-209">d.</span><span class="sxs-lookup"><span data-stu-id="8148e-209">d.</span></span> <span data-ttu-id="8148e-210">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8148e-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="8148e-211">Creación de un usuario de prueba de QuickHelp</span><span class="sxs-lookup"><span data-stu-id="8148e-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="8148e-212">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="8148e-212">The objective of this section is to create a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="8148e-213">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de QuickHelp para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8148e-213">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp to a user in Azure AD is.</span></span> <span data-ttu-id="8148e-214">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="8148e-214">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="8148e-215">QuickHelp admite el aprovisionamiento Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="8148e-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="8148e-216">Esto significa que, si fuera necesario, se creará automáticamente una cuenta de usuario en QuickHelp y la cuenta se vinculará a la cuenta de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8148e-216">This means, if necessary, a user account is automatically created in QuickHelp and the account is linked to the Azure AD account.</span></span>

<span data-ttu-id="8148e-217">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="8148e-217">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8148e-218">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8148e-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8148e-219">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="8148e-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to QuickHelp.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8148e-221">**Para asignar a Britta Simon a QuickHelp, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="8148e-221">**To assign Britta Simon to QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="8148e-222">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8148e-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8148e-224">En la lista de aplicaciones, seleccione **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="8148e-224">In the applications list, select **QuickHelp**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="8148e-226">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8148e-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8148e-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8148e-228">Click **Add** button.</span></span> <span data-ttu-id="8148e-229">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8148e-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8148e-231">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="8148e-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8148e-232">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8148e-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8148e-233">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8148e-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8148e-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="8148e-234">Testing single sign-on</span></span>

<span data-ttu-id="8148e-235">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8148e-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="8148e-236">Al hacer clic en el icono de QuickHelp en el panel de acceso, debería iniciar sesión automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8148e-236">When you click the QuickHelp tile in the Access Panel, you should get automatically signed-on to your QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8148e-237">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8148e-237">Additional resources</span></span>

* [<span data-ttu-id="8148e-238">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8148e-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8148e-239">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8148e-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png

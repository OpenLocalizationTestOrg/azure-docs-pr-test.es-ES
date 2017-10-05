---
title: "Tutorial: Integración de Azure Active Directory con Oneteam | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Oneteam."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2e94916c-64ae-4e1a-a8b5-bc6ef7d28c29
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: c4381ca3166bd75bda1179b9a67b2224ba58ae68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oneteam"></a><span data-ttu-id="26db2-103">Tutorial: Integración de Azure Active Directory con Oneteam</span><span class="sxs-lookup"><span data-stu-id="26db2-103">Tutorial: Azure Active Directory integration with Oneteam</span></span>

<span data-ttu-id="26db2-104">En este tutorial, obtendrá información sobre cómo integrar Oneteam con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26db2-104">In this tutorial, you learn how to integrate Oneteam with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="26db2-105">La integración de Oneteam con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="26db2-105">Integrating Oneteam with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="26db2-106">Puede controlar en Azure AD quién tiene acceso a Oneteam.</span><span class="sxs-lookup"><span data-stu-id="26db2-106">You can control in Azure AD who has access to Oneteam</span></span>
- <span data-ttu-id="26db2-107">Puede permitir que los usuarios inicien sesión automáticamente en Oneteam (inicio de sesión único) con las cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26db2-107">You can enable your users to automatically get signed-on to Oneteam (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="26db2-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="26db2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="26db2-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="26db2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26db2-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="26db2-110">Prerequisites</span></span>

<span data-ttu-id="26db2-111">Para configurar la integración de Azure AD con Oneteam, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="26db2-111">To configure Azure AD integration with Oneteam, you need the following items:</span></span>

- <span data-ttu-id="26db2-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="26db2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="26db2-113">Una suscripción habilitada para inicio de sesión único en Oneteam</span><span class="sxs-lookup"><span data-stu-id="26db2-113">A Oneteam single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="26db2-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="26db2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="26db2-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="26db2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="26db2-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="26db2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="26db2-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26db2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="26db2-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="26db2-118">Scenario description</span></span>
<span data-ttu-id="26db2-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="26db2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="26db2-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="26db2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="26db2-121">Agregar Oneteam desde la galería</span><span class="sxs-lookup"><span data-stu-id="26db2-121">Adding Oneteam from the gallery</span></span>
2. <span data-ttu-id="26db2-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="26db2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oneteam-from-the-gallery"></a><span data-ttu-id="26db2-123">Agregar Oneteam desde la galería</span><span class="sxs-lookup"><span data-stu-id="26db2-123">Adding Oneteam from the gallery</span></span>
<span data-ttu-id="26db2-124">Para configurar la integración de Oneteam en Azure AD, debe agregar Oneteam desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="26db2-124">To configure the integration of Oneteam into Azure AD, you need to add Oneteam from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="26db2-125">**Para agregar Oneteam desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="26db2-125">**To add Oneteam from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="26db2-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="26db2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="26db2-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="26db2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="26db2-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="26db2-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="26db2-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26db2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="26db2-133">En el cuadro de búsqueda, escriba **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="26db2-133">In the search box, type **Oneteam**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_search.png)

5. <span data-ttu-id="26db2-135">En el panel de resultados, seleccione **Oneteam** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="26db2-135">In the results panel, select **Oneteam**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="26db2-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="26db2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="26db2-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Oneteam con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="26db2-138">In this section, you configure and test Azure AD single sign-on with Oneteam based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="26db2-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Oneteam para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26db2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Oneteam is to a user in Azure AD.</span></span> <span data-ttu-id="26db2-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Oneteam.</span><span class="sxs-lookup"><span data-stu-id="26db2-140">In other words, a link relationship between an Azure AD user and the related user in Oneteam needs to be established.</span></span>

<span data-ttu-id="26db2-141">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de Oneteam.</span><span class="sxs-lookup"><span data-stu-id="26db2-141">In Oneteam, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="26db2-142">Para configurar y probar el inicio de sesión único de Azure AD con Oneteam, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="26db2-142">To configure and test Azure AD single sign-on with Oneteam, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="26db2-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="26db2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="26db2-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26db2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="26db2-145">**[Creación de un usuario de prueba de Oneteam](#creating-a-oneteam-test-user)**: el objetivo es tener un homólogo de Britta Simon en Oneteam que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26db2-145">**[Creating a Oneteam test user](#creating-a-oneteam-test-user)** - to have a counterpart of Britta Simon in Oneteam that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="26db2-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26db2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="26db2-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="26db2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="26db2-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="26db2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="26db2-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Oneteam.</span><span class="sxs-lookup"><span data-stu-id="26db2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Oneteam application.</span></span>

<span data-ttu-id="26db2-150">**Para configurar el inicio de sesión único de Azure AD con Oneteam, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="26db2-150">**To configure Azure AD single sign-on with Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="26db2-151">En la página de integración de la aplicación **Oneteam** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="26db2-151">In the Azure portal, on the **Oneteam** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="26db2-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="26db2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_samlbase.png)

3. <span data-ttu-id="26db2-155">Vaya a la sección **Dominio y direcciones URL de Oneteam**, si quiere configurar la aplicación en modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="26db2-155">On the **Oneteam Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url.png)

    <span data-ttu-id="26db2-157">a.</span><span class="sxs-lookup"><span data-stu-id="26db2-157">a.</span></span> <span data-ttu-id="26db2-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://api.one-team.io/teams/<team name>`</span><span class="sxs-lookup"><span data-stu-id="26db2-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>`</span></span>

    <span data-ttu-id="26db2-159">b.</span><span class="sxs-lookup"><span data-stu-id="26db2-159">b.</span></span> <span data-ttu-id="26db2-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://api.one-team.io/teams/<team name>/auth/saml/callback`.</span><span class="sxs-lookup"><span data-stu-id="26db2-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/callback`</span></span>

4. <span data-ttu-id="26db2-161">Active **Mostrar configuración avanzada de URL**, si desea volver a configurar la aplicación en modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="26db2-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url1.png)

    <span data-ttu-id="26db2-163">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<team name>.one-team.io/`.</span><span class="sxs-lookup"><span data-stu-id="26db2-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<team name>.one-team.io/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="26db2-164">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="26db2-164">These values are not real.</span></span> <span data-ttu-id="26db2-165">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="26db2-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="26db2-166">Póngase en contacto con el [equipo de soporte de cliente de Oneteam](https://support.one-team.com/hc/requests/new) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="26db2-166">Contact [Oneteam Client support team](https://support.one-team.com/hc/requests/new) to get these values.</span></span> 



5. <span data-ttu-id="26db2-167">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="26db2-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_certificate.png) 

6. <span data-ttu-id="26db2-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="26db2-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-oneteam-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="26db2-171">Para configurar el inicio de sesión único en la aplicación, puede presentar una incidencia de soporte técnico al [equipo de soporte técnico de Oneteam](https://support.one-team.com/hc/requests/new) y proporcionarle los **metadatos** descargados.</span><span class="sxs-lookup"><span data-stu-id="26db2-171">To get SSO configured for your application, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new) and provide them the downloaded **Metadata**.</span></span> 

> [!TIP]
> <span data-ttu-id="26db2-172">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="26db2-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="26db2-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="26db2-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="26db2-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="26db2-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="26db2-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="26db2-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="26db2-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="26db2-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="26db2-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="26db2-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="26db2-179">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="26db2-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="26db2-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="26db2-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="26db2-183">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26db2-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="26db2-185">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="26db2-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="26db2-187">a.</span><span class="sxs-lookup"><span data-stu-id="26db2-187">a.</span></span> <span data-ttu-id="26db2-188">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="26db2-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="26db2-189">b.</span><span class="sxs-lookup"><span data-stu-id="26db2-189">b.</span></span> <span data-ttu-id="26db2-190">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26db2-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="26db2-191">c.</span><span class="sxs-lookup"><span data-stu-id="26db2-191">c.</span></span> <span data-ttu-id="26db2-192">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="26db2-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="26db2-193">d.</span><span class="sxs-lookup"><span data-stu-id="26db2-193">d.</span></span> <span data-ttu-id="26db2-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="26db2-194">Click **Create**.</span></span>
 
### <a name="creating-a-oneteam-test-user"></a><span data-ttu-id="26db2-195">Creación de un usuario de prueba de Oneteam</span><span class="sxs-lookup"><span data-stu-id="26db2-195">Creating a Oneteam test user</span></span>

<span data-ttu-id="26db2-196">El objetivo de esta sección es crear un usuario llamado Britta Simon en Oneteam.</span><span class="sxs-lookup"><span data-stu-id="26db2-196">The objective of this section is to create a user called Britta Simon in Oneteam.</span></span> <span data-ttu-id="26db2-197">Oneteam admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="26db2-197">Oneteam supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="26db2-198">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="26db2-198">There is no action item for you in this section.</span></span> <span data-ttu-id="26db2-199">Al intentar acceder a Oneteam, se creará un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="26db2-199">A new user will be created during an attempt to access Oneteam, if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="26db2-200">Si tiene que crear manualmente un usuario, puede presentar la incidencia de soporte técnico al [equipo de soporte técnico de Oneteam](https://support.one-team.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="26db2-200">If you need to create an user manually, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="26db2-201">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="26db2-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="26db2-202">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Oneteam.</span><span class="sxs-lookup"><span data-stu-id="26db2-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Oneteam.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="26db2-204">**Para asignar a Britta Simon a Oneteam, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="26db2-204">**To assign Britta Simon to Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="26db2-205">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="26db2-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="26db2-207">En la lista de aplicaciones, seleccione **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="26db2-207">In the applications list, select **Oneteam**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_app.png) 

3. <span data-ttu-id="26db2-209">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="26db2-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="26db2-211">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="26db2-211">Click **Add** button.</span></span> <span data-ttu-id="26db2-212">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="26db2-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="26db2-214">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="26db2-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="26db2-215">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="26db2-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="26db2-216">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="26db2-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="26db2-217">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="26db2-217">Testing single sign-on</span></span>

<span data-ttu-id="26db2-218">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="26db2-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="26db2-219">Al hacer clic en el icono de Oneteam en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Oneteam.</span><span class="sxs-lookup"><span data-stu-id="26db2-219">When you click the Oneteam tile in the Access Panel, you should get automatically signed-on to your Oneteam application.</span></span>
<span data-ttu-id="26db2-220">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="26db2-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="26db2-221">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="26db2-221">Additional resources</span></span>

* [<span data-ttu-id="26db2-222">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26db2-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="26db2-223">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="26db2-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_203.png


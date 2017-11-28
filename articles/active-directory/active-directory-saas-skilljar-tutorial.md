---
title: "Tutorial: Integración de Azure Active Directory con Skilljar | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Skilljar."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c572f556-98a3-48e6-8e4c-e634b7a2ba70
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: d5238a0471b6ae4b367ca5c1ed5e1f273a0c476b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skilljar"></a><span data-ttu-id="8552f-103">Tutorial: Integración de Azure Active Directory con Skilljar</span><span class="sxs-lookup"><span data-stu-id="8552f-103">Tutorial: Azure Active Directory integration with Skilljar</span></span>

<span data-ttu-id="8552f-104">En este tutorial, aprenderá cómo integrar Skilljar con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8552f-104">In this tutorial, you learn how to integrate Skilljar with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8552f-105">Integrar Skilljar con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8552f-105">Integrating Skilljar with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8552f-106">Puede controlar en Azure AD quién tiene acceso a Skilljar.</span><span class="sxs-lookup"><span data-stu-id="8552f-106">You can control in Azure AD who has access to Skilljar</span></span>
- <span data-ttu-id="8552f-107">Puede permitir que los usuarios inicien sesión automáticamente en Skilljar (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8552f-107">You can enable your users to automatically get signed-on to Skilljar (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8552f-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8552f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8552f-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8552f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8552f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8552f-110">Prerequisites</span></span>

<span data-ttu-id="8552f-111">Para configurar la integración de Azure AD con Skilljar, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8552f-111">To configure Azure AD integration with Skilljar, you need the following items:</span></span>

- <span data-ttu-id="8552f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8552f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8552f-113">Una suscripción habilitada para el inicio de sesión único en Skilljar</span><span class="sxs-lookup"><span data-stu-id="8552f-113">A Skilljar single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8552f-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8552f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8552f-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8552f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8552f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8552f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8552f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8552f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8552f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8552f-118">Scenario description</span></span>
<span data-ttu-id="8552f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8552f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8552f-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="8552f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8552f-121">Adición de Skilljar desde la galería</span><span class="sxs-lookup"><span data-stu-id="8552f-121">Adding Skilljar from the gallery</span></span>
2. <span data-ttu-id="8552f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8552f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skilljar-from-the-gallery"></a><span data-ttu-id="8552f-123">Adición de Skilljar desde la galería</span><span class="sxs-lookup"><span data-stu-id="8552f-123">Adding Skilljar from the gallery</span></span>
<span data-ttu-id="8552f-124">Para configurar la integración de Skilljar en Azure AD, es preciso agregar Skilljar desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="8552f-124">To configure the integration of Skilljar into Azure AD, you need to add Skilljar from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8552f-125">**Para agregar Skilljar desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="8552f-125">**To add Skilljar from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8552f-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8552f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8552f-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8552f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8552f-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8552f-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8552f-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8552f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8552f-133">En el cuadro de búsqueda, escriba **Skilljar**.</span><span class="sxs-lookup"><span data-stu-id="8552f-133">In the search box, type **Skilljar**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_search.png)

5. <span data-ttu-id="8552f-135">En el panel de resultados, seleccione **Skilljar** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8552f-135">In the results panel, select **Skilljar**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8552f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8552f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8552f-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Skilljar con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8552f-138">In this section, you configure and test Azure AD single sign-on with Skilljar based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8552f-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Skilljar para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8552f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Skilljar is to a user in Azure AD.</span></span> <span data-ttu-id="8552f-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Skilljar.</span><span class="sxs-lookup"><span data-stu-id="8552f-140">In other words, a link relationship between an Azure AD user and the related user in Skilljar needs to be established.</span></span>

<span data-ttu-id="8552f-141">Para establecer la relación de vínculo, en Skilljar, asigne el valor del **nombre de usuario** en Azure AD como valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="8552f-141">In Skilljar, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8552f-142">Para configurar y probar el inicio de sesión único de Azure AD con Skilljar, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8552f-142">To configure and test Azure AD single sign-on with Skilljar, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8552f-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="8552f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8552f-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8552f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8552f-145">**[Crear un usuario de prueba Skilljar](#creating-a-skilljar-test-user)**: para tener un homólogo de Britta Simon en Skilljar que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8552f-145">**[Creating a Skilljar test user](#creating-a-skilljar-test-user)** - to have a counterpart of Britta Simon in Skilljar that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8552f-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8552f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8552f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8552f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8552f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8552f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8552f-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Skilljar.</span><span class="sxs-lookup"><span data-stu-id="8552f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skilljar application.</span></span>

<span data-ttu-id="8552f-150">**Para configurar el inicio de sesión único de Azure AD con Skilljar, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="8552f-150">**To configure Azure AD single sign-on with Skilljar, perform the following steps:**</span></span>

1. <span data-ttu-id="8552f-151">En Azure Portal, en la página de integración de la aplicación **Skilljar**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8552f-151">In the Azure portal, on the **Skilljar** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8552f-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8552f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_samlbase.png)

3. <span data-ttu-id="8552f-155">En la sección **Dominio y direcciones URL de Skilljar**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8552f-155">On the **Skilljar Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_url.png)

    <span data-ttu-id="8552f-157">a.</span><span class="sxs-lookup"><span data-stu-id="8552f-157">a.</span></span> <span data-ttu-id="8552f-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.skilljar.com/`.</span><span class="sxs-lookup"><span data-stu-id="8552f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.skilljar.com/`</span></span>

    <span data-ttu-id="8552f-159">b.</span><span class="sxs-lookup"><span data-stu-id="8552f-159">b.</span></span> <span data-ttu-id="8552f-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.skilljar.com/`</span><span class="sxs-lookup"><span data-stu-id="8552f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.skilljar.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8552f-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="8552f-161">These values are not real.</span></span> <span data-ttu-id="8552f-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="8552f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8552f-163">Póngase en contacto con el [equipo de soporte técnico de Skilljar](http://support.skilljar.com/hc/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="8552f-163">Contact [Skilljar Client support team](http://support.skilljar.com/hc/) to get these values.</span></span> 
 
4. <span data-ttu-id="8552f-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8552f-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_certificate.png) 

5. <span data-ttu-id="8552f-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8552f-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skilljar-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8552f-168">Para configurar el inicio de sesión único en **Skilljar**, hay que enviar el **XML de metadatos** descargado y el **valor de formato de identificador de nombre urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress** al [equipo de soporte técnico de Skilljar](http://support.skilljar.com/hc/).</span><span class="sxs-lookup"><span data-stu-id="8552f-168">To configure single sign-on on **Skilljar** side, you need to send the downloaded **Metadata XML**, and **Name Identifier Format Value - urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress** to [Skilljar support team](http://support.skilljar.com/hc/).</span></span> <span data-ttu-id="8552f-169">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="8552f-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8552f-170">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8552f-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8552f-171">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="8552f-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8552f-172">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8552f-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8552f-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8552f-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="8552f-174">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8552f-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8552f-176">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="8552f-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8552f-177">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8552f-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8552f-179">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8552f-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8552f-181">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8552f-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8552f-183">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="8552f-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skilljar-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8552f-185">a.</span><span class="sxs-lookup"><span data-stu-id="8552f-185">a.</span></span> <span data-ttu-id="8552f-186">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8552f-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8552f-187">b.</span><span class="sxs-lookup"><span data-stu-id="8552f-187">b.</span></span> <span data-ttu-id="8552f-188">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8552f-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8552f-189">c.</span><span class="sxs-lookup"><span data-stu-id="8552f-189">c.</span></span> <span data-ttu-id="8552f-190">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8552f-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8552f-191">d.</span><span class="sxs-lookup"><span data-stu-id="8552f-191">d.</span></span> <span data-ttu-id="8552f-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8552f-192">Click **Create**.</span></span>
 
### <a name="creating-a-skilljar-test-user"></a><span data-ttu-id="8552f-193">Crear un usuario de prueba Skilljar</span><span class="sxs-lookup"><span data-stu-id="8552f-193">Creating a Skilljar test user</span></span>

<span data-ttu-id="8552f-194">El objetivo de esta sección es crear un usuario llamado Britta Simon en Skilljar.</span><span class="sxs-lookup"><span data-stu-id="8552f-194">The objective of this section is to create a user called Britta Simon in Skilljar.</span></span> <span data-ttu-id="8552f-195">Skilljar admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8552f-195">Skilljar supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="8552f-196">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="8552f-196">There is no action item for you in this section.</span></span> <span data-ttu-id="8552f-197">Durante un intento de obtener acceso a Skilljar se creará un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="8552f-197">A new user is created during an attempt to access Skilljar if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="8552f-198">Si necesita crear manualmente un usuario, es preciso que se ponga contacto con el [equipo de soporte técnico de Skilljar](http://support.skilljar.com/hc/).</span><span class="sxs-lookup"><span data-stu-id="8552f-198">If you need to create a user manually, you need to contact the [Skilljar support team](http://support.skilljar.com/hc/).</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8552f-199">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8552f-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8552f-200">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Skilljar.</span><span class="sxs-lookup"><span data-stu-id="8552f-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skilljar.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8552f-202">**Para asignar a Britta Simon a Skilljar, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="8552f-202">**To assign Britta Simon to Skilljar, perform the following steps:**</span></span>

1. <span data-ttu-id="8552f-203">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8552f-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8552f-205">En la lista de aplicaciones, seleccione **Skilljar**.</span><span class="sxs-lookup"><span data-stu-id="8552f-205">In the applications list, select **Skilljar**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skilljar-tutorial/tutorial_skilljar_app.png) 

3. <span data-ttu-id="8552f-207">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8552f-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8552f-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8552f-209">Click **Add** button.</span></span> <span data-ttu-id="8552f-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8552f-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8552f-212">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="8552f-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8552f-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8552f-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8552f-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8552f-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8552f-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="8552f-215">Testing single sign-on</span></span>

<span data-ttu-id="8552f-216">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8552f-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="8552f-217">Al hacer clic en el icono de Skilljar en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Skilljar.</span><span class="sxs-lookup"><span data-stu-id="8552f-217">When you click the Skilljar tile in the Access Panel, you should get automatically signed-on to your Skilljar application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8552f-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8552f-218">Additional resources</span></span>

* [<span data-ttu-id="8552f-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8552f-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8552f-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8552f-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skilljar-tutorial/tutorial_general_203.png


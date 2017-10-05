---
title: "Tutorial: integración de Azure Active Directory con Brightspace by Desire2Learn | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Brightspace by Desire2Learn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2d3065b-1f6c-4c45-af78-0d5da3266999
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 7076b476ba71c5d94ae4728e5f6032b0d7e047ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-brightspace-by-desire2learn"></a><span data-ttu-id="dc3ec-103">Tutorial: Integración de Azure Active Directory con Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="dc3ec-103">Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn</span></span>

<span data-ttu-id="dc3ec-104">En este tutorial, obtendrá información sobre cómo integrar Brightspace by Desire2Learn con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc3ec-104">In this tutorial, you learn how to integrate Brightspace by Desire2Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc3ec-105">La integración de Brightspace by Desire2Learn con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="dc3ec-105">Integrating Brightspace by Desire2Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dc3ec-106">En Azure AD puede controlar quién tiene acceso a Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="dc3ec-106">You can control in Azure AD who has access to Brightspace by Desire2Learn</span></span>
- <span data-ttu-id="dc3ec-107">Puede permitir que los usuarios inicien sesión automáticamente en Brightspace by Desire2Learn (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc3ec-107">You can enable your users to automatically get signed-on to Brightspace by Desire2Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dc3ec-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dc3ec-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dc3ec-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc3ec-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dc3ec-110">Prerequisites</span></span>

<span data-ttu-id="dc3ec-111">Para configurar la integración de Azure AD con Brightspace by Desire2Learn, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="dc3ec-111">To configure Azure AD integration with Brightspace by Desire2Learn, you need the following items:</span></span>

- <span data-ttu-id="dc3ec-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc3ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc3ec-113">Una suscripción habilitada para inicio de sesión único de Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="dc3ec-113">A Brightspace by Desire2Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc3ec-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dc3ec-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="dc3ec-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dc3ec-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dc3ec-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc3ec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc3ec-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="dc3ec-118">Scenario description</span></span>
<span data-ttu-id="dc3ec-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc3ec-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="dc3ec-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc3ec-121">Incorporación de Brightspace by Desire2Learn desde la galería</span><span class="sxs-lookup"><span data-stu-id="dc3ec-121">Adding Brightspace by Desire2Learn from the gallery</span></span>
2. <span data-ttu-id="dc3ec-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc3ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-brightspace-by-desire2learn-from-the-gallery"></a><span data-ttu-id="dc3ec-123">Incorporación de Brightspace by Desire2Learn desde la galería</span><span class="sxs-lookup"><span data-stu-id="dc3ec-123">Adding Brightspace by Desire2Learn from the gallery</span></span>
<span data-ttu-id="dc3ec-124">Para configurar la integración de Brightspace by Desire2Learn en Azure AD, deberá agregar Brightspace by Desire2Learn desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-124">To configure the integration of Brightspace by Desire2Learn into Azure AD, you need to add Brightspace by Desire2Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dc3ec-125">**Para agregar Brightspace by Desire2Learn desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="dc3ec-125">**To add Brightspace by Desire2Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dc3ec-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dc3ec-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dc3ec-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="dc3ec-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="dc3ec-133">En el cuadro de búsqueda, escriba **Brightspace by Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-133">In the search box, type **Brightspace by Desire2Learn**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_search.png)

5. <span data-ttu-id="dc3ec-135">En el panel de resultados, seleccione **Brightspace by Desire2Learn** y, luego, haga clic en **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-135">In the results panel, select **Brightspace by Desire2Learn**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dc3ec-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc3ec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dc3ec-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Brightspace by Desire2Learn con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dc3ec-138">In this section, you configure and test Azure AD single sign-on with Brightspace by Desire2Learn based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dc3ec-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Brightspace by Desire2Learn para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Brightspace by Desire2Learn is to a user in Azure AD.</span></span> <span data-ttu-id="dc3ec-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-140">In other words, a link relationship between an Azure AD user and the related user in Brightspace by Desire2Learn needs to be established.</span></span>

<span data-ttu-id="dc3ec-141">Para establecer la relación de vínculo, en Brightspace by Desire2Learn, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-141">In Brightspace by Desire2Learn, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dc3ec-142">Para configurar y probar el inicio de sesión único de Azure AD con Brightspace by Desire2Learn, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="dc3ec-142">To configure and test Azure AD single sign-on with Brightspace by Desire2Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dc3ec-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dc3ec-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dc3ec-145">**[Creación de un usuario de prueba de Brightspace by Desire2Learn](#creating-a-brightspace-by-desire2learn-test-user)**: para tener un homólogo de Britta Simon en Brightspace by Desire2Learn que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-145">**[Creating a Brightspace by Desire2Learn test user](#creating-a-brightspace-by-desire2learn-test-user)** - to have a counterpart of Britta Simon in Brightspace by Desire2Learn that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dc3ec-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dc3ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dc3ec-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc3ec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dc3ec-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Brightspace by Desire2Learn application.</span></span>

<span data-ttu-id="dc3ec-150">**Para configurar el inicio de sesión único de Azure AD con Brightspace by Desire2Learn, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="dc3ec-150">**To configure Azure AD single sign-on with Brightspace by Desire2Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="dc3ec-151">En Azure Portal, en la página de integración de la aplicación **Brightspace by Desire2Learn**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-151">In the Azure portal, on the **Brightspace by Desire2Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="dc3ec-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_samlbase.png)

3. <span data-ttu-id="dc3ec-155">En la sección **Dominio y direcciones URL de Brightspace by Desire2Learn**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="dc3ec-155">On the **Brightspace by Desire2Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_url.png)

    <span data-ttu-id="dc3ec-157">a.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-157">a.</span></span> <span data-ttu-id="dc3ec-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="dc3ec-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.tenants.brightspace.com/samlLogin`|
    | `https://<companyname>.desire2learn.com/shibboleth-sp`|

    <span data-ttu-id="dc3ec-159">b.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-159">b.</span></span> <span data-ttu-id="dc3ec-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dc3ec-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-161">These values are not real.</span></span> <span data-ttu-id="dc3ec-162">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="dc3ec-163">Póngase en contacto con el [equipo de soporte técnico de Brightspace by Desire2Learn](https://www.d2l.com/contact/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-163">Contact [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/) to get these values.</span></span>
 


4. <span data-ttu-id="dc3ec-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_certificate.png) 

5. <span data-ttu-id="dc3ec-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="dc3ec-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dc3ec-168">Para configurar el inicio de sesión único en **Brightspace by Desire2Learn**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Brightspace by Desire2Learn](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="dc3ec-168">To configure single sign-on on **Brightspace by Desire2Learn** side, you need to send the downloaded **Metadata XML** to [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="dc3ec-169">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dc3ec-170">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dc3ec-171">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dc3ec-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dc3ec-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc3ec-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="dc3ec-173">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dc3ec-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="dc3ec-175">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="dc3ec-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dc3ec-176">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dc3ec-178">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dc3ec-180">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dc3ec-182">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="dc3ec-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dc3ec-184">a.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-184">a.</span></span> <span data-ttu-id="dc3ec-185">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dc3ec-186">b.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-186">b.</span></span> <span data-ttu-id="dc3ec-187">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dc3ec-188">c.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-188">c.</span></span> <span data-ttu-id="dc3ec-189">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dc3ec-190">d.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-190">d.</span></span> <span data-ttu-id="dc3ec-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-191">Click **Create**.</span></span>
 
### <a name="creating-a-brightspace-by-desire2learn-test-user"></a><span data-ttu-id="dc3ec-192">Creación de un usuario de prueba de Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="dc3ec-192">Creating a Brightspace by Desire2Learn test user</span></span>

<span data-ttu-id="dc3ec-193">Para permitir que los usuarios de Azure AD inicien sesión en Brightspace by Desire2Learn, tienen que aprovisionarse en Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-193">In order to enable Azure AD users to log into Brightspace by Desire2Learn, they must be provisioned into Brightspace by Desire2Learn.</span></span>  

<span data-ttu-id="dc3ec-194">En el caso de Brightspace by Desire2Learn, las cuentas de usuario tiene que crearlas el [equipo de soporte técnico de Brightspace by Desire2Learn](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="dc3ec-194">In the case of Brightspace by Desire2Learn, the user accounts need to be created by your [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

>[!NOTE]
><span data-ttu-id="dc3ec-195">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Brightspace by Desire2Learn que proporcione Brightspace by Desire2Learn para aprovisionar cuentas de usuario de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-195">You can use any other Brightspace by Desire2Learn user account creation tools or APIs provided by Brightspace by Desire2Learn to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dc3ec-196">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc3ec-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dc3ec-197">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Brightspace by Desire2Learn.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="dc3ec-199">**Para asignar a Britta Simon a Brightspace by Desire2Learn, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="dc3ec-199">**To assign Britta Simon to Brightspace by Desire2Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="dc3ec-200">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="dc3ec-202">En la lista de aplicaciones, seleccione **Brightspace by Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-202">In the applications list, select **Brightspace by Desire2Learn**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_app.png) 

3. <span data-ttu-id="dc3ec-204">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="dc3ec-206">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-206">Click **Add** button.</span></span> <span data-ttu-id="dc3ec-207">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="dc3ec-209">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dc3ec-210">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dc3ec-211">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dc3ec-212">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="dc3ec-212">Testing single sign-on</span></span>

<span data-ttu-id="dc3ec-213">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dc3ec-214">Al hacer clic en el icono de Brightspace by Desire2Learn en el Panel de acceso, iniciará sesión automáticamente en la aplicación Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="dc3ec-214">When you click the Brightspace by Desire2Learn tile in the Access Panel, you should get automatically signed-on to your Brightspace by Desire2Learn application.</span></span>
<span data-ttu-id="dc3ec-215">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dc3ec-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dc3ec-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="dc3ec-216">Additional resources</span></span>

* [<span data-ttu-id="dc3ec-217">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc3ec-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dc3ec-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dc3ec-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_203.png


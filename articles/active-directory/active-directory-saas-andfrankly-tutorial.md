---
title: "Tutorial: Integración de Azure Active Directory con &frankly | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y &frankly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: ea18a9f9bff258337a3de6d7703b4c548efa37df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a><span data-ttu-id="65e72-103">Tutorial: integración de Azure Active Directory con &frankly</span><span class="sxs-lookup"><span data-stu-id="65e72-103">Tutorial: Azure Active Directory integration with &frankly</span></span>

<span data-ttu-id="65e72-104">En este tutorial, obtendrá información sobre cómo integrar Aha! con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65e72-104">In this tutorial, you learn how to integrate &frankly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65e72-105">Integrar &frankly con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="65e72-105">Integrating &frankly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="65e72-106">Puede controlar en Azure AD quién tiene acceso a &frankly.</span><span class="sxs-lookup"><span data-stu-id="65e72-106">You can control in Azure AD who has access to &frankly</span></span>
- <span data-ttu-id="65e72-107">Puede permitir que los usuarios inicien sesión automáticamente en &frankly (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65e72-107">You can enable your users to automatically get signed-on to &frankly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65e72-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="65e72-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="65e72-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65e72-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65e72-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="65e72-110">Prerequisites</span></span>

<span data-ttu-id="65e72-111">Para configurar la integración de Azure AD con &frankly, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="65e72-111">To configure Azure AD integration with &frankly, you need the following items:</span></span>

- <span data-ttu-id="65e72-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="65e72-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65e72-113">Una suscripción habilitada para el inicio de sesión único en &frankly</span><span class="sxs-lookup"><span data-stu-id="65e72-113">A &frankly single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65e72-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="65e72-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65e72-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="65e72-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65e72-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="65e72-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65e72-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65e72-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65e72-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="65e72-118">Scenario description</span></span>
<span data-ttu-id="65e72-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="65e72-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65e72-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="65e72-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65e72-121">Adición de &frankly desde la galería</span><span class="sxs-lookup"><span data-stu-id="65e72-121">Adding &frankly from the gallery</span></span>
2. <span data-ttu-id="65e72-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="65e72-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-frankly-from-the-gallery"></a><span data-ttu-id="65e72-123">Adición de &frankly desde la galería</span><span class="sxs-lookup"><span data-stu-id="65e72-123">Adding &frankly from the gallery</span></span>
<span data-ttu-id="65e72-124">Para configurar la integración de &frankly en Azure AD, deberá agregar &frankly desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="65e72-124">To configure the integration of &frankly into Azure AD, you need to add &frankly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="65e72-125">**Para agregar &frankly desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="65e72-125">**To add &frankly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="65e72-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="65e72-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65e72-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="65e72-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="65e72-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="65e72-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="65e72-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="65e72-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="65e72-133">En el cuadro de búsqueda, escriba **&frankly**.</span><span class="sxs-lookup"><span data-stu-id="65e72-133">In the search box, type **&frankly**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_search.png)

5. <span data-ttu-id="65e72-135">En el panel de resultados, seleccione **&frankly** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="65e72-135">In the results panel, select **&frankly**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65e72-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="65e72-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65e72-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con &frankly con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="65e72-138">In this section, you configure and test Azure AD single sign-on with &frankly based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="65e72-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de &frankly para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65e72-139">For single sign-on to work, Azure AD needs to know what the counterpart user in &frankly is to a user in Azure AD.</span></span> <span data-ttu-id="65e72-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de &frankly.</span><span class="sxs-lookup"><span data-stu-id="65e72-140">In other words, a link relationship between an Azure AD user and the related user in &frankly needs to be established.</span></span>

<span data-ttu-id="65e72-141">Para establecer la relación de vínculo, en &frankly, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="65e72-141">In &frankly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="65e72-142">Para configurar y probar el inicio de sesión único de Azure AD con &frankly, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="65e72-142">To configure and test Azure AD single sign-on with &frankly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="65e72-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="65e72-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="65e72-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65e72-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65e72-145">**[Creación de un usuario de prueba de &frankly](#creating-a-frankly-test-user)**: para tener un homólogo de Britta Simon en &frankly que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65e72-145">**[Creating a &frankly test user](#creating-a-frankly-test-user)** - to have a counterpart of Britta Simon in &frankly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="65e72-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65e72-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65e72-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="65e72-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65e72-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="65e72-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65e72-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación &frankly.</span><span class="sxs-lookup"><span data-stu-id="65e72-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your &frankly application.</span></span>

<span data-ttu-id="65e72-150">**Para configurar el inicio de sesión único de Azure AD con &frankly, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="65e72-150">**To configure Azure AD single sign-on with &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="65e72-151">En Azure Portal, en la página de integración de la aplicación **&frankly**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="65e72-151">In the Azure portal, on the **&frankly** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="65e72-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="65e72-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_samlbase.png)

3. <span data-ttu-id="65e72-155">En la sección **Dominio y direcciones URL de &frankly**, si quiere configurar la aplicación en modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="65e72-155">On the **&frankly Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url.png)

    <span data-ttu-id="65e72-157">a.</span><span class="sxs-lookup"><span data-stu-id="65e72-157">a.</span></span> <span data-ttu-id="65e72-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="65e72-158">In the **Identifier** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span></span>

    <span data-ttu-id="65e72-159">b.</span><span class="sxs-lookup"><span data-stu-id="65e72-159">b.</span></span> <span data-ttu-id="65e72-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`.</span><span class="sxs-lookup"><span data-stu-id="65e72-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span></span>

4. <span data-ttu-id="65e72-161">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="65e72-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="65e72-162">Si quiere volver a configurar la aplicación en modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="65e72-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url1.png)

    <span data-ttu-id="65e72-164">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`.</span><span class="sxs-lookup"><span data-stu-id="65e72-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span></span>
    > [!NOTE] 
    > <span data-ttu-id="65e72-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="65e72-165">These values are not real.</span></span> <span data-ttu-id="65e72-166">Actualice estos valores con el identificador y la dirección URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="65e72-166">Update these values with the actual Identifier, Sign-on, and Reply URL.</span></span> <span data-ttu-id="65e72-167">Póngase en contacto con el [equipo de soporte técnico de &frankly](mailto:help@andfrankly.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="65e72-167">Contact [andfrankly support team](mailto:help@andfrankly.com) to get these values.</span></span>

5. <span data-ttu-id="65e72-168">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="65e72-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_certificate.png) 

6. <span data-ttu-id="65e72-170">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="65e72-170">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-andfrankly-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="65e72-172">Para configurar el inicio de sesión único en el lado de **&frankly**, es preciso enviar los datos descargados de **XML de metadatos** al [equipo de soporte técnico de &frankly](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="65e72-172">To configure single sign-on on **&frankly** side, you need to send the downloaded **Metadata XML** to [andfrankly support team](mailto:help@andfrankly.com).</span></span> 

> [!TIP]
> <span data-ttu-id="65e72-173">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="65e72-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="65e72-174">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="65e72-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="65e72-175">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65e72-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65e72-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="65e72-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="65e72-177">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="65e72-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="65e72-179">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="65e72-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="65e72-180">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="65e72-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65e72-182">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="65e72-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65e72-184">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="65e72-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65e72-186">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="65e72-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65e72-188">a.</span><span class="sxs-lookup"><span data-stu-id="65e72-188">a.</span></span> <span data-ttu-id="65e72-189">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65e72-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65e72-190">b.</span><span class="sxs-lookup"><span data-stu-id="65e72-190">b.</span></span> <span data-ttu-id="65e72-191">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65e72-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65e72-192">c.</span><span class="sxs-lookup"><span data-stu-id="65e72-192">c.</span></span> <span data-ttu-id="65e72-193">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="65e72-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="65e72-194">d.</span><span class="sxs-lookup"><span data-stu-id="65e72-194">d.</span></span> <span data-ttu-id="65e72-195">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="65e72-195">Click **Create**.</span></span>
 
### <a name="creating-a-frankly-test-user"></a><span data-ttu-id="65e72-196">Crear un usuario de prueba de &frankly</span><span class="sxs-lookup"><span data-stu-id="65e72-196">Creating a &frankly test user</span></span>

<span data-ttu-id="65e72-197">En esta sección, creará un usuario llamado Britta Simon en &frankly.</span><span class="sxs-lookup"><span data-stu-id="65e72-197">In this section, you create a user called Britta Simon in &frankly.</span></span> <span data-ttu-id="65e72-198">Trabaje con el [equipo de soporte técnico de &frankly](mailto:help@andfrankly.com) para agregar a los usuarios a la plataforma de &frankly.</span><span class="sxs-lookup"><span data-stu-id="65e72-198">Work with  [andfrankly support team](mailto:help@andfrankly.com) to add the users in the &frankly platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="65e72-199">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="65e72-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="65e72-200">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a &frankly.</span><span class="sxs-lookup"><span data-stu-id="65e72-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to &frankly.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="65e72-202">**Para asignar Britta Simon a &frankly, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="65e72-202">**To assign Britta Simon to &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="65e72-203">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="65e72-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="65e72-205">En la lista de aplicaciones, seleccione **&frankly**.</span><span class="sxs-lookup"><span data-stu-id="65e72-205">In the applications list, select **&frankly**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_app.png) 

3. <span data-ttu-id="65e72-207">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="65e72-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="65e72-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="65e72-209">Click **Add** button.</span></span> <span data-ttu-id="65e72-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="65e72-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="65e72-212">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="65e72-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="65e72-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="65e72-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65e72-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="65e72-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65e72-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="65e72-215">Testing single sign-on</span></span>

<span data-ttu-id="65e72-216">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="65e72-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="65e72-217">Al hacer clic en el icono de &frankly en el panel de acceso, debería iniciar sesión automáticamente en su aplicación &frankly.</span><span class="sxs-lookup"><span data-stu-id="65e72-217">When you click the &frankly tile in the Access Panel, you should get automatically signed-on to your &frankly application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65e72-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="65e72-218">Additional resources</span></span>

* [<span data-ttu-id="65e72-219">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65e72-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65e72-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="65e72-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_203.png


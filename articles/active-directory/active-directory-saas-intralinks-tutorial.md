---
title: "Tutorial: Integración de Azure Active Directory con Intralinks | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Intralinks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ee7fd5b88ac806104002ffb41af11bab4fd1b2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="e2b2f-103">Tutorial: integración de Azure Active Directory con Intralinks</span><span class="sxs-lookup"><span data-stu-id="e2b2f-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="e2b2f-104">En este tutorial, obtendrá información sobre cómo integrar Intralinks con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e2b2f-104">In this tutorial, you learn how to integrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e2b2f-105">Integrar Intralinks con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e2b2f-105">Integrating Intralinks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e2b2f-106">Puede controlar en Azure AD quién tiene acceso a Intralinks.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-106">You can control in Azure AD who has access to Intralinks</span></span>
- <span data-ttu-id="e2b2f-107">Puede permitir que los usuarios inicien sesión automáticamente en Intralinks (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-107">You can enable your users to automatically get signed-on to Intralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e2b2f-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e2b2f-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e2b2f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2b2f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e2b2f-110">Prerequisites</span></span>

<span data-ttu-id="e2b2f-111">Para configurar la integración de Azure AD con Intralinks, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e2b2f-111">To configure Azure AD integration with Intralinks, you need the following items:</span></span>

- <span data-ttu-id="e2b2f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2b2f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e2b2f-113">Una suscripción habilitada para el inicio de sesión único en Intralinks</span><span class="sxs-lookup"><span data-stu-id="e2b2f-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e2b2f-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e2b2f-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e2b2f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e2b2f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e2b2f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e2b2f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e2b2f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e2b2f-118">Scenario description</span></span>
<span data-ttu-id="e2b2f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e2b2f-120">El escenario descrito en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="e2b2f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e2b2f-121">Adición de Intralinks desde la Galería</span><span class="sxs-lookup"><span data-stu-id="e2b2f-121">Adding Intralinks from the gallery</span></span>
2. <span data-ttu-id="e2b2f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2b2f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-the-gallery"></a><span data-ttu-id="e2b2f-123">Adición de Intralinks desde la Galería</span><span class="sxs-lookup"><span data-stu-id="e2b2f-123">Adding Intralinks from the gallery</span></span>
<span data-ttu-id="e2b2f-124">Para configurar la integración de Intralinks en Azure AD, será preciso que agregue Intralinks desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-124">To configure the integration of Intralinks into Azure AD, you need to add Intralinks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e2b2f-125">**Para agregar Intralinks desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="e2b2f-125">**To add Intralinks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e2b2f-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e2b2f-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e2b2f-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e2b2f-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e2b2f-133">En el cuadro de búsqueda, escriba **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-133">In the search box, type **Intralinks**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="e2b2f-135">En el panel de resultados, seleccione **Intralinks** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-135">In the results panel, select **Intralinks**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e2b2f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2b2f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e2b2f-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Intralinks con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e2b2f-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e2b2f-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Intralinks para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intralinks is to a user in Azure AD.</span></span> <span data-ttu-id="e2b2f-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Intralinks.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-140">In other words, a link relationship between an Azure AD user and the related user in Intralinks needs to be established.</span></span>

<span data-ttu-id="e2b2f-141">Para establecer la relación de vínculo, en Intralinks, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-141">In Intralinks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e2b2f-142">Para configurar y probar el inicio de sesión único de Azure AD con Intralinks, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e2b2f-142">To configure and test Azure AD single sign-on with Intralinks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e2b2f-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e2b2f-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e2b2f-145">**[Creación de un usuario de prueba de Intralinks](#creating-an-intralinks-test-user)**: para tener un homólogo de Britta Simon en Intralinks que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - to have a counterpart of Britta Simon in Intralinks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e2b2f-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e2b2f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e2b2f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2b2f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e2b2f-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Intralinks.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="e2b2f-150">**Para configurar el inicio de sesión único de Azure AD con Intralinks, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e2b2f-150">**To configure Azure AD single sign-on with Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="e2b2f-151">En Azure Portal, en la página de integración de la aplicación **Intralinks**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-151">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e2b2f-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="e2b2f-155">En la sección **Dominio y direcciones URL de Intralinks**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e2b2f-155">On the **Intralinks Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="e2b2f-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="e2b2f-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e2b2f-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-158">This value is not real.</span></span> <span data-ttu-id="e2b2f-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="e2b2f-160">Póngase en contacto con el [equipo de atención al cliente de Intralinks](https://www.intralinks.com/contact-1) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) to get this value.</span></span> 
 
4. <span data-ttu-id="e2b2f-161">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="e2b2f-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e2b2f-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e2b2f-165">Para configurar el inicio de sesión único en **Intralinks**, necesita enviar el archivo **XML de metadatos** descargado al [equipo de soporte técnico de Intralinks](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="e2b2f-165">To configure single sign-on on **Intralinks** side, you need to send the downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="e2b2f-166">El equipo de soporte técnico lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e2b2f-167">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e2b2f-168">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e2b2f-169">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e2b2f-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e2b2f-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2b2f-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="e2b2f-171">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e2b2f-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e2b2f-173">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="e2b2f-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e2b2f-174">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e2b2f-176">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e2b2f-178">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e2b2f-180">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="e2b2f-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e2b2f-182">a.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-182">a.</span></span> <span data-ttu-id="e2b2f-183">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e2b2f-184">b.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-184">b.</span></span> <span data-ttu-id="e2b2f-185">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e2b2f-186">c.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-186">c.</span></span> <span data-ttu-id="e2b2f-187">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e2b2f-188">d.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-188">d.</span></span> <span data-ttu-id="e2b2f-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="e2b2f-190">Creación de un usuario de prueba de Intralinks</span><span class="sxs-lookup"><span data-stu-id="e2b2f-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="e2b2f-191">En esta sección, creará un usuario llamado Britta Simon en Intralinks.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="e2b2f-192">Póngase en contacto con el [equipo de soporte técnico de Intralinks](https://www.intralinks.com/contact-1) para agregar los usuarios a la plataforma de Intralinks.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) to add the users in the Intralinks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e2b2f-193">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2b2f-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e2b2f-194">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Intralinks.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intralinks.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e2b2f-196">**Para asignar Britta Simon a Intralinks, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e2b2f-196">**To assign Britta Simon to Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="e2b2f-197">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e2b2f-199">En la lista de aplicaciones, seleccione **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-199">In the applications list, select **Intralinks**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="e2b2f-201">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e2b2f-203">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-203">Click **Add** button.</span></span> <span data-ttu-id="e2b2f-204">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e2b2f-206">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e2b2f-207">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e2b2f-208">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="e2b2f-209">Adición de la aplicación VIA o Elite de Intralinks</span><span class="sxs-lookup"><span data-stu-id="e2b2f-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="e2b2f-210">Intralinks usa la misma plataforma de identidad de inicio de sesión único para todas las demás aplicaciones de Intralinks, excepto la aplicación Deal Nexus.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-210">Intralinks uses the same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="e2b2f-211">Por tanto, si piensa usar cualquier otra aplicación de Intralinks, primero tendrá que configurar el inicio de sesión único para una aplicación de Intralinks principal mediante el procedimiento descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-211">So if you plan to use any other Intralinks application then first you have to configure SSO for one Primary Intralinks application using the procedure described above.</span></span>

<span data-ttu-id="e2b2f-212">Después, podrá realizar el procedimiento siguiente para agregar otra aplicación de Intralinks en el inquilino, que puede aprovechar esta aplicación principal para el SSO.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-212">After that you can follow the below procedure to add another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="e2b2f-213">Esta característica solo está disponible para los clientes de la SKU Premium de Azure AD y no está disponible para los clientes de SKU Básico o Gratis.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-213">This feature is available only to Azure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="e2b2f-214">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-214">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="e2b2f-216">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-216">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e2b2f-217">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-217">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e2b2f-219">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-219">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e2b2f-221">En el cuadro de búsqueda, escriba **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-221">In the search box, type **Intralinks**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="e2b2f-223">En **Agregar aplicación Intralinks** realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e2b2f-223">On **Intralinks Add app** perform the following steps:</span></span>

    ![Adición de la aplicación VIA o Elite de Intralinks](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="e2b2f-225">a.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-225">a.</span></span> <span data-ttu-id="e2b2f-226">En el cuadro de texto **Nombre**, escriba un nombre adecuado para la aplicación, por ejemplo, **Intralinks Elite**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-226">In **Name** textbox, enter appropriate name of the application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="e2b2f-227">b.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-227">b.</span></span> <span data-ttu-id="e2b2f-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="e2b2f-229">En Azure Portal, en la página de integración de la aplicación **Intralinks**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-229">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

7. <span data-ttu-id="e2b2f-231">En el cuadro de diálogo **Inicio de sesión único**, seleccione **Modo** como **Inicio de sesión vinculado**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-231">On the **Single sign-on** dialog, select **Mode** as **Linked Sign-on**.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="e2b2f-233">Obtenga la dirección URL de SSO iniciado por el proveedor de servicios del [equipo de soporte técnico de Intralinks](https://www.intralinks.com/contact-1) para la otra aplicación de Intralinks y escríbala en **Configurar dirección URL de inicio de sesión** como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-233">Get the the SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for the other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="e2b2f-235">En el cuadro de texto URL de inicio de sesión, escriba la dirección URL que utilizan los usuarios para iniciar sesión en la aplicación de Intralinks con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="e2b2f-235">In the Sign On URL textbox, type the URL used by your users to sign-on to your Intralinks application using the following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="e2b2f-236">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e2b2f-236">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="e2b2f-238">Asigne la aplicación al usuario o a los grupos, como se muestra en la sección **[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-238">Assign the application to user or groups as shown in the section **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="e2b2f-239">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e2b2f-239">Testing single sign-on</span></span>

<span data-ttu-id="e2b2f-240">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e2b2f-241">Al hacer clic en el icono de Intralinks en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Intralinks.</span><span class="sxs-lookup"><span data-stu-id="e2b2f-241">When you click the Intralinks tile in the Access Panel, you should get automatically signed-on to your Intralinks application.</span></span>
<span data-ttu-id="e2b2f-242">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e2b2f-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e2b2f-243">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e2b2f-243">Additional resources</span></span>

* [<span data-ttu-id="e2b2f-244">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2b2f-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e2b2f-245">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e2b2f-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png


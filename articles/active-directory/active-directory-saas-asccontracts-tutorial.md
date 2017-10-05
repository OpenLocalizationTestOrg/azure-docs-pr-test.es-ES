---
title: "Tutorial: Integración de Azure Active Directory con ASC Contracts | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y ASC Contracts."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7f54202-1581-4e55-a97e-02633ff9382d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: jeedes
ms.openlocfilehash: 87ea3cc55f9683e7d5b9912a87d675575cea0347
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asc-contracts"></a><span data-ttu-id="3ea3d-103">Tutorial: Integración de Azure Active Directory con ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="3ea3d-103">Tutorial: Azure Active Directory integration with ASC Contracts</span></span>

<span data-ttu-id="3ea3d-104">En este tutorial, va a aprender a integrar ASC Contracts con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3ea3d-104">In this tutorial, you learn how to integrate ASC Contracts with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ea3d-105">Integrar ASC Contracts con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3ea3d-105">Integrating ASC Contracts with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3ea3d-106">Puede controlar en Azure AD quién tiene acceso a ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-106">You can control in Azure AD who has access to ASC Contracts</span></span>
- <span data-ttu-id="3ea3d-107">Puede permitir que los usuarios inicien sesión automáticamente en ASC Contracts (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-107">You can enable your users to automatically get signed-on to ASC Contracts (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3ea3d-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3ea3d-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3ea3d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ea3d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3ea3d-110">Prerequisites</span></span>

<span data-ttu-id="3ea3d-111">Para configurar la integración de Azure AD con ASC Contracts, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3ea3d-111">To configure Azure AD integration with ASC Contracts, you need the following items:</span></span>

- <span data-ttu-id="3ea3d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ea3d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3ea3d-113">Una suscripción habilitada para inicio de sesión único en ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="3ea3d-113">An ASC Contracts single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ea3d-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ea3d-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3ea3d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ea3d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ea3d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ea3d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ea3d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3ea3d-118">Scenario description</span></span>
<span data-ttu-id="3ea3d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ea3d-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="3ea3d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ea3d-121">Incorporación de ASC Contracts desde la galería</span><span class="sxs-lookup"><span data-stu-id="3ea3d-121">Adding ASC Contracts from the gallery</span></span>
2. <span data-ttu-id="3ea3d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ea3d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asc-contracts-from-the-gallery"></a><span data-ttu-id="3ea3d-123">Incorporación de ASC Contracts desde la galería</span><span class="sxs-lookup"><span data-stu-id="3ea3d-123">Adding ASC Contracts from the gallery</span></span>
<span data-ttu-id="3ea3d-124">Para configurar la integración de ASC Contracts en Azure AD, tiene que agregar ASC Contracts desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-124">To configure the integration of ASC Contracts into Azure AD, you need to add ASC Contracts from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3ea3d-125">**Para agregar ASC Contracts desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3ea3d-125">**To add ASC Contracts from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3ea3d-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3ea3d-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3ea3d-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3ea3d-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3ea3d-133">En el cuadro de búsqueda, escriba **ASC Contracts**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-133">In the search box, type **ASC Contracts**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_search.png)

5. <span data-ttu-id="3ea3d-135">En el panel de resultados, seleccione **ASC Contracts** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-135">In the results panel, select **ASC Contracts**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3ea3d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ea3d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3ea3d-138">En esta sección, puede configurar y probar el inicio de sesión único de Azure AD con ASC Contracts con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3ea3d-138">In this section, you configure and test Azure AD single sign-on with ASC Contracts based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3ea3d-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de ASC Contracts para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ASC Contracts is to a user in Azure AD.</span></span> <span data-ttu-id="3ea3d-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-140">In other words, a link relationship between an Azure AD user and the related user in ASC Contracts needs to be established.</span></span>

<span data-ttu-id="3ea3d-141">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como valor del **nombre de usuario** en ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ASC Contracts.</span></span>

<span data-ttu-id="3ea3d-142">Para configurar y probar el inicio de sesión único de Azure AD con ASC Contracts, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3ea3d-142">To configure and test Azure AD single sign-on with ASC Contracts, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3ea3d-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3ea3d-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3ea3d-145">**[Creación de un usuario de prueba de ASC Contracts](#creating-an-asc-contracts-test-user)**: para tener un homólogo de Britta Simon en ASC Contracts que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-145">**[Creating an ASC Contracts test user](#creating-an-asc-contracts-test-user)** - to have a counterpart of Britta Simon in ASC Contracts that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3ea3d-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3ea3d-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3ea3d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ea3d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3ea3d-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ASC Contracts application.</span></span>

<span data-ttu-id="3ea3d-150">**Para configurar el inicio de sesión único de Azure AD con ASC Contracts, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3ea3d-150">**To configure Azure AD single sign-on with ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="3ea3d-151">En Azure Portal, en la página de integración de la aplicación **ASC Contracts**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-151">In the Azure portal, on the **ASC Contracts** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3ea3d-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_samlbase.png)

3. <span data-ttu-id="3ea3d-155">En la sección **Dominio y direcciones URL de ASC Contracts**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3ea3d-155">On the **ASC Contracts Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_url.png)

    <span data-ttu-id="3ea3d-157">a.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-157">a.</span></span> <span data-ttu-id="3ea3d-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.asccontracts.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="3ea3d-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth`</span></span>

    <span data-ttu-id="3ea3d-159">b.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-159">b.</span></span> <span data-ttu-id="3ea3d-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3ea3d-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-161">These values are not real.</span></span> <span data-ttu-id="3ea3d-162">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="3ea3d-163">Póngase en contacto con el equipo de ASC Networks Inc. (ASC) en el **613-599-6178** para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-163">Contact ASC Networks Inc. (ASC) team at **613.599.6178** to get these values.</span></span>

4. <span data-ttu-id="3ea3d-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_certificate.png) 

5. <span data-ttu-id="3ea3d-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3ea3d-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-asccontracts-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3ea3d-168">Para configurar el inicio de sesión único en **ASC Contracts**, llame al soporte técnico de ASC Networks Inc. (ASC) en el **613-599-6178** y proporcióneles el **XML de metadatos** descargado.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-168">To configure single sign-on on **ASC Contracts** side, call ASC Networks Inc. (ASC) support at **613.599.6178** and provide them with the downloaded **Metadata XML**.</span></span> <span data-ttu-id="3ea3d-169">Ellos configuran esta aplicación para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-169">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3ea3d-170">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3ea3d-171">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3ea3d-172">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3ea3d-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3ea3d-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ea3d-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="3ea3d-174">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3ea3d-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3ea3d-176">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="3ea3d-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3ea3d-177">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3ea3d-179">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3ea3d-181">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3ea3d-183">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="3ea3d-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3ea3d-185">a.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-185">a.</span></span> <span data-ttu-id="3ea3d-186">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ea3d-187">b.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-187">b.</span></span> <span data-ttu-id="3ea3d-188">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3ea3d-189">c.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-189">c.</span></span> <span data-ttu-id="3ea3d-190">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3ea3d-191">d.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-191">d.</span></span> <span data-ttu-id="3ea3d-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-192">Click **Create**.</span></span>
 
### <a name="creating-an-asc-contracts-test-user"></a><span data-ttu-id="3ea3d-193">Creación de un usuario de prueba de ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="3ea3d-193">Creating an ASC Contracts test user</span></span>

<span data-ttu-id="3ea3d-194">Trabaje con el equipo de soporte técnico de ASC Networks Inc. (ASC) en el **613-599-6178** para agregar a los usuarios a la plataforma ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-194">Work with ASC Networks Inc. (ASC) support team at **613.599.6178** to get the users added in the ASC Contracts platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3ea3d-195">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ea3d-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3ea3d-196">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ASC Contracts.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3ea3d-198">**Para asignar Britta Simon a ASC Contracts, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3ea3d-198">**To assign Britta Simon to ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="3ea3d-199">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3ea3d-201">En la lista de aplicaciones, seleccione **ASC Contracts**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-201">In the applications list, select **ASC Contracts**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_app.png) 

3. <span data-ttu-id="3ea3d-203">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3ea3d-205">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-205">Click **Add** button.</span></span> <span data-ttu-id="3ea3d-206">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3ea3d-208">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3ea3d-209">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3ea3d-210">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3ea3d-211">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3ea3d-211">Testing single sign-on</span></span>

<span data-ttu-id="3ea3d-212">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3ea3d-213">Al hacer clic en el icono de ASC Contracts en el panel de acceso, debería iniciar sesión automáticamente en su aplicación ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="3ea3d-213">When you click the ASC Contracts tile in the Access Panel, you should get automatically signed-on to your ASC Contracts application.</span></span> <span data-ttu-id="3ea3d-214">Para obtener más información sobre el panel de acceso, consulte</span><span class="sxs-lookup"><span data-stu-id="3ea3d-214">For more information about the Access Panel, see.</span></span> <span data-ttu-id="3ea3d-215">[Introducción al panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="3ea3d-215">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3ea3d-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3ea3d-216">Additional resources</span></span>

* [<span data-ttu-id="3ea3d-217">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ea3d-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3ea3d-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3ea3d-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_203.png


---
title: "Tutorial: Integración de Azure Active Directory con Keeper Password Manager & Digital Vault | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Keeper Password Manager & Digital Vault."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 36504a281756b980e3348e7f892ba08821873b52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a><span data-ttu-id="6da23-103">Tutorial: Integración de Azure Active Directory con Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="6da23-103">Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault</span></span>

<span data-ttu-id="6da23-104">En este tutorial, obtendrá información sobre cómo integrar Keeper Password Manager & Digital Vault con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6da23-104">In this tutorial, you learn how to integrate Keeper Password Manager & Digital Vault with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6da23-105">La integración de Keeper Password Manager & Digital Vault con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="6da23-105">Integrating Keeper Password Manager & Digital Vault with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6da23-106">Desde Azure AD puede controlar quién tiene acceso a Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="6da23-106">You can control in Azure AD who has access to Keeper Password Manager & Digital Vault</span></span>
- <span data-ttu-id="6da23-107">Puede permitir que los usuarios inicien sesión automáticamente en Keeper Password Manager & Digital Vault (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6da23-107">You can enable your users to automatically get signed-on to Keeper Password Manager & Digital Vault (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6da23-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6da23-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6da23-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6da23-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6da23-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6da23-110">Prerequisites</span></span>

<span data-ttu-id="6da23-111">Para configurar la integración de Azure AD con Keeper Password Manager & Digital Vault, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="6da23-111">To configure Azure AD integration with Keeper Password Manager & Digital Vault, you need the following items:</span></span>

- <span data-ttu-id="6da23-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6da23-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6da23-113">Una suscripción habilitada con inicio de sesión único de Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="6da23-113">A Keeper Password Manager & Digital Vault single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6da23-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="6da23-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6da23-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="6da23-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6da23-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6da23-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6da23-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6da23-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6da23-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="6da23-118">Scenario description</span></span>
<span data-ttu-id="6da23-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="6da23-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6da23-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="6da23-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6da23-121">Incorporación de Keeper Password Manager & Digital Vault desde la galería</span><span class="sxs-lookup"><span data-stu-id="6da23-121">Adding Keeper Password Manager & Digital Vault from the gallery</span></span>
2. <span data-ttu-id="6da23-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6da23-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-keeper-password-manager--digital-vault-from-the-gallery"></a><span data-ttu-id="6da23-123">Incorporación de Keeper Password Manager & Digital Vault desde la galería</span><span class="sxs-lookup"><span data-stu-id="6da23-123">Adding Keeper Password Manager & Digital Vault from the gallery</span></span>
<span data-ttu-id="6da23-124">Para configurar la integración de Keeper Password Manager & Digital Vault en Azure AD, es preciso agregar esta aplicación desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="6da23-124">To configure the integration of Keeper Password Manager & Digital Vault into Azure AD, you need to add Keeper Password Manager & Digital Vault from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6da23-125">**Para agregar Keeper Password Manager & Digital Vault desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="6da23-125">**To add Keeper Password Manager & Digital Vault from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6da23-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6da23-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6da23-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="6da23-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6da23-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6da23-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="6da23-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6da23-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="6da23-133">En el cuadro de búsqueda, escriba **Keeper Password Manager & Digital Vault**.</span><span class="sxs-lookup"><span data-stu-id="6da23-133">In the search box, type **Keeper Password Manager & Digital Vault**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. <span data-ttu-id="6da23-135">En el panel de resultados, seleccione **Keeper Password Manager & Digital Vault** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6da23-135">In the results panel, select **Keeper Password Manager & Digital Vault**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6da23-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6da23-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6da23-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Keeper Password Manager & Digital Vault con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6da23-138">In this section, you configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6da23-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Keeper Password Manager & Digital Vault para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6da23-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Keeper Password Manager & Digital Vault is to a user in Azure AD.</span></span> <span data-ttu-id="6da23-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Keeper Password Manager & Digital Vault.</span><span class="sxs-lookup"><span data-stu-id="6da23-140">In other words, a link relationship between an Azure AD user and the related user in Keeper Password Manager & Digital Vault needs to be established.</span></span>

<span data-ttu-id="6da23-141">Para establecer la relación de vínculo, en Keeper Password Manager & Digital Vault, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="6da23-141">In Keeper Password Manager & Digital Vault, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6da23-142">Para configurar y probar el inicio de sesión único de Azure AD con Keeper Password Manager & Digital Vault, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="6da23-142">To configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6da23-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="6da23-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6da23-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6da23-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6da23-145">**[Creación de un usuario de prueba de Keeper Password Manager & Digital Vault](#creating-a-keeperpasswordmanager-test-user)**: para tener un homólogo de Britta Simon en esta aplicación que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6da23-145">**[Creating a Keeper Password Manager & Digital Vault test user](#creating-a-keeperpasswordmanager-test-user)** - to have a counterpart of Britta Simon in Keeper Password Manager & Digital Vault that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6da23-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6da23-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6da23-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="6da23-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6da23-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6da23-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6da23-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Keeper Password Manager & Digital Vault.</span><span class="sxs-lookup"><span data-stu-id="6da23-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Keeper Password Manager & Digital Vault application.</span></span>

<span data-ttu-id="6da23-150">**Para configurar el inicio de sesión único de Azure AD con Keeper Password Manager & Digital Vault, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="6da23-150">**To configure Azure AD single sign-on with Keeper Password Manager & Digital Vault, perform the following steps:**</span></span>

1. <span data-ttu-id="6da23-151">En Azure Portal, en la página de integración de aplicaciones de **Keeper Password Manager & Digital Vault**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6da23-151">In the Azure portal, on the **Keeper Password Manager & Digital Vault** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="6da23-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6da23-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. <span data-ttu-id="6da23-155">En la sección **Dominio y direcciones URL de Keeper Password Manager & Digital Vault** haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6da23-155">On the **Keeper Password Manager & Digital Vault Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    <span data-ttu-id="6da23-157">a.</span><span class="sxs-lookup"><span data-stu-id="6da23-157">a.</span></span> <span data-ttu-id="6da23-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`.</span><span class="sxs-lookup"><span data-stu-id="6da23-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span></span>

    <span data-ttu-id="6da23-159">b.</span><span class="sxs-lookup"><span data-stu-id="6da23-159">b.</span></span> <span data-ttu-id="6da23-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`.</span><span class="sxs-lookup"><span data-stu-id="6da23-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span></span>

    <span data-ttu-id="6da23-161">c.</span><span class="sxs-lookup"><span data-stu-id="6da23-161">c.</span></span> <span data-ttu-id="6da23-162">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://{SSO CONNECT SERVER}/sso-connect`</span><span class="sxs-lookup"><span data-stu-id="6da23-162">In the **Identifier** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6da23-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="6da23-163">These values are not real.</span></span> <span data-ttu-id="6da23-164">Actualice estos valores con los valores reales de URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="6da23-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="6da23-165">Póngase en contacto con el [equipo de soporte técnico de Keeper Password Manager & Digital Vault](https://keepersecurity.com/contact.html) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="6da23-165">Contact [Keeper Password Manager & Digital Vault Client support team](https://keepersecurity.com/contact.html) to get these values.</span></span> 

4. <span data-ttu-id="6da23-166">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6da23-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. <span data-ttu-id="6da23-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="6da23-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="6da23-170">En la sección de **configuración de Keeper Password Manager & Digital Vault**, haga clic en **Configurar Keeper Password Manager & Digital Vault** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="6da23-170">On the **Keeper Password Manager & Digital Vault Configuration** section, click **Configure Keeper Password Manager & Digital Vault** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6da23-171">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="6da23-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. <span data-ttu-id="6da23-173">Para configurar el inicio de sesión único en la sección de **configuración de Keeper Password Manager & Digital Vault**, siga las instrucciones proporcionadas en la [guía de soporte técnico de Keeper](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span><span class="sxs-lookup"><span data-stu-id="6da23-173">To configure single sign-on on **Keeper Password Manager & Digital Vault Configuration** side, follow the guidelines given at [Keeper Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span></span>

> [!TIP]
> <span data-ttu-id="6da23-174">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6da23-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6da23-175">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="6da23-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6da23-176">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6da23-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6da23-177">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6da23-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="6da23-178">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6da23-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="6da23-180">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="6da23-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6da23-181">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6da23-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6da23-183">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="6da23-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6da23-185">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6da23-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6da23-187">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="6da23-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6da23-189">a.</span><span class="sxs-lookup"><span data-stu-id="6da23-189">a.</span></span> <span data-ttu-id="6da23-190">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6da23-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6da23-191">b.</span><span class="sxs-lookup"><span data-stu-id="6da23-191">b.</span></span> <span data-ttu-id="6da23-192">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6da23-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6da23-193">c.</span><span class="sxs-lookup"><span data-stu-id="6da23-193">c.</span></span> <span data-ttu-id="6da23-194">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="6da23-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6da23-195">d.</span><span class="sxs-lookup"><span data-stu-id="6da23-195">d.</span></span> <span data-ttu-id="6da23-196">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6da23-196">Click **Create**.</span></span>
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a><span data-ttu-id="6da23-197">Creación de un usuario de prueba de Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="6da23-197">Creating a Keeper Password Manager & Digital Vault test user</span></span>

<span data-ttu-id="6da23-198">Para permitir que los usuarios de Azure AD inicien sesión en Keeper Password Manager & Digital Vault, se les debe aprovisionar en esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="6da23-198">To enable Azure AD users to log in to Keeper Password Manager & Digital Vault, they must be provisioned into Keeper Password Manager & Digital Vault.</span></span> <span data-ttu-id="6da23-199">La aplicación admite aprovisionamiento de usuarios Just-In-Time y, tras la autenticación, los usuarios se crearán automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6da23-199">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="6da23-200">Puede ponerse en contacto con el [soporte técnico de Keeper](https://keepersecurity.com/contact.html), si desea configurar manualmente los usuarios.</span><span class="sxs-lookup"><span data-stu-id="6da23-200">You can contact [Keeper Support](https://keepersecurity.com/contact.html), if you want to setup users manually.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6da23-201">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6da23-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6da23-202">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Keeper Password Manager & Digital Vault.</span><span class="sxs-lookup"><span data-stu-id="6da23-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Keeper Password Manager & Digital Vault.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="6da23-204">**Para asignar a Britta Simon a Keeper Password Manager & Digital Vault, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="6da23-204">**To assign Britta Simon to Keeper Password Manager & Digital Vault, perform the following steps:**</span></span>

1. <span data-ttu-id="6da23-205">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6da23-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="6da23-207">En la lista de aplicaciones, seleccione **Keeper Password Manager & Digital Vault**.</span><span class="sxs-lookup"><span data-stu-id="6da23-207">In the applications list, select **Keeper Password Manager & Digital Vault**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. <span data-ttu-id="6da23-209">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6da23-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="6da23-211">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6da23-211">Click **Add** button.</span></span> <span data-ttu-id="6da23-212">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6da23-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="6da23-214">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="6da23-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6da23-215">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6da23-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6da23-216">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6da23-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6da23-217">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="6da23-217">Testing single sign-on</span></span>

<span data-ttu-id="6da23-218">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="6da23-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6da23-219">Al hacer clic en el icono de Keeper Password Manager & Digital Vault en el Panel de acceso, debería aparecer la página de inicio de sesión de esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="6da23-219">When you click the Keeper Password Manager & Digital Vault tile in the Access Panel, you should get login page of Keeper Password Manager & Digital Vault application.</span></span> <span data-ttu-id="6da23-220">Después de autenticarse correctamente, podrá entrar en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6da23-220">Upon successful authentication, you should get into the application.</span></span> <span data-ttu-id="6da23-221">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6da23-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6da23-222">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="6da23-222">Additional resources</span></span>

* [<span data-ttu-id="6da23-223">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6da23-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6da23-224">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6da23-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png


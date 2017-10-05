---
title: "Tutorial: Integración de Azure Active Directory con LockPath Keylight | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y LockPath Keylight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: e64a966f24411818abc4cc4ab29a428b5577d012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="789a9-103">Tutorial: Integración de Azure Active Directory con LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="789a9-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="789a9-104">En este tutorial, obtendrá información sobre cómo integrar LockPath Keylight con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="789a9-104">In this tutorial, you learn how to integrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="789a9-105">La integración de LockPath Keylight con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="789a9-105">Integrating LockPath Keylight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="789a9-106">En Azure AD puede controlar quién tiene acceso a LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="789a9-106">You can control in Azure AD who has access to LockPath Keylight</span></span>
- <span data-ttu-id="789a9-107">Puede permitir que los usuarios inicien sesión automáticamente en LockPath Keylight (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="789a9-107">You can enable your users to automatically get signed-on to LockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="789a9-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="789a9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="789a9-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="789a9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="789a9-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="789a9-110">Prerequisites</span></span>

<span data-ttu-id="789a9-111">Para configurar la integración de Azure AD con LockPath Keylight, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="789a9-111">To configure Azure AD integration with LockPath Keylight, you need the following items:</span></span>

- <span data-ttu-id="789a9-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="789a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="789a9-113">Una suscripción habilitada para el inicio de sesión único en LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="789a9-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="789a9-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="789a9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="789a9-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="789a9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="789a9-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="789a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="789a9-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="789a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="789a9-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="789a9-118">Scenario description</span></span>
<span data-ttu-id="789a9-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="789a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="789a9-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="789a9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="789a9-121">Incorporación de LockPath Keylight desde la galería</span><span class="sxs-lookup"><span data-stu-id="789a9-121">Adding LockPath Keylight from the gallery</span></span>
2. <span data-ttu-id="789a9-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="789a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-the-gallery"></a><span data-ttu-id="789a9-123">Incorporación de LockPath Keylight desde la galería</span><span class="sxs-lookup"><span data-stu-id="789a9-123">Adding LockPath Keylight from the gallery</span></span>
<span data-ttu-id="789a9-124">Para configurar la integración de LockPath Keylight en Azure AD, es preciso agregar LockPath Keylight desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="789a9-124">To configure the integration of LockPath Keylight into Azure AD, you need to add LockPath Keylight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="789a9-125">**Para agregar LockPath Keylight desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="789a9-125">**To add LockPath Keylight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="789a9-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="789a9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="789a9-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="789a9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="789a9-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="789a9-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="789a9-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="789a9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="789a9-133">En el cuadro de búsqueda, escriba **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="789a9-133">In the search box, type **LockPath Keylight**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="789a9-135">En el panel de resultados, seleccione **LockPath Keylight** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="789a9-135">In the results panel, select **LockPath Keylight**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="789a9-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="789a9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="789a9-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con LockPath Keylight con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="789a9-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="789a9-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de LockPath Keylight para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="789a9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LockPath Keylight is to a user in Azure AD.</span></span> <span data-ttu-id="789a9-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="789a9-140">In other words, a link relationship between an Azure AD user and the related user in LockPath Keylight needs to be established.</span></span>

<span data-ttu-id="789a9-141">Para establecer la relación de vínculo, en LockPath Keylight, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="789a9-141">In LockPath Keylight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="789a9-142">Para configurar y probar el inicio de sesión único de Azure AD con LockPath Keylight, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="789a9-142">To configure and test Azure AD single sign-on with LockPath Keylight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="789a9-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="789a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="789a9-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="789a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="789a9-145">**[Crear un usuario de prueba de LockPath Keylight](#creating-a-lockpath-keylight-test-user)** : para tener un homólogo de Britta Simon en LockPath Keylight que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="789a9-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - to have a counterpart of Britta Simon in LockPath Keylight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="789a9-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="789a9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="789a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="789a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="789a9-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="789a9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="789a9-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="789a9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="789a9-150">**Para configurar el inicio de sesión único de Azure AD con LockPath Keylight, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="789a9-150">**To configure Azure AD single sign-on with LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="789a9-151">En la página de integración de la aplicación **LockPath Keylight** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="789a9-151">In the Azure portal, on the **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="789a9-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="789a9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="789a9-155">En la sección **Dominio y direcciones URL de LockPath Keylight**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="789a9-155">On the **LockPath Keylight Domain and URLs** section, perform the following steps::</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="789a9-157">a.</span><span class="sxs-lookup"><span data-stu-id="789a9-157">a.</span></span> <span data-ttu-id="789a9-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company name>.keylightgrc.com/`.</span><span class="sxs-lookup"><span data-stu-id="789a9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="789a9-159">b.</span><span class="sxs-lookup"><span data-stu-id="789a9-159">b.</span></span> <span data-ttu-id="789a9-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="789a9-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="789a9-161">c.</span><span class="sxs-lookup"><span data-stu-id="789a9-161">c.</span></span> <span data-ttu-id="789a9-162">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<company name>.keylightgrc.com/Login.aspx`.</span><span class="sxs-lookup"><span data-stu-id="789a9-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="789a9-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="789a9-163">These values are not real.</span></span> <span data-ttu-id="789a9-164">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="789a9-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="789a9-165">Póngase en contacto con el [equipo de soporte técnico de cliente de LockPath Keylight](https://www.lockpath.com/contact/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="789a9-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) to get these values.</span></span> 

4. <span data-ttu-id="789a9-166">En la sección **Certificado de firma de SAML**, haga clic en **Certificado** y, a continuación, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="789a9-166">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="789a9-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="789a9-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="789a9-170">En la sección **Configuración de LockPath Keylight**, haga clic en **Configurar LockPath Keylight** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="789a9-170">On the **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** to open **Configure sign-on** window.</span></span> <span data-ttu-id="789a9-171">Copie las **direcciones URL del servicio de inicio de sesión único de SAML y de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="789a9-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="789a9-173">Realice los pasos siguientes para habilitar el inicio de sesión único en LockPath Keylight:</span><span class="sxs-lookup"><span data-stu-id="789a9-173">To enable SSO in LockPath Keylight, perform the following steps:</span></span>
   
    <span data-ttu-id="789a9-174">a.</span><span class="sxs-lookup"><span data-stu-id="789a9-174">a.</span></span> <span data-ttu-id="789a9-175">Inicie sesión en su cuenta de LockPath Keylight como administrador.</span><span class="sxs-lookup"><span data-stu-id="789a9-175">Sign-on to your LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="789a9-176">b.</span><span class="sxs-lookup"><span data-stu-id="789a9-176">b.</span></span> <span data-ttu-id="789a9-177">En el menú de la parte superior, haga clic en el icono de la **persona** y seleccione **Keylight Setup** (Configuración de Keylight).</span><span class="sxs-lookup"><span data-stu-id="789a9-177">In the menu on the top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="789a9-179">c.</span><span class="sxs-lookup"><span data-stu-id="789a9-179">c.</span></span> <span data-ttu-id="789a9-180">En la vista de árbol de la izquierda, haga clic en **SAML**.</span><span class="sxs-lookup"><span data-stu-id="789a9-180">In the treeview on the left, click **SAML**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="789a9-182">d.</span><span class="sxs-lookup"><span data-stu-id="789a9-182">d.</span></span> <span data-ttu-id="789a9-183">En el cuadro de diálogo **SAML Settings** (Configuración de SAML), haga clic en **Edit** (Editar).</span><span class="sxs-lookup"><span data-stu-id="789a9-183">On the **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="789a9-185">En la página del cuadro de diálogo **Edit SAML Settings** (Editar la configuración de SAML), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="789a9-185">On the **Edit SAML Settings** dialog page, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="789a9-187">a.</span><span class="sxs-lookup"><span data-stu-id="789a9-187">a.</span></span> <span data-ttu-id="789a9-188">Establezca **SAML authentication** (Autenticación SAML) como **Active** (Activada).</span><span class="sxs-lookup"><span data-stu-id="789a9-188">Set **SAML authentication** to **Active**.</span></span>

    <span data-ttu-id="789a9-189">b.</span><span class="sxs-lookup"><span data-stu-id="789a9-189">b.</span></span> <span data-ttu-id="789a9-190">Pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) que copió de Azure Portal en el cuadro de texto **Identity provider Login URL** (Dirección URL de inicio de sesión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="789a9-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="789a9-191">c.</span><span class="sxs-lookup"><span data-stu-id="789a9-191">c.</span></span> <span data-ttu-id="789a9-192">Pegue el valor de **Single Sign-Out Service URL** (Dirección URL del servicio de cierre de sesión único) que copió de Azure Portal en el cuadro de texto **Identity Provider Logout URL** (Dirección URL de cierre de sesión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="789a9-192">Paste the **Single Sign-Out Service URL** value which you have copied from the Azure portal into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="789a9-193">d.</span><span class="sxs-lookup"><span data-stu-id="789a9-193">d.</span></span> <span data-ttu-id="789a9-194">Haga clic en **Elegir archivo** para seleccionar el certificado de LockPath Keylight descargado y después haga clic en **Abrir** para cargarlo.</span><span class="sxs-lookup"><span data-stu-id="789a9-194">Click **Choose File** to select your downloaded LockPath Keylight certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="789a9-195">e.</span><span class="sxs-lookup"><span data-stu-id="789a9-195">e.</span></span> <span data-ttu-id="789a9-196">Establezca **SAML User Id location** (Ubicación de id. de usuario de SAML) en **NameIdentifier element of the subject statement** (Elemento NameIdentifier de la instrucción Subject).</span><span class="sxs-lookup"><span data-stu-id="789a9-196">Set **SAML User Id location** to **NameIdentifier element of the subject statement**.</span></span>
    
    <span data-ttu-id="789a9-197">f.</span><span class="sxs-lookup"><span data-stu-id="789a9-197">f.</span></span> <span data-ttu-id="789a9-198">Proporcione el **proveedor de servicios de Keylight** mediante el siguiente patrón: **https://&lt;NombreDeEmpresa&gt;.keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="789a9-198">Provide the **Keylight Service Provider** using the following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="789a9-199">g.</span><span class="sxs-lookup"><span data-stu-id="789a9-199">g.</span></span> <span data-ttu-id="789a9-200">Establezca **Auto-provision users** (Usuarios de aprovisionamiento automático) en **Active** (Activado).</span><span class="sxs-lookup"><span data-stu-id="789a9-200">Set **Auto-provision users** to **Active**.</span></span>

    <span data-ttu-id="789a9-201">h.</span><span class="sxs-lookup"><span data-stu-id="789a9-201">h.</span></span> <span data-ttu-id="789a9-202">Establezca **Auto-provision account type** (Tipo de cuenta de aprovisionamiento automático) en **Full User** (Usuario completo).</span><span class="sxs-lookup"><span data-stu-id="789a9-202">Set **Auto-provision account type** to **Full User**.</span></span>

    <span data-ttu-id="789a9-203">i.</span><span class="sxs-lookup"><span data-stu-id="789a9-203">i.</span></span> <span data-ttu-id="789a9-204">Establezca **Auto-provision security role** (Rol de seguridad de aprovisionamiento automático) y seleccione **Standard User with SAML** (Usuario estándar con SAML).</span><span class="sxs-lookup"><span data-stu-id="789a9-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="789a9-205">j.</span><span class="sxs-lookup"><span data-stu-id="789a9-205">j.</span></span> <span data-ttu-id="789a9-206">Establezca **Auto-provision security config** (Configuración de seguridad de aprovisionamiento automático) y seleccione **Standard User Configuration** (Configuración de usuario estándar).</span><span class="sxs-lookup"><span data-stu-id="789a9-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="789a9-207">k.</span><span class="sxs-lookup"><span data-stu-id="789a9-207">k.</span></span> <span data-ttu-id="789a9-208">En el cuadro **Atributo de correo electrónico**, escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="789a9-208">In the **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="789a9-209">l.</span><span class="sxs-lookup"><span data-stu-id="789a9-209">l.</span></span> <span data-ttu-id="789a9-210">En el cuadro de texto **Atributo de nombre**, escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="789a9-210">In the **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="789a9-211">m.</span><span class="sxs-lookup"><span data-stu-id="789a9-211">m.</span></span> <span data-ttu-id="789a9-212">En el cuadro de texto **Atributo de apellido**, escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="789a9-212">In the **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="789a9-213">n.</span><span class="sxs-lookup"><span data-stu-id="789a9-213">n.</span></span> <span data-ttu-id="789a9-214">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="789a9-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="789a9-215">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="789a9-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="789a9-216">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="789a9-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="789a9-217">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="789a9-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="789a9-218">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="789a9-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="789a9-219">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="789a9-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="789a9-221">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="789a9-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="789a9-222">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="789a9-222">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="789a9-224">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="789a9-224">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="789a9-226">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="789a9-226">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="789a9-228">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="789a9-228">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="789a9-230">a.</span><span class="sxs-lookup"><span data-stu-id="789a9-230">a.</span></span> <span data-ttu-id="789a9-231">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="789a9-231">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="789a9-232">b.</span><span class="sxs-lookup"><span data-stu-id="789a9-232">b.</span></span> <span data-ttu-id="789a9-233">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="789a9-233">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="789a9-234">c.</span><span class="sxs-lookup"><span data-stu-id="789a9-234">c.</span></span> <span data-ttu-id="789a9-235">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="789a9-235">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="789a9-236">d.</span><span class="sxs-lookup"><span data-stu-id="789a9-236">d.</span></span> <span data-ttu-id="789a9-237">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="789a9-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="789a9-238">Creación de un usuario de prueba de LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="789a9-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="789a9-239">En esta sección, creará un usuario llamado Britta Simon en LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="789a9-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="789a9-240">LockPath Keylight admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="789a9-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="789a9-241">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="789a9-241">There is no action item for you in this section.</span></span> <span data-ttu-id="789a9-242">Se crea un nuevo usuario al acceder a LockPath Keylight en caso de que el usuario todavía no exista.</span><span class="sxs-lookup"><span data-stu-id="789a9-242">A new user is created when accessing LockPath Keylight if the user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="789a9-243">Si necesita crear manualmente un usuario, es preciso que se ponga en contacto con el [equipo de soporte técnico de cliente de LockPath Keylight](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="789a9-243">If you need to create a user manually, you need to contact the [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="789a9-244">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="789a9-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="789a9-245">En esta sección, concederá acceso a Britta Simon a LockPath Keylight para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="789a9-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LockPath Keylight.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="789a9-247">**Para asignar a Britta Simon a LockPath Keylight, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="789a9-247">**To assign Britta Simon to LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="789a9-248">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="789a9-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="789a9-250">En la lista de aplicaciones, seleccione **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="789a9-250">In the applications list, select **LockPath Keylight**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="789a9-252">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="789a9-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="789a9-254">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="789a9-254">Click **Add** button.</span></span> <span data-ttu-id="789a9-255">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="789a9-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="789a9-257">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="789a9-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="789a9-258">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="789a9-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="789a9-259">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="789a9-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="789a9-260">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="789a9-260">Testing single sign-on</span></span>

<span data-ttu-id="789a9-261">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="789a9-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="789a9-262">Al hacer clic en el icono de LockPath Keylight en el Panel de acceso, debería iniciar sesión automáticamente en la aplicación LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="789a9-262">When you click the LockPath Keylight tile in the Access Panel, you should get automatically signed-on to your LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="789a9-263">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="789a9-263">Additional resources</span></span>

* [<span data-ttu-id="789a9-264">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="789a9-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="789a9-265">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="789a9-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png


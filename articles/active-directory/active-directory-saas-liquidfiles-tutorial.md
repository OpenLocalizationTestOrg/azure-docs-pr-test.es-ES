---
title: "Tutorial: Integración de Azure Active Directory con LiquidFiles | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y LiquidFiles."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cb517134-0b34-4a74-b40c-5a3223ca81b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: b858c6d26b78be4641a46b3453f53d103b512356
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a><span data-ttu-id="66de1-103">Tutorial: Integración de Azure Active Directory con LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="66de1-103">Tutorial: Azure Active Directory integration with LiquidFiles</span></span>

<span data-ttu-id="66de1-104">En este tutorial, obtendrá información sobre cómo integrar LiquidFiles con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="66de1-104">In this tutorial, you learn how to integrate LiquidFiles with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66de1-105">La integración de LiquidFiles con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="66de1-105">Integrating LiquidFiles with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="66de1-106">En Azure AD puede controlar quién tiene acceso a LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="66de1-106">You can control in Azure AD who has access to LiquidFiles</span></span>
- <span data-ttu-id="66de1-107">Puede permitir que los usuarios inicien sesión automáticamente en LiquidFiles (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66de1-107">You can enable your users to automatically get signed-on to LiquidFiles (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66de1-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="66de1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="66de1-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="66de1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66de1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="66de1-110">Prerequisites</span></span>

<span data-ttu-id="66de1-111">Para configurar la integración de Azure AD con LiquidFiles, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="66de1-111">To configure Azure AD integration with LiquidFiles, you need the following items:</span></span>

- <span data-ttu-id="66de1-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66de1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66de1-113">Una suscripción habilitada para el inicio de sesión único en LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="66de1-113">A LiquidFiles single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66de1-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="66de1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66de1-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="66de1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66de1-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="66de1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66de1-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66de1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66de1-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="66de1-118">Scenario description</span></span>
<span data-ttu-id="66de1-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="66de1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66de1-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="66de1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66de1-121">Incorporación de LiquidFiles desde la galería</span><span class="sxs-lookup"><span data-stu-id="66de1-121">Adding LiquidFiles from the gallery</span></span>
2. <span data-ttu-id="66de1-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66de1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-liquidfiles-from-the-gallery"></a><span data-ttu-id="66de1-123">Incorporación de LiquidFiles desde la galería</span><span class="sxs-lookup"><span data-stu-id="66de1-123">Adding LiquidFiles from the gallery</span></span>
<span data-ttu-id="66de1-124">Para configurar la integración de LiquidFiles en Azure AD, será preciso que agregue LiquidFiles desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="66de1-124">To configure the integration of LiquidFiles into Azure AD, you need to add LiquidFiles from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="66de1-125">**Para agregar LiquidFiles desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="66de1-125">**To add LiquidFiles from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="66de1-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="66de1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="66de1-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="66de1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="66de1-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="66de1-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="66de1-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66de1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="66de1-133">En el cuadro de búsqueda, escriba **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="66de1-133">In the search box, type **LiquidFiles**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_search.png)

5. <span data-ttu-id="66de1-135">En el panel de resultados, seleccione **LiquidFiles** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="66de1-135">In the results panel, select **LiquidFiles**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="66de1-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66de1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="66de1-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con LiquidFiles con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="66de1-138">In this section, you configure and test Azure AD single sign-on with LiquidFiles based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="66de1-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de LiquidFiles para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66de1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LiquidFiles is to a user in Azure AD.</span></span> <span data-ttu-id="66de1-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="66de1-140">In other words, a link relationship between an Azure AD user and the related user in LiquidFiles needs to be established.</span></span>

<span data-ttu-id="66de1-141">Para establecer la relación de vínculo, en LiquidFiles, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="66de1-141">In LiquidFiles, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="66de1-142">Para configurar y probar el inicio de sesión único de Azure AD con LiquidFiles, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="66de1-142">To configure and test Azure AD single sign-on with LiquidFiles, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="66de1-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="66de1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="66de1-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="66de1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66de1-145">**[Creación de un usuario de prueba de LiquidFiles](#creating-a-liquidfiles-test-user)**: para tener un homólogo de Britta Simon en LiquidFiles que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66de1-145">**[Creating a LiquidFiles test user](#creating-a-liquidfiles-test-user)** - to have a counterpart of Britta Simon in LiquidFiles that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="66de1-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66de1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="66de1-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="66de1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="66de1-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66de1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="66de1-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="66de1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LiquidFiles application.</span></span>

<span data-ttu-id="66de1-150">**Para configurar el inicio de sesión único de Azure AD con LiquidFiles, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="66de1-150">**To configure Azure AD single sign-on with LiquidFiles, perform the following steps:**</span></span>

1. <span data-ttu-id="66de1-151">En Azure Portal, en la página de integración de la aplicación **LiquidFiles**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="66de1-151">In the Azure portal, on the **LiquidFiles** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="66de1-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="66de1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_samlbase.png)

3. <span data-ttu-id="66de1-155">En la sección **Dominio y direcciones URL de LiquidFiles**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="66de1-155">On the **LiquidFiles Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_url.png)

    <span data-ttu-id="66de1-157">a.</span><span class="sxs-lookup"><span data-stu-id="66de1-157">a.</span></span> <span data-ttu-id="66de1-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<YOUR_SERVER_URL>/saml/init`.</span><span class="sxs-lookup"><span data-stu-id="66de1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>/saml/init`</span></span>

    <span data-ttu-id="66de1-159">b.</span><span class="sxs-lookup"><span data-stu-id="66de1-159">b.</span></span> <span data-ttu-id="66de1-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<YOUR_SERVER_URL>`</span><span class="sxs-lookup"><span data-stu-id="66de1-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>`</span></span>

    <span data-ttu-id="66de1-161">c.</span><span class="sxs-lookup"><span data-stu-id="66de1-161">c.</span></span> <span data-ttu-id="66de1-162">b.</span><span class="sxs-lookup"><span data-stu-id="66de1-162">b.</span></span> <span data-ttu-id="66de1-163">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<YOUR_SERVER_URL>/saml/consume`.</span><span class="sxs-lookup"><span data-stu-id="66de1-163">In the **Reply URL** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="66de1-164">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="66de1-164">These values are not real.</span></span> <span data-ttu-id="66de1-165">Actualícelos con la dirección URL de inicio de sesión, el identificador y la dirección URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="66de1-165">Update these values with the actual Sign-On URL, Identifier and, Reply URL.</span></span> <span data-ttu-id="66de1-166">Póngase en contacto con el [equipo de soporte de cliente de LiquidFiles](https://www.liquidfiles.com/support.html) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="66de1-166">Contact [LiquidFiles Client support team](https://www.liquidfiles.com/support.html) to get these values.</span></span> 
 
4. <span data-ttu-id="66de1-167">En la sección **Certificado de firma de SAML**, copie el valor de **HUELLA DIGITAL** del certificado.</span><span class="sxs-lookup"><span data-stu-id="66de1-167">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_certificate.png) 

5. <span data-ttu-id="66de1-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="66de1-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="66de1-171">En la sección **Configuración de LiquidFiles**, haga clic en **Configurar LiquidFiles** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="66de1-171">On the **LiquidFiles Configuration** section, click **Configure LiquidFiles** to open **Configure sign-on** window.</span></span> <span data-ttu-id="66de1-172">Copie la **dirección URL de cierre de sesión y la dirección URL del servicio de inicio de sesión único de SAML** de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="66de1-172">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_configure.png)
 
7. <span data-ttu-id="66de1-174">Inicie sesión en su sitio de la empresa de LiquidFiles como administrador.</span><span class="sxs-lookup"><span data-stu-id="66de1-174">Sign-on to your LiquidFiles company site as administrator.</span></span>

8. <span data-ttu-id="66de1-175">Haga clic en **Inicio de sesión único** en **Administración > Configuración** en el menú.</span><span class="sxs-lookup"><span data-stu-id="66de1-175">Click **Single Sign-On** in the **Admin > Configuration** from the menu.</span></span>

9. <span data-ttu-id="66de1-176">En la página **Configuración de inicio de sesión único**, siga estos pasos</span><span class="sxs-lookup"><span data-stu-id="66de1-176">On the **Single Sign-On Configuration** page, perform the following steps</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_single_01.png)

    <span data-ttu-id="66de1-178">a.</span><span class="sxs-lookup"><span data-stu-id="66de1-178">a.</span></span> <span data-ttu-id="66de1-179">Como **método de inicio de sesión único**, seleccione **SAML 2**.</span><span class="sxs-lookup"><span data-stu-id="66de1-179">As **Single Sign On Method**, select **SAML 2**.</span></span>

    <span data-ttu-id="66de1-180">b.</span><span class="sxs-lookup"><span data-stu-id="66de1-180">b.</span></span> <span data-ttu-id="66de1-181">En el cuadro de texto **IDP Login URL** (Dirección URL de inicio de sesión de IDP), pegue el valor de la **dirección URL de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="66de1-181">In the **IDP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="66de1-182">c.</span><span class="sxs-lookup"><span data-stu-id="66de1-182">c.</span></span> <span data-ttu-id="66de1-183">En el cuadro de texto **IDP Logout URL** (Dirección URL de cierre de sesión de IDP), pegue el valor de la **dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="66de1-183">In the **IDP Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="66de1-184">d.</span><span class="sxs-lookup"><span data-stu-id="66de1-184">d.</span></span> <span data-ttu-id="66de1-185">En el cuadro de texto **IDP Cert Fingerprint** (Huella digital del certificado de IDP), pegue el valor **THUMBPRINT** (Huella digital) que copió desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="66de1-185">In the **IDP Cert Fingerprint** textbox, paste the **THUMBPRINT** value which you have copied from Azure portal..</span></span>

    <span data-ttu-id="66de1-186">e.</span><span class="sxs-lookup"><span data-stu-id="66de1-186">e.</span></span> <span data-ttu-id="66de1-187">En el cuadro de texto Name Identifier Format (Formato de identificador de nombre), escriba el valor **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="66de1-187">In the Name Identifier Format textbox, type the value **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="66de1-188">f.</span><span class="sxs-lookup"><span data-stu-id="66de1-188">f.</span></span> <span data-ttu-id="66de1-189">En el cuadro de texto Authn Context (Contexto de autenticación), escriba el valor **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span><span class="sxs-lookup"><span data-stu-id="66de1-189">In the Authn Context textbox, type the value **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span></span>

    <span data-ttu-id="66de1-190">g.</span><span class="sxs-lookup"><span data-stu-id="66de1-190">g.</span></span> <span data-ttu-id="66de1-191">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="66de1-191">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="66de1-192">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="66de1-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="66de1-193">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="66de1-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="66de1-194">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66de1-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="66de1-195">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66de1-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="66de1-196">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="66de1-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="66de1-198">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="66de1-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="66de1-199">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="66de1-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="66de1-201">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="66de1-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="66de1-203">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66de1-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="66de1-205">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="66de1-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66de1-207">a.</span><span class="sxs-lookup"><span data-stu-id="66de1-207">a.</span></span> <span data-ttu-id="66de1-208">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="66de1-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66de1-209">b.</span><span class="sxs-lookup"><span data-stu-id="66de1-209">b.</span></span> <span data-ttu-id="66de1-210">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="66de1-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="66de1-211">c.</span><span class="sxs-lookup"><span data-stu-id="66de1-211">c.</span></span> <span data-ttu-id="66de1-212">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="66de1-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="66de1-213">d.</span><span class="sxs-lookup"><span data-stu-id="66de1-213">d.</span></span> <span data-ttu-id="66de1-214">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="66de1-214">Click **Create**.</span></span>
 
### <a name="creating-a-liquidfiles-test-user"></a><span data-ttu-id="66de1-215">Creación de un usuario de prueba de LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="66de1-215">Creating a LiquidFiles test user</span></span>

<span data-ttu-id="66de1-216">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="66de1-216">The objective of this section is to create a user called Britta Simon in LiquidFiles.</span></span> <span data-ttu-id="66de1-217">Colabore con el administrador del servidor de LiquidFiles para agregarse como usuario antes de iniciar sesión en la aplicación de LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="66de1-217">Work with your LiquidFiles server administrator to get yourself added as a user before logging in to your LiquidFiles application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="66de1-218">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66de1-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="66de1-219">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="66de1-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LiquidFiles.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="66de1-221">**Para asignar Britta Simon a LiquidFiles, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="66de1-221">**To assign Britta Simon to LiquidFiles, perform the following steps:**</span></span>

1. <span data-ttu-id="66de1-222">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="66de1-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="66de1-224">En la lista de aplicaciones, seleccione **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="66de1-224">In the applications list, select **LiquidFiles**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_app.png) 

3. <span data-ttu-id="66de1-226">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="66de1-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="66de1-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="66de1-228">Click **Add** button.</span></span> <span data-ttu-id="66de1-229">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="66de1-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="66de1-231">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="66de1-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="66de1-232">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="66de1-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66de1-233">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="66de1-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="66de1-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="66de1-234">Testing single sign-on</span></span>

<span data-ttu-id="66de1-235">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="66de1-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="66de1-236">Al hacer clic en el icono de LiquidFiles en el Panel de acceso, debe iniciar sesión automáticamente en su aplicación de LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="66de1-236">When you click the LiquidFiles tile in the Access Panel, you should get automatically signed-on to your LiquidFiles application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66de1-237">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="66de1-237">Additional resources</span></span>

* [<span data-ttu-id="66de1-238">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66de1-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66de1-239">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="66de1-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_203.png


---
title: "Tutorial: Integración de Azure Active Directory con Rightscale | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Rightscale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 222c4414a9f736a3589b4cdd0ed934696f6c31ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="2e74a-103">Tutorial: Integración de Azure Active Directory con Rightscale</span><span class="sxs-lookup"><span data-stu-id="2e74a-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="2e74a-104">En este tutorial, aprenderá a integrar Rightscale con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e74a-104">In this tutorial, you learn how to integrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e74a-105">Integrar Rightscale con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2e74a-105">Integrating Rightscale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2e74a-106">Puede controlar en Azure AD quién tiene acceso a Rightscale</span><span class="sxs-lookup"><span data-stu-id="2e74a-106">You can control in Azure AD who has access to Rightscale</span></span>
- <span data-ttu-id="2e74a-107">Puede permitir que los usuarios inicien sesión automáticamente en Rightscale (Inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e74a-107">You can enable your users to automatically get signed-on to Rightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2e74a-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2e74a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2e74a-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e74a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e74a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2e74a-110">Prerequisites</span></span>

<span data-ttu-id="2e74a-111">Para configurar la integración de Azure AD con Rightscale, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2e74a-111">To configure Azure AD integration with Rightscale, you need the following items:</span></span>

- <span data-ttu-id="2e74a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e74a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2e74a-113">Una suscripción habilitada para el inicio de sesión único en Rightscale</span><span class="sxs-lookup"><span data-stu-id="2e74a-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e74a-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2e74a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2e74a-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2e74a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2e74a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2e74a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2e74a-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e74a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e74a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2e74a-118">Scenario description</span></span>
<span data-ttu-id="2e74a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2e74a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2e74a-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="2e74a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e74a-121">Adición de Rightscale desde la galería</span><span class="sxs-lookup"><span data-stu-id="2e74a-121">Adding Rightscale from the gallery</span></span>
2. <span data-ttu-id="2e74a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e74a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-the-gallery"></a><span data-ttu-id="2e74a-123">Adición de Rightscale desde la galería</span><span class="sxs-lookup"><span data-stu-id="2e74a-123">Adding Rightscale from the gallery</span></span>
<span data-ttu-id="2e74a-124">Para configurar la integración de Rightscale en Azure AD, deberá agregar Rightscale desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="2e74a-124">To configure the integration of Rightscale into Azure AD, you need to add Rightscale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2e74a-125">**Para agregar Rightscale desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2e74a-125">**To add Rightscale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2e74a-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2e74a-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2e74a-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="2e74a-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e74a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="2e74a-133">En el cuadro de búsqueda, escriba **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-133">In the search box, type **Rightscale**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="2e74a-135">En el panel de resultados, seleccione **Rightscale** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2e74a-135">In the results panel, select **Rightscale**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2e74a-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e74a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2e74a-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Rightscale con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2e74a-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e74a-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de RightsScale para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e74a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Rightscale is to a user in Azure AD.</span></span> <span data-ttu-id="2e74a-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Rightscale.</span><span class="sxs-lookup"><span data-stu-id="2e74a-140">In other words, a link relationship between an Azure AD user and the related user in Rightscale needs to be established.</span></span>

<span data-ttu-id="2e74a-141">Para establecer la relación de vínculo, en Rightscale, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-141">In Rightscale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2e74a-142">Para configurar y probar el inicio de sesión único de Azure AD con Rightscale, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2e74a-142">To configure and test Azure AD single sign-on with Rightscale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2e74a-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="2e74a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2e74a-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e74a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2e74a-145">**[Creación de un usuario de prueba de Rightscale](#creating-a-rightscale-test-user)**: para tener un homólogo de Britta Simon en Rightscale que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e74a-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - to have a counterpart of Britta Simon in Rightscale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2e74a-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e74a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2e74a-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="2e74a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2e74a-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e74a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2e74a-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Rightscale.</span><span class="sxs-lookup"><span data-stu-id="2e74a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="2e74a-150">**Para configurar el inicio de sesión único de Azure AD con Rightscale, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2e74a-150">**To configure Azure AD single sign-on with Rightscale, perform the following steps:**</span></span>

1. <span data-ttu-id="2e74a-151">En Azure Portal, en la página de integración de la aplicación **Rightscale**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-151">In the Azure portal, on the **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="2e74a-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2e74a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="2e74a-155">En el **Rightscale dominio y las direcciones URL** sección, si desea volver a configurar la aplicación en **modo iniciado por IDP** no es necesario realizar los pasos porque la aplicación ya está integrada previamente con Azure.</span><span class="sxs-lookup"><span data-stu-id="2e74a-155">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **IDP initiated mode** you do not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="2e74a-157">En la sección **Dominio y direcciones URL de Rightscale**, si quiere configurar la aplicación en **SP initiated mode** (Modo iniciado por SP), realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2e74a-157">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="2e74a-159">a.</span><span class="sxs-lookup"><span data-stu-id="2e74a-159">a.</span></span> <span data-ttu-id="2e74a-160">Haga clic en la opción **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-160">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="2e74a-161">b.</span><span class="sxs-lookup"><span data-stu-id="2e74a-161">b.</span></span> <span data-ttu-id="2e74a-162">En el cuadro de texto **Dirección URL de inicio de sesión**, escriba una dirección URL similar a la siguiente: `https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="2e74a-162">In the **Sign On URL** textbox, type the URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="2e74a-163">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2e74a-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="2e74a-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2e74a-165">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="2e74a-167">En la sección **Configuración de Rightscale**, haga clic en **Configurar Rightscale** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-167">On the **Rightscale Configuration** section, click **Configure Rightscale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2e74a-168">Copie los valores de **SAML Entity ID y SAML Single Sign-On Service URL** (Identificador de entidad de SAML y Dirección URL del servicio de inicio de sesión único de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-168">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="2e74a-169">![Configuración del inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="2e74a-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="2e74a-170">Para configurar SSO para la aplicación, debe iniciar sesión en su inquilino de RightScale como administrador.</span><span class="sxs-lookup"><span data-stu-id="2e74a-170">To get SSO configured for your application, you need to sign-on to your RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="2e74a-171">a.</span><span class="sxs-lookup"><span data-stu-id="2e74a-171">a.</span></span> <span data-ttu-id="2e74a-172">En el menú de la parte superior, haga clic en la pestaña **Configuración** y seleccione **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="2e74a-174">b.</span><span class="sxs-lookup"><span data-stu-id="2e74a-174">b.</span></span> <span data-ttu-id="2e74a-175">Haga clic en el botón "**nuevo**" para agregar **sus proveedores de identidades SAML**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-175">Click the "**new**" button to add **Your SAML Identity Providers**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="2e74a-177">c.</span><span class="sxs-lookup"><span data-stu-id="2e74a-177">c.</span></span> <span data-ttu-id="2e74a-178">En el cuadro de texto **Nombre para mostrar**, escriba el nombre de la compañía.</span><span class="sxs-lookup"><span data-stu-id="2e74a-178">In the textbox of **Display Name**, input your company name.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="2e74a-180">d.</span><span class="sxs-lookup"><span data-stu-id="2e74a-180">d.</span></span> <span data-ttu-id="2e74a-181">Seleccione **Permitir SSO iniciado por RightScale con una sugerencia de detección** y escriba el **nombre de dominio** en el cuadro de texto siguiente.</span><span class="sxs-lookup"><span data-stu-id="2e74a-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in the below textbox.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="2e74a-183">e.</span><span class="sxs-lookup"><span data-stu-id="2e74a-183">e.</span></span> <span data-ttu-id="2e74a-184">Pegue el valor del **Dirección URL del servicio de inicio de sesión único de SAML** que copió de Azure Portal en **SAML SSO Endpoint** (Punto de conexión SSO de SAML) en Rightscale.</span><span class="sxs-lookup"><span data-stu-id="2e74a-184">Paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="2e74a-186">f.</span><span class="sxs-lookup"><span data-stu-id="2e74a-186">f.</span></span> <span data-ttu-id="2e74a-187">Pegue el valor del **identificador de entidad de SAML** que copió de Azure Portal en **SAML EntityID** (Identificador de entidad de SAML) en Rightscale.</span><span class="sxs-lookup"><span data-stu-id="2e74a-187">Paste the value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="2e74a-189">g.</span><span class="sxs-lookup"><span data-stu-id="2e74a-189">g.</span></span> <span data-ttu-id="2e74a-190">Haga clic en el botón **Explorador** para cargar el certificado que descargó de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2e74a-190">Click **Browser** button to upload the certificate which you downloaded from Azure portal.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="2e74a-192">h.</span><span class="sxs-lookup"><span data-stu-id="2e74a-192">h.</span></span> <span data-ttu-id="2e74a-193">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="2e74a-194">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2e74a-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2e74a-195">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2e74a-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2e74a-196">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2e74a-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2e74a-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e74a-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="2e74a-198">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2e74a-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="2e74a-200">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="2e74a-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2e74a-201">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2e74a-203">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2e74a-205">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e74a-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2e74a-207">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2e74a-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2e74a-209">a.</span><span class="sxs-lookup"><span data-stu-id="2e74a-209">a.</span></span> <span data-ttu-id="2e74a-210">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e74a-211">b.</span><span class="sxs-lookup"><span data-stu-id="2e74a-211">b.</span></span> <span data-ttu-id="2e74a-212">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e74a-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2e74a-213">c.</span><span class="sxs-lookup"><span data-stu-id="2e74a-213">c.</span></span> <span data-ttu-id="2e74a-214">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2e74a-215">d.</span><span class="sxs-lookup"><span data-stu-id="2e74a-215">d.</span></span> <span data-ttu-id="2e74a-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="2e74a-217">Creación de un usuario de prueba de Rightscale</span><span class="sxs-lookup"><span data-stu-id="2e74a-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="2e74a-218">En esta sección, creará un usuario denominado Britta Simon en RightScale.</span><span class="sxs-lookup"><span data-stu-id="2e74a-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="2e74a-219">Colabore con el [equipo de soporte técnico de Rightscale](mailto:support@rightscale.com) para agregar usuarios en la plataforma de Rightscale.</span><span class="sxs-lookup"><span data-stu-id="2e74a-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) to add the users in the RightScale platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2e74a-220">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e74a-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2e74a-221">En esta sección, concederá acceso a Britta Simon a Rightscale para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="2e74a-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rightscale.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="2e74a-223">**Para asignar a Britta Simon a Rightscale, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="2e74a-223">**To assign Britta Simon to Rightscale, perform the following steps:**</span></span>

1. <span data-ttu-id="2e74a-224">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2e74a-226">En la lista de aplicaciones, seleccione **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-226">In the applications list, select **Rightscale**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="2e74a-228">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="2e74a-230">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-230">Click **Add** button.</span></span> <span data-ttu-id="2e74a-231">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="2e74a-233">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="2e74a-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2e74a-234">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2e74a-235">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2e74a-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2e74a-236">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="2e74a-236">Testing single sign-on</span></span>

<span data-ttu-id="2e74a-237">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2e74a-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="2e74a-238">Al hacer clic en el icono de RightScale en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación RightScale.</span><span class="sxs-lookup"><span data-stu-id="2e74a-238">When you click the RightScale tile in the Access Panel, you should get automatically signed-on to your RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2e74a-239">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2e74a-239">Additional resources</span></span>

* [<span data-ttu-id="2e74a-240">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e74a-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e74a-241">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2e74a-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png


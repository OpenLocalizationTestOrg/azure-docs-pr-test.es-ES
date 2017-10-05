---
title: "Tutorial: Integración de Azure Active Directory con TalentLMS | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y TalentLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: f28d6fbfad9dae578a20db7218b7e3b174ed859c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="1d06c-103">Tutorial: integración de Azure Active Directory con TalentLMS</span><span class="sxs-lookup"><span data-stu-id="1d06c-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="1d06c-104">En este tutorial, aprenderá a integrar TalentLMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1d06c-104">In this tutorial, you learn how to integrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1d06c-105">Integrar TalentLMS con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="1d06c-105">Integrating TalentLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1d06c-106">En Azure AD se puede controlar quién tiene acceso a TalentLMS</span><span class="sxs-lookup"><span data-stu-id="1d06c-106">You can control in Azure AD who has access to TalentLMS</span></span>
- <span data-ttu-id="1d06c-107">Puede permitir que los usuarios inicien sesión automáticamente en TalentLMS (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d06c-107">You can enable your users to automatically get signed-on to TalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1d06c-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1d06c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1d06c-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1d06c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d06c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1d06c-110">Prerequisites</span></span>

<span data-ttu-id="1d06c-111">Para configurar la integración de Azure AD con TalentLMS, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1d06c-111">To configure Azure AD integration with TalentLMS, you need the following items:</span></span>

- <span data-ttu-id="1d06c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d06c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1d06c-113">Una suscripción habilitada para el inicio de sesión único en TalentLMS</span><span class="sxs-lookup"><span data-stu-id="1d06c-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1d06c-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1d06c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1d06c-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="1d06c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1d06c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1d06c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1d06c-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1d06c-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1d06c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="1d06c-118">Scenario description</span></span>
<span data-ttu-id="1d06c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="1d06c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1d06c-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="1d06c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1d06c-121">Incorporación de TalentLMS desde la galería</span><span class="sxs-lookup"><span data-stu-id="1d06c-121">Adding TalentLMS from the gallery</span></span>
2. <span data-ttu-id="1d06c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d06c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-the-gallery"></a><span data-ttu-id="1d06c-123">Incorporación de TalentLMS desde la galería</span><span class="sxs-lookup"><span data-stu-id="1d06c-123">Adding TalentLMS from the gallery</span></span>
<span data-ttu-id="1d06c-124">Para configurar la integración de TalentLMS en Azure AD, deberá agregar TalentLMS desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="1d06c-124">To configure the integration of TalentLMS into Azure AD, you need to add TalentLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1d06c-125">**Para agregar TalentLMS desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="1d06c-125">**To add TalentLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1d06c-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1d06c-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1d06c-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="1d06c-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1d06c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="1d06c-133">En el cuadro de búsqueda, escriba **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-133">In the search box, type **TalentLMS**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="1d06c-135">En el panel de resultados, seleccione **TalentLMS** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1d06c-135">In the results panel, select **TalentLMS**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1d06c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d06c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1d06c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con TalentLMS con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1d06c-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1d06c-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de TalentLMS para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d06c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TalentLMS is to a user in Azure AD.</span></span> <span data-ttu-id="1d06c-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="1d06c-140">In other words, a link relationship between an Azure AD user and the related user in TalentLMS needs to be established.</span></span>

<span data-ttu-id="1d06c-141">Para establecer la relación de vínculo, en TalentLMS, asigne el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-141">In TalentLMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1d06c-142">Para configurar y probar el inicio de sesión único de Azure AD con TalentLMS, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="1d06c-142">To configure and test Azure AD single sign-on with TalentLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1d06c-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="1d06c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1d06c-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1d06c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1d06c-145">**[Creación de un usuario de prueba de TalentLMS](#creating-a-talentlms-test-user)**: para tener un homólogo de Britta Simon en TalentLMS que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d06c-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - to have a counterpart of Britta Simon in TalentLMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1d06c-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d06c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1d06c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="1d06c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1d06c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d06c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1d06c-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="1d06c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="1d06c-150">**Para configurar el inicio de sesión único de Azure AD con TalentLMS, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1d06c-150">**To configure Azure AD single sign-on with TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="1d06c-151">En Azure Portal, en la página de integración de la aplicación **TalentLMS**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-151">In the Azure portal, on the **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="1d06c-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1d06c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="1d06c-155">En la sección **Dominio y direcciones URL de TalentLMS**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1d06c-155">On the **TalentLMS Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="1d06c-157">a.</span><span class="sxs-lookup"><span data-stu-id="1d06c-157">a.</span></span> <span data-ttu-id="1d06c-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenant-name>.TalentLMSapp.com`.</span><span class="sxs-lookup"><span data-stu-id="1d06c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="1d06c-159">b.</span><span class="sxs-lookup"><span data-stu-id="1d06c-159">b.</span></span> <span data-ttu-id="1d06c-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="1d06c-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1d06c-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="1d06c-161">These values are not real.</span></span> <span data-ttu-id="1d06c-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="1d06c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1d06c-163">Póngase en contacto con el [equipo de soporte técnico de TalentLMS](https://www.talentlms.com/contact) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="1d06c-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="1d06c-164">En la sección **Certificado de firma de SAML**, copie el valor de **HUELLA DIGITAL** del certificado.</span><span class="sxs-lookup"><span data-stu-id="1d06c-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="1d06c-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="1d06c-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1d06c-168">En la sección **Configuración de TalentLMS**, haga clic en **Configurar TalentLMS** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-168">On the **TalentLMS Configuration** section, click **Configure TalentLMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1d06c-169">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="1d06c-171">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de TalentLMS como administrador.</span><span class="sxs-lookup"><span data-stu-id="1d06c-171">In a different web browser window, log in to your TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="1d06c-172">En la sección **Account & Settings** (Cuenta y configuración), haga clic en la pestaña **Users** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="1d06c-172">In the **Account & Settings** section, click the **Users** tab.</span></span>
   
    <span data-ttu-id="1d06c-173">![Cuenta y configuración](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Cuenta y configuración")</span><span class="sxs-lookup"><span data-stu-id="1d06c-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="1d06c-174">Haga clic en **Inicio de sesión único (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="1d06c-175">En la sección Inicio de sesión único, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1d06c-175">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="1d06c-176">![Inicio de sesión único](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="1d06c-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="1d06c-177">a.</span><span class="sxs-lookup"><span data-stu-id="1d06c-177">a.</span></span> <span data-ttu-id="1d06c-178">En la lista **SSO integration type** (Tipo de integración de SSO), seleccione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-178">From the **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="1d06c-179">b.</span><span class="sxs-lookup"><span data-stu-id="1d06c-179">b.</span></span> <span data-ttu-id="1d06c-180">En el cuadro de texto **Identity provider (IDP)** (Proveedor de identidad [IDP]), pegue el valor del **identificador de entidad de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1d06c-180">In the **Identity provider (IDP)** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="1d06c-181">c.</span><span class="sxs-lookup"><span data-stu-id="1d06c-181">c.</span></span> <span data-ttu-id="1d06c-182">Pegue el valor de **Huella digital** de Azure Portal en el cuadro de texto de **Certificate fingerprint** (Huella digital de certificado).</span><span class="sxs-lookup"><span data-stu-id="1d06c-182">Paste the **Thumbprint** value from Azure portal into the **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="1d06c-183">d.</span><span class="sxs-lookup"><span data-stu-id="1d06c-183">d.</span></span>  <span data-ttu-id="1d06c-184">En el cuadro de texto **Remote sign-in URL** (Dirección URL de inicio de sesión remoto), pegue el valor de la **dirección URL de servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1d06c-184">In the **Remote sign-in URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="1d06c-185">e.</span><span class="sxs-lookup"><span data-stu-id="1d06c-185">e.</span></span> <span data-ttu-id="1d06c-186">En el cuadro de texto **Remote Log Out URL** (Dirección URL de cierre de sesión remoto), pegue el valor de **dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1d06c-186">In the **Remote sign-out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1d06c-187">f.</span><span class="sxs-lookup"><span data-stu-id="1d06c-187">f.</span></span> <span data-ttu-id="1d06c-188">Rellene lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1d06c-188">Fill in the following:</span></span> 

    * <span data-ttu-id="1d06c-189">En el cuadro de texto **TargetedID** (Id. dirigido), escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="1d06c-189">In the **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="1d06c-190">En el cuadro de texto **First name** (Nombre), escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="1d06c-190">In the **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="1d06c-191">En el cuadro de texto **Last name** (Apellidos), escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="1d06c-191">In the **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="1d06c-192">En el cuadro de texto **Email** (Correo electrónico), escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="1d06c-192">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="1d06c-193">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="1d06c-194">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1d06c-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1d06c-195">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1d06c-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1d06c-196">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1d06c-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1d06c-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d06c-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="1d06c-198">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1d06c-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="1d06c-200">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="1d06c-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1d06c-201">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1d06c-203">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1d06c-205">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1d06c-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1d06c-207">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="1d06c-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1d06c-209">a.</span><span class="sxs-lookup"><span data-stu-id="1d06c-209">a.</span></span> <span data-ttu-id="1d06c-210">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1d06c-211">b.</span><span class="sxs-lookup"><span data-stu-id="1d06c-211">b.</span></span> <span data-ttu-id="1d06c-212">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1d06c-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1d06c-213">c.</span><span class="sxs-lookup"><span data-stu-id="1d06c-213">c.</span></span> <span data-ttu-id="1d06c-214">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1d06c-215">d.</span><span class="sxs-lookup"><span data-stu-id="1d06c-215">d.</span></span> <span data-ttu-id="1d06c-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="1d06c-217">Creación de un usuario de prueba de TalentLMS</span><span class="sxs-lookup"><span data-stu-id="1d06c-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="1d06c-218">Para permitir que los usuarios de Azure AD inicien sesión en TalentLMS, deben aprovisionarse en TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="1d06c-218">To enable Azure AD users to log in to TalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="1d06c-219">En el caso de TalentLMS, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="1d06c-219">In the case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="1d06c-220">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="1d06c-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="1d06c-221">Inicie sesión en su inquilino de **TalentLMS** .</span><span class="sxs-lookup"><span data-stu-id="1d06c-221">Log in to your **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="1d06c-222">Haga clic en **Users** (Usuarios) y, luego, en **Add User** (Agregar usuario).</span><span class="sxs-lookup"><span data-stu-id="1d06c-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="1d06c-223">En la página del cuadro de diálogo **Agregar usuario** , realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="1d06c-223">On the **Add user** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="1d06c-224">![Agregar usuario](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="1d06c-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="1d06c-225">a.</span><span class="sxs-lookup"><span data-stu-id="1d06c-225">a.</span></span> <span data-ttu-id="1d06c-226">En el cuadro de texto **Nombre**, escriba el nombre de usuario, en este caso **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-226">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="1d06c-227">b.</span><span class="sxs-lookup"><span data-stu-id="1d06c-227">b.</span></span> <span data-ttu-id="1d06c-228">En el cuadro de texto **Apellidos**, escriba el apellido del usuario, en este caso **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-228">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="1d06c-229">c.</span><span class="sxs-lookup"><span data-stu-id="1d06c-229">c.</span></span> <span data-ttu-id="1d06c-230">En el cuadro de texto **Email address** (Dirección de correo electrónico), escriba el correo electrónico del usuario, en este caso, **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-230">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="1d06c-231">d.</span><span class="sxs-lookup"><span data-stu-id="1d06c-231">d.</span></span> <span data-ttu-id="1d06c-232">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="1d06c-233">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de TalentLMS ofrecida por TalentLMS para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="1d06c-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1d06c-234">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d06c-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1d06c-235">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="1d06c-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TalentLMS.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="1d06c-237">**Para asignar Britta Simon a TalentLMS, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1d06c-237">**To assign Britta Simon to TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="1d06c-238">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="1d06c-240">En la lista de aplicaciones, seleccione **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-240">In the applications list, select **TalentLMS**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="1d06c-242">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="1d06c-244">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-244">Click **Add** button.</span></span> <span data-ttu-id="1d06c-245">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="1d06c-247">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="1d06c-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1d06c-248">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1d06c-249">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1d06c-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1d06c-250">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="1d06c-250">Testing single sign-on</span></span>

<span data-ttu-id="1d06c-251">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1d06c-251">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1d06c-252">Al hacer clic en el icono de TalentLMS en el panel de acceso, debería iniciar sesión automáticamente en su aplicación TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="1d06c-252">When you click the TalentLMS tile in the Access Panel, you should get automatically signed-on to your TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1d06c-253">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1d06c-253">Additional resources</span></span>

* [<span data-ttu-id="1d06c-254">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d06c-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1d06c-255">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1d06c-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png


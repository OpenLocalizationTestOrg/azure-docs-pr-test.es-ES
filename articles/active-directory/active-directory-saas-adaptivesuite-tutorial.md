---
title: "Tutorial: Integración de Azure Active Directory con Adaptive Suite | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Adaptive Suite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 5d7ba2f4c7d814e3aaa1bf804ddc5030380ccb2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="c0da0-103">Tutorial: Integración de Azure Active Directory con Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="c0da0-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="c0da0-104">En este tutorial, aprenderá a integrar Adaptive Suite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0da0-104">In this tutorial, you learn how to integrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0da0-105">La integración de Adaptive Suite con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c0da0-105">Integrating Adaptive Suite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c0da0-106">Puede controlar en Azure AD quién tiene acceso a Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="c0da0-106">You can control in Azure AD who has access to Adaptive Suite</span></span>
- <span data-ttu-id="c0da0-107">Puede permitir que los usuarios inicien sesión automáticamente en Adaptive Suite (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0da0-107">You can enable your users to automatically get signed-on to Adaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0da0-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c0da0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c0da0-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0da0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0da0-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c0da0-110">Prerequisites</span></span>

<span data-ttu-id="c0da0-111">Para configurar la integración de Azure AD con Adaptive Suite, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c0da0-111">To configure Azure AD integration with Adaptive Suite, you need the following items:</span></span>

- <span data-ttu-id="c0da0-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0da0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0da0-113">Una suscripción habilitada para el inicio de sesión único en Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="c0da0-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0da0-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c0da0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0da0-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c0da0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0da0-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c0da0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0da0-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0da0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0da0-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c0da0-118">Scenario description</span></span>
<span data-ttu-id="c0da0-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c0da0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0da0-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="c0da0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0da0-121">Incorporación de Adaptive Suite desde la Galería</span><span class="sxs-lookup"><span data-stu-id="c0da0-121">Adding Adaptive Suite from the gallery</span></span>
2. <span data-ttu-id="c0da0-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0da0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-the-gallery"></a><span data-ttu-id="c0da0-123">Incorporación de Adaptive Suite desde la Galería</span><span class="sxs-lookup"><span data-stu-id="c0da0-123">Adding Adaptive Suite from the gallery</span></span>
<span data-ttu-id="c0da0-124">Para configurar la integración de Adaptive Suite en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="c0da0-124">To configure the integration of Adaptive Suite into Azure AD, you need to add Adaptive Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c0da0-125">**Para agregar Adaptive Suite desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="c0da0-125">**To add Adaptive Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c0da0-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0da0-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c0da0-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c0da0-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c0da0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c0da0-133">En el cuadro de búsqueda, escriba **Adaptive Suite**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-133">In the search box, type **Adaptive Suite**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="c0da0-135">En el panel de resultados, seleccione **Adaptive Suite** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0da0-135">In the results panel, select **Adaptive Suite**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0da0-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0da0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0da0-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Adaptive Suite con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0da0-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c0da0-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Adaptive Suite para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0da0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adaptive Suite is to a user in Azure AD.</span></span> <span data-ttu-id="c0da0-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario asociado en Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="c0da0-140">In other words, a link relationship between an Azure AD user and the related user in Adaptive Suite needs to be established.</span></span>

<span data-ttu-id="c0da0-141">Para establecer la relación de vínculo, en Adaptive Suite, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-141">In Adaptive Suite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c0da0-142">Para configurar y probar el inicio de sesión único de Azure AD con Adaptive Suite, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c0da0-142">To configure and test Azure AD single sign-on with Adaptive Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c0da0-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="c0da0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c0da0-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0da0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0da0-145">**[Creación de un usuario de prueba de Adaptive Suite](#creating-an-adaptive-suite-test-user)**: para tener un homólogo de Britta Simon en Adaptive Suite vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0da0-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - to have a counterpart of Britta Simon in Adaptive Suite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0da0-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0da0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0da0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c0da0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0da0-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0da0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0da0-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="c0da0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="c0da0-150">**Para configurar el inicio de sesión único de Azure AD con Adaptive Suite, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c0da0-150">**To configure Azure AD single sign-on with Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="c0da0-151">En Azure Portal, en la página de integración de la aplicación **Adaptive Suite**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-151">In the Azure portal, on the **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c0da0-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c0da0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="c0da0-155">En la sección **Adaptive Suite Domain and URLs** (Dominio y direcciones URL de Adaptive Suite), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c0da0-155">On the **Adaptive Suite Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="c0da0-157">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`.</span><span class="sxs-lookup"><span data-stu-id="c0da0-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="c0da0-158">Puede obtener este valor de la página **SAML SSO Settings** (Configuración SSO de SAML) de Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="c0da0-158">You can get this value from the Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="c0da0-159">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c0da0-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="c0da0-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c0da0-161">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c0da0-163">En la sección **Adaptive Suite Configuration** (Configuración de Adaptive Suite), haga clic en **Configure Adaptive Suite** (Configurar Adaptive Suite) para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-163">On the **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c0da0-164">Copie los valores de **SAML Entity ID y SAML Single Sign-On Service URL** (Identificador de entidad de SAML y URL del servicio de inicio de sesión único de SAML) de la sección de **referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="c0da0-166">En otra ventana del explorador web, inicie sesión en el sitio de Adaptive Suite de la compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="c0da0-166">In a different web browser window, log in to your Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="c0da0-167">Vaya a **Administración**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-167">Go to **Admin**.</span></span>
   
    <span data-ttu-id="c0da0-168">![Administración](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="c0da0-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="c0da0-169">En la sección **Users and Roles** (Usuarios y roles), haga clic en **Manage SAML SSO Settings** (Administrar configuración de SSO de SAML).</span><span class="sxs-lookup"><span data-stu-id="c0da0-169">In the **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="c0da0-170">![Manage SAML SSO Settings (Administrar configuración de SSO de SAML)](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings (Administrar configuración de SSO de SAML)")</span><span class="sxs-lookup"><span data-stu-id="c0da0-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="c0da0-171">En la página **SAML SSO Settings** (Configuración de SSO de SAML), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c0da0-171">On the **SAML SSO Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="c0da0-172">![SAML SSO Settings (Configuración de SSO de) SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings (Configuración de SSO de) SAML")</span><span class="sxs-lookup"><span data-stu-id="c0da0-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="c0da0-173">a.</span><span class="sxs-lookup"><span data-stu-id="c0da0-173">a.</span></span> <span data-ttu-id="c0da0-174">En el cuadro de texto **Identity provider name** (Nombre del proveedor de identidades), escriba el nombre de la configuración.</span><span class="sxs-lookup"><span data-stu-id="c0da0-174">In the **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="c0da0-175">b.</span><span class="sxs-lookup"><span data-stu-id="c0da0-175">b.</span></span> <span data-ttu-id="c0da0-176">Pegue el valor del **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal en el cuadro de texto **Identity Provider Entity ID** (Id. de entidad del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="c0da0-176">Paste the **SAML Entity ID** value copied from Azure portal into the **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="c0da0-177">c.</span><span class="sxs-lookup"><span data-stu-id="c0da0-177">c.</span></span> <span data-ttu-id="c0da0-178">Pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) que copió de Azure Portal en el cuadro de texto **Identity provider SSO URL** (Dirección URL de SSO del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="c0da0-178">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="c0da0-179">d.</span><span class="sxs-lookup"><span data-stu-id="c0da0-179">d.</span></span> <span data-ttu-id="c0da0-180">Pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) que copió de Azure Portal en el cuadro de texto **Custom logout URL** (Dirección URL de cierre de sesión personalizada).</span><span class="sxs-lookup"><span data-stu-id="c0da0-180">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="c0da0-181">e.</span><span class="sxs-lookup"><span data-stu-id="c0da0-181">e.</span></span> <span data-ttu-id="c0da0-182">Para cargar el certificado descargado, haga clic en **Choose file**(Elegir archivo).</span><span class="sxs-lookup"><span data-stu-id="c0da0-182">To upload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="c0da0-183">f.</span><span class="sxs-lookup"><span data-stu-id="c0da0-183">f.</span></span> <span data-ttu-id="c0da0-184">Seleccione las opciones siguientes en cada caso:</span><span class="sxs-lookup"><span data-stu-id="c0da0-184">Select the following, for:</span></span>
    * <span data-ttu-id="c0da0-185">En **SAML user id** (identificador de usuario de SAML), seleccione **User’s Adaptive Insights user name** (Nombre de usuario de Adaptive Insights del usuario).</span><span class="sxs-lookup"><span data-stu-id="c0da0-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="c0da0-186">En **SAML user id location** (Ubicación del id. de usuario de SAML), seleccione **User id in NameID of Subject** (identificador de usuario en NameID del tema).</span><span class="sxs-lookup"><span data-stu-id="c0da0-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="c0da0-187">En **SAML NameID format** (Formato de NameID de SAML), seleccione **Email address** (Dirección de correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="c0da0-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="c0da0-188">En **Enable SAML** (Habilitar SAML), seleccione **Allow SAML SSO and direct Adaptive Insights login** (Permitir inicio de sesión único de SAML e inicio de sesión directo de Adaptive Insights).</span><span class="sxs-lookup"><span data-stu-id="c0da0-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="c0da0-189">g.</span><span class="sxs-lookup"><span data-stu-id="c0da0-189">g.</span></span> <span data-ttu-id="c0da0-190">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c0da0-191">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0da0-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c0da0-192">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c0da0-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c0da0-193">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0da0-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0da0-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0da0-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0da0-195">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c0da0-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c0da0-197">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="c0da0-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c0da0-198">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0da0-200">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0da0-202">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c0da0-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0da0-204">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="c0da0-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0da0-206">a.</span><span class="sxs-lookup"><span data-stu-id="c0da0-206">a.</span></span> <span data-ttu-id="c0da0-207">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0da0-208">b.</span><span class="sxs-lookup"><span data-stu-id="c0da0-208">b.</span></span> <span data-ttu-id="c0da0-209">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0da0-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0da0-210">c.</span><span class="sxs-lookup"><span data-stu-id="c0da0-210">c.</span></span> <span data-ttu-id="c0da0-211">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c0da0-212">d.</span><span class="sxs-lookup"><span data-stu-id="c0da0-212">d.</span></span> <span data-ttu-id="c0da0-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="c0da0-214">Creación de un usuario de prueba de Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="c0da0-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="c0da0-215">Para permitir que los usuarios de Azure AD inicien sesión en Adaptive Suite, deben aprovisionarse en este último.</span><span class="sxs-lookup"><span data-stu-id="c0da0-215">To enable Azure AD users to log in to Adaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="c0da0-216">En el caso de Adaptive Suite, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="c0da0-216">In the case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="c0da0-217">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="c0da0-217">**To configure user provisioning, perform the following steps:**</span></span> 

1. <span data-ttu-id="c0da0-218">Inicie sesión en el sitio de la compañía de **Adaptive Suite** como administrador.</span><span class="sxs-lookup"><span data-stu-id="c0da0-218">Log in to your **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="c0da0-219">Vaya a **Administración**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-219">Go to **Admin**.</span></span>
   
   <span data-ttu-id="c0da0-220">![Administración](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="c0da0-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="c0da0-221">En la sección **Users and Roles** (Usuarios y roles), haga clic en **Add User** (Agregar usuario).</span><span class="sxs-lookup"><span data-stu-id="c0da0-221">In the **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="c0da0-222">![Agregar usuario](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="c0da0-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="c0da0-223">En la sección **Nuevo usuario** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c0da0-223">In the **New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="c0da0-224">![Enviar](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Enviar")</span><span class="sxs-lookup"><span data-stu-id="c0da0-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="c0da0-225">a.</span><span class="sxs-lookup"><span data-stu-id="c0da0-225">a.</span></span> <span data-ttu-id="c0da0-226">Escriba el **nombre**, el **inicio de sesión**, la **dirección de correo electrónico** y la **contraseña** o de un usuario válido de Azure Active Directory que quiera aprovisionar en los cuadros de texto relacionados.</span><span class="sxs-lookup"><span data-stu-id="c0da0-226">Type the **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want to provision into the related textboxes.</span></span>
  
   <span data-ttu-id="c0da0-227">b.</span><span class="sxs-lookup"><span data-stu-id="c0da0-227">b.</span></span> <span data-ttu-id="c0da0-228">Seleccione un **Role**(rol).</span><span class="sxs-lookup"><span data-stu-id="c0da0-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="c0da0-229">c.</span><span class="sxs-lookup"><span data-stu-id="c0da0-229">c.</span></span> <span data-ttu-id="c0da0-230">Haga clic en **Submit**(Enviar).</span><span class="sxs-lookup"><span data-stu-id="c0da0-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="c0da0-231">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Adaptive Suite ofrecida por Adaptive Suite para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="c0da0-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c0da0-232">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0da0-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c0da0-233">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="c0da0-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adaptive Suite.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c0da0-235">**Para asignar Britta Simon a Adaptive Suite, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c0da0-235">**To assign Britta Simon to Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="c0da0-236">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c0da0-238">En la lista de aplicaciones, seleccione **Adaptive Suite**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-238">In the applications list, select **Adaptive Suite**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="c0da0-240">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c0da0-242">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-242">Click **Add** button.</span></span> <span data-ttu-id="c0da0-243">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c0da0-245">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="c0da0-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c0da0-246">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0da0-247">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c0da0-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0da0-248">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c0da0-248">Testing single sign-on</span></span>

<span data-ttu-id="c0da0-249">El objetivo de esta sección es probar la configuración del inicio de sesión único de Microsoft Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c0da0-249">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="c0da0-250">Al hacer clic en el icono Adaptive Suite en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="c0da0-250">When you click the Adaptive Suite tile in the Access Panel, you should get automatically signed-on to your Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c0da0-251">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c0da0-251">Additional resources</span></span>

* [<span data-ttu-id="c0da0-252">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0da0-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0da0-253">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c0da0-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png


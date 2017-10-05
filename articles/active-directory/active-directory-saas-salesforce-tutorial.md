---
title: "Tutorial: Integración de Azure Active Directory con Salesforce | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 639e40ca7e406a1726033e9f5c5363c289087589
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="c91ff-103">Tutorial: Integración de Azure Active Directory con Salesforce</span><span class="sxs-lookup"><span data-stu-id="c91ff-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="c91ff-104">En este tutorial, aprenderá a integrar Salesforce con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c91ff-104">In this tutorial, you learn how to integrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c91ff-105">La integración de Salesforce con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c91ff-105">Integrating Salesforce with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c91ff-106">Puede controlar en Azure AD quién tiene acceso a Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c91ff-106">You can control in Azure AD who has access to Salesforce</span></span>
- <span data-ttu-id="c91ff-107">Puede permitir que los usuarios inicien sesión automáticamente en Salesforce (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c91ff-107">You can enable your users to automatically get signed-on to Salesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c91ff-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c91ff-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c91ff-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c91ff-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c91ff-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c91ff-110">Prerequisites</span></span>

<span data-ttu-id="c91ff-111">Para configurar la integración de Azure AD con Salesforce, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c91ff-111">To configure Azure AD integration with Salesforce, you need the following items:</span></span>

- <span data-ttu-id="c91ff-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c91ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c91ff-113">Una suscripción habilitada para el inicio de sesión único en Salesforce</span><span class="sxs-lookup"><span data-stu-id="c91ff-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c91ff-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c91ff-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c91ff-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c91ff-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c91ff-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c91ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c91ff-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c91ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c91ff-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c91ff-118">Scenario description</span></span>
<span data-ttu-id="c91ff-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c91ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c91ff-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="c91ff-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c91ff-121">Adición de Salesforce desde la galería</span><span class="sxs-lookup"><span data-stu-id="c91ff-121">Adding Salesforce from the gallery</span></span>
2. <span data-ttu-id="c91ff-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c91ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-the-gallery"></a><span data-ttu-id="c91ff-123">Adición de Salesforce desde la galería</span><span class="sxs-lookup"><span data-stu-id="c91ff-123">Adding Salesforce from the gallery</span></span>
<span data-ttu-id="c91ff-124">Para configurar la integración de Salesforce en Azure AD, deberá agregar Salesforce desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="c91ff-124">To configure the integration of Salesforce into Azure AD, you need to add Salesforce from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c91ff-125">**Para agregar Salesforce desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c91ff-125">**To add Salesforce from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c91ff-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c91ff-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c91ff-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c91ff-131">Haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c91ff-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c91ff-133">En el cuadro de búsqueda, escriba **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-133">In the search box, type **Salesforce**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="c91ff-135">En el panel de resultados, seleccione **Salesforce** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c91ff-135">In the results panel, select **Salesforce**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c91ff-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c91ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c91ff-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Salesforce con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c91ff-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c91ff-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Salesforce para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c91ff-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce is to a user in Azure AD.</span></span> <span data-ttu-id="c91ff-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c91ff-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce needs to be established.</span></span>

<span data-ttu-id="c91ff-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c91ff-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce.</span></span>

<span data-ttu-id="c91ff-142">Para configurar y probar el inicio de sesión único de Azure AD con Salesforce, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c91ff-142">To configure and test Azure AD single sign-on with Salesforce, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c91ff-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="c91ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c91ff-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c91ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c91ff-145">**[Creación de un usuario de prueba en Ssalesforce](#creating-a-salesforce-test-user)**: el objetivo es tener un homólogo de Britta Simon en Salesforce que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c91ff-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - to have a counterpart of Britta Simon in Salesforce that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c91ff-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c91ff-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c91ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c91ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c91ff-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c91ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c91ff-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c91ff-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="c91ff-150">**Para configurar el inicio de sesión único de Azure AD con Salesforce, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c91ff-150">**To configure Azure AD single sign-on with Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="c91ff-151">En la página de integración de la aplicación **Salesforce** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-151">In the Azure portal, on the **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c91ff-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c91ff-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="c91ff-155">En la sección **Dominio y direcciones URL de Salesforce**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c91ff-155">On the **Salesforce Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="c91ff-157">En el cuadro de texto **URL de inicio de sesión**, escriba el valor con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="c91ff-157">In the **Sign-on URL** textbox, type the value using the following pattern:</span></span> 
   * <span data-ttu-id="c91ff-158">Cuenta de empresa: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="c91ff-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="c91ff-159">Cuenta de desarrollador: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="c91ff-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c91ff-160">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="c91ff-160">These values are not the real.</span></span> <span data-ttu-id="c91ff-161">Debe actualizarlos con la dirección de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="c91ff-161">Update these values with the actual Sign-on URL.</span></span> <span data-ttu-id="c91ff-162">Póngase en contacto con el [equipo de atención al cliente de Salesforce](https://help.salesforce.com/support) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="c91ff-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="c91ff-163">En la sección **Certificado de firma de SAML**, haga clic en **Certificado** y, a continuación, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c91ff-163">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="c91ff-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c91ff-165">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c91ff-167">En la sección **Configuración de Salesforce**, haga clic en **Configurar Salesforce** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-167">On the **Salesforce Configuration** section, click **Configure Salesforce** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c91ff-168">Copie **SAML Entity ID and SAML Single Sign-On Service URL** (URL del servicio de inicio de sesión único de SAML e Identificador de entidad de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-168">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    <span data-ttu-id="c91ff-169">![Configuración del inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="c91ff-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="c91ff-170">Abra una nueva pestaña en el explorador e inicie sesión en su cuenta de administrador de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c91ff-170">Open a new tab in your browser and log in to your Salesforce administrator account.</span></span>

8.  <span data-ttu-id="c91ff-171">En el panel de navegación **Administrador**, haga clic en **Controles de seguridad** para expandir la sección relacionada.</span><span class="sxs-lookup"><span data-stu-id="c91ff-171">Under the **Administrator** navigation pane, click **Security Controls** to expand the related section.</span></span> <span data-ttu-id="c91ff-172">A continuación, haga clic en **Configuración de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-172">Then click **Single Sign-On Settings**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="c91ff-174">En la página **Configuración de inicio de sesión único**, haga clic en el botón **Editar**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-174">On the **Single Sign-On Settings** page, click the **Edit** button.</span></span>
    <span data-ttu-id="c91ff-175">![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="c91ff-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="c91ff-176">Si no puede habilitar la configuración de inicio de sesión único para su cuenta de Salesforce, puede que necesite ponerse en contacto con el [equipo de soporte técnico de Salesforce](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="c91ff-176">If you are unable to enable Single Sign-On settings for your Salesforce account, you may need to contact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="c91ff-177">Seleccione **SAML habilitado** y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="c91ff-179">Para establecer la configuración de inicio de sesión único de SAML, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-179">To configure your SAML single sign-on settings, click **New**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="c91ff-181">En la página **Edición de la configuración de inicio de sesión único de SAML** , realice las siguientes configuraciones:</span><span class="sxs-lookup"><span data-stu-id="c91ff-181">On the **SAML Single Sign-On Setting Edit** page, make the following configurations:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="c91ff-183">a.</span><span class="sxs-lookup"><span data-stu-id="c91ff-183">a.</span></span> <span data-ttu-id="c91ff-184">En el campo **Nombre** , escriba un nombre descriptivo para esta configuración.</span><span class="sxs-lookup"><span data-stu-id="c91ff-184">For the **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="c91ff-185">Si se proporciona un valor para **Name** (Nombre), se completa automáticamente el cuadro de texto **API Name** (Nombre de API).</span><span class="sxs-lookup"><span data-stu-id="c91ff-185">Providing a value for **Name** automatically populate the **API Name** textbox.</span></span>

    <span data-ttu-id="c91ff-186">b.</span><span class="sxs-lookup"><span data-stu-id="c91ff-186">b.</span></span> <span data-ttu-id="c91ff-187">Pegue el valor **SMAL Entity ID** (Id. de entidad de SAML) en el campo **Issuer** (Emisor) de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c91ff-187">Paste **SMAL Entity ID** value into the **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="c91ff-188">c.</span><span class="sxs-lookup"><span data-stu-id="c91ff-188">c.</span></span> <span data-ttu-id="c91ff-189">En el **Cuadro de texto de identificador de entidades**, escriba el nombre de dominio de Salesforce con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="c91ff-189">In the **Entity Id textbox**, type your Salesforce domain name using the following pattern:</span></span>
      
      * <span data-ttu-id="c91ff-190">Cuenta de empresa: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="c91ff-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="c91ff-191">Cuenta de desarrollador: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="c91ff-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="c91ff-192">d.</span><span class="sxs-lookup"><span data-stu-id="c91ff-192">d.</span></span> <span data-ttu-id="c91ff-193">Haga clic en **Browse** (Examinar) o **Choose File** (Elegir archivo) para abrir el cuadro de diálogo **Choose File to Upload** (Elegir archivos para cargar), seleccione el certificado de Salesforce y haga clic en **Open** (Abrir) para cargar el certificado.</span><span class="sxs-lookup"><span data-stu-id="c91ff-193">Click **Browse** or **Choose File** to open the **Choose File to Upload** dialog, select your Salesforce certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="c91ff-194">e.</span><span class="sxs-lookup"><span data-stu-id="c91ff-194">e.</span></span> <span data-ttu-id="c91ff-195">En **SAML Identity Type** (Tipo de identidad de SAML), seleccione **Assertion contains User's salesforce.com username** (La aserción contiene el nombre de usuario de salesforce.com del usuario).</span><span class="sxs-lookup"><span data-stu-id="c91ff-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="c91ff-196">f.</span><span class="sxs-lookup"><span data-stu-id="c91ff-196">f.</span></span> <span data-ttu-id="c91ff-197">En **SAML Identity Location** (Ubicación de identidad de SAML), seleccione **Identity is in the NameIdentifier element of the Subject statement** (La identidad está en el elemento NameIdentifier de la instrucción de asunto).</span><span class="sxs-lookup"><span data-stu-id="c91ff-197">For **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**</span></span>

    <span data-ttu-id="c91ff-198">g.</span><span class="sxs-lookup"><span data-stu-id="c91ff-198">g.</span></span> <span data-ttu-id="c91ff-199">Pegue la **URL de servicio de inicio de sesión** en el campo **Identity Provider Login URL** (URL de inicio de sesión del proveedor de identidades) de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c91ff-199">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="c91ff-200">h.</span><span class="sxs-lookup"><span data-stu-id="c91ff-200">h.</span></span> <span data-ttu-id="c91ff-201">En **Service Provider Initiated Request Binding** (Vinculación de solicitud iniciada del proveedor de servicios), seleccione **HTTP Redirect** (Redirección HTTP).</span><span class="sxs-lookup"><span data-stu-id="c91ff-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="c91ff-202">i.</span><span class="sxs-lookup"><span data-stu-id="c91ff-202">i.</span></span> <span data-ttu-id="c91ff-203">Por último, haga clic en **Guardar** para aplicar la configuración de inicio de sesión único de SAML.</span><span class="sxs-lookup"><span data-stu-id="c91ff-203">Finally, click **Save** to apply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="c91ff-204">En el panel de navegación izquierdo de Salesforce, haga clic en **Domain Management** (Administración de dominios) para expandir la sección relacionada y haga clic en **My Domain** (Mi dominio).</span><span class="sxs-lookup"><span data-stu-id="c91ff-204">On the left navigation pane in Salesforce, click **Domain Management** to expand the related section, and then click **My Domain**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="c91ff-206">Desplácese hacia abajo hasta la sección **Authentication Configuration** (Configuración de autenticación) y haga clic en el botón **Edit** (Editar).</span><span class="sxs-lookup"><span data-stu-id="c91ff-206">Scroll down to the **Authentication Configuration** section, and click the **Edit** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="c91ff-208">En la sección **Authentication Service** (Servicio de autenticación), seleccione el nombre descriptivo de la configuración de SSO de SAML y haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="c91ff-208">In the **Authentication Service** section, select the friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="c91ff-210">Si se selecciona más de un servicio de autenticación, cuando los usuarios intentan realizar un inicio de sesión único para el entorno Salesforce, se les pedirá que seleccionen el servicio de autenticación con el que les gustaría iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="c91ff-210">If more than one authentication service is selected, users are prompted to select which authentication service they like to sign in with while initiating single sign-on to your Salesforce environment.</span></span> <span data-ttu-id="c91ff-211">Si no desea que esto ocurra, **deje sin activar todos los demás servicios de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-211">If you don’t want it to happen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="c91ff-212">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c91ff-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c91ff-213">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada mediante la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c91ff-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c91ff-214">Puede leer más sobre la característica de documentación insertada aquí: [Documentación insertada sobre Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c91ff-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c91ff-215">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c91ff-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="c91ff-216">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c91ff-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c91ff-218">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="c91ff-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c91ff-219">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-219">On the left navigation pane in the **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c91ff-221">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-221">To display the list of users, Go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c91ff-223">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-223">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c91ff-225">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="c91ff-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c91ff-227">a.</span><span class="sxs-lookup"><span data-stu-id="c91ff-227">a.</span></span> <span data-ttu-id="c91ff-228">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c91ff-229">b.</span><span class="sxs-lookup"><span data-stu-id="c91ff-229">b.</span></span> <span data-ttu-id="c91ff-230">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c91ff-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c91ff-231">c.</span><span class="sxs-lookup"><span data-stu-id="c91ff-231">c.</span></span> <span data-ttu-id="c91ff-232">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c91ff-233">d.</span><span class="sxs-lookup"><span data-stu-id="c91ff-233">d.</span></span> <span data-ttu-id="c91ff-234">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="c91ff-235">Creación de un usuario de prueba de Salesforce</span><span class="sxs-lookup"><span data-stu-id="c91ff-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="c91ff-236">En esta sección, creará un usuario llamado a Britta Simon en Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c91ff-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="c91ff-237">Salesforce admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c91ff-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="c91ff-238">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="c91ff-238">There is no action item for you in this section.</span></span> <span data-ttu-id="c91ff-239">Si el usuario no existe aún en Salesforce, se crea uno nuevo cuando se intenta acceder a esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="c91ff-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt to access Salesforce.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c91ff-240">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c91ff-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c91ff-241">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c91ff-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c91ff-243">**Para asignar a Britta Simon a Salesforce, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="c91ff-243">**To assign Britta Simon to Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="c91ff-244">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c91ff-246">En la lista de aplicaciones, seleccione **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-246">In the applications list, select **Salesforce**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="c91ff-248">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c91ff-250">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-250">Click **Add** button.</span></span> <span data-ttu-id="c91ff-251">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c91ff-253">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="c91ff-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c91ff-254">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c91ff-255">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c91ff-256">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c91ff-256">Testing single sign-on</span></span>

<span data-ttu-id="c91ff-257">Para probar la configuración de inicio de sesión único, abra el Panel de acceso en [https://myapps.microsoft.com](https://myapps.microsoft.com/) y, a continuación, inicie sesión en la cuenta de prueba y haga clic en **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="c91ff-257">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into the test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c91ff-258">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c91ff-258">Additional resources</span></span>

* [<span data-ttu-id="c91ff-259">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c91ff-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c91ff-260">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c91ff-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="c91ff-261">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="c91ff-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png


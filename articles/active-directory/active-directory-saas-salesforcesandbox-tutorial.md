---
title: "Tutorial: Integración de Azure Active Directory con Salesforce Sandbox | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Salesforce Sandbox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 90e08b9cf2feb93de4877bec9734352949896dca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="29a1c-103">Tutorial: Integración de Azure Active Directory con Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="29a1c-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="29a1c-104">En este tutorial, aprenderá a integrar Salesforce Sandbox con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="29a1c-104">In this tutorial, you learn how to integrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29a1c-105">La integración de Salesforce Sandbox con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="29a1c-105">Integrating Salesforce Sandbox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="29a1c-106">Puede controlar en Azure AD quién tiene acceso a Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="29a1c-106">You can control in Azure AD who has access to Salesforce Sandbox</span></span>
- <span data-ttu-id="29a1c-107">Puede permitir que los usuarios inicien sesión automáticamente en Salesforce Sandbox (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="29a1c-107">You can enable your users to automatically get signed-on to Salesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="29a1c-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="29a1c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="29a1c-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29a1c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29a1c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="29a1c-110">Prerequisites</span></span>

<span data-ttu-id="29a1c-111">Para configurar la integración de Azure AD con Salesforce Sandbox, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="29a1c-111">To configure Azure AD integration with Salesforce Sandbox, you need the following items:</span></span>

- <span data-ttu-id="29a1c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="29a1c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="29a1c-113">Una suscripción habilitada para el inicio de sesión único en Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="29a1c-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29a1c-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="29a1c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="29a1c-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="29a1c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="29a1c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="29a1c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="29a1c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29a1c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29a1c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="29a1c-118">Scenario description</span></span>
<span data-ttu-id="29a1c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="29a1c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29a1c-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="29a1c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29a1c-121">Adición de Salesforce Sandbox desde la galería</span><span class="sxs-lookup"><span data-stu-id="29a1c-121">Adding Salesforce Sandbox from the gallery</span></span>
2. <span data-ttu-id="29a1c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="29a1c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-the-gallery"></a><span data-ttu-id="29a1c-123">Adición de Salesforce Sandbox desde la galería</span><span class="sxs-lookup"><span data-stu-id="29a1c-123">Adding Salesforce Sandbox from the gallery</span></span>
<span data-ttu-id="29a1c-124">Para configurar la integración de Salesforce Sandbox, deberá agregar Salesforce Sandbox desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="29a1c-124">To configure the integration of Salesforce Sandbox into Azure AD, you need to add Salesforce Sandbox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="29a1c-125">**Para agregar Salesforce Sandbox desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="29a1c-125">**To add Salesforce Sandbox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="29a1c-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="29a1c-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="29a1c-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="29a1c-131">Haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="29a1c-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="29a1c-133">En el cuadro de búsqueda, escriba **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-133">In the search box, type **Salesforce Sandbox**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="29a1c-135">En el panel de resultados, seleccione **Salesforce Sandbox** y, luego, haga clic en **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="29a1c-135">In the results panel, select **Salesforce Sandbox**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="29a1c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="29a1c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="29a1c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Salesforce Sandbox con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="29a1c-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="29a1c-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Salesforce Sandbox para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29a1c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce Sandbox is to a user in Azure AD.</span></span> <span data-ttu-id="29a1c-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="29a1c-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce Sandbox needs to be established.</span></span>

<span data-ttu-id="29a1c-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="29a1c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="29a1c-142">Para configurar y probar el inicio de sesión único de Azure AD con Salesforce Sandbox, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="29a1c-142">To configure and test Azure AD single sign-on with Salesforce Sandbox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="29a1c-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="29a1c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="29a1c-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29a1c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29a1c-145">**[Creación de un usuario de prueba de Salesforce Sandbox](#creating-a-salesforce-sandbox-test-user)**: el objetivo es tener un homólogo de Britta Simon en Salesforce Sandbox que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29a1c-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - to have a counterpart of Britta Simon in Salesforce Sandbox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="29a1c-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29a1c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29a1c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="29a1c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="29a1c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="29a1c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="29a1c-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="29a1c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="29a1c-150">**Para configurar el inicio de sesión único de Azure AD con Salesforce Sandbox, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="29a1c-150">**To configure Azure AD single sign-on with Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="29a1c-151">En la página de integración de la aplicación **Salesforce Sandbox** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-151">In the Azure portal, on the **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="29a1c-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="29a1c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="29a1c-155">En la sección **Dominio y direcciones URL de Salesforce Sandbox**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="29a1c-155">On the **Salesforce Sandbox Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="29a1c-157">En el cuadro de texto **URL de inicio de sesión**, escriba el valor con el siguiente patrón: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="29a1c-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="29a1c-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="29a1c-158">This value is not the real.</span></span> <span data-ttu-id="29a1c-159">Actualícelo con la dirección URL de inicio de sesión real. Póngase en contacto con el [equipo de atención al cliente de Salesforce Sandbox](https://help.salesforce.com/support) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="29a1c-159">Update this value with the actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) to get this value.</span></span>


4. <span data-ttu-id="29a1c-160">Si ya configuró un inicio de sesión único para otra instancia de Salesforce Sandbox en su directorio, también debe configurar el **Identificador** para que tenga el mismo valor que la **URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="29a1c-161">El campo **Identificador** puede encontrarse al activar la casilla **Mostrar configuración avanzada** en la página **Configure App URL** (Configurar dirección URL de la aplicación) del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="29a1c-161">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog</span></span> 


5. <span data-ttu-id="29a1c-162">En la sección **Certificado de firma de SAML**, haga clic en **Certificado** y, a continuación, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="29a1c-162">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="29a1c-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="29a1c-164">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="29a1c-166">En la sección **Configuración de Salesforce Sandbox**, haga clic en **Configurar Salesforce Sandbox** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-166">On the **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="29a1c-167">Copie **SAML Entity ID and SAML Single Sign-On Service URL** (URL del servicio de inicio de sesión único de SAML e Identificador de entidad de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-167">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="29a1c-168">![Configuración del inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="29a1c-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="29a1c-169">Abra una nueva pestaña en el explorador e inicie sesión en su cuenta de administrador de Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="29a1c-169">Open a new tab in your browser and log in to your Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="29a1c-170">En el menú de la parte superior, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-170">In the menu on the top, click **Setup**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="29a1c-172">En el panel de navegación de la izquierda, haga clic en **Controles de seguridad** y luego haga clic en **Configuración de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-172">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="29a1c-174">En la sección Configuración de inicio de sesión único, siga estos pasos: ![Configurar el inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="29a1c-174">On the Single Sign-On Settings section, perform the following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="29a1c-175">a.</span><span class="sxs-lookup"><span data-stu-id="29a1c-175">a.</span></span>  <span data-ttu-id="29a1c-176">Seleccione **SAML habilitado**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="29a1c-177">b.</span><span class="sxs-lookup"><span data-stu-id="29a1c-177">b.</span></span>  <span data-ttu-id="29a1c-178">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-178">Click **New**.</span></span>

12. <span data-ttu-id="29a1c-179">En la sección Configuración del inicio de sesión único de SAML siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="29a1c-179">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="29a1c-181">En el cuadro de texto Name (Nombre), escriba el nombre de la configuración (por ejemplo, *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="29a1c-181">a.In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="29a1c-182">b.</span><span class="sxs-lookup"><span data-stu-id="29a1c-182">b.</span></span> <span data-ttu-id="29a1c-183">Pegue el valor de **id. de entidad de SMAL** en el cuadro de texto **Issuer** (Emisor).</span><span class="sxs-lookup"><span data-stu-id="29a1c-183">Paste **SMAL Entity ID** value into the **Issuer** textbox.</span></span>

    <span data-ttu-id="29a1c-184">c.</span><span class="sxs-lookup"><span data-stu-id="29a1c-184">c.</span></span> <span data-ttu-id="29a1c-185">En el cuadro de texto **Entity Id** (Id. de entidad), escriba **https://test.salesforce.com** si se trata de la primera instancia de Salesforce Sandbox que va a agregar a su directorio.</span><span class="sxs-lookup"><span data-stu-id="29a1c-185">In the **Entity Id** textbox, type **https://test.salesforce.com** if it is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="29a1c-186">Si ya agregó una instancia de Salesforce Sandbox, para el **Id. de entidad** escriba la **URL de inicio de sesión**, que debe tener este formato: `http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="29a1c-186">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="29a1c-187">d.</span><span class="sxs-lookup"><span data-stu-id="29a1c-187">d.</span></span> <span data-ttu-id="29a1c-188">Haga clic en **Examinar** para cargar el certificado descargado.</span><span class="sxs-lookup"><span data-stu-id="29a1c-188">Click **Browse** to upload the downloaded certificate.</span></span>  

    <span data-ttu-id="29a1c-189">e.</span><span class="sxs-lookup"><span data-stu-id="29a1c-189">e.</span></span> <span data-ttu-id="29a1c-190">Como **SAML Identity Type** (Tipo de identidad SAML), seleccione **Assertion contains the Federation ID from the User object** (La aserción contiene el id. de federación del objeto Usuario).</span><span class="sxs-lookup"><span data-stu-id="29a1c-190">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
 
    <span data-ttu-id="29a1c-191">f.</span><span class="sxs-lookup"><span data-stu-id="29a1c-191">f.</span></span> <span data-ttu-id="29a1c-192">Como **SAML Identity Location**(Ubicación de identidad de SAML), seleccione **Identity is in the NameIdentifier element of the Subject statement** (La identidad está en el elemento NameIdentifier de la instrucción de sujeto).</span><span class="sxs-lookup"><span data-stu-id="29a1c-192">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>

    <span data-ttu-id="29a1c-193">g.</span><span class="sxs-lookup"><span data-stu-id="29a1c-193">g.</span></span> <span data-ttu-id="29a1c-194">Pegue la **dirección URL de servicio de inicio de sesión único** en el cuadro de texto **Identity Provider Login URL** (URL de inicio de sesión del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="29a1c-194">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="29a1c-195">h.</span><span class="sxs-lookup"><span data-stu-id="29a1c-195">h.</span></span> <span data-ttu-id="29a1c-196">SFDC no admite el cierre de sesión SAML.</span><span class="sxs-lookup"><span data-stu-id="29a1c-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="29a1c-197">Como alternativa, pegue "https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0" en el cuadro de texto **URL de cierre de sesión del proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="29a1c-198">i.</span><span class="sxs-lookup"><span data-stu-id="29a1c-198">i.</span></span> <span data-ttu-id="29a1c-199">Para **Service Provider Initiated Request Binding** (Enlace de solicitud iniciada por el proveedor de servicio), seleccione **HTTP POST** (Método HTTP POST).</span><span class="sxs-lookup"><span data-stu-id="29a1c-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="29a1c-200">j.</span><span class="sxs-lookup"><span data-stu-id="29a1c-200">j.</span></span> <span data-ttu-id="29a1c-201">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="29a1c-202">Habilitación del dominio</span><span class="sxs-lookup"><span data-stu-id="29a1c-202">Enable your domain</span></span>
<span data-ttu-id="29a1c-203">En esta sección se supone que ya ha creado un dominio.</span><span class="sxs-lookup"><span data-stu-id="29a1c-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="29a1c-204">Para más información, consulte [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US) (Definición del nombre de dominio).</span><span class="sxs-lookup"><span data-stu-id="29a1c-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="29a1c-205">**Realice los pasos siguientes para habilitar su dominio:**</span><span class="sxs-lookup"><span data-stu-id="29a1c-205">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="29a1c-206">En el panel de navegación de la izquierda, haga clic en **Administración de dominios** y, luego, en **Mi dominio**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-206">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="29a1c-208">Asegúrese de que su dominio se ha configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="29a1c-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="29a1c-209">En la sección **Configuración de la página de inicio de sesión**, haga clic en**Editar**, luego, como **Servicio de autenticación**, seleccione el nombre de la configuración de inicio de sesión único de SAML en la sección anterior y finalmente haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-209">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="29a1c-211">Tan pronto como tenga un dominio configurado, los usuarios deberán usar la dirección URL de dominio para iniciar sesión en el espacio aislado de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="29a1c-211">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="29a1c-212">Para obtener el valor de la dirección URL, haga clic en el perfil de SSO que haya creado en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="29a1c-212">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="29a1c-213">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="29a1c-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="29a1c-214">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="29a1c-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="29a1c-215">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="29a1c-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="29a1c-216">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="29a1c-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="29a1c-217">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="29a1c-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="29a1c-219">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="29a1c-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="29a1c-220">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="29a1c-222">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-222">to display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="29a1c-224">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-224">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="29a1c-226">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="29a1c-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="29a1c-228">a.</span><span class="sxs-lookup"><span data-stu-id="29a1c-228">a.</span></span> <span data-ttu-id="29a1c-229">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29a1c-230">b.</span><span class="sxs-lookup"><span data-stu-id="29a1c-230">b.</span></span> <span data-ttu-id="29a1c-231">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29a1c-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="29a1c-232">c.</span><span class="sxs-lookup"><span data-stu-id="29a1c-232">c.</span></span> <span data-ttu-id="29a1c-233">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="29a1c-234">d.</span><span class="sxs-lookup"><span data-stu-id="29a1c-234">d.</span></span> <span data-ttu-id="29a1c-235">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="29a1c-236">Creación de un usuario de prueba de Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="29a1c-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="29a1c-237">En esta sección, creará un usuario llamado a Britta Simon en Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="29a1c-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="29a1c-238">Salesforce Sandbox admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="29a1c-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="29a1c-239">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="29a1c-239">There is no action item for you in this section.</span></span> <span data-ttu-id="29a1c-240">Si un usuario ya no existe en Salesforce Sandbox, se crea uno nuevo cuando se intenta acceder a esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="29a1c-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt to access Salesforce Sandbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="29a1c-241">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="29a1c-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="29a1c-242">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="29a1c-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce Sandbox.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="29a1c-244">**Para asignar a Britta Simon a Salesforce Sandbox, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="29a1c-244">**To assign Britta Simon to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="29a1c-245">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="29a1c-247">En la lista de aplicaciones, seleccione **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-247">In the applications list, select **Salesforce Sandbox**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="29a1c-249">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="29a1c-251">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-251">Click **Add** button.</span></span> <span data-ttu-id="29a1c-252">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="29a1c-254">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="29a1c-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="29a1c-255">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="29a1c-256">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="29a1c-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="29a1c-257">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="29a1c-257">Testing single sign-on</span></span>

<span data-ttu-id="29a1c-258">Si desea probar la configuración de inicio de sesión único (SSO), abra el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="29a1c-258">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="29a1c-259">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="29a1c-259">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="29a1c-260">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="29a1c-260">Additional resources</span></span>

* [<span data-ttu-id="29a1c-261">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29a1c-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29a1c-262">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="29a1c-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="29a1c-263">Configuración del aprovisionamiento de usuarios</span><span class="sxs-lookup"><span data-stu-id="29a1c-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png


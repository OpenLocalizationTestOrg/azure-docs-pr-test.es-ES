---
title: "Tutorial: Integración de Azure Active Directory con Teamphoria | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 2a35efb04d7fe22abc6894c149caf090666ce016
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="b53e3-103">Tutorial: Integración de Azure Active Directory con Teamphoria</span><span class="sxs-lookup"><span data-stu-id="b53e3-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="b53e3-104">En este tutorial, obtendrá información sobre cómo integrar Teamphoria con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b53e3-104">In this tutorial, you learn how to integrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b53e3-105">La integración de Teamphoria con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b53e3-105">Integrating Teamphoria with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b53e3-106">Puede controlar en Azure AD quién tiene acceso a Teamphoria</span><span class="sxs-lookup"><span data-stu-id="b53e3-106">You can control in Azure AD who has access to Teamphoria</span></span>
- <span data-ttu-id="b53e3-107">Puede permitir que los usuarios inicien sesión automáticamente en Teamphoria (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b53e3-107">You can enable your users to automatically get signed-on to Teamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b53e3-108">Puede administrar sus cuentas en una ubicación central: el Portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="b53e3-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="b53e3-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b53e3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Teamphoria, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="b53e3-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b53e3-110">Prerequisites</span></span>

<span data-ttu-id="b53e3-111">Para configurar la integración de Azure AD con Teamphoria, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b53e3-111">To configure Azure AD integration with Teamphoria, you need the following items:</span></span>

- <span data-ttu-id="b53e3-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b53e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b53e3-113">Una suscripción habilitada para el inicio de sesión único en Teamphoria</span><span class="sxs-lookup"><span data-stu-id="b53e3-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b53e3-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b53e3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b53e3-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b53e3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b53e3-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b53e3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b53e3-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b53e3-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b53e3-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b53e3-118">Scenario description</span></span>
<span data-ttu-id="b53e3-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b53e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b53e3-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="b53e3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b53e3-121">Agregar Teamphoria desde la galería</span><span class="sxs-lookup"><span data-stu-id="b53e3-121">Adding Teamphoria from the gallery</span></span>
2. <span data-ttu-id="b53e3-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b53e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-the-gallery"></a><span data-ttu-id="b53e3-123">Agregar Teamphoria desde la galería</span><span class="sxs-lookup"><span data-stu-id="b53e3-123">Adding Teamphoria from the gallery</span></span>
<span data-ttu-id="b53e3-124">Para configurar la integración de Teamphoria en Azure AD, es preciso agregar Teamphoria desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="b53e3-124">To configure the integration of Teamphoria into Azure AD, you need to add Teamphoria from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b53e3-125">**Para agregar Teamphoria desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b53e3-125">**To add Teamphoria from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b53e3-126">En el panel de navegación izquierdo del **[Portal de administración de Azure](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b53e3-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b53e3-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="b53e3-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b53e3-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="b53e3-133">En el cuadro de búsqueda, escriba **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-133">In the search box, type **Teamphoria**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="b53e3-135">En el panel de resultados, seleccione **Teamphoria** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b53e3-135">In the results panel, select **Teamphoria**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b53e3-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b53e3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b53e3-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Teamphoria con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b53e3-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b53e3-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Teamphoria para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b53e3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamphoria is to a user in Azure AD.</span></span> <span data-ttu-id="b53e3-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="b53e3-140">In other words, a link relationship between an Azure AD user and the related user in Teamphoria needs to be established.</span></span>

<span data-ttu-id="b53e3-141">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="b53e3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamphoria.</span></span>

<span data-ttu-id="b53e3-142">Para configurar y probar el inicio de sesión único de Azure AD con Teamphoria, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b53e3-142">To configure and test Azure AD single sign-on with Teamphoria, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b53e3-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="b53e3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b53e3-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b53e3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b53e3-145">**[Creación de un usuario de prueba para Teamphoria](#creating-a-teamphoria-test-user)** : para tener un homólogo de Britta Simon en Teamphoria que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b53e3-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - to have a counterpart of Britta Simon in Teamphoria that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b53e3-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b53e3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b53e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="b53e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b53e3-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b53e3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b53e3-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="b53e3-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="b53e3-150">**Para configurar el inicio de sesión único de Azure AD con Teamphoria, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b53e3-150">**To configure Azure AD single sign-on with Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="b53e3-151">En el Portal de administración de Azure, en la página de integración de la aplicación **Teamphoria**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-151">In the Azure Management portal, on the **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="b53e3-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b53e3-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="b53e3-155">En la sección de **dominio y direcciones URL de Teamphoria**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b53e3-155">On the **Teamphoria Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="b53e3-157">a.</span><span class="sxs-lookup"><span data-stu-id="b53e3-157">a.</span></span> <span data-ttu-id="b53e3-158">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL con el siguiente patrón: `https://<sub-domain>.teamphoria.com/login`.</span><span class="sxs-lookup"><span data-stu-id="b53e3-158">In the **Sign-on URL** textbox, type the URL using the following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="b53e3-159">Tenga en cuenta que estos no son valores reales.</span><span class="sxs-lookup"><span data-stu-id="b53e3-159">Please note that these are not the real values.</span></span> <span data-ttu-id="b53e3-160">Tendrá que actualizar estos valores con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="b53e3-160">You have to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="b53e3-161">Póngase en contacto con el [equipo de soporte técnico de Teamphoria](https://www.teamphoria.com/) para obtener la dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="b53e3-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) to get the Sign-on URL.</span></span> 

4. <span data-ttu-id="b53e3-162">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b53e3-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="b53e3-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="b53e3-164">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b53e3-166">En la sección **Configuración de Teamphoria**, haga clic en **Configurar Teamphoria** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-166">On the **Teamphoria Configuration** section, click **Configure Teamphoria** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b53e3-167">Copie la **SAML Single Sign-On Service URL** (URL del servicio de inicio de sesión único de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="b53e3-169">Para configurar el inicio de sesión único en **Teamphoria**, inicie sesión en la aplicación Teamphoria como administrador.</span><span class="sxs-lookup"><span data-stu-id="b53e3-169">To configure single sign-on on **Teamphoria** side, Login to your Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="b53e3-170">Vaya a la opción **ADMIN SETTINGS** (Configuración de administración) de la barra de herramientas izquierda y, en la pestaña Configure (Configurar), haga clic en **SINGLE SIGN-ON** (Inicio de sesión único) para abrir la ventana de configuración de SSO.</span><span class="sxs-lookup"><span data-stu-id="b53e3-170">Go to **ADMIN SETTINGS** option in the left toolbar and under the the Configure Tab click on **SINGLE SIGN-ON** to open the SSO configuration window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="b53e3-172">Haga clic en la opción **ADD NEW IDENTITY PROVIDER** (Agregar nuevo proveedor de identidades) en la esquina superior derecha para abrir el formulario para agregar la configuración de SSO.</span><span class="sxs-lookup"><span data-stu-id="b53e3-172">Click on **ADD NEW IDENTITY PROVIDER** option in the top right corner to open the form for adding the settings for SSO.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="b53e3-174">Escriba la información en los campos, tal como se describe a continuación:</span><span class="sxs-lookup"><span data-stu-id="b53e3-174">Enter the details in the fields as described below-</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="b53e3-176">a.</span><span class="sxs-lookup"><span data-stu-id="b53e3-176">a.</span></span> <span data-ttu-id="b53e3-177">**DISPLAY NAME**: escriba el nombre para mostrar del complemento en la página de administración.</span><span class="sxs-lookup"><span data-stu-id="b53e3-177">**DISPLAY NAME** : Enter the display name of the plugin on the admin page.</span></span>

    <span data-ttu-id="b53e3-178">b.</span><span class="sxs-lookup"><span data-stu-id="b53e3-178">b.</span></span> <span data-ttu-id="b53e3-179">**BUTTON NAME**: el nombre de la pestaña que se mostrará en la página de inicio de sesión mediante SSO.</span><span class="sxs-lookup"><span data-stu-id="b53e3-179">**BUTTON NAME** : The name of the tab which will display on the login page for logging in via SSO.</span></span>

    <span data-ttu-id="b53e3-180">c.</span><span class="sxs-lookup"><span data-stu-id="b53e3-180">c.</span></span> <span data-ttu-id="b53e3-181">**CERTIFICATE**: abra el certificado descargado anteriormente desde Azure Portal con el Bloc de notas, copie el contenido del mismo y péguelo en este cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="b53e3-181">**CERTIFICATE** : Open the Certificate downloaded earlier from the Azure portal in notepad, copy the contents of the same and paste it here in the box.</span></span>

    <span data-ttu-id="b53e3-182">d.</span><span class="sxs-lookup"><span data-stu-id="b53e3-182">d.</span></span> <span data-ttu-id="b53e3-183">**ENTRY POINT**: pegar la **dirección URL del servicio Single Sign-On de SAML** copiada anteriormente de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b53e3-183">**ENTRY POINT** : Paste the **SAML Single Sign-On Service URL** copied earlier form the Azure portal.</span></span>

    <span data-ttu-id="b53e3-184">e.</span><span class="sxs-lookup"><span data-stu-id="b53e3-184">e.</span></span> <span data-ttu-id="b53e3-185">Cambie la opción a **ON** y haga clic en **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-185">Switch the option to **ON** and click on **SAVE**.</span></span>   

<!--### Next steps

To ensure users can sign-in to Teamphoria after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Teamphoria in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b53e3-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b53e3-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="b53e3-187">El objetivo de esta sección es crear un usuario de prueba en el Portal de administración de Azure llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b53e3-187">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="b53e3-189">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="b53e3-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b53e3-190">En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-190">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b53e3-192">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="b53e3-192">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b53e3-194">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-194">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b53e3-196">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="b53e3-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b53e3-198">a.</span><span class="sxs-lookup"><span data-stu-id="b53e3-198">a.</span></span> <span data-ttu-id="b53e3-199">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b53e3-200">b.</span><span class="sxs-lookup"><span data-stu-id="b53e3-200">b.</span></span> <span data-ttu-id="b53e3-201">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b53e3-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b53e3-202">c.</span><span class="sxs-lookup"><span data-stu-id="b53e3-202">c.</span></span> <span data-ttu-id="b53e3-203">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b53e3-204">d.</span><span class="sxs-lookup"><span data-stu-id="b53e3-204">d.</span></span> <span data-ttu-id="b53e3-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="b53e3-206">Crear un usuario de prueba Teamphoria</span><span class="sxs-lookup"><span data-stu-id="b53e3-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="b53e3-207">Para permitir que los usuarios de Azure AD inicien sesión en Teamphoria, deben aprovisionarse en Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="b53e3-207">In order to enable Azure AD users to log into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="b53e3-208">En el caso de Teamphoria, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="b53e3-208">In the case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="b53e3-209">**Para aprovisionar cuentas de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="b53e3-209">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="b53e3-210">Inicie sesión en su sitio de la compañía de Teamphoria como administrador.</span><span class="sxs-lookup"><span data-stu-id="b53e3-210">Log in to your Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="b53e3-211">Haga clic en **ADMIN** en la barra de herramientas izquierda y haga clic en la pestaña **MANAGE** en **USERS** para abrir la página de administración para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="b53e3-211">Click on **ADMIN** settings on the left toolbar and under the **MANAGE** tab Click on **USERS** to open the admin page for users.</span></span>

    ![Agregar empleado](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="b53e3-213">Haga clic en la opción **MANUAL INVITE**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-213">Click on the **MANUAL INVITE** option.</span></span>

    ![Invitar a contactos](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="b53e3-215">En esta página, realizar las acciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="b53e3-215">On this page, perform following action.</span></span> 
    
    ![Invitar a contactos](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="b53e3-217">a.</span><span class="sxs-lookup"><span data-stu-id="b53e3-217">a.</span></span> <span data-ttu-id="b53e3-218">En el cuadro de texto **EMAIL ADDRESS**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b53e3-218">In the **EMAIL ADDRESS** textbox, the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b53e3-219">b.</span><span class="sxs-lookup"><span data-stu-id="b53e3-219">b.</span></span> <span data-ttu-id="b53e3-220">En el cuadro de texto **FIRST NAME**, escriba **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-220">In the **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="b53e3-221">c.</span><span class="sxs-lookup"><span data-stu-id="b53e3-221">c.</span></span> <span data-ttu-id="b53e3-222">En el cuadro de texto **LAST NAME**, escriba **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-222">In the **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="b53e3-223">d.</span><span class="sxs-lookup"><span data-stu-id="b53e3-223">d.</span></span> <span data-ttu-id="b53e3-224">Haga clic en **INVITE 1 USER**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="b53e3-225">El usuario debe aceptar la invitación para su creación en el sistema.</span><span class="sxs-lookup"><span data-stu-id="b53e3-225">User needs to accept the invite to get created in the system.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b53e3-226">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b53e3-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b53e3-227">En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="b53e3-227">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamphoria.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="b53e3-229">**Para asignar Britta Simon a Teamphoria, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b53e3-229">**To assign Britta Simon to Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="b53e3-230">En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. A continuación, haga clic en **All applications** (Todas las aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="b53e3-230">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b53e3-232">En la lista de aplicaciones, seleccione **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-232">In the applications list, select **Teamphoria**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="b53e3-234">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="b53e3-236">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-236">Click **Add** button.</span></span> <span data-ttu-id="b53e3-237">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="b53e3-239">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="b53e3-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b53e3-240">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b53e3-241">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b53e3-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b53e3-242">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="b53e3-242">Testing single sign-on</span></span>

<span data-ttu-id="b53e3-243">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b53e3-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b53e3-244">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b53e3-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="b53e3-245">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b53e3-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b53e3-246">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b53e3-246">Additional resources</span></span>

* [<span data-ttu-id="b53e3-247">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b53e3-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b53e3-248">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b53e3-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png


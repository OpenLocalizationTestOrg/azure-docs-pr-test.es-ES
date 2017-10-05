---
title: "Tutorial: Integración de Azure Active Directory con Pingboard | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Pingboard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 008c670a8043da0c67ccefde48d5ef721c75d97c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="347b1-103">Tutorial: Integración de Azure Active Directory con Pingboard</span><span class="sxs-lookup"><span data-stu-id="347b1-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="347b1-104">En este tutorial, aprenderá a integrar Pingboard con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="347b1-104">In this tutorial, you learn how to integrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="347b1-105">La integración de Pingboard con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="347b1-105">Integrating Pingboard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="347b1-106">Puede controlar en Azure AD quién tiene acceso a Pingboard.</span><span class="sxs-lookup"><span data-stu-id="347b1-106">You can control in Azure AD who has access to Pingboard</span></span>
- <span data-ttu-id="347b1-107">Puede permitir que los usuarios inicien sesión automáticamente en Pingboard (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="347b1-107">You can enable your users to automatically get signed-on to Pingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="347b1-108">Puede administrar sus cuentas en una ubicación central: el Portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="347b1-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="347b1-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="347b1-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="347b1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="347b1-110">Prerequisites</span></span>

<span data-ttu-id="347b1-111">Para configurar la integración de Azure AD con Pingboard, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="347b1-111">To configure Azure AD integration with Pingboard, you need the following items:</span></span>

- <span data-ttu-id="347b1-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="347b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="347b1-113">Una suscripción a Pingboard habilitada para inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="347b1-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="347b1-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="347b1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="347b1-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="347b1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="347b1-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="347b1-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="347b1-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="347b1-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="347b1-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="347b1-118">Scenario description</span></span>
<span data-ttu-id="347b1-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="347b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="347b1-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="347b1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="347b1-121">Agregar Pingboard desde la galería</span><span class="sxs-lookup"><span data-stu-id="347b1-121">Adding Pingboard from the gallery</span></span>
2. <span data-ttu-id="347b1-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="347b1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-the-gallery"></a><span data-ttu-id="347b1-123">Agregar Pingboard desde la galería</span><span class="sxs-lookup"><span data-stu-id="347b1-123">Adding Pingboard from the gallery</span></span>
<span data-ttu-id="347b1-124">Para configurar la integración de Pingboard en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="347b1-124">To configure the integration of Pingboard into Azure AD, you need to add Pingboard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="347b1-125">**Para agregar Pingboard desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="347b1-125">**To add Pingboard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="347b1-126">En el panel de navegación izquierdo del **[Portal de administración de Azure](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="347b1-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="347b1-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="347b1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="347b1-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="347b1-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="347b1-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="347b1-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="347b1-133">En el cuadro de búsqueda, escriba En el cuadro de búsqueda, escriba **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="347b1-133">In the search box, type **Pingboard**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="347b1-135">En el panel de resultados, seleccione **Pingboard** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="347b1-135">In the results panel, select **Pingboard**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="347b1-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="347b1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="347b1-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Pingboard con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="347b1-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="347b1-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Pingboard para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="347b1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pingboard is to a user in Azure AD.</span></span> <span data-ttu-id="347b1-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Pingboard.</span><span class="sxs-lookup"><span data-stu-id="347b1-140">In other words, a link relationship between an Azure AD user and the related user in Pingboard needs to be established.</span></span>

<span data-ttu-id="347b1-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Pingboard.</span><span class="sxs-lookup"><span data-stu-id="347b1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pingboard.</span></span>

<span data-ttu-id="347b1-142">Para configurar y probar el inicio de sesión único de Azure AD con Pingboard, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="347b1-142">To configure and test Azure AD single sign-on with Pingboard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="347b1-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="347b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="347b1-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="347b1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="347b1-145">**[Creación de un usuario de prueba de Pingboard](#creating-a-pingboard-test-user)**: para tener un homólogo de Britta Simon en Pingboard que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="347b1-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - to have a counterpart of Britta Simon in Pingboard that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="347b1-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="347b1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="347b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="347b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="347b1-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="347b1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="347b1-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación Pingboard.</span><span class="sxs-lookup"><span data-stu-id="347b1-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="347b1-150">**Para configurar el inicio de sesión único de Azure AD con Pingboard, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="347b1-150">**To configure Azure AD single sign-on with Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="347b1-151">En el Portal de administración de Azure, en la página de integración de aplicaciones de **Pingboard**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="347b1-151">In the Azure Management portal, on the **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="347b1-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="347b1-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="347b1-155">En la sección **Dominio y direcciones URL de Pingboard**, realice los siguientes pasos si quiere configurar la aplicación en el modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="347b1-155">On the **Pingboard Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="347b1-157">a.</span><span class="sxs-lookup"><span data-stu-id="347b1-157">a.</span></span> <span data-ttu-id="347b1-158">En el cuadro de texto **Identificador**, escriba el valor como `http://<entity-id>.pingboard.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="347b1-158">In the **Identifier** textbox, type the value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="347b1-159">b.</span><span class="sxs-lookup"><span data-stu-id="347b1-159">b.</span></span> <span data-ttu-id="347b1-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<entity-id>.pingboard.com/auth/saml/consume`.</span><span class="sxs-lookup"><span data-stu-id="347b1-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="347b1-161">Tenga en cuenta que estos no son valores reales.</span><span class="sxs-lookup"><span data-stu-id="347b1-161">Please note that these are not the real values.</span></span> <span data-ttu-id="347b1-162">Estos valores se tienen que actualizar con los valores reales de Identificador y URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="347b1-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="347b1-163">Aquí le recomendamos que utilice el valor de cadena único en el identificador.</span><span class="sxs-lookup"><span data-stu-id="347b1-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="347b1-164">Póngase en contacto con el [equipo de soporte técnico de Pingboard](https://support.pingboard.com/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="347b1-164">Contact [Pingboard Client support team](https://support.pingboard.com/) to get these values.</span></span> 

4. <span data-ttu-id="347b1-165">Active **Mostrar configuración avanzada de URL**, si desea volver a configurar la aplicación en modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="347b1-165">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="347b1-167">a.</span><span class="sxs-lookup"><span data-stu-id="347b1-167">a.</span></span> <span data-ttu-id="347b1-168">En el cuadro de texto **URL de inicio de sesión**, escriba el valor como: `http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="347b1-168">In the **Sign-on URL** textbox, type the value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="347b1-169">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="347b1-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="347b1-171">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="347b1-171">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="347b1-173">Para configurar SSO en Pingboard, abra una nueva ventana del explorador e inicie sesión en su cuenta de Pingboard.</span><span class="sxs-lookup"><span data-stu-id="347b1-173">To configure SSO on Pingboard side, open a new browser window and log in to your Pingboard Account.</span></span> <span data-ttu-id="347b1-174">Debe ser un administrador de Pingboard para configurar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="347b1-174">You must be a Pingboard admin to set up single sign on.</span></span>

8. <span data-ttu-id="347b1-175">En el menú superior, seleccione **Aplicaciones > Integraciones**</span><span class="sxs-lookup"><span data-stu-id="347b1-175">From the top menu select **Apps > Integrations**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="347b1-177">En la página **Integraciones**, busque el icono **"Azure Active Directory"** y haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="347b1-177">On the **Integrations** page, find the **"Azure Active Directory"** tile, and click it.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="347b1-179">En el estado modal que sigue, haga clic en **"Configurar"**.</span><span class="sxs-lookup"><span data-stu-id="347b1-179">In the modal that follows click **"Configure"**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="347b1-181">En la siguiente página, observará que la "integración de Azure SSO está habilitada".</span><span class="sxs-lookup"><span data-stu-id="347b1-181">On the following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="347b1-182">Abra el archivo XML de metadatos descargado en el Bloc de notas y pegue el contenido en **metadatos de IDP**.</span><span class="sxs-lookup"><span data-stu-id="347b1-182">Open the downloaded Metadata XML file in a notepad and paste the content in **IDP Metadata**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="347b1-184">El archivo se validará y, si todo está correcto, se habilitará el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="347b1-184">The file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="347b1-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="347b1-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="347b1-186">El objetivo de esta sección es crear un usuario de prueba en el Portal de administración de Azure llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="347b1-186">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="347b1-188">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="347b1-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="347b1-189">En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="347b1-189">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="347b1-191">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="347b1-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="347b1-193">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="347b1-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="347b1-195">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="347b1-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="347b1-197">a.</span><span class="sxs-lookup"><span data-stu-id="347b1-197">a.</span></span> <span data-ttu-id="347b1-198">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="347b1-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="347b1-199">b.</span><span class="sxs-lookup"><span data-stu-id="347b1-199">b.</span></span> <span data-ttu-id="347b1-200">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="347b1-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="347b1-201">c.</span><span class="sxs-lookup"><span data-stu-id="347b1-201">c.</span></span> <span data-ttu-id="347b1-202">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="347b1-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="347b1-203">d.</span><span class="sxs-lookup"><span data-stu-id="347b1-203">d.</span></span> <span data-ttu-id="347b1-204">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="347b1-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="347b1-205">Creación de un usuario de prueba de Pingboard</span><span class="sxs-lookup"><span data-stu-id="347b1-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="347b1-206">Para permitir que los usuarios de Azure AD inicien sesión en Pingboard, tienen que aprovisionarse en Pingboard.</span><span class="sxs-lookup"><span data-stu-id="347b1-206">In order to enable Azure AD users to log into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="347b1-207">En el caso de Pingboard, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="347b1-207">In the case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="347b1-208">**Para aprovisionar cuentas de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="347b1-208">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="347b1-209">Inicie sesión en el sitio de la compañía Pingboard como administrador.</span><span class="sxs-lookup"><span data-stu-id="347b1-209">Log in to your Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="347b1-210">Haga clic en el botón **“Add Employee”** (Agregar empleado) en la página **Directory** (Directorio).</span><span class="sxs-lookup"><span data-stu-id="347b1-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Agregar empleado](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="347b1-212">En la página del cuadro de diálogo **"Add Employee"** (Agregar empleado), realice los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="347b1-212">On the **“Add Employee”** dialog page, perform the following steps.</span></span>

    ![Invitar a contactos](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="347b1-214">a.</span><span class="sxs-lookup"><span data-stu-id="347b1-214">a.</span></span> <span data-ttu-id="347b1-215">En el cuadro de texto **Nombre completo**, escriba el nombre completo de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="347b1-215">In the **Full Name** textbox, type the full name of Britta Simon.</span></span>

    <span data-ttu-id="347b1-216">b.</span><span class="sxs-lookup"><span data-stu-id="347b1-216">b.</span></span> <span data-ttu-id="347b1-217">En el cuadro de texto **Correo electrónico**, escriba la dirección de correo electrónico de la cuenta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="347b1-217">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="347b1-218">c.</span><span class="sxs-lookup"><span data-stu-id="347b1-218">c.</span></span> <span data-ttu-id="347b1-219">En el cuadro de texto **Puesto**, escriba el puesto de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="347b1-219">In the **Job Title** textbox, type the job title of Britta Simon.</span></span>

    <span data-ttu-id="347b1-220">d.</span><span class="sxs-lookup"><span data-stu-id="347b1-220">d.</span></span> <span data-ttu-id="347b1-221">En la lista desplegable **Ubicación**, seleccione la ubicación de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="347b1-221">In the **Location** dropdown, select the location  of Britta Simon.</span></span>
    
    <span data-ttu-id="347b1-222">e.</span><span class="sxs-lookup"><span data-stu-id="347b1-222">e.</span></span> <span data-ttu-id="347b1-223">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="347b1-223">Click **Add**.</span></span>   

4. <span data-ttu-id="347b1-224">Se muestra una pantalla de confirmación para confirmar la adición del usuario.</span><span class="sxs-lookup"><span data-stu-id="347b1-224">A confirmation screen will come up to confirm the addition of user.</span></span>
    
    ![confirmar](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="347b1-226">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo y seguirá un vínculo para confirmar su cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="347b1-226">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="347b1-227">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="347b1-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="347b1-228">En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a Pingboard.</span><span class="sxs-lookup"><span data-stu-id="347b1-228">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Pingboard.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="347b1-230">**Para asignar a Britta Simon a Pingboard, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="347b1-230">**To assign Britta Simon to Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="347b1-231">En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. A continuación, haga clic en **All applications** (Todas las aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="347b1-231">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="347b1-233">En la lista de aplicaciones, seleccione **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="347b1-233">In the applications list, select **Pingboard**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="347b1-235">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="347b1-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="347b1-237">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="347b1-237">Click **Add** button.</span></span> <span data-ttu-id="347b1-238">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="347b1-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="347b1-240">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="347b1-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="347b1-241">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="347b1-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="347b1-242">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="347b1-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="347b1-243">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="347b1-243">Testing single sign-on</span></span>

<span data-ttu-id="347b1-244">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="347b1-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="347b1-245">Al hacer clic en el icono de Pingboard en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Pingboard.</span><span class="sxs-lookup"><span data-stu-id="347b1-245">When you click the Pingboard tile in the Access Panel, you should get automatically signed-on to your Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="347b1-246">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="347b1-246">Additional resources</span></span>

* [<span data-ttu-id="347b1-247">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="347b1-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="347b1-248">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="347b1-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png

---
title: "Tutorial: Integración de Azure Active Directory con SAML SSO for Confluence by resolution GmbH | Documentos de Microsoft"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y SAML SSO for Confluence by resolution GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a36d686ba39b5168860a20e8c4db357888df6a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a><span data-ttu-id="832c9-103">Tutorial: Integración de Azure Active Directory con SAML SSO for Confluence by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="832c9-103">Tutorial: Azure Active Directory integration with SAML SSO for Confluence by resolution GmbH</span></span>

<span data-ttu-id="832c9-104">En este tutorial, aprenderá a integrar SAML SSO for Confluence by resolution GmbH con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="832c9-104">In this tutorial, you learn how to integrate SAML SSO for Confluence by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="832c9-105">La integración de SAML SSO for Confluence by resolution GmbH con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="832c9-105">Integrating SAML SSO for Confluence by resolution GmbH with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="832c9-106">Puede controlar en Azure AD quién tiene acceso a SAML SSO for Confluence by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="832c9-106">You can control in Azure AD who has access to SAML SSO for Confluence by resolution GmbH</span></span>
- <span data-ttu-id="832c9-107">Puede permitir que los usuarios inicien sesión automáticamente en SAML SSO for Confluence by resolution GmbH (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="832c9-107">You can enable your users to automatically get signed-on to SAML SSO for Confluence by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="832c9-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="832c9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="832c9-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="832c9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="832c9-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="832c9-110">Prerequisites</span></span>

<span data-ttu-id="832c9-111">Para configurar la integración de Azure AD con SAML SSO for Confluence by resolution GmbH, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="832c9-111">To configure Azure AD integration with SAML SSO for Confluence by resolution GmbH, you need the following items:</span></span>

- <span data-ttu-id="832c9-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="832c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="832c9-113">Una suscripción habilitada para el inicio de sesión único de SAML SSO for Confluence by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="832c9-113">A SAML SSO for Confluence by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="832c9-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="832c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="832c9-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="832c9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="832c9-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="832c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="832c9-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="832c9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="832c9-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="832c9-118">Scenario description</span></span>
<span data-ttu-id="832c9-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="832c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="832c9-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="832c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="832c9-121">Adición de SAML SSO for Confluence by resolution GmbH desde la galería</span><span class="sxs-lookup"><span data-stu-id="832c9-121">Adding SAML SSO for Confluence by resolution GmbH from the gallery</span></span>
2. <span data-ttu-id="832c9-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="832c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-the-gallery"></a><span data-ttu-id="832c9-123">Adición de SAML SSO for Confluence by resolution GmbH desde la galería</span><span class="sxs-lookup"><span data-stu-id="832c9-123">Adding SAML SSO for Confluence by resolution GmbH from the gallery</span></span>

<span data-ttu-id="832c9-124">Para configurar la integración de SAML SSO for Confluence by resolution GmbH en Azure AD, debe agregar SAML SSO for Confluence by resolution GmbH desde la galería a la lista de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="832c9-124">To configure the integration of SAML SSO for Confluence by resolution GmbH into Azure AD, you need to add SAML SSO for Confluence by resolution GmbH from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="832c9-125">**Para agregar SAML SSO for Confluence by resolution GmbH desde la galería, siga los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="832c9-125">**To add SAML SSO for Confluence by resolution GmbH from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="832c9-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="832c9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="832c9-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="832c9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="832c9-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="832c9-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="832c9-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="832c9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="832c9-133">En el cuadro de búsqueda, escriba **SAML SSO for Confluence by resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="832c9-133">In the search box, type **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. <span data-ttu-id="832c9-135">En el panel de resultados, seleccione **SAML SSO for Confluence by resolution GmbH** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="832c9-135">In the results panel, select **SAML SSO for Confluence by resolution GmbH**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="832c9-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="832c9-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="832c9-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con SAML SSO for Confluence by resolution GmbH con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="832c9-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="832c9-139">Para que el inicio de sesión único funcione, es preciso que Azure AD sepa cuál es el usuario homólogo de SAML SSO for Confluence by resolution GmbH para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="832c9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Confluence by resolution GmbH is to a user in Azure AD.</span></span> <span data-ttu-id="832c9-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de SAML SSO for Confluence by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="832c9-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Confluence by resolution GmbH needs to be established.</span></span>

<span data-ttu-id="832c9-141">Para establecer la relación de vínculo, en SAML SSO for Confluence by resolution GmbH, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="832c9-141">In SAML SSO for Confluence by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="832c9-142">Para configurar y probar el inicio de sesión único de Azure AD con SAML SSO for Confluence by resolution GmbH, se deben completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="832c9-142">To configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="832c9-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="832c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="832c9-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="832c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="832c9-145">**[Creación de un usuario de prueba de SAML SSO for Confluence by resolution GmbH](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**: para tener un homólogo de Britta Simon en SAML SSO for Confluence by resolution GmbH que esté vinculado a la representación del usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="832c9-145">**[Creating a SAML SSO for Confluence by resolution GmbH test user](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Confluence by resolution GmbH that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="832c9-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="832c9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="832c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="832c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="832c9-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="832c9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="832c9-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación SAML SSO for Confluence by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="832c9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Confluence by resolution GmbH application.</span></span>

<span data-ttu-id="832c9-150">**Para configurar el inicio de sesión único de Azure AD con SAML SSO for Confluence by resolution GmbH, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="832c9-150">**To configure Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="832c9-151">En Azure Portal, en la página de integración de aplicaciones de **SAML SSO for Confluence by resolution GmbH**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="832c9-151">In the Azure portal, on the **SAML SSO for Confluence by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="832c9-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="832c9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. <span data-ttu-id="832c9-155">En la sección **SAML SSO for Confluence by resolution GmbH Domain and URLs** (Dominio y direcciones URL de SAML SSO for Confluence by resolution GmbH), si quiere configurar la aplicación en modo iniciado por **IdP**:</span><span class="sxs-lookup"><span data-stu-id="832c9-155">On the **SAML SSO for Confluence by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    <span data-ttu-id="832c9-157">a.</span><span class="sxs-lookup"><span data-stu-id="832c9-157">a.</span></span> <span data-ttu-id="832c9-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="832c9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="832c9-159">b.</span><span class="sxs-lookup"><span data-stu-id="832c9-159">b.</span></span> <span data-ttu-id="832c9-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<server-base-url>/plugins/servlet/samlsso`.</span><span class="sxs-lookup"><span data-stu-id="832c9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="832c9-161">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="832c9-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="832c9-162">Si quiere volver a configurar la aplicación en modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="832c9-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    <span data-ttu-id="832c9-164">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<server-base-url>/plugins/servlet/samlsso`.</span><span class="sxs-lookup"><span data-stu-id="832c9-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="832c9-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="832c9-165">These values are not real.</span></span> <span data-ttu-id="832c9-166">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="832c9-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="832c9-167">Póngase en contacto con el [equipo de soporte técnico de clientes de SAML SSO for Confluence by resolution GmbH](https://www.resolution.de/go/support) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="832c9-167">Contact [SAML SSO for Confluence by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span></span> 

5. <span data-ttu-id="832c9-168">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="832c9-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. <span data-ttu-id="832c9-170">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="832c9-170">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. <span data-ttu-id="832c9-172">En otra ventana del explorador web, inicie sesión en el **Portal de administración de SAML SSO for Confluence by resolution GmbH** como administrador.</span><span class="sxs-lookup"><span data-stu-id="832c9-172">In a different web browser window, log in to your **SAML SSO for Confluence by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="832c9-173">Mantenga el mouse encima del icono de engranaje y haga clic en **Complementos**.</span><span class="sxs-lookup"><span data-stu-id="832c9-173">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. <span data-ttu-id="832c9-175">Se le redirigirá a la página Acceso de administrador.</span><span class="sxs-lookup"><span data-stu-id="832c9-175">You are redirected to Administrator Access page.</span></span> <span data-ttu-id="832c9-176">Escriba la contraseña y haga clic en el botón **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="832c9-176">Enter the password and click **Confirm** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. <span data-ttu-id="832c9-178">En la pestaña **ATLASSIAN MARKETPLACE** (MARKETPLACE DE ATLASSIAN), haga clic en **Find new add-ons** (Buscar nuevos complementos).</span><span class="sxs-lookup"><span data-stu-id="832c9-178">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. <span data-ttu-id="832c9-180">Busque **SAML Single Sign On (SSO) for Confluence** y haga clic en el botón **Instalar** para instalar el nuevo complemento SAML.</span><span class="sxs-lookup"><span data-stu-id="832c9-180">Search **SAML Single Sign On (SSO) for Confluence** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. <span data-ttu-id="832c9-182">Se iniciará la instalación del complemento.</span><span class="sxs-lookup"><span data-stu-id="832c9-182">The plugin installation will start.</span></span> <span data-ttu-id="832c9-183">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="832c9-183">Click **Close**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. <span data-ttu-id="832c9-186">Haga clic en **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="832c9-186">Click **Manage**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. <span data-ttu-id="832c9-188">Haga clic en **Configurar** para configurar el nuevo complemento.</span><span class="sxs-lookup"><span data-stu-id="832c9-188">Click **Configure** to configure the new plugin.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. <span data-ttu-id="832c9-190">Este nuevo complemento también puede encontrarse en la pestaña **USERS & SECURITY** (USUARIOS Y SEGURIDAD).</span><span class="sxs-lookup"><span data-stu-id="832c9-190">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. <span data-ttu-id="832c9-192">En la página **SAML SingleSignOn Plugin Configuration** (Configuración del complemento SingleSignOn de SAML), haga clic en el botón **Add additional Identity Provider** (Agregar proveedor de identidad adicional) para configurar las opciones del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="832c9-192">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button to configure the settings of Identity Provider.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. <span data-ttu-id="832c9-194">Siga los pasos indicados en esta página:</span><span class="sxs-lookup"><span data-stu-id="832c9-194">Perform following steps on this page:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    <span data-ttu-id="832c9-196">a.</span><span class="sxs-lookup"><span data-stu-id="832c9-196">a.</span></span> <span data-ttu-id="832c9-197">Agregue el **nombre** del proveedor de identidades (p. ej., Azure AD).</span><span class="sxs-lookup"><span data-stu-id="832c9-197">Add **Name** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="832c9-198">b.</span><span class="sxs-lookup"><span data-stu-id="832c9-198">b.</span></span> <span data-ttu-id="832c9-199">Agregue la **descripción** del proveedor de identidades (p. ej., Azure AD).</span><span class="sxs-lookup"><span data-stu-id="832c9-199">Add **Description** of the Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="832c9-200">c.</span><span class="sxs-lookup"><span data-stu-id="832c9-200">c.</span></span> <span data-ttu-id="832c9-201">Haga clic en **XML** y seleccione el archivo **Metadata** que ha descargado en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="832c9-201">Click **XML** and select the **Metadata** file that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="832c9-202">d.</span><span class="sxs-lookup"><span data-stu-id="832c9-202">d.</span></span> <span data-ttu-id="832c9-203">Haga clic en el botón **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="832c9-203">Click **Load** button.</span></span>

    <span data-ttu-id="832c9-204">e.</span><span class="sxs-lookup"><span data-stu-id="832c9-204">e.</span></span> <span data-ttu-id="832c9-205">Lee los metadatos de IdP y rellena los campos tal y como se resalta en la captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="832c9-205">It reads the IdP metadata and populates the fields as highlighted in the screenshot.</span></span> 
18. <span data-ttu-id="832c9-206">Haga clic en el botón **Guardar configuración** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="832c9-206">Click **Save settings** button to save the settings.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="832c9-208">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="832c9-208">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="832c9-209">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="832c9-209">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="832c9-210">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="832c9-210">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="832c9-211">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="832c9-211">Creating an Azure AD test user</span></span>
<span data-ttu-id="832c9-212">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="832c9-212">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="832c9-214">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="832c9-214">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="832c9-215">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="832c9-215">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="832c9-217">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="832c9-217">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="832c9-219">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="832c9-219">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="832c9-221">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="832c9-221">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="832c9-223">a.</span><span class="sxs-lookup"><span data-stu-id="832c9-223">a.</span></span> <span data-ttu-id="832c9-224">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="832c9-224">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="832c9-225">b.</span><span class="sxs-lookup"><span data-stu-id="832c9-225">b.</span></span> <span data-ttu-id="832c9-226">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="832c9-226">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="832c9-227">c.</span><span class="sxs-lookup"><span data-stu-id="832c9-227">c.</span></span> <span data-ttu-id="832c9-228">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="832c9-228">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="832c9-229">d.</span><span class="sxs-lookup"><span data-stu-id="832c9-229">d.</span></span> <span data-ttu-id="832c9-230">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="832c9-230">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a><span data-ttu-id="832c9-231">Creación del usuario de prueba de SAML SSO for Confluence by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="832c9-231">Creating a SAML SSO for Confluence by resolution GmbH test user</span></span>

<span data-ttu-id="832c9-232">Para permitir que los usuarios de Azure AD inicien sesión en SAML SSO for Confluence by resolution GmbH, deben estar aprovisionados en SAML SSO for Confluence by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="832c9-232">To enable Azure AD users to log in to SAML SSO for Confluence by resolution GmbH, they must be provisioned into SAML SSO for Confluence by resolution GmbH.</span></span>  
<span data-ttu-id="832c9-233">En SAML SSO for Confluence by resolution GmbH, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="832c9-233">In SAML SSO for Confluence by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="832c9-234">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="832c9-234">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="832c9-235">Inicie sesión en el sitio de la empresa de SAML SSO for Confluence by resolution GmbH como administrador.</span><span class="sxs-lookup"><span data-stu-id="832c9-235">Log in to your SAML SSO for Confluence by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="832c9-236">Mantenga el mouse encima del icono de engranaje y haga clic en **Administración de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="832c9-236">Hover on cog and click the **User management**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. <span data-ttu-id="832c9-238">En la sección Usuarios, haga clic en la pestaña **Agregar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="832c9-238">Under Users section, click **Add users** tab.</span></span> <span data-ttu-id="832c9-239">En la página del cuadro de diálogo **Agregar un usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="832c9-239">On the **“Add a User”** dialog page, perform the following steps:</span></span>

    ![Agregar empleado](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    <span data-ttu-id="832c9-241">a.</span><span class="sxs-lookup"><span data-stu-id="832c9-241">a.</span></span> <span data-ttu-id="832c9-242">En el cuadro de texto **Nombre de usuario**, escriba el correo electrónico de un usuario, por ejemplo, Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="832c9-242">In the **Username** textbox, type the email of user like Britta Simon.</span></span>

    <span data-ttu-id="832c9-243">b.</span><span class="sxs-lookup"><span data-stu-id="832c9-243">b.</span></span> <span data-ttu-id="832c9-244">En el cuadro de texto **Nombre completo**, escriba el nombre completo de un usuario, por ejemplo, Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="832c9-244">In the **Full Name** textbox, type the full name of user like Britta Simon.</span></span>

    <span data-ttu-id="832c9-245">c.</span><span class="sxs-lookup"><span data-stu-id="832c9-245">c.</span></span> <span data-ttu-id="832c9-246">En el cuadro de texto **Correo electrónico**, escriba la dirección de correo electrónico de un usuario, por ejemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="832c9-246">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="832c9-247">d.</span><span class="sxs-lookup"><span data-stu-id="832c9-247">d.</span></span> <span data-ttu-id="832c9-248">En el cuadro de texto **Contraseña**, escriba la contraseña de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="832c9-248">In the **Password** textbox, type the password for Britta Simon.</span></span>

    <span data-ttu-id="832c9-249">e.</span><span class="sxs-lookup"><span data-stu-id="832c9-249">e.</span></span> <span data-ttu-id="832c9-250">Haga clic en **Confirmar contraseña** y vuelva a escribir la contraseña.</span><span class="sxs-lookup"><span data-stu-id="832c9-250">Click **Confirm Password** reenter the password.</span></span>
    
    <span data-ttu-id="832c9-251">f.</span><span class="sxs-lookup"><span data-stu-id="832c9-251">f.</span></span> <span data-ttu-id="832c9-252">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="832c9-252">Click **Add** button.</span></span>    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="832c9-253">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="832c9-253">Assigning the Azure AD test user</span></span>

<span data-ttu-id="832c9-254">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a SAML SSO for Confluence by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="832c9-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Confluence by resolution GmbH.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="832c9-256">**Para asignar a Britta Simon a SAML SSO for Confluence by resolution GmbH, siga los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="832c9-256">**To assign Britta Simon to SAML SSO for Confluence by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="832c9-257">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="832c9-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="832c9-259">En la lista de aplicaciones, seleccione **SAML SSO for Confluence by resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="832c9-259">In the applications list, select **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. <span data-ttu-id="832c9-261">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="832c9-261">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="832c9-263">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="832c9-263">Click **Add** button.</span></span> <span data-ttu-id="832c9-264">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="832c9-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="832c9-266">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="832c9-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="832c9-267">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="832c9-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="832c9-268">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="832c9-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="832c9-269">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="832c9-269">Testing single sign-on</span></span>

<span data-ttu-id="832c9-270">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="832c9-270">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="832c9-271">Al hacer clic en el icono SAML SSO for Confluence by resolution GmbH en el Panel de acceso, su sesión debería iniciarse automáticamente en la aplicación SAML SSO for Confluence by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="832c9-271">When you click the SAML SSO for Confluence by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Confluence by resolution GmbH application.</span></span>
<span data-ttu-id="832c9-272">Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="832c9-272">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="832c9-273">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="832c9-273">Additional resources</span></span>

* [<span data-ttu-id="832c9-274">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="832c9-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="832c9-275">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="832c9-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png


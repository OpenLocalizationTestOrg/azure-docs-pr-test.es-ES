---
title: "Tutorial: Integración de Azure Active Directory con GitHub | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y GitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 9dc12bc2e313bcb2000724d035156c5054d14e1c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="b77ef-103">Tutorial: Integración de Azure Active Directory con GitHub</span><span class="sxs-lookup"><span data-stu-id="b77ef-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="b77ef-104">En este tutorial, obtendrá información sobre cómo integrar GitHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b77ef-104">In this tutorial, you learn how to integrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b77ef-105">Integrar GitHub con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b77ef-105">Integrating GitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b77ef-106">Puede controlar en Azure AD quién tiene acceso a GitHub.</span><span class="sxs-lookup"><span data-stu-id="b77ef-106">You can control in Azure AD who has access to GitHub</span></span>
- <span data-ttu-id="b77ef-107">Puede permitir que los usuarios inicien sesión automáticamente en GitHub mediante inicio de sesión único (SSO) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b77ef-107">You can enable your users to automatically get signed-on to GitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b77ef-108">Puede administrar sus cuentas en una ubicación central: el Portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="b77ef-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="b77ef-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b77ef-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b77ef-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b77ef-110">Prerequisites</span></span>

<span data-ttu-id="b77ef-111">Para configurar la integración de Azure AD con GitHub, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b77ef-111">To configure Azure AD integration with GitHub, you need the following items:</span></span>

- <span data-ttu-id="b77ef-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b77ef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b77ef-113">Una suscripción habilitada para inicio de sesión único en GitHub</span><span class="sxs-lookup"><span data-stu-id="b77ef-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="b77ef-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b77ef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="b77ef-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b77ef-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b77ef-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b77ef-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b77ef-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b77ef-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="b77ef-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b77ef-118">Scenario description</span></span>
<span data-ttu-id="b77ef-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b77ef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b77ef-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="b77ef-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b77ef-121">Adición de GitHub desde la galería</span><span class="sxs-lookup"><span data-stu-id="b77ef-121">Adding GitHub from the gallery</span></span>
2. <span data-ttu-id="b77ef-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b77ef-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-the-gallery"></a><span data-ttu-id="b77ef-123">Adición de GitHub desde la galería</span><span class="sxs-lookup"><span data-stu-id="b77ef-123">Adding GitHub from the gallery</span></span>
<span data-ttu-id="b77ef-124">Para configurar la integración de GitHub en Azure AD, debe agregar GitHub desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="b77ef-124">To configure the integration of GitHub into Azure AD, you need to add GitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b77ef-125">**Para agregar GitHub desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b77ef-125">**To add GitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b77ef-126">En el panel de navegación izquierdo del **[Portal de administración de Azure](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b77ef-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b77ef-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="b77ef-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b77ef-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="b77ef-133">En el cuadro de búsqueda, escriba **Github.com**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-133">In the search box, type **GitHub.com**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="b77ef-135">En el panel de resultados, seleccione **GitHub** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b77ef-135">In the results panel, select **GitHub**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b77ef-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b77ef-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b77ef-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con GitHub mediante un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b77ef-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b77ef-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo en GitHub de un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b77ef-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GitHub is to a user in Azure AD.</span></span> <span data-ttu-id="b77ef-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de GitHub.</span><span class="sxs-lookup"><span data-stu-id="b77ef-140">In other words, a link relationship between an Azure AD user and the related user in GitHub needs to be established.</span></span>

<span data-ttu-id="b77ef-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en GitHub.</span><span class="sxs-lookup"><span data-stu-id="b77ef-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in GitHub.</span></span>

<span data-ttu-id="b77ef-142">Para configurar y probar el SSO de Azure AD con GitHub, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b77ef-142">To configure and test Azure AD single sign-on with GitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b77ef-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="b77ef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b77ef-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b77ef-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b77ef-145">**[Creación de un usuario de prueba de GitHub](#creating-a-GitHub-test-user)**: para tener un homólogo de Britta Simon en GitHub que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b77ef-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - to have a counterpart of Britta Simon in GitHub that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b77ef-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b77ef-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b77ef-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="b77ef-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b77ef-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b77ef-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b77ef-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación GitHub.</span><span class="sxs-lookup"><span data-stu-id="b77ef-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="b77ef-150">**Para configurar el inicio de sesión único de Azure AD con GitHub, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b77ef-150">**To configure Azure AD single sign-on with GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="b77ef-151">En el Portal de administración de Azure, en la página de integración de la aplicación **GitHub**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-151">In the Azure Management portal, on the **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="b77ef-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b77ef-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="b77ef-155">En la sección de **dominio y direcciones URL de GitHub**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b77ef-155">On the **GitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="b77ef-157">a.</span><span class="sxs-lookup"><span data-stu-id="b77ef-157">a.</span></span> <span data-ttu-id="b77ef-158">En el cuadro de texto **URL de inicio de sesión**, escriba el valor como: `https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="b77ef-158">In the **Sign-on URL** textbox, type the value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="b77ef-159">b.</span><span class="sxs-lookup"><span data-stu-id="b77ef-159">b.</span></span> <span data-ttu-id="b77ef-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="b77ef-160">In the **Identifier** textbox, type a URL using the following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b77ef-161">Tenga en cuenta que estos no son valores reales.</span><span class="sxs-lookup"><span data-stu-id="b77ef-161">Please note that these are not the real values.</span></span> <span data-ttu-id="b77ef-162">Tendrá que actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="b77ef-162">You have to update these values with the actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="b77ef-163">Aquí le recomendamos que utilice el valor de cadena único en el identificador.</span><span class="sxs-lookup"><span data-stu-id="b77ef-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="b77ef-164">Vaya a la sección de administración de GitHub para recuperar estos valores.</span><span class="sxs-lookup"><span data-stu-id="b77ef-164">Go to GitHub Admin section to retrieve these values.</span></span> 

4. <span data-ttu-id="b77ef-165">En la sección **Atributos de usuario**, seleccione user.mail como **Identificador de usuario**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-165">On the **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="b77ef-167">En la sección **Certificado de firma de SAML**, haga clic en **Crear nuevo certificado**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-167">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="b77ef-169">En el cuadro de diálogo **Crear nuevo certificado**, haga clic en el icono del calendario y seleccione una valor en **Fecha de expiración**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-169">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="b77ef-170">Luego haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-170">Then click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="b77ef-172">En la sección **Certificado de firma de SAML**, seleccione **Make new certificate active** (Activar el nuevo certificado) y haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-172">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="b77ef-174">En la ventana emergente **Rollover certificate** (Certificado de sustitución), haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-174">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="b77ef-176">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b77ef-176">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="b77ef-178">En la sección **Configuración de GitHub**, haga clic en **Configurar GitHub** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-178">On the **GitHub Configuration** section, click **Configure GitHub** to open **Configure sign-on** window.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="b77ef-181">En otra ventana del navegador web, inicie sesión en el sitio de la organización de GitHub como administrador.</span><span class="sxs-lookup"><span data-stu-id="b77ef-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="b77ef-182">Vaya a **Configuración** y haga clic en **Seguridad**</span><span class="sxs-lookup"><span data-stu-id="b77ef-182">Navigate to **Settings** and click **Security**</span></span>

    ![Configuración](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="b77ef-184">Active la casilla **Habilitar autenticación SAML** para ver los campos de configuración del inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b77ef-184">Check the **Enable SAML authentication** box, revealing the Single Sign-on configuration fields.</span></span> <span data-ttu-id="b77ef-185">Luego, use el valor de URL de inicio de sesión único para actualizar la URL de inicio de sesión único en la configuración de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b77ef-185">Then, use the single sign-on URL value to update the Single sign-on URL on Azure AD configuration.</span></span>

    ![Configuración](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="b77ef-187">Configure los campos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b77ef-187">Configure the following fields:</span></span>

    <span data-ttu-id="b77ef-188">a.</span><span class="sxs-lookup"><span data-stu-id="b77ef-188">a.</span></span> <span data-ttu-id="b77ef-189">**Sign on URL** (URL de inicio de sesión): escriba la **URL de servicio de inicio de sesión único de SAML** de la sección **Configurar GitHub** en Azure AD</span><span class="sxs-lookup"><span data-stu-id="b77ef-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="b77ef-190">b.</span><span class="sxs-lookup"><span data-stu-id="b77ef-190">b.</span></span> <span data-ttu-id="b77ef-191">**Issuer** (Emisor): escriba el **id. de entidad de SAML** de la sección **Configurar GitHub** en Azure AD</span><span class="sxs-lookup"><span data-stu-id="b77ef-191">**Issuer**: Enter **SAML Entity ID** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="b77ef-192">c.</span><span class="sxs-lookup"><span data-stu-id="b77ef-192">c.</span></span> <span data-ttu-id="b77ef-193">**Certificado público**: abra el certificado que se descargó de Azure AD en un bloc de notas y copie el contenido, incluido "BEGIN CERTIFICATE" y "END CERTIFICATE"</span><span class="sxs-lookup"><span data-stu-id="b77ef-193">**Public Certificate**: Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![Configuración](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="b77ef-195">Haga clic en **Test SAML configuration** (Probar configuración de SAML) para configura que no hay errores de validación durante el SSO.</span><span class="sxs-lookup"><span data-stu-id="b77ef-195">Click on **Test SAML configuration** to confirm that no validation failures or errors during SSO.</span></span>

    ![Configuración](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="b77ef-197">Haga clic en **Guardar**</span><span class="sxs-lookup"><span data-stu-id="b77ef-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b77ef-198">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b77ef-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="b77ef-199">El objetivo de esta sección es crear un usuario de prueba en el Portal de administración de Azure llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b77ef-199">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="b77ef-201">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="b77ef-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b77ef-202">En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-202">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b77ef-204">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="b77ef-204">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b77ef-206">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-206">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b77ef-208">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="b77ef-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b77ef-210">a.</span><span class="sxs-lookup"><span data-stu-id="b77ef-210">a.</span></span> <span data-ttu-id="b77ef-211">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b77ef-212">b.</span><span class="sxs-lookup"><span data-stu-id="b77ef-212">b.</span></span> <span data-ttu-id="b77ef-213">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b77ef-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b77ef-214">c.</span><span class="sxs-lookup"><span data-stu-id="b77ef-214">c.</span></span> <span data-ttu-id="b77ef-215">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b77ef-216">d.</span><span class="sxs-lookup"><span data-stu-id="b77ef-216">d.</span></span> <span data-ttu-id="b77ef-217">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="b77ef-218">Creación de un usuario de prueba de GitHub</span><span class="sxs-lookup"><span data-stu-id="b77ef-218">Creating a GitHub test user</span></span>

<span data-ttu-id="b77ef-219">Para permitir que los usuarios de Azure AD inicien sesión en GitHub, tienen que aprovisionarse en GitHub.</span><span class="sxs-lookup"><span data-stu-id="b77ef-219">In order to enable Azure AD users to log into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="b77ef-220">En el caso de GitHub, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="b77ef-220">In the case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="b77ef-221">**Para aprovisionar cuentas de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="b77ef-221">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="b77ef-222">Inicie sesión en el sitio de la empresa de GitHub como administrador.</span><span class="sxs-lookup"><span data-stu-id="b77ef-222">Log in to your GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="b77ef-223">Haga clic en **Contactos**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-223">Click **People**.</span></span>

    <span data-ttu-id="b77ef-224">![Personas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="b77ef-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="b77ef-225">Haga clic en **Invitar a miembros**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-225">Click **Invite member**.</span></span>

    <span data-ttu-id="b77ef-226">![Invitar a usuarios](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invitar a usuarios")</span><span class="sxs-lookup"><span data-stu-id="b77ef-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="b77ef-227">En la página de diálogo **Invitar a miembros**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="b77ef-227">On the **Invite member** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="b77ef-228">a.</span><span class="sxs-lookup"><span data-stu-id="b77ef-228">a.</span></span> <span data-ttu-id="b77ef-229">En el cuadro de texto **Correo electrónico**, escriba la dirección de correo electrónico de la cuenta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b77ef-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="b77ef-230">![Invitar a personas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invitar a personas")</span><span class="sxs-lookup"><span data-stu-id="b77ef-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="b77ef-231">b.</span><span class="sxs-lookup"><span data-stu-id="b77ef-231">b.</span></span> <span data-ttu-id="b77ef-232">Haga clic en **Enviar invitación**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="b77ef-233">![Invitar a personas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invitar a personas")</span><span class="sxs-lookup"><span data-stu-id="b77ef-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="b77ef-234">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo y seguirá un vínculo para confirmar su cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="b77ef-234">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b77ef-235">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b77ef-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b77ef-236">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a GitHub.</span><span class="sxs-lookup"><span data-stu-id="b77ef-236">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to GitHub.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="b77ef-238">**Para asignar a Britta Simon a GitHub, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b77ef-238">**To assign Britta Simon to GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="b77ef-239">En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y seleccione **Aplicaciones empresariales**. Después, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-239">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b77ef-241">En la lista de aplicaciones, seleccione **Github.com**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-241">In the applications list, select **GitHub.com**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="b77ef-243">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-243">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="b77ef-245">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-245">Click **Add** button.</span></span> <span data-ttu-id="b77ef-246">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="b77ef-248">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="b77ef-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b77ef-249">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b77ef-250">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b77ef-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="b77ef-251">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="b77ef-251">Testing single sign-on</span></span>

<span data-ttu-id="b77ef-252">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b77ef-252">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b77ef-253">Al hacer clic en el icono de GitHub del panel de acceso, debería iniciar sesión automáticamente en su aplicación GitHub.</span><span class="sxs-lookup"><span data-stu-id="b77ef-253">When you click the GitHub tile in the Access Panel, you should get signed-on to your GitHub application.</span></span> <span data-ttu-id="b77ef-254">Iniciará sesión como una cuenta de organización, pero deberá iniciar sesión con su cuenta personal.</span><span class="sxs-lookup"><span data-stu-id="b77ef-254">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b77ef-255">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b77ef-255">Additional resources</span></span>

* [<span data-ttu-id="b77ef-256">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b77ef-256">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b77ef-257">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b77ef-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png

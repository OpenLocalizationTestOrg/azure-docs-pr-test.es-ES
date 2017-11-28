---
title: "Tutorial: Integración de Azure Active Directory con Kantega SSO for JIRA | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Kantega SSO for JIRA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2af4891-e3c8-43b3-bdcb-0500c493e9b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 06a1d301818f025270137f7eaa9f40e5e4503112
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-jira"></a><span data-ttu-id="48291-103">Tutorial: Integración de Azure Active Directory con Kantega SSO for JIRA</span><span class="sxs-lookup"><span data-stu-id="48291-103">Tutorial: Azure Active Directory integration with Kantega SSO for JIRA</span></span>

<span data-ttu-id="48291-104">En este tutorial obtendrá información sobre cómo integrar Kantega SSO for JIRA con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48291-104">In this tutorial, you learn how to integrate Kantega SSO for JIRA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48291-105">La integración de Kantega SSO for JIRA con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="48291-105">Integrating Kantega SSO for JIRA with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="48291-106">Puede controlar en Azure AD quién tiene acceso a Kantega SSO for JIRA.</span><span class="sxs-lookup"><span data-stu-id="48291-106">You can control in Azure AD who has access to Kantega SSO for JIRA</span></span>
- <span data-ttu-id="48291-107">Puede permitir que los usuarios inicien sesión automáticamente en Kantega SSO for JIRA (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48291-107">You can enable your users to automatically get signed-on to Kantega SSO for JIRA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="48291-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="48291-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="48291-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="48291-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48291-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="48291-110">Prerequisites</span></span>

<span data-ttu-id="48291-111">Para configurar la integración de Azure AD con Kantega SSO for JIRA, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="48291-111">To configure Azure AD integration with Kantega SSO for JIRA, you need the following items:</span></span>

- <span data-ttu-id="48291-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="48291-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48291-113">Una suscripción habilitada para el inicio de sesión único de Kantega SSO for JIRA</span><span class="sxs-lookup"><span data-stu-id="48291-113">A Kantega SSO for JIRA single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48291-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="48291-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48291-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="48291-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48291-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="48291-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48291-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48291-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48291-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="48291-118">Scenario description</span></span>
<span data-ttu-id="48291-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="48291-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48291-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="48291-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48291-121">Agregar Kantega SSO for JIRA desde la galería</span><span class="sxs-lookup"><span data-stu-id="48291-121">Adding Kantega SSO for JIRA from the gallery</span></span>
2. <span data-ttu-id="48291-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="48291-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-jira-from-the-gallery"></a><span data-ttu-id="48291-123">Agregar Kantega SSO for JIRA desde la galería</span><span class="sxs-lookup"><span data-stu-id="48291-123">Adding Kantega SSO for JIRA from the gallery</span></span>
<span data-ttu-id="48291-124">Para configurar la integración de Kantega SSO for JIRA en Azure AD, tiene que agregar Kantega SSO for JIRA desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="48291-124">To configure the integration of Kantega SSO for JIRA into Azure AD, you need to add Kantega SSO for JIRA from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="48291-125">**Para agregar Kantega SSO for JIRA desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="48291-125">**To add Kantega SSO for JIRA from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="48291-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="48291-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="48291-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="48291-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="48291-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="48291-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="48291-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="48291-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="48291-133">En el cuadro de búsqueda, escriba **Kantega SSO for JIRA**.</span><span class="sxs-lookup"><span data-stu-id="48291-133">In the search box, type **Kantega SSO for JIRA**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_search.png)

5. <span data-ttu-id="48291-135">En el panel de resultados, seleccione **Kantega SSO for JIRA** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48291-135">In the results panel, select **Kantega SSO for JIRA**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48291-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="48291-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48291-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Kantega SSO for JIRA con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="48291-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for JIRA based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="48291-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Kantega SSO for JIRA para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48291-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for JIRA is to a user in Azure AD.</span></span> <span data-ttu-id="48291-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Kantega SSO for JIRA.</span><span class="sxs-lookup"><span data-stu-id="48291-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for JIRA needs to be established.</span></span>

<span data-ttu-id="48291-141">Para establecer la relación de vínculo, en Kantega SSO for JIRA, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="48291-141">In Kantega SSO for JIRA, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="48291-142">Para configurar y probar el inicio de sesión único de Azure AD con Kantega SSO for JIRA, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="48291-142">To configure and test Azure AD single sign-on with Kantega SSO for JIRA, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="48291-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="48291-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="48291-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48291-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48291-145">**[Creación de un usuario de prueba de Kantega SSO for JIRA](#creating-a-kantega-sso-for-jira-test-user)**: Para tener un homólogo de Britta Simon en Kantega SSO for JIRA que esté vinculado a la representación de Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="48291-145">**[Creating a Kantega SSO for JIRA test user](#creating-a-kantega-sso-for-jira-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for JIRA that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="48291-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48291-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48291-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="48291-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48291-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="48291-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="48291-149">En esta sección habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Kantega SSO for JIRA.</span><span class="sxs-lookup"><span data-stu-id="48291-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for JIRA application.</span></span>

<span data-ttu-id="48291-150">**Para configurar el inicio de sesión único de Azure AD con Kantega SSO for JIRA, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="48291-150">**To configure Azure AD single sign-on with Kantega SSO for JIRA, perform the following steps:**</span></span>

1. <span data-ttu-id="48291-151">En Azure Portal, en la página de integración de la aplicación **Kantega SSO for JIRA**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="48291-151">In the Azure portal, on the **Kantega SSO for JIRA** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="48291-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="48291-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_samlbase.png)

3. <span data-ttu-id="48291-155">En el modo de inicio de **IDP**, en la sección **Dominio y direcciones URL de Kantega SSO for JIRA** realice el paso siguiente:</span><span class="sxs-lookup"><span data-stu-id="48291-155">In **IDP** initiated mode, on the **Kantega SSO for JIRA Domain and URLs** section perform the following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url1.png)

    <span data-ttu-id="48291-157">a.</span><span class="sxs-lookup"><span data-stu-id="48291-157">a.</span></span> <span data-ttu-id="48291-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="48291-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="48291-159">b.</span><span class="sxs-lookup"><span data-stu-id="48291-159">b.</span></span> <span data-ttu-id="48291-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`.</span><span class="sxs-lookup"><span data-stu-id="48291-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="48291-161">En el modo de inicio de **SP**, active la casilla **Mostrar configuración avanzada de URL** y realice el siguiente paso:</span><span class="sxs-lookup"><span data-stu-id="48291-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform the following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url2.png)

    <span data-ttu-id="48291-163">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`.</span><span class="sxs-lookup"><span data-stu-id="48291-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="48291-164">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="48291-164">These values are not real.</span></span> <span data-ttu-id="48291-165">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="48291-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="48291-166">Estos valores se reciben durante la configuración del complemento de Jira, que se explica más adelante en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="48291-166">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="48291-167">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="48291-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_certificate.png) 

6. <span data-ttu-id="48291-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="48291-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="48291-171">En otra ventana del explorador web, inicie sesión en el servidor local de JIRA como administrador.</span><span class="sxs-lookup"><span data-stu-id="48291-171">In a different web browser window, log in to your JIRA on premise server as an administrator.</span></span>

8. <span data-ttu-id="48291-172">Mantenga el mouse encima del icono de engranaje y haga clic en **Complementos**.</span><span class="sxs-lookup"><span data-stu-id="48291-172">Hover on cog and click the **Add-ons**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon1.png)

9. <span data-ttu-id="48291-174">En la sección de la pestaña Complementos, haga clic en **Find new add-ons** (Buscar nuevos complementos).</span><span class="sxs-lookup"><span data-stu-id="48291-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="48291-175">Busque **Kantega SSO for JIRA (SAML & Kerberos)** y haga clic en el botón **Instalar** para instalar el nuevo complemento SAML.</span><span class="sxs-lookup"><span data-stu-id="48291-175">Search **Kantega SSO for JIRA (SAML & Kerberos)** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon2.png)

10. <span data-ttu-id="48291-177">Se inicia la instalación del complemento.</span><span class="sxs-lookup"><span data-stu-id="48291-177">The plugin installation starts.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon3.png)

11. <span data-ttu-id="48291-179">Una vez completada la instalación.</span><span class="sxs-lookup"><span data-stu-id="48291-179">Once the installation is complete.</span></span> <span data-ttu-id="48291-180">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="48291-180">Click **Close**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon33.png)

12. <span data-ttu-id="48291-182">Haga clic en **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="48291-182">Click **Manage**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon34.png)
    
13. <span data-ttu-id="48291-184">El nuevo complemento aparece en **INTEGRACIONES**.</span><span class="sxs-lookup"><span data-stu-id="48291-184">New plugin is listed under **INTEGRATIONS**.</span></span> <span data-ttu-id="48291-185">Haga clic en **Configurar** para configurar el nuevo complemento.</span><span class="sxs-lookup"><span data-stu-id="48291-185">Click **Configure** to configure the new plugin.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon35.png)

14. <span data-ttu-id="48291-187">En la sección **SAML**.</span><span class="sxs-lookup"><span data-stu-id="48291-187">In the **SAML** section.</span></span> <span data-ttu-id="48291-188">Seleccione **Azure Active Directory (Azure AD)** en la lista desplegable **Agregar proveedor de identidades**.</span><span class="sxs-lookup"><span data-stu-id="48291-188">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon4.png)

15. <span data-ttu-id="48291-190">Seleccione el nivel de suscripción **Básica**.</span><span class="sxs-lookup"><span data-stu-id="48291-190">Select subscription level as **Basic**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon5.png)     

16. <span data-ttu-id="48291-192">En la sección **Agregar propiedades**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="48291-192">On the **App properties** section, perform following steps:</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon6.png)

    <span data-ttu-id="48291-194">a.</span><span class="sxs-lookup"><span data-stu-id="48291-194">a.</span></span> <span data-ttu-id="48291-195">Copie el valor **URI de id. de aplicación** y úselo como **Identificador, Dirección URL de respuesta y Dirección URL de inicio de sesión** en la sección **Dominio y direcciones URL de Kantega SSO for JIRA** en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="48291-195">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for JIRA Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="48291-196">b.</span><span class="sxs-lookup"><span data-stu-id="48291-196">b.</span></span> <span data-ttu-id="48291-197">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="48291-197">Click **Next**.</span></span>

17. <span data-ttu-id="48291-198">En la sección **Importar metadatos**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="48291-198">On the **Metadata import** section, perform following steps:</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon7.png)

    <span data-ttu-id="48291-200">a.</span><span class="sxs-lookup"><span data-stu-id="48291-200">a.</span></span> <span data-ttu-id="48291-201">Seleccione **Archivo de metadatos en el equipo** y cargue el archivo de metadatos que descargó desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="48291-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="48291-202">b.</span><span class="sxs-lookup"><span data-stu-id="48291-202">b.</span></span> <span data-ttu-id="48291-203">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="48291-203">Click **Next**.</span></span>

18. <span data-ttu-id="48291-204">En la sección**Name and SSO location** (Nombre y ubicación de SSO), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="48291-204">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon8.png)
    
    <span data-ttu-id="48291-206">a.</span><span class="sxs-lookup"><span data-stu-id="48291-206">a.</span></span> <span data-ttu-id="48291-207">Agregue el nombre del proveedor de identidades en el cuadro de texto **Nombre del proveedor de identidades** (por ejemplo, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48291-207">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="48291-208">b.</span><span class="sxs-lookup"><span data-stu-id="48291-208">b.</span></span> <span data-ttu-id="48291-209">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="48291-209">Click **Next**.</span></span>

19. <span data-ttu-id="48291-210">Compruebe el certificado de firma y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="48291-210">Verify the Signing certificate and click **Next**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon9.png)

20. <span data-ttu-id="48291-212">En la sección **Cuentas de usuario de JIRA**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="48291-212">On the **JIRA user accounts** section, perform following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon10.png)

    <span data-ttu-id="48291-214">a.</span><span class="sxs-lookup"><span data-stu-id="48291-214">a.</span></span> <span data-ttu-id="48291-215">Seleccione **Create users in JIRA's internal Directory if needed** (Crear usuarios en el directorio interno de JIRA si es necesario) y escriba el nombre adecuado del grupo de usuarios (puede ser un número múltiple</span><span class="sxs-lookup"><span data-stu-id="48291-215">Select **Create users in JIRA's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="48291-216">de grupos separados por coma).</span><span class="sxs-lookup"><span data-stu-id="48291-216">of groups separated by comma).</span></span>

    <span data-ttu-id="48291-217">b.</span><span class="sxs-lookup"><span data-stu-id="48291-217">b.</span></span> <span data-ttu-id="48291-218">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="48291-218">Click **Next**.</span></span>

21. <span data-ttu-id="48291-219">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="48291-219">Click **Finish**.</span></span>   

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon11.png)

22. <span data-ttu-id="48291-221">En la sección **Known domains for Azure AD** (Dominios conocidos para Azure AD), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="48291-221">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/addon12.png)

    <span data-ttu-id="48291-223">a.</span><span class="sxs-lookup"><span data-stu-id="48291-223">a.</span></span> <span data-ttu-id="48291-224">Seleccione **Known domains** (Dominios conocidos) en el panel izquierdo de la página.</span><span class="sxs-lookup"><span data-stu-id="48291-224">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="48291-225">b.</span><span class="sxs-lookup"><span data-stu-id="48291-225">b.</span></span> <span data-ttu-id="48291-226">Escriba el nombre de dominio en el cuadro de texto **Known domains** (Dominios conocidos).</span><span class="sxs-lookup"><span data-stu-id="48291-226">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="48291-227">c.</span><span class="sxs-lookup"><span data-stu-id="48291-227">c.</span></span> <span data-ttu-id="48291-228">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="48291-228">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="48291-229">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48291-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="48291-230">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="48291-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="48291-231">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48291-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48291-232">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="48291-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="48291-233">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="48291-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="48291-235">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="48291-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="48291-236">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="48291-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="48291-238">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="48291-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="48291-240">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="48291-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="48291-242">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="48291-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="48291-244">a.</span><span class="sxs-lookup"><span data-stu-id="48291-244">a.</span></span> <span data-ttu-id="48291-245">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48291-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48291-246">b.</span><span class="sxs-lookup"><span data-stu-id="48291-246">b.</span></span> <span data-ttu-id="48291-247">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48291-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="48291-248">c.</span><span class="sxs-lookup"><span data-stu-id="48291-248">c.</span></span> <span data-ttu-id="48291-249">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="48291-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="48291-250">d.</span><span class="sxs-lookup"><span data-stu-id="48291-250">d.</span></span> <span data-ttu-id="48291-251">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="48291-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-jira-test-user"></a><span data-ttu-id="48291-252">Crear un usuario de prueba de Kantega SSO for JIRA</span><span class="sxs-lookup"><span data-stu-id="48291-252">Creating a Kantega SSO for JIRA test user</span></span>

<span data-ttu-id="48291-253">Para permitir que los usuarios de Azure AD inicien sesión en JIRA, tienen que aprovisionarse en JIRA.</span><span class="sxs-lookup"><span data-stu-id="48291-253">To enable Azure AD users to log in to JIRA, they must be provisioned into JIRA.</span></span> <span data-ttu-id="48291-254">En Kantega SSO for JIRA, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="48291-254">In Kantega SSO for JIRA, provisioning is a manual task.</span></span>

<span data-ttu-id="48291-255">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="48291-255">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="48291-256">Inicie sesión como administrador en el servidor local de JIRA.</span><span class="sxs-lookup"><span data-stu-id="48291-256">Log in to your JIRA on premise server as an administrator.</span></span>

2. <span data-ttu-id="48291-257">Mantenga el mouse encima del icono de engranaje y haga clic en **Administración de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="48291-257">Hover on cog and click the **User management**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-kantegassoforjira-tutorial/user1.png) 

3. <span data-ttu-id="48291-259">En la sección de la pestaña **Administración de usuarios**, haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="48291-259">Under **User management** tab section, click **Create user**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-kantegassoforjira-tutorial/user2.png) 

4. <span data-ttu-id="48291-261">En la página del cuadro de diálogo **"Create New User"** (Crear nuevo usuario), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="48291-261">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Agregar empleado](./media/active-directory-saas-kantegassoforjira-tutorial/user3.png) 

    <span data-ttu-id="48291-263">a.</span><span class="sxs-lookup"><span data-stu-id="48291-263">a.</span></span> <span data-ttu-id="48291-264">En el cuadro de texto **Dirección de correo electrónico**, escriba la dirección de correo electrónico de un usuario, por ejemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="48291-264">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="48291-265">b.</span><span class="sxs-lookup"><span data-stu-id="48291-265">b.</span></span> <span data-ttu-id="48291-266">En el cuadro de texto **Nombre completo**, escriba el nombre completo de un usuario, por ejemplo, Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48291-266">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="48291-267">c.</span><span class="sxs-lookup"><span data-stu-id="48291-267">c.</span></span> <span data-ttu-id="48291-268">En el cuadro de texto **Nombre de usuario**, escriba el correo electrónico de un usuario, por ejemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="48291-268">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="48291-269">d.</span><span class="sxs-lookup"><span data-stu-id="48291-269">d.</span></span> <span data-ttu-id="48291-270">En el cuadro de texto **Contraseña**, escriba la contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="48291-270">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="48291-271">e.</span><span class="sxs-lookup"><span data-stu-id="48291-271">e.</span></span> <span data-ttu-id="48291-272">Haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="48291-272">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="48291-273">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="48291-273">Assigning the Azure AD test user</span></span>

<span data-ttu-id="48291-274">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Kantega SSO for JIRA.</span><span class="sxs-lookup"><span data-stu-id="48291-274">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for JIRA.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="48291-276">**Para asignar a Britta Simon a Kantega SSO for JIRA, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="48291-276">**To assign Britta Simon to Kantega SSO for JIRA, perform the following steps:**</span></span>

1. <span data-ttu-id="48291-277">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="48291-277">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="48291-279">En la lista de aplicaciones, seleccione **Kantega SSO for JIRA**.</span><span class="sxs-lookup"><span data-stu-id="48291-279">In the applications list, select **Kantega SSO for JIRA**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_app.png) 

3. <span data-ttu-id="48291-281">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="48291-281">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="48291-283">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="48291-283">Click **Add** button.</span></span> <span data-ttu-id="48291-284">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="48291-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="48291-286">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="48291-286">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="48291-287">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="48291-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="48291-288">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="48291-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="48291-289">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="48291-289">Testing single sign-on</span></span>

<span data-ttu-id="48291-290">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="48291-290">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="48291-291">Al hacer clic en el icono de Kantega SSO for JIRA en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Kantega SSO for JIRA.</span><span class="sxs-lookup"><span data-stu-id="48291-291">When you click the Kantega SSO for JIRA tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for JIRA application.</span></span>
<span data-ttu-id="48291-292">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="48291-292">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="48291-293">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="48291-293">Additional resources</span></span>

* [<span data-ttu-id="48291-294">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48291-294">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48291-295">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="48291-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_203.png


---
title: "Tutorial: Integración de Azure Active Directory con Tableau Server | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Tableau Server."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 6b35609d88fbbf649e15863901d521886db2a4d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="e04e4-103">Tutorial: Integración de Azure Active Directory con Tableau Server</span><span class="sxs-lookup"><span data-stu-id="e04e4-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="e04e4-104">En este tutorial, aprenderá a integrar Tableau Server con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e04e4-104">In this tutorial, you learn how to integrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e04e4-105">Integrar Tableau Server con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e04e4-105">Integrating Tableau Server with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e04e4-106">Puede controlar en Azure AD quién tiene acceso a Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="e04e4-106">You can control in Azure AD who has access to Tableau Server</span></span>
- <span data-ttu-id="e04e4-107">Puede permitir que los usuarios inicien sesión automáticamente en Tableau Server (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e04e4-107">You can enable your users to automatically get signed-on to Tableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e04e4-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e04e4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e04e4-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e04e4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e04e4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e04e4-110">Prerequisites</span></span>

<span data-ttu-id="e04e4-111">Para configurar la integración de Azure AD con Tableau Server, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e04e4-111">To configure Azure AD integration with Tableau Server, you need the following items:</span></span>

- <span data-ttu-id="e04e4-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e04e4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e04e4-113">Una suscripción habilitada para el inicio de sesión único en Tableau Server</span><span class="sxs-lookup"><span data-stu-id="e04e4-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e04e4-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e04e4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e04e4-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e04e4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e04e4-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e04e4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e04e4-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e04e4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e04e4-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e04e4-118">Scenario description</span></span>
<span data-ttu-id="e04e4-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e04e4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e04e4-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="e04e4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e04e4-121">Incorporación de Tableau Server desde la galería</span><span class="sxs-lookup"><span data-stu-id="e04e4-121">Adding Tableau Server from the gallery</span></span>
2. <span data-ttu-id="e04e4-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e04e4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-the-gallery"></a><span data-ttu-id="e04e4-123">Incorporación de Tableau Server desde la galería</span><span class="sxs-lookup"><span data-stu-id="e04e4-123">Adding Tableau Server from the gallery</span></span>
<span data-ttu-id="e04e4-124">Para configurar la integración de Tableau Server en Azure AD, será preciso que agregue Tableau Server desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="e04e4-124">To configure the integration of Tableau Server into Azure AD, you need to add Tableau Server from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e04e4-125">**Para agregar Tableau Server desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e04e4-125">**To add Tableau Server from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e04e4-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e04e4-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e04e4-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e04e4-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e04e4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e04e4-133">En el cuadro de búsqueda, escriba **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-133">In the search box, type **Tableau Server**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="e04e4-135">En el panel de resultados, seleccione **Tableau Server** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e04e4-135">In the results panel, select **Tableau Server**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e04e4-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e04e4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e04e4-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Tableau Server con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e04e4-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e04e4-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Tableau Server para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e04e4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Server is to a user in Azure AD.</span></span> <span data-ttu-id="e04e4-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="e04e4-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Server needs to be established.</span></span>

<span data-ttu-id="e04e4-141">Para establecer la relación de vínculo, en Tableau Server, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-141">In Tableau Server, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e04e4-142">Para configurar y probar el inicio de sesión único de Azure AD con Tableau Server, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e04e4-142">To configure and test Azure AD single sign-on with Tableau Server, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e04e4-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="e04e4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e04e4-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e04e4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e04e4-145">**[Creación de un usuario de prueba de Tableau Server](#creating-a-tableau-server-test-user)** : para tener un homólogo de Britta Simon en Tableau Server vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e04e4-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - to have a counterpart of Britta Simon in Tableau Server that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e04e4-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e04e4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e04e4-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e04e4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e04e4-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e04e4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e04e4-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="e04e4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="e04e4-150">**Para configurar el inicio de sesión único de Azure AD con Tableau Server, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e04e4-150">**To configure Azure AD single sign-on with Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="e04e4-151">En Azure Portal, en la página de integración de la aplicación **Tableau Server**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-151">In the Azure portal, on the **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e04e4-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e04e4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="e04e4-155">En la sección **Tableau Server Domain and URLs** (Dominio y direcciones URL de Tableau Server), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e04e4-155">On the **Tableau Server Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="e04e4-157">a.</span><span class="sxs-lookup"><span data-stu-id="e04e4-157">a.</span></span> <span data-ttu-id="e04e4-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://azure.<domain name>.link`.</span><span class="sxs-lookup"><span data-stu-id="e04e4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="e04e4-159">b.</span><span class="sxs-lookup"><span data-stu-id="e04e4-159">b.</span></span> <span data-ttu-id="e04e4-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="e04e4-160">In the **Identifier** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="e04e4-161">c.</span><span class="sxs-lookup"><span data-stu-id="e04e4-161">c.</span></span> <span data-ttu-id="e04e4-162">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://azure.<domain name>.link/wg/saml/SSO/index.html`.</span><span class="sxs-lookup"><span data-stu-id="e04e4-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="e04e4-163">Los valores anteriores no son valores reales.</span><span class="sxs-lookup"><span data-stu-id="e04e4-163">The preceding values are not real values.</span></span> <span data-ttu-id="e04e4-164">Más adelante, actualice los valores con la dirección URL y el identificador reales de la página de configuración de Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="e04e4-164">Later, you update the values with the actual URL and identifier from the Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="e04e4-165">La aplicación Tableau Server espera las aserciones de SAML en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="e04e4-165">Tableau Server application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="e04e4-166">Configure las siguientes notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="e04e4-166">Configure the following claims for this application.</span></span> <span data-ttu-id="e04e4-167">Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e04e4-167">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="e04e4-168">En la siguiente captura de pantalla se muestra un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e04e4-168">The following screenshot shows an example for the same.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="e04e4-170">En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo Token SAML como muestra la imagen anterior y realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="e04e4-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="e04e4-171">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="e04e4-171">Attribute Name</span></span> | <span data-ttu-id="e04e4-172">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="e04e4-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="e04e4-173">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="e04e4-173">username</span></span> | <span data-ttu-id="e04e4-174">*user.displayname*</span><span class="sxs-lookup"><span data-stu-id="e04e4-174">*user.displayname*</span></span> |

    <span data-ttu-id="e04e4-175">a.</span><span class="sxs-lookup"><span data-stu-id="e04e4-175">a.</span></span> <span data-ttu-id="e04e4-176">Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="e04e4-179">b.</span><span class="sxs-lookup"><span data-stu-id="e04e4-179">b.</span></span> <span data-ttu-id="e04e4-180">En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.</span><span class="sxs-lookup"><span data-stu-id="e04e4-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="e04e4-181">c.</span><span class="sxs-lookup"><span data-stu-id="e04e4-181">c.</span></span> <span data-ttu-id="e04e4-182">En la lista **Valor**, seleccione el atributo que se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="e04e4-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="e04e4-183">d.</span><span class="sxs-lookup"><span data-stu-id="e04e4-183">d.</span></span> <span data-ttu-id="e04e4-184">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-184">Click **Ok**</span></span>


6. <span data-ttu-id="e04e4-185">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e04e4-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="e04e4-187">Haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-187">Click **Save** button.</span></span>

    <span data-ttu-id="e04e4-188">![Configuración del inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="e04e4-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="e04e4-189">Para configurar SSO para la aplicación, debe iniciar sesión en su inquilino de Tableau Server como administrador.</span><span class="sxs-lookup"><span data-stu-id="e04e4-189">To get SSO configured for your application, you need to sign-on to your Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="e04e4-190">a.</span><span class="sxs-lookup"><span data-stu-id="e04e4-190">a.</span></span> <span data-ttu-id="e04e4-191">En la configuración de Tableau Server, haga clic en la pestaña **SAML** .</span><span class="sxs-lookup"><span data-stu-id="e04e4-191">In the Tableau Server configuration, click the **SAML** tab.</span></span>
  
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="e04e4-193">b.</span><span class="sxs-lookup"><span data-stu-id="e04e4-193">b.</span></span> <span data-ttu-id="e04e4-194">Active la casilla de **Use SAML for single sign-on**(Usar SAML para inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="e04e4-194">Select the checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="e04e4-195">c.</span><span class="sxs-lookup"><span data-stu-id="e04e4-195">c.</span></span> <span data-ttu-id="e04e4-196">URL de retorno de Tableau Server: es la URL a la que accederán los usuarios de Tableau Server, como http://servidor_de_tableau.</span><span class="sxs-lookup"><span data-stu-id="e04e4-196">Tableau Server return URL—The URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="e04e4-197">No se recomienda usar http://localhost.</span><span class="sxs-lookup"><span data-stu-id="e04e4-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="e04e4-198">No se permite usar una dirección URL con una barra diagonal final (por ejemplo, http://servidor_de_tableau/).</span><span class="sxs-lookup"><span data-stu-id="e04e4-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="e04e4-199">Copie el valor de **Tableau Server return URL** (URL de retorno de Tableau Server) y péguelo en el cuadro de texto **URL de inicio de sesión** de la sección **Tableau Server Domain and URLs** (Dominio y direcciones URL de Tableau Server) de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e04e4-199">Copy **Tableau Server return URL** and paste it to Azure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="e04e4-200">d.</span><span class="sxs-lookup"><span data-stu-id="e04e4-200">d.</span></span> <span data-ttu-id="e04e4-201">SAML entity ID (Id. de entidad SAML): el identificador de entidad identifica de forma exclusiva la instalación de Tableau Server en el IdP.</span><span class="sxs-lookup"><span data-stu-id="e04e4-201">SAML entity ID—The entity ID uniquely identifies your Tableau Server installation to the IdP.</span></span> <span data-ttu-id="e04e4-202">Aquí, si quiere, puede especificar de nuevo la dirección URL de Tableau Server, pero no tiene que ser esa misma URL.</span><span class="sxs-lookup"><span data-stu-id="e04e4-202">You can enter your Tableau Server URL again here, if you like, but it does not have to be your Tableau Server URL.</span></span> <span data-ttu-id="e04e4-203">Copie el valor de **SAML entity ID** (Id. de entidad SAML) y péguelo en el cuadro de texto **Identificador** de la sección **Tableau Server Domain and URLs** (Dominio y direcciones URL de Tableau Server) de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e04e4-203">Copy **SAML entity ID** and paste it to Azure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="e04e4-204">e.</span><span class="sxs-lookup"><span data-stu-id="e04e4-204">e.</span></span> <span data-ttu-id="e04e4-205">Haga clic en **Export Metadata File** (Exportar archivo de metadatos) y ábralo en la aplicación del editor de texto.</span><span class="sxs-lookup"><span data-stu-id="e04e4-205">Click the **Export Metadata File** and open it in the text editor application.</span></span> <span data-ttu-id="e04e4-206">Busque la URL del Servicio de consumidor de aserciones con Http Post e índice 0 y copie la URL.</span><span class="sxs-lookup"><span data-stu-id="e04e4-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy the URL.</span></span> <span data-ttu-id="e04e4-207">Ahora, péguelo en el cuadro de texto **URL de respuesta** de la sección **Tableau Server Domain and URLs** (Dominio y direcciones URL de Tableau Server) de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e04e4-207">Now paste it to Azure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="e04e4-208">f.</span><span class="sxs-lookup"><span data-stu-id="e04e4-208">f.</span></span> <span data-ttu-id="e04e4-209">Busque el archivo de metadatos de federación descargado desde Azure Portal y cárguelo en el **SAML Idp metadata file**(Archivo de metadatos del proveedor de identidades SAML).</span><span class="sxs-lookup"><span data-stu-id="e04e4-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in the **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="e04e4-210">g.</span><span class="sxs-lookup"><span data-stu-id="e04e4-210">g.</span></span> <span data-ttu-id="e04e4-211">Haga clic en el botón **Aceptar** de la página de configuración de Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="e04e4-211">Click the **OK** button in the Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="e04e4-212">El cliente tiene que cargar los certificados en la configuración de SSO de SAML de Tableau Server para que se omitan en el flujo de SSO.</span><span class="sxs-lookup"><span data-stu-id="e04e4-212">Customer have to upload any certificate in the Tableau Server SAML SSO configuration and it will get ignored in the SSO flow.</span></span>
    ><span data-ttu-id="e04e4-213">Si necesita ayuda para configurar SAML en Tableau Server, vea el artículo [Configuración de SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="e04e4-213">If you need help configuring SAML on Tableau Server then please refer to this article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="e04e4-214">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e04e4-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e04e4-215">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e04e4-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e04e4-216">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e04e4-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e04e4-217">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e04e4-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="e04e4-218">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e04e4-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e04e4-220">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="e04e4-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e04e4-221">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e04e4-223">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e04e4-225">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e04e4-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e04e4-227">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="e04e4-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e04e4-229">a.</span><span class="sxs-lookup"><span data-stu-id="e04e4-229">a.</span></span> <span data-ttu-id="e04e4-230">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e04e4-231">b.</span><span class="sxs-lookup"><span data-stu-id="e04e4-231">b.</span></span> <span data-ttu-id="e04e4-232">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e04e4-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e04e4-233">c.</span><span class="sxs-lookup"><span data-stu-id="e04e4-233">c.</span></span> <span data-ttu-id="e04e4-234">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e04e4-235">d.</span><span class="sxs-lookup"><span data-stu-id="e04e4-235">d.</span></span> <span data-ttu-id="e04e4-236">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="e04e4-237">Crear un usuario de prueba de Tableau Server</span><span class="sxs-lookup"><span data-stu-id="e04e4-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="e04e4-238">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="e04e4-238">The objective of this section is to create a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="e04e4-239">Debe aprovisionar todos los usuarios en el servidor de Tableau.</span><span class="sxs-lookup"><span data-stu-id="e04e4-239">You need to provision all the users in the Tableau server.</span></span> 

<span data-ttu-id="e04e4-240">Tenga en cuenta que el nombre de usuario debe coincidir con el valor que ha configurado en el atributo personalizado de **nombre de usuario** de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e04e4-240">That username of the user should match the value which you have configured in the Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="e04e4-241">Con la asignación correcta, la integración debería funcionar. [Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="e04e4-241">With the correct mapping the integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="e04e4-242">Si necesita crear un usuario manualmente, póngase en contacto con el administrador de Tableau Server de su organización.</span><span class="sxs-lookup"><span data-stu-id="e04e4-242">If you need to create a user manually, you need to contact the Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e04e4-243">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e04e4-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e04e4-244">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="e04e4-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Server.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e04e4-246">**Para asignar Britta Simon a Tableau Server, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e04e4-246">**To assign Britta Simon to Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="e04e4-247">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e04e4-249">En la lista de aplicaciones, seleccione **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-249">In the applications list, select **Tableau Server**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="e04e4-251">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e04e4-253">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-253">Click **Add** button.</span></span> <span data-ttu-id="e04e4-254">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e04e4-256">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e04e4-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e04e4-257">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e04e4-258">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e04e4-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e04e4-259">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e04e4-259">Testing single sign-on</span></span>

<span data-ttu-id="e04e4-260">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e04e4-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e04e4-261">Al hacer clic en el icono de Tableau Server en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="e04e4-261">When you click the Tableau Server tile in the Access Panel, you should get automatically signed-on to your Tableau Server application.</span></span>
<span data-ttu-id="e04e4-262">Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="e04e4-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e04e4-263">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e04e4-263">Additional resources</span></span>

* [<span data-ttu-id="e04e4-264">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e04e4-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e04e4-265">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e04e4-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png


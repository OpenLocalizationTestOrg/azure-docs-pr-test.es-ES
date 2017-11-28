---
title: "Tutorial: Integración de Azure Active Directory con Velpic SAML | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Velpic SAML."
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
ms.openlocfilehash: 5325f3cca00167e6b7b687509ce43435447ad2f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="6c0e5-103">Tutorial: Integración de Azure Active Directory con Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="6c0e5-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="6c0e5-104">En este tutorial, aprenderá a integrar Velpic SAML con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6c0e5-104">In this tutorial, you learn how to integrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6c0e5-105">La integración de Velpic SAML con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="6c0e5-105">Integrating Velpic SAML with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6c0e5-106">En Azure AD se puede controlar quién tiene acceso a Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-106">You can control in Azure AD who has access to Velpic SAML</span></span>
- <span data-ttu-id="6c0e5-107">Puede permitir que los usuarios inicien sesión automáticamente en Velpic SAML (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-107">You can enable your users to automatically get signed-on to Velpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6c0e5-108">Puede administrar sus cuentas en una ubicación central: el Portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="6c0e5-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6c0e5-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c0e5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6c0e5-110">Prerequisites</span></span>

<span data-ttu-id="6c0e5-111">Para configurar la integración de Azure AD con Velpic SAML, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6c0e5-111">To configure Azure AD integration with Velpic SAML, you need the following items:</span></span>

- <span data-ttu-id="6c0e5-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c0e5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6c0e5-113">Una suscripción habilitada para el inicio de sesión único en Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="6c0e5-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6c0e5-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6c0e5-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="6c0e5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6c0e5-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="6c0e5-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6c0e5-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6c0e5-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="6c0e5-118">Scenario description</span></span>
<span data-ttu-id="6c0e5-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6c0e5-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="6c0e5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6c0e5-121">Agregar Velpic SAML desde la galería</span><span class="sxs-lookup"><span data-stu-id="6c0e5-121">Adding Velpic SAML from the gallery</span></span>
2. <span data-ttu-id="6c0e5-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c0e5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-the-gallery"></a><span data-ttu-id="6c0e5-123">Agregar Velpic SAML desde la galería</span><span class="sxs-lookup"><span data-stu-id="6c0e5-123">Adding Velpic SAML from the gallery</span></span>
<span data-ttu-id="6c0e5-124">Para configurar la integración de Velpic SAML en Azure AD, es preciso agregar Velpic SAML desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-124">To configure the integration of Velpic SAML into Azure AD, you need to add Velpic SAML from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6c0e5-125">**Para agregar Velpic SAML desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="6c0e5-125">**To add Velpic SAML from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6c0e5-126">En el panel de navegación izquierdo del **[Portal de administración de Azure](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6c0e5-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6c0e5-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="6c0e5-131">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="6c0e5-133">En el cuadro de búsqueda, escriba **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-133">In the search box, type **Velpic SAML**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="6c0e5-135">En el panel de resultados, seleccione **Velpic SAML** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-135">In the results panel, select **Velpic SAML**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6c0e5-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c0e5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6c0e5-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Velpic SAML utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6c0e5-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6c0e5-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Velpic SAML para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Velpic SAML is to a user in Azure AD.</span></span> <span data-ttu-id="6c0e5-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-140">In other words, a link relationship between an Azure AD user and the related user in Velpic SAML needs to be established.</span></span>

<span data-ttu-id="6c0e5-141">Esta relación de vínculo se establece mediante la asignación del valor de **nombre de usuario** en Azure AD como valor de **Username** (Nombre de usuario) en Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Velpic SAML.</span></span>

<span data-ttu-id="6c0e5-142">Para configurar y probar el inicio de sesión único de Azure AD con Velpic SAML, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="6c0e5-142">To configure and test Azure AD single sign-on with Velpic SAML, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6c0e5-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6c0e5-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6c0e5-145">**[Creación de un usuario de prueba de Velpic SAML](#creating-a-velpic-saml-test-user)**: para tener un homólogo de Britta Simon en Velpic SAML que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - to have a counterpart of Britta Simon in Velpic SAML that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="6c0e5-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6c0e5-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6c0e5-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c0e5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6c0e5-149">En esta sección, habilitará el inicio de sesión único de Azure AD en el Portal de administración de Azure y configurará el inicio de sesión único en la aplicación Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="6c0e5-150">**Para configurar el inicio de sesión único de Azure AD con Velpic SAML, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="6c0e5-150">**To configure Azure AD single sign-on with Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="6c0e5-151">En el Portal de administración de Azure, en la página de integración de aplicaciones de **Velpic SAML**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-151">In the Azure Management portal, on the **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="6c0e5-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="6c0e5-155">Escriba los datos en la sección **Dominio y direcciones URL de Velpic SAML**:</span><span class="sxs-lookup"><span data-stu-id="6c0e5-155">Enter the details in the **Velpic SAML Domain and URLs** section-</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="6c0e5-157">a.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-157">a.</span></span> <span data-ttu-id="6c0e5-158">En el cuadro de texto **URL de inicio de sesión**, escriba el valor como: `https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="6c0e5-158">In the **Sign-on URL** textbox, type the value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="6c0e5-159">b.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-159">b.</span></span> <span data-ttu-id="6c0e5-160">En el cuadro de texto **Identificador**, pegue el valor de **"Single sign on URL"** (URL de inicio de sesión único), `https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="6c0e5-160">In the **Identifier** textbox, paste the **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="6c0e5-161">Tenga en cuenta que la URL de inicio de sesión se la proporcionará el equipo de Velpic SAML y el valor del identificador estará disponible cuando configure el complemento de SSO en Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-161">Please note that the Sign on URL will be provided by the Velpic SAML team and Identifier value will be available when you configure the SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="6c0e5-162">Tiene que copiar ese valor de la página de la aplicación Velpic SAML y pegarlo aquí.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-162">You need to copy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="6c0e5-163">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo XML en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="6c0e5-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="6c0e5-165">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6c0e5-167">En la sección Configuración de Velpic SAML, haga clic en Configurar Velpic SAML para abrir la ventana Configurar inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-167">On the Velpic SAML Configuration section, click Configure Velpic SAML to open Configure sign-on window.</span></span> <span data-ttu-id="6c0e5-168">Copie el Id. de entidad de SAML de la sección Referencia rápida.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-168">Copy the SAML Entity ID from the Quick Reference section.</span></span>

7. <span data-ttu-id="6c0e5-169">En otra ventana del explorador web, inicie sesión como administrador en su sitio de la compañía de Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="6c0e5-170">Haga clic en la pestaña **Manage** (Administrar) y vaya a la sección **Integration** (Integración), donde tiene que hacer clic en el botón **Plugins** (Complementos) para crear el complemento Sign-In (Inicio de sesión).</span><span class="sxs-lookup"><span data-stu-id="6c0e5-170">Click on **Manage** tab and go to **Integration** section where you need to click on **Plugins** button to create new plugin for Sign-In.</span></span>

    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="6c0e5-172">Haga clic en el botón **"Add plugin"** (Agregar complemento).</span><span class="sxs-lookup"><span data-stu-id="6c0e5-172">Click on the **‘Add plugin’** button.</span></span>
    
    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="6c0e5-174">Haga clic en el icono **SAML** de la página Add Plugin (Agregar complemento).</span><span class="sxs-lookup"><span data-stu-id="6c0e5-174">Click on the **SAML** tile in the Add Plugin page.</span></span>
    
    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="6c0e5-176">Escriba el nombre del nuevo complemento SAML y haga clic en el botón **"Add"** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="6c0e5-176">Enter the name of the new SAML plugin and click the **‘Add’** button.</span></span>

    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="6c0e5-178">Especifique los detalles de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="6c0e5-178">Enter the details as follows:</span></span>

    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="6c0e5-180">a.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-180">a.</span></span> <span data-ttu-id="6c0e5-181">En el cuadro de texto **Name** (Nombre), escriba el nombre del complemento SAML.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-181">In the **Name** textbox, type the name of SAML plugin.</span></span>

    <span data-ttu-id="6c0e5-182">b.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-182">b.</span></span> <span data-ttu-id="6c0e5-183">En el cuadro de texto **Issuer URL** (URL del emisor), pegue el **Id. de entidad de SAML** que copió de la ventana **Configurar inicio de sesión** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-183">In the **Issuer URL** textbox, paste the **SAML Entity ID** you copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="6c0e5-184">c.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-184">c.</span></span> <span data-ttu-id="6c0e5-185">En **Provider Metadata Config** (Config. de metadatos del proveedor), cargue el archivo XML de metadatos que descargó de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-185">In the **Provider Metadata Config** upload the Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="6c0e5-186">d.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-186">d.</span></span> <span data-ttu-id="6c0e5-187">También puede habilitar aprovisionamiento Just-In-Time de SAML activando la casilla **"Auto create new users"** (Crear nuevos usuarios automáticamente).</span><span class="sxs-lookup"><span data-stu-id="6c0e5-187">You can also choose to enable SAML just in time provisioning by enabling the **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="6c0e5-188">Si no existe ningún usuario de Velpic y no se habilita esta marca, el inicio desde Azure no se producirá.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-188">If a user doesn’t exist in Velpic and this flag is not enabled, the login from Azure will fail.</span></span> <span data-ttu-id="6c0e5-189">Si se habilita la marca, el usuario se aprovisionará automáticamente en Velpic en el momento de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-189">If the flag is enabled the user will automatically be provisioned into Velpic at the time of login.</span></span> 

    <span data-ttu-id="6c0e5-190">e.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-190">e.</span></span> <span data-ttu-id="6c0e5-191">Copie la **Single sign on URL** (URL de inicio de sesión) en el cuadro de texto y péguela en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-191">Copy the **Single sign on URL** from the text box and paste it in the Azure portal.</span></span>
    
    <span data-ttu-id="6c0e5-192">f.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-192">f.</span></span> <span data-ttu-id="6c0e5-193">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6c0e5-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c0e5-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="6c0e5-195">El objetivo de esta sección es crear un usuario de prueba en el Portal de administración de Azure llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="6c0e5-197">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="6c0e5-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6c0e5-198">En el panel de navegación izquierdo del **Portal de administración de Azure**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6c0e5-200">Vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6c0e5-202">En la parte superior del diálogo, haga clic en **Agregar** para abrir el diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6c0e5-204">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="6c0e5-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6c0e5-206">a.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-206">a.</span></span> <span data-ttu-id="6c0e5-207">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6c0e5-208">b.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-208">b.</span></span> <span data-ttu-id="6c0e5-209">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6c0e5-210">c.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-210">c.</span></span> <span data-ttu-id="6c0e5-211">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6c0e5-212">d.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-212">d.</span></span> <span data-ttu-id="6c0e5-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="6c0e5-214">Creación de un usuario de prueba de Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="6c0e5-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="6c0e5-215">Este paso no suele ser necesario porque la aplicación admite aprovisionamiento de usuarios Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-215">This step is usually not required as the application supports just in time user provisioning.</span></span> <span data-ttu-id="6c0e5-216">Si el aprovisionamiento automático de usuarios no se habilita, puede llevarse a cabo la creación manual de usuarios tal y como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-216">If the automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="6c0e5-217">Inicie sesión como administrador en su sitio de la compañía de Velpic SAML y realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6c0e5-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="6c0e5-218">Haga clic en la pestaña Manage (Administrar), vaya a la sección Users (Usuarios) y haga clic en el botón New (Nuevo) para agregar usuarios.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-218">Click on Manage tab and go to Users section, then click on New button to add users.</span></span>

    ![agregar usuario](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="6c0e5-220">En el cuadro de diálogo **"Create New User"** (Crear nuevo usuario), realice los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-220">On the **“Create New User”** dialog page, perform the following steps.</span></span>

    ![user](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="6c0e5-222">a.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-222">a.</span></span> <span data-ttu-id="6c0e5-223">En el cuadro de texto **First Name** (Nombre), escriba el nombre de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-223">In the **First Name** textbox, type the first name of Britta Simon.</span></span>

    <span data-ttu-id="6c0e5-224">b.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-224">b.</span></span> <span data-ttu-id="6c0e5-225">En el cuadro de texto **Last Name** (Apellido), escriba el apellido de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-225">In the **Last Name** textbox, type the last name of Britta Simon.</span></span>

    <span data-ttu-id="6c0e5-226">c.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-226">c.</span></span> <span data-ttu-id="6c0e5-227">En el cuadro de texto **User Name** (Nombre de usuario), escriba el nombre del usuario de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-227">In the **User Name** textbox, type the user name of Britta Simon.</span></span>

    <span data-ttu-id="6c0e5-228">d.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-228">d.</span></span> <span data-ttu-id="6c0e5-229">En el cuadro de texto **Correo electrónico**, escriba la dirección de correo electrónico de la cuenta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="6c0e5-230">e.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-230">e.</span></span> <span data-ttu-id="6c0e5-231">El resto de la información es opcional, puede rellenarla si es necesario.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-231">Rest of the information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="6c0e5-232">f.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-232">f.</span></span> <span data-ttu-id="6c0e5-233">Haga clic en **GUARDAR**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-233">Click **SAVE**.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6c0e5-234">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c0e5-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6c0e5-235">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Velpic SAML.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="6c0e5-237">**Para asignar a Britta Simon a Velpic SAML, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="6c0e5-237">**To assign Britta Simon to Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="6c0e5-238">En el Portal de administración de Azure, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. A continuación, haga clic en **All applications** (Todas las aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="6c0e5-238">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="6c0e5-240">En la lista de aplicaciones, seleccione **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-240">In the applications list, select **Velpic SAML**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="6c0e5-242">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="6c0e5-244">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-244">Click **Add** button.</span></span> <span data-ttu-id="6c0e5-245">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="6c0e5-247">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6c0e5-248">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6c0e5-249">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6c0e5-250">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="6c0e5-250">Testing single sign-on</span></span>

<span data-ttu-id="6c0e5-251">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="6c0e5-252">Al hacer clic en el icono de Velpic SAML del panel de acceso, debería entrar en la página de inicio de sesión de la aplicación Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-252">When you click the Velpic SAML tile in the Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="6c0e5-253">Debe ver el botón **"Log In With Azure AD"** (Iniciar sesión con Azure AD) en la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-253">You should see the **‘Log In With Azure AD’** button on the sign in page.</span></span>

    ![Complemento](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="6c0e5-255">Haga clic en el botón **"Log In With Azure AD"** (Iniciar sesión con Azure AD) para iniciar sesión en Velpic con su cuenta de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c0e5-255">Click on the **‘Log In With Azure AD’** button to log in to Velpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6c0e5-256">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="6c0e5-256">Additional resources</span></span>

* [<span data-ttu-id="6c0e5-257">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6c0e5-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6c0e5-258">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6c0e5-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png


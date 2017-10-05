---
title: "Tutorial: integración de Azure Active Directory con EverBridge | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y EverBridge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: f5a97fc8df978dd55a73ae53516a82f884c14bec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="abc05-103">Tutorial: Integración de Azure Active Directory con EverBridge</span><span class="sxs-lookup"><span data-stu-id="abc05-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>

<span data-ttu-id="abc05-104">En este tutorial, aprenderá a integrar EverBridge con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="abc05-104">In this tutorial, you learn how to integrate EverBridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="abc05-105">La integración de EverBridge con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="abc05-105">Integrating EverBridge with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="abc05-106">Le permite controlar en Azure AD quién tiene acceso a EverBridge</span><span class="sxs-lookup"><span data-stu-id="abc05-106">You can control in Azure AD who has access to EverBridge</span></span>
- <span data-ttu-id="abc05-107">Puede habilitar a los usuarios para que inicien sesión automáticamente en EverBridge (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="abc05-107">You can enable your users to automatically get signed-on to EverBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="abc05-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="abc05-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="abc05-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="abc05-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abc05-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="abc05-110">Prerequisites</span></span>

<span data-ttu-id="abc05-111">Para configurar la integración de Azure AD con EverBridge, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="abc05-111">To configure Azure AD integration with EverBridge, you need the following items:</span></span>

- <span data-ttu-id="abc05-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="abc05-112">An Azure AD subscription</span></span>
- <span data-ttu-id="abc05-113">Una suscripción habilitada para el inicio de sesión único en EverBridge</span><span class="sxs-lookup"><span data-stu-id="abc05-113">An EverBridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="abc05-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="abc05-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="abc05-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="abc05-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="abc05-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="abc05-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="abc05-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="abc05-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="abc05-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="abc05-118">Scenario description</span></span>
<span data-ttu-id="abc05-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="abc05-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="abc05-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="abc05-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="abc05-121">Adición de EverBridge desde la galería</span><span class="sxs-lookup"><span data-stu-id="abc05-121">Adding EverBridge from the gallery</span></span>
2. <span data-ttu-id="abc05-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="abc05-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-the-gallery"></a><span data-ttu-id="abc05-123">Adición de EverBridge desde la galería</span><span class="sxs-lookup"><span data-stu-id="abc05-123">Adding EverBridge from the gallery</span></span>
<span data-ttu-id="abc05-124">Para configurar la integración de EverBridge en Azure AD, es preciso agregar EverBridge desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="abc05-124">To configure the integration of EverBridge into Azure AD, you need to add EverBridge from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="abc05-125">**Para agregar EverBridge desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="abc05-125">**To add EverBridge from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="abc05-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="abc05-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="abc05-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="abc05-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="abc05-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="abc05-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="abc05-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="abc05-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="abc05-133">En el cuadro de búsqueda, escriba **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="abc05-133">In the search box, type **EverBridge**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. <span data-ttu-id="abc05-135">En el panel de resultados, seleccione **EverBridge** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="abc05-135">In the results panel, select **EverBridge**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="abc05-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="abc05-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="abc05-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con EverBridge con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="abc05-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="abc05-139">Para que el inicio de sesión único funcione, Azure AD tiene que saber cuál es el usuario homólogo de EverBridge para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="abc05-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EverBridge is to a user in Azure AD.</span></span> <span data-ttu-id="abc05-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de EverBridge.</span><span class="sxs-lookup"><span data-stu-id="abc05-140">In other words, a link relationship between an Azure AD user and the related user in EverBridge needs to be established.</span></span>

<span data-ttu-id="abc05-141">Para establecer la relación de vínculo, en EverBridge, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="abc05-141">In EverBridge, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="abc05-142">Para configurar y probar el inicio de sesión único de Azure AD con EverBridge, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="abc05-142">To configure and test Azure AD single sign-on with EverBridge, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="abc05-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="abc05-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="abc05-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="abc05-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="abc05-145">**[Creación de un usuario de prueba para EverBridge](#creating-an-everbridge-test-user)**: para tener un homólogo de Britta Simon en EverBridge que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="abc05-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - to have a counterpart of Britta Simon in EverBridge that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="abc05-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="abc05-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="abc05-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="abc05-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="abc05-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="abc05-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="abc05-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación EverBridge.</span><span class="sxs-lookup"><span data-stu-id="abc05-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EverBridge application.</span></span>

<span data-ttu-id="abc05-150">**Para configurar el inicio de sesión único de Azure AD con EverBridge, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="abc05-150">**To configure Azure AD single sign-on with EverBridge, perform the following steps:**</span></span>

1. <span data-ttu-id="abc05-151">En Azure Portal, en la página de integración de la aplicación **EverBridge**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="abc05-151">In the Azure portal, on the **EverBridge** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="abc05-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="abc05-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. <span data-ttu-id="abc05-155">En la sección **Dominio y direcciones URL de EverBridge**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="abc05-155">On the **EverBridge Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    <span data-ttu-id="abc05-157">a.</span><span class="sxs-lookup"><span data-stu-id="abc05-157">a.</span></span> <span data-ttu-id="abc05-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://sso.everbridge.net/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="abc05-158">In the **Identifier** textbox, type a URL using the following pattern: `https://sso.everbridge.net/<companyname>`</span></span>

    <span data-ttu-id="abc05-159">b.</span><span class="sxs-lookup"><span data-stu-id="abc05-159">b.</span></span> <span data-ttu-id="abc05-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`.</span><span class="sxs-lookup"><span data-stu-id="abc05-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="abc05-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="abc05-161">These values are not real.</span></span> <span data-ttu-id="abc05-162">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="abc05-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="abc05-163">Póngase en contacto con el [equipo de soporte técnico de EverBridge](mailto:support@everbridge.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="abc05-163">Contact [EverBridge support team](mailto:support@everbridge.com) to get these values.</span></span>
 
4. <span data-ttu-id="abc05-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="abc05-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. <span data-ttu-id="abc05-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="abc05-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="abc05-168">En la sección **Configuración de EverBridge**, haga clic en **Configurar EverBridge** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="abc05-168">On the **EverBridge Configuration** section, click **Configure EverBridge** to open **Configure sign-on** window.</span></span> <span data-ttu-id="abc05-169">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="abc05-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. <span data-ttu-id="abc05-171">Para configurar SSO para la aplicación, tiene que iniciar sesión en su inquilino de Everbridge como administrador.</span><span class="sxs-lookup"><span data-stu-id="abc05-171">To get SSO configured for your application, you need to sign-on to your Everbridge tenant as an administrator.</span></span>

7. <span data-ttu-id="abc05-172">En el menú de la parte superior, haga clic en la pestaña **Settings** (Configuración) y seleccione **Single Sign-On** (Inicio de sesión único) en **Security** (Seguridad).</span><span class="sxs-lookup"><span data-stu-id="abc05-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="abc05-174">a.</span><span class="sxs-lookup"><span data-stu-id="abc05-174">a.</span></span> <span data-ttu-id="abc05-175">En el cuadro de texto **Nombre**, escriba el nombre del proveedor de identificadores (por ejemplo, el nombre de la compañía).</span><span class="sxs-lookup"><span data-stu-id="abc05-175">In the **Name** textbox, type the name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="abc05-176">b.</span><span class="sxs-lookup"><span data-stu-id="abc05-176">b.</span></span> <span data-ttu-id="abc05-177">En el cuadro de texto **API Name** (nombre de API), escriba el nombre de la API.</span><span class="sxs-lookup"><span data-stu-id="abc05-177">In the **API Name** textbox, type the name of API.</span></span>
   
    <span data-ttu-id="abc05-178">c.</span><span class="sxs-lookup"><span data-stu-id="abc05-178">c.</span></span> <span data-ttu-id="abc05-179">Haga clic en el botón **Elegir archivo** para cargar el archivo de metadatos que descargó en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="abc05-179">Click **Choose File** button to upload the metadata file which you downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="abc05-180">d.</span><span class="sxs-lookup"><span data-stu-id="abc05-180">d.</span></span> <span data-ttu-id="abc05-181">Como SAML Identity Location (Ubicación de identidad de SAML), seleccione **Identity is in the NameIdentifier element of the Subject statement** (La identidad está en el elemento NameIdentifier de la instrucción de sujeto).</span><span class="sxs-lookup"><span data-stu-id="abc05-181">In the SAML Identity Location, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
   
    <span data-ttu-id="abc05-182">e.</span><span class="sxs-lookup"><span data-stu-id="abc05-182">e.</span></span> <span data-ttu-id="abc05-183">En el cuadro de texto **URL de inicio de sesión del proveedor de identidades**, pegue el valor de dirección URL de inicio de sesión único de SAM de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="abc05-183">In the **Identity Provider Login URL** textbox, paste the value of SAML SSO URL from Azure AD.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="abc05-185">f.</span><span class="sxs-lookup"><span data-stu-id="abc05-185">f.</span></span> <span data-ttu-id="abc05-186">Para Service Provider Initiated Request Binding (Vinculación de solicitud iniciada por el proveedor de servicios), seleccione **Redirección HTTP**.</span><span class="sxs-lookup"><span data-stu-id="abc05-186">In the Service Provider Initiated Request Binding, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="abc05-187">g.</span><span class="sxs-lookup"><span data-stu-id="abc05-187">g.</span></span> <span data-ttu-id="abc05-188">Haga clic en **Guardar**</span><span class="sxs-lookup"><span data-stu-id="abc05-188">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="abc05-189">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="abc05-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="abc05-190">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="abc05-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="abc05-191">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="abc05-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="abc05-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="abc05-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="abc05-193">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="abc05-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="abc05-195">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="abc05-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="abc05-196">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="abc05-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="abc05-198">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="abc05-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="abc05-200">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="abc05-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="abc05-202">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="abc05-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="abc05-204">a.</span><span class="sxs-lookup"><span data-stu-id="abc05-204">a.</span></span> <span data-ttu-id="abc05-205">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="abc05-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="abc05-206">b.</span><span class="sxs-lookup"><span data-stu-id="abc05-206">b.</span></span> <span data-ttu-id="abc05-207">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="abc05-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="abc05-208">c.</span><span class="sxs-lookup"><span data-stu-id="abc05-208">c.</span></span> <span data-ttu-id="abc05-209">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="abc05-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="abc05-210">d.</span><span class="sxs-lookup"><span data-stu-id="abc05-210">d.</span></span> <span data-ttu-id="abc05-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="abc05-211">Click **Create**.</span></span>
 
### <a name="creating-an-everbridge-test-user"></a><span data-ttu-id="abc05-212">Creación de un usuario de prueba para EverBridge</span><span class="sxs-lookup"><span data-stu-id="abc05-212">Creating an EverBridge test user</span></span>

<span data-ttu-id="abc05-213">En esta sección, creará una usuaria llamada Britta Simon en Everbridge.</span><span class="sxs-lookup"><span data-stu-id="abc05-213">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="abc05-214">Colabore con el [equipo de soporte técnico de EverBridge](mailto:support@everbridge.com) mediante para agregar los usuarios a la plataforma EverBridge.</span><span class="sxs-lookup"><span data-stu-id="abc05-214">Work with [EverBridge support team](mailto:support@everbridge.com) to add the users in the Everbridge platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="abc05-215">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="abc05-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="abc05-216">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a EverBridge.</span><span class="sxs-lookup"><span data-stu-id="abc05-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EverBridge.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="abc05-218">**Para asignar a Britta Simon a EverBridge, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="abc05-218">**To assign Britta Simon to EverBridge, perform the following steps:**</span></span>

1. <span data-ttu-id="abc05-219">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="abc05-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="abc05-221">En la lista de aplicaciones, seleccione **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="abc05-221">In the applications list, select **EverBridge**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. <span data-ttu-id="abc05-223">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="abc05-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="abc05-225">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="abc05-225">Click **Add** button.</span></span> <span data-ttu-id="abc05-226">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="abc05-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="abc05-228">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="abc05-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="abc05-229">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="abc05-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="abc05-230">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="abc05-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="abc05-231">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="abc05-231">Testing single sign-on</span></span>

<span data-ttu-id="abc05-232">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="abc05-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="abc05-233">Al hacer clic en el icono de Everbridge en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Everbridge.</span><span class="sxs-lookup"><span data-stu-id="abc05-233">When you click the Everbridge tile in the Access Panel, you should get automatically signed-on to your Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="abc05-234">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="abc05-234">Additional resources</span></span>

* [<span data-ttu-id="abc05-235">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="abc05-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="abc05-236">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="abc05-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png


---
title: "Tutorial: Integración de Azure Active Directory con Kiteworks | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Kiteworks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 2fd9b346cb6d838069ef94ee9c2a8d113f22779c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="3b6a3-103">Tutorial: Integración de Azure Active Directory con Kiteworks</span><span class="sxs-lookup"><span data-stu-id="3b6a3-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="3b6a3-104">En este tutorial, obtendrá información sobre cómo integrar Kiteworks con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3b6a3-104">In this tutorial, you learn how to integrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3b6a3-105">Integrar Kiteworks con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3b6a3-105">Integrating Kiteworks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3b6a3-106">Puede controlar en Azure AD quién tiene acceso a Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-106">You can control in Azure AD who has access to Kiteworks</span></span>
- <span data-ttu-id="3b6a3-107">Puede permitir que los usuarios inicien sesión automáticamente en Kiteworks (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-107">You can enable your users to automatically get signed-on to Kiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3b6a3-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3b6a3-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3b6a3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b6a3-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3b6a3-110">Prerequisites</span></span>

<span data-ttu-id="3b6a3-111">Para configurar la integración de Azure AD con Kiteworks, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3b6a3-111">To configure Azure AD integration with Kiteworks, you need the following items:</span></span>

- <span data-ttu-id="3b6a3-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b6a3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3b6a3-113">Una suscripción habilitada para inicio de sesión único en Kiteworks</span><span class="sxs-lookup"><span data-stu-id="3b6a3-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3b6a3-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3b6a3-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3b6a3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3b6a3-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3b6a3-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3b6a3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3b6a3-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3b6a3-118">Scenario description</span></span>
<span data-ttu-id="3b6a3-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3b6a3-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="3b6a3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3b6a3-121">Adición de Kiteworks desde la galería</span><span class="sxs-lookup"><span data-stu-id="3b6a3-121">Adding Kiteworks from the gallery</span></span>
2. <span data-ttu-id="3b6a3-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b6a3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-the-gallery"></a><span data-ttu-id="3b6a3-123">Adición de Kiteworks desde la galería</span><span class="sxs-lookup"><span data-stu-id="3b6a3-123">Adding Kiteworks from the gallery</span></span>
<span data-ttu-id="3b6a3-124">Para configurar la integración de Kiteworks en Azure AD, es preciso agregar Kiteworks desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-124">To configure the integration of Kiteworks into Azure AD, you need to add Kiteworks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3b6a3-125">**Para agregar Kiteworks desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="3b6a3-125">**To add Kiteworks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3b6a3-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3b6a3-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3b6a3-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3b6a3-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3b6a3-133">En el cuadro de búsqueda, escriba **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-133">In the search box, type **Kiteworks**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="3b6a3-135">En el panel de resultados, seleccione **Kiteworks** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-135">In the results panel, select **Kiteworks**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3b6a3-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b6a3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3b6a3-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Kiteworks con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3b6a3-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3b6a3-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Kiteworks para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kiteworks is to a user in Azure AD.</span></span> <span data-ttu-id="3b6a3-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-140">In other words, a link relationship between an Azure AD user and the related user in Kiteworks needs to be established.</span></span>

<span data-ttu-id="3b6a3-141">Para establecer la relación de vínculo, en Kiteworks, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-141">In Kiteworks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3b6a3-142">Para configurar y probar el inicio de sesión único de Azure AD con Kiteworks, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3b6a3-142">To configure and test Azure AD single sign-on with Kiteworks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3b6a3-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3b6a3-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3b6a3-145">**[Creación de un usuario de prueba en Kiteworks](#creating-a-kiteworks-test-user)**: para tener un homólogo de Britta Simon en Kiteworks que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - to have a counterpart of Britta Simon in Kiteworks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3b6a3-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3b6a3-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3b6a3-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b6a3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3b6a3-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="3b6a3-150">**Para configurar el inicio de sesión único de Azure AD con Kiteworks, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3b6a3-150">**To configure Azure AD single sign-on with Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="3b6a3-151">En Azure Portal, en la página de integración de la aplicación **Kiteworks**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-151">In the Azure portal, on the **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3b6a3-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="3b6a3-155">En la sección **Dominio y direcciones URL de Kiteworks**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3b6a3-155">On the **Kiteworks Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="3b6a3-157">a.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-157">a.</span></span> <span data-ttu-id="3b6a3-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.kiteworks.com`.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="3b6a3-159">b.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-159">b.</span></span> <span data-ttu-id="3b6a3-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="3b6a3-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3b6a3-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-161">These values are not real.</span></span> <span data-ttu-id="3b6a3-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3b6a3-163">Póngase en contacto con el [equipo de soporte de cliente de Kiteworks](http://accellion.com/support) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-163">Contact [Kiteworks Client support team](http://accellion.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="3b6a3-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="3b6a3-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3b6a3-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3b6a3-168">En la sección **Configuración de Kiteworks**, haga clic en **Configurar Kiteworks** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-168">On the **Kiteworks Configuration** section, click **Configure Kiteworks** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3b6a3-169">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="3b6a3-171">Inicie sesión en su sitio de la compañía de Kiteworks como administrador.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-171">Sign on to your Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="3b6a3-172">En la barra de herramientas de la parte superior, haga clic en el icono de **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-172">In the toolbar on the top, click **Settings**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="3b6a3-174">En la sección **Autenticación y autorización**, haga clic en **SSO Setup** (Instalación de SSO).</span><span class="sxs-lookup"><span data-stu-id="3b6a3-174">In the **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="3b6a3-176">En la página Configuración de SSO, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3b6a3-176">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="3b6a3-178">a.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-178">a.</span></span> <span data-ttu-id="3b6a3-179">Seleccione **Autenticar mediante SSO**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="3b6a3-180">b.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-180">b.</span></span> <span data-ttu-id="3b6a3-181">Seleccione **Iniciar AuthnRequest**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="3b6a3-182">c.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-182">c.</span></span> <span data-ttu-id="3b6a3-183">En el cuadro de texto **IdP Entity ID** (Id. de entidad IdP), pegue el valor de **SAML Entity ID** (Identificador de entidad de SAML) que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="3b6a3-184">d.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-184">d.</span></span> <span data-ttu-id="3b6a3-185">Copie la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal en el cuadro de texto de la **dirección URL del servicio de inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-185">In the **Single Sign-On Service URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3b6a3-186">e.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-186">e.</span></span> <span data-ttu-id="3b6a3-187">En el cuadro de texto **Dirección URL del servicio de cierre de sesión único**, pegue el valor de la **dirección URL de cierre de sesión** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-187">In the **Single Logout Service URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3b6a3-188">f.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-188">f.</span></span> <span data-ttu-id="3b6a3-189">Abra el certificado descargado en el Bloc de notas, copie el contenido y péguelo en el cuadro de texto **Certificado de clave pública RSA** .</span><span class="sxs-lookup"><span data-stu-id="3b6a3-189">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="3b6a3-190">g.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-190">g.</span></span> <span data-ttu-id="3b6a3-191">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3b6a3-192">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3b6a3-193">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3b6a3-194">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3b6a3-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3b6a3-195">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b6a3-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="3b6a3-196">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3b6a3-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3b6a3-198">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="3b6a3-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3b6a3-199">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3b6a3-201">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3b6a3-203">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3b6a3-205">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="3b6a3-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3b6a3-207">a.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-207">a.</span></span> <span data-ttu-id="3b6a3-208">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3b6a3-209">b.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-209">b.</span></span> <span data-ttu-id="3b6a3-210">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3b6a3-211">c.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-211">c.</span></span> <span data-ttu-id="3b6a3-212">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3b6a3-213">d.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-213">d.</span></span> <span data-ttu-id="3b6a3-214">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="3b6a3-215">Creación de un usuario de prueba en Kiteworks</span><span class="sxs-lookup"><span data-stu-id="3b6a3-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="3b6a3-216">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-216">The objective of this section is to create a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="3b6a3-217">Kiteworks admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="3b6a3-218">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-218">There is no action item for you in this section.</span></span> <span data-ttu-id="3b6a3-219">Durante un intento de obtener acceso a Kitewors se creará un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-219">A new user is created during an attempt to access Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="3b6a3-220">Si necesita crear manualmente un usuario, es preciso que se ponga contacto con el [equipo de soporte técnico de Kiteworks](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="3b6a3-220">If you need to create a user manually, you need to contact the [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3b6a3-221">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b6a3-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3b6a3-222">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kiteworks.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3b6a3-224">**Para asignar Britta Simon a Kiteworks, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="3b6a3-224">**To assign Britta Simon to Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="3b6a3-225">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3b6a3-227">En la lista de aplicaciones, seleccione **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-227">In the applications list, select **Kiteworks**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="3b6a3-229">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3b6a3-231">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-231">Click **Add** button.</span></span> <span data-ttu-id="3b6a3-232">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3b6a3-234">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3b6a3-235">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3b6a3-236">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3b6a3-237">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3b6a3-237">Testing single sign-on</span></span>

<span data-ttu-id="3b6a3-238">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-238">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="3b6a3-239">Al hacer clic en el icono de Kiteworks en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="3b6a3-239">When you click the Kiteworks tile in the Access Panel, you should get automatically signed-on to your Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3b6a3-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3b6a3-240">Additional resources</span></span>

* [<span data-ttu-id="3b6a3-241">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3b6a3-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3b6a3-242">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3b6a3-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

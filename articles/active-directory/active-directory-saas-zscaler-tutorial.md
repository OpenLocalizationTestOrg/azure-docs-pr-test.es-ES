---
title: "Tutorial: integración de Azure Active Directory con Zscaler | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Zscaler."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 73c81691b68ee820e1d905a17b4f2ab6b6ceb5fd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a><span data-ttu-id="11b94-103">Tutorial: Integración de Azure Active Directory con Zscaler</span><span class="sxs-lookup"><span data-stu-id="11b94-103">Tutorial: Azure Active Directory integration with Zscaler</span></span>

<span data-ttu-id="11b94-104">En este tutorial, aprenderá a integrar Zscaler con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="11b94-104">In this tutorial, you learn how to integrate Zscaler with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="11b94-105">La integración de Zscaler con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="11b94-105">Integrating Zscaler with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="11b94-106">Puede controlar en Azure AD quién tiene acceso a Zscaler</span><span class="sxs-lookup"><span data-stu-id="11b94-106">You can control in Azure AD who has access to Zscaler</span></span>
- <span data-ttu-id="11b94-107">Puede permitir que los usuarios inicien sesión automáticamente en Zscaler (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11b94-107">You can enable your users to automatically get signed-on to Zscaler (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="11b94-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="11b94-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="11b94-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="11b94-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11b94-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="11b94-110">Prerequisites</span></span>

<span data-ttu-id="11b94-111">Para configurar la integración de Azure AD con Zscaler, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="11b94-111">To configure Azure AD integration with Zscaler, you need the following items:</span></span>

- <span data-ttu-id="11b94-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11b94-112">An Azure AD subscription</span></span>
- <span data-ttu-id="11b94-113">Una suscripción habilitada para el inicio de sesión único en Zscaler</span><span class="sxs-lookup"><span data-stu-id="11b94-113">A Zscaler single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="11b94-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="11b94-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="11b94-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="11b94-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="11b94-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="11b94-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="11b94-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="11b94-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11b94-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="11b94-118">Scenario description</span></span>
<span data-ttu-id="11b94-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="11b94-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="11b94-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="11b94-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11b94-121">Incorporación de Zscaler desde la galería</span><span class="sxs-lookup"><span data-stu-id="11b94-121">Adding Zscaler from the gallery</span></span>
2. <span data-ttu-id="11b94-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11b94-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-from-the-gallery"></a><span data-ttu-id="11b94-123">Incorporación de Zscaler desde la galería</span><span class="sxs-lookup"><span data-stu-id="11b94-123">Adding Zscaler from the gallery</span></span>
<span data-ttu-id="11b94-124">Para configurar la integración de Zscaler en Azure AD, deberá agregar Zscaler desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="11b94-124">To configure the integration of Zscaler into Azure AD, you need to add Zscaler from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="11b94-125">**Para agregar Zscaler desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="11b94-125">**To add Zscaler from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="11b94-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11b94-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="11b94-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="11b94-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="11b94-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="11b94-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="11b94-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="11b94-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="11b94-133">En el cuadro de búsqueda, escriba **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="11b94-133">In the search box, type **Zscaler**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_search.png)

5. <span data-ttu-id="11b94-135">En el panel de resultados, seleccione **Zscaler** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="11b94-135">In the results panel, select **Zscaler**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="11b94-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11b94-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="11b94-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Zscaler con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="11b94-138">In this section, you configure and test Azure AD single sign-on with Zscaler based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="11b94-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Zscaler para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11b94-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler is to a user in Azure AD.</span></span> <span data-ttu-id="11b94-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario asociado de Zscaler.</span><span class="sxs-lookup"><span data-stu-id="11b94-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler needs to be established.</span></span>

<span data-ttu-id="11b94-141">Para establecer la relación de vínculo, en Zscaler, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="11b94-141">In Zscaler, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="11b94-142">Para configurar y probar el inicio de sesión único de Azure AD con Zscaler, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="11b94-142">To configure and test Azure AD single sign-on with Zscaler, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="11b94-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="11b94-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="11b94-144">**[Configuración de las opciones del proxy](#configuring-proxy-settings)**: para definir la configuración del proxy en Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="11b94-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="11b94-145">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11b94-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="11b94-146">**[Creación de un usuario de prueba de Zscaler](#creating-a-zscaler-test-user)**: para tener un homólogo de Britta Simon en Zscaler vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11b94-146">**[Creating a Zscaler test user](#creating-a-zscaler-test-user)** - to have a counterpart of Britta Simon in Zscaler that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="11b94-147">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11b94-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="11b94-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="11b94-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="11b94-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11b94-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="11b94-150">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Zscaler.</span><span class="sxs-lookup"><span data-stu-id="11b94-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler application.</span></span>

<span data-ttu-id="11b94-151">**Para configurar el inicio de sesión único de Azure AD con Zscaler, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="11b94-151">**To configure Azure AD single sign-on with Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="11b94-152">En Azure Portal, en la página de integración de la aplicación **Zscaler**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="11b94-152">In the Azure portal, on the **Zscaler** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="11b94-154">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="11b94-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_samlbase.png)

3. <span data-ttu-id="11b94-156">En la sección **Zscaler Domain and URLs** (Dominio y direcciones URL de Zscaler), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="11b94-156">On the **Zscaler Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_url.png)

    <span data-ttu-id="11b94-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.zsclaer.net`.</span><span class="sxs-lookup"><span data-stu-id="11b94-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zsclaer.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="11b94-159">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="11b94-159">This value is not real.</span></span> <span data-ttu-id="11b94-160">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="11b94-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="11b94-161">Póngase en contacto con el [equipo de soporte técnico de Zscaler](https://www.zscaler.com/company/contact) para obtenerlo.</span><span class="sxs-lookup"><span data-stu-id="11b94-161">Contact [Zscaler Client support team](https://www.zscaler.com/company/contact) to get this value.</span></span> 

4. <span data-ttu-id="11b94-162">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="11b94-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_certificate.png) 

5. <span data-ttu-id="11b94-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="11b94-164">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="11b94-166">En la sección **Zscaler Configuration** (Configuración de Zscaler), haga clic en **Configure Zscaler** (Configurar Zscaler) para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="11b94-166">On the **Zscaler Configuration** section, click **Configure Zscaler** to open **Configure sign-on** window.</span></span> <span data-ttu-id="11b94-167">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="11b94-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_configure.png) 

7. <span data-ttu-id="11b94-169">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Zscaler como administrador.</span><span class="sxs-lookup"><span data-stu-id="11b94-169">In a different web browser window, log in to your ZScaler company site as an administrator.</span></span>

8. <span data-ttu-id="11b94-170">En el menú de la parte superior, haga clic en **Administration**(Administración).</span><span class="sxs-lookup"><span data-stu-id="11b94-170">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="11b94-171">![Administración](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="11b94-171">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="11b94-172">En **Manage Administrators & Roles (Administrar administradores y roles)** haga clic en **Manage Users & Authentication (Administrar usuarios y autenticación)**.</span><span class="sxs-lookup"><span data-stu-id="11b94-172">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="11b94-173">![Administración de usuarios y autenticación](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Administración de usuarios y autenticación")</span><span class="sxs-lookup"><span data-stu-id="11b94-173">![Manage Users & Authentication](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="11b94-174">En la sección **Choose Authentication Options for your Organization** (Elegir opciones de autenticación para su organización), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="11b94-174">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="11b94-175">![Autenticación](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Autenticación")</span><span class="sxs-lookup"><span data-stu-id="11b94-175">![Authentication](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="11b94-176">a.</span><span class="sxs-lookup"><span data-stu-id="11b94-176">a.</span></span> <span data-ttu-id="11b94-177">Seleccione **Authenticate using SAML Single Sign-On**(Autenticarse mediante el inicio de sesión único SAML).</span><span class="sxs-lookup"><span data-stu-id="11b94-177">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="11b94-178">b.</span><span class="sxs-lookup"><span data-stu-id="11b94-178">b.</span></span> <span data-ttu-id="11b94-179">Haga clic en **Configure SAML Single Sign-On Parameters**(Configurar parámetros de inicio de sesión único SAML).</span><span class="sxs-lookup"><span data-stu-id="11b94-179">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="11b94-180">En la página de diálogo **Configure SAML Single Sign-On Parameters** (Configurar parámetros de inicio de sesión único SAML), realice estos pasos y luego haga clic en **Done** (Listo)</span><span class="sxs-lookup"><span data-stu-id="11b94-180">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="11b94-181">![Inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="11b94-181">![Single Sign-On](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="11b94-182">a.</span><span class="sxs-lookup"><span data-stu-id="11b94-182">a.</span></span> <span data-ttu-id="11b94-183">Pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML), que ha copiado de Azure Portal, en el cuadro de texto **de la dirección URL del portal de SAML al que se dirige a los usuarios para la autenticación**.</span><span class="sxs-lookup"><span data-stu-id="11b94-183">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="11b94-184">b.</span><span class="sxs-lookup"><span data-stu-id="11b94-184">b.</span></span> <span data-ttu-id="11b94-185">En el cuadro de texto **Attribute containing Login Name** (Atributo que contiene el nombre de inicio de sesión), escriba **NameID**.</span><span class="sxs-lookup"><span data-stu-id="11b94-185">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="11b94-186">c.</span><span class="sxs-lookup"><span data-stu-id="11b94-186">c.</span></span> <span data-ttu-id="11b94-187">Para cargar el certificado descargado, haga clic en **pem de Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="11b94-187">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="11b94-188">d.</span><span class="sxs-lookup"><span data-stu-id="11b94-188">d.</span></span> <span data-ttu-id="11b94-189">Seleccione **Habilitar aprovisionamiento automático de SAML**.</span><span class="sxs-lookup"><span data-stu-id="11b94-189">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="11b94-190">En la página del cuadro de diálogo **Configurar autenticación de usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="11b94-190">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="11b94-191">![Administración](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="11b94-191">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="11b94-192">a.</span><span class="sxs-lookup"><span data-stu-id="11b94-192">a.</span></span> <span data-ttu-id="11b94-193">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="11b94-193">Click **Save**.</span></span>

    <span data-ttu-id="11b94-194">b.</span><span class="sxs-lookup"><span data-stu-id="11b94-194">b.</span></span> <span data-ttu-id="11b94-195">Haga clic en **Activar ahora**.</span><span class="sxs-lookup"><span data-stu-id="11b94-195">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="11b94-196">Configuración de los valores de proxy</span><span class="sxs-lookup"><span data-stu-id="11b94-196">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="11b94-197">Para definir la configuración de proxy en Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="11b94-197">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="11b94-198">Inicie **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="11b94-198">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="11b94-199">Seleccione **Opciones de Internet** en el menú **Herramientas** para abrir el diálogo **Opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="11b94-199">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="11b94-200">![Opciones de Internet](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Opciones de Internet")</span><span class="sxs-lookup"><span data-stu-id="11b94-200">![Internet Options](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="11b94-201">Haga clic en la pestaña **Conexiones** .</span><span class="sxs-lookup"><span data-stu-id="11b94-201">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="11b94-202">![Conexiones](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Conexiones")</span><span class="sxs-lookup"><span data-stu-id="11b94-202">![Connections](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="11b94-203">Haga clic en **Configuración de LAN** para abrir el diálogo **Configuración de LAN**.</span><span class="sxs-lookup"><span data-stu-id="11b94-203">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="11b94-204">En la sección del servidor proxy, lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="11b94-204">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="11b94-205">![Servidor proxy](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Servidor proxy")</span><span class="sxs-lookup"><span data-stu-id="11b94-205">![Proxy server](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="11b94-206">a.</span><span class="sxs-lookup"><span data-stu-id="11b94-206">a.</span></span> <span data-ttu-id="11b94-207">Seleccione **Usar un servidor proxy para la LAN**.</span><span class="sxs-lookup"><span data-stu-id="11b94-207">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="11b94-208">b.</span><span class="sxs-lookup"><span data-stu-id="11b94-208">b.</span></span> <span data-ttu-id="11b94-209">En el cuadro de texto Dirección, escriba **gateway.zscaler.net**.</span><span class="sxs-lookup"><span data-stu-id="11b94-209">In the Address textbox, type **gateway.zscaler.net**.</span></span>

    <span data-ttu-id="11b94-210">c.</span><span class="sxs-lookup"><span data-stu-id="11b94-210">c.</span></span> <span data-ttu-id="11b94-211">En el cuadro de texto Puerto, escriba **80**.</span><span class="sxs-lookup"><span data-stu-id="11b94-211">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="11b94-212">d.</span><span class="sxs-lookup"><span data-stu-id="11b94-212">d.</span></span> <span data-ttu-id="11b94-213">Seleccione **No usar servidor proxy para direcciones locales**.</span><span class="sxs-lookup"><span data-stu-id="11b94-213">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="11b94-214">e.</span><span class="sxs-lookup"><span data-stu-id="11b94-214">e.</span></span> <span data-ttu-id="11b94-215">Haga clic en **Aceptar** para cerrar el diálogo **Configuración de red de área local (LAN)**.</span><span class="sxs-lookup"><span data-stu-id="11b94-215">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="11b94-216">Haga clic en **Aceptar** para cerrar el diálogo **Opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="11b94-216">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="11b94-217">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="11b94-217">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="11b94-218">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="11b94-218">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="11b94-219">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="11b94-219">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="11b94-220">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11b94-220">Creating an Azure AD test user</span></span>
<span data-ttu-id="11b94-221">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="11b94-221">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="11b94-223">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="11b94-223">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="11b94-224">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11b94-224">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="11b94-226">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="11b94-226">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="11b94-228">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="11b94-228">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="11b94-230">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="11b94-230">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="11b94-232">a.</span><span class="sxs-lookup"><span data-stu-id="11b94-232">a.</span></span> <span data-ttu-id="11b94-233">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="11b94-233">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11b94-234">b.</span><span class="sxs-lookup"><span data-stu-id="11b94-234">b.</span></span> <span data-ttu-id="11b94-235">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11b94-235">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="11b94-236">c.</span><span class="sxs-lookup"><span data-stu-id="11b94-236">c.</span></span> <span data-ttu-id="11b94-237">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="11b94-237">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="11b94-238">d.</span><span class="sxs-lookup"><span data-stu-id="11b94-238">d.</span></span> <span data-ttu-id="11b94-239">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="11b94-239">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-test-user"></a><span data-ttu-id="11b94-240">Creación de un usuario de prueba de Zscaler</span><span class="sxs-lookup"><span data-stu-id="11b94-240">Creating a Zscaler test user</span></span>

<span data-ttu-id="11b94-241">Para permitir que los usuarios de Azure AD inicien sesión en Zscaler, deben aprovisionarse en Zscaler.</span><span class="sxs-lookup"><span data-stu-id="11b94-241">To enable Azure AD users to log in to ZScaler, they must be provisioned to ZScaler.</span></span>  
<span data-ttu-id="11b94-242">En el caso de Zscaler, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="11b94-242">In the case of ZScaler, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="11b94-243">Siga estos pasos para configurar el aprovisionamiento de usuario:</span><span class="sxs-lookup"><span data-stu-id="11b94-243">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="11b94-244">Inicie sesión en su inquilino de **Zscaler** .</span><span class="sxs-lookup"><span data-stu-id="11b94-244">Log in to your **Zscaler** tenant.</span></span>

2. <span data-ttu-id="11b94-245">Haga clic en **Administración**.</span><span class="sxs-lookup"><span data-stu-id="11b94-245">Click **Administration**.</span></span>   
   
    <span data-ttu-id="11b94-246">![Administración](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="11b94-246">![Administration](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="11b94-247">Haga clic en **User Management**(Administración de usuarios).</span><span class="sxs-lookup"><span data-stu-id="11b94-247">Click **User Management**.</span></span>   
        
     <span data-ttu-id="11b94-248">![Agregar](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Agregar")</span><span class="sxs-lookup"><span data-stu-id="11b94-248">![Add](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="11b94-249">En la pestaña **Usuarios**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="11b94-249">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="11b94-250">![Agregar](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Agregar")</span><span class="sxs-lookup"><span data-stu-id="11b94-250">![Add](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="11b94-251">En la sección Agregar usuario, lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="11b94-251">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="11b94-252">![Agregar usuario](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="11b94-252">![Add User](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="11b94-253">a.</span><span class="sxs-lookup"><span data-stu-id="11b94-253">a.</span></span> <span data-ttu-id="11b94-254">Escriba el **Id. de usuario**, el **Nombre para mostrar del usuario**, la **Contraseña**, **Confirmar contraseña** y después seleccione **Grupos** y el **Departamento** de una cuenta de AAD válida que quiera aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="11b94-254">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="11b94-255">b.</span><span class="sxs-lookup"><span data-stu-id="11b94-255">b.</span></span> <span data-ttu-id="11b94-256">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="11b94-256">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="11b94-257">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Zscaler ofrecida por Zscaler para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="11b94-257">You can use any other ZScaler user account creation tools or APIs provided by ZScaler to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="11b94-258">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="11b94-258">Assigning the Azure AD test user</span></span>

<span data-ttu-id="11b94-259">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Zscaler.</span><span class="sxs-lookup"><span data-stu-id="11b94-259">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="11b94-261">**Para asignar a Britta Simon a Zscaler, lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="11b94-261">**To assign Britta Simon to Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="11b94-262">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="11b94-262">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="11b94-264">En la lista de aplicaciones, seleccione **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="11b94-264">In the applications list, select **Zscaler**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_app.png) 

3. <span data-ttu-id="11b94-266">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="11b94-266">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="11b94-268">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="11b94-268">Click **Add** button.</span></span> <span data-ttu-id="11b94-269">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="11b94-269">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="11b94-271">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="11b94-271">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="11b94-272">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="11b94-272">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="11b94-273">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="11b94-273">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="11b94-274">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="11b94-274">Testing single sign-on</span></span>

<span data-ttu-id="11b94-275">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="11b94-275">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="11b94-276">Al hacer clic en el icono de Zscaler del Panel de acceso, iniciará sesión en la aplicación Zscaler automáticamente.</span><span class="sxs-lookup"><span data-stu-id="11b94-276">When you click the Zscaler tile in the Access Panel, you should get automatically signed-on to your Zscaler application.</span></span>
<span data-ttu-id="11b94-277">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="11b94-277">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="11b94-278">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="11b94-278">Additional resources</span></span>

* [<span data-ttu-id="11b94-279">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11b94-279">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="11b94-280">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="11b94-280">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_203.png


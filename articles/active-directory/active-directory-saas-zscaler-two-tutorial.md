---
title: "Tutorial: Integración de Azure Active Directory con Zscaler Two | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Zscaler Two."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1fd8a940-7320-47e0-a176-2dd4eeca6db2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 38c9da0a6599bb66c452fdb8a8911338601155f9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-two"></a><span data-ttu-id="f960a-103">Tutorial: Integración de Azure Active Directory con Zscaler Two</span><span class="sxs-lookup"><span data-stu-id="f960a-103">Tutorial: Azure Active Directory integration with Zscaler Two</span></span>

<span data-ttu-id="f960a-104">En este tutorial, aprenderá a integrar Zscaler Two con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f960a-104">In this tutorial, you learn how to integrate Zscaler Two with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f960a-105">La integración de Zscaler Two con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f960a-105">Integrating Zscaler Two with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f960a-106">Puede controlar en Azure AD quién tiene acceso a Zscaler Two</span><span class="sxs-lookup"><span data-stu-id="f960a-106">You can control in Azure AD who has access to Zscaler Two</span></span>
- <span data-ttu-id="f960a-107">Puede permitir que los usuarios inicien sesión automáticamente en Zscaler Two (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f960a-107">You can enable your users to automatically get signed-on to Zscaler Two (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f960a-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f960a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f960a-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f960a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f960a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f960a-110">Prerequisites</span></span>

<span data-ttu-id="f960a-111">Para configurar la integración de Azure AD con Zscaler Two, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f960a-111">To configure Azure AD integration with Zscaler Two, you need the following items:</span></span>

- <span data-ttu-id="f960a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f960a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f960a-113">Una suscripción habilitada para el inicio de sesión único en Zscaler Two</span><span class="sxs-lookup"><span data-stu-id="f960a-113">A Zscaler Two single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f960a-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f960a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f960a-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f960a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f960a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f960a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f960a-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f960a-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f960a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f960a-118">Scenario description</span></span>
<span data-ttu-id="f960a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f960a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f960a-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="f960a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f960a-121">Incorporación de Zscaler Two desde la galería</span><span class="sxs-lookup"><span data-stu-id="f960a-121">Adding Zscaler Two from the gallery</span></span>
2. <span data-ttu-id="f960a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f960a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-two-from-the-gallery"></a><span data-ttu-id="f960a-123">Incorporación de Zscaler Two desde la galería</span><span class="sxs-lookup"><span data-stu-id="f960a-123">Adding Zscaler Two from the gallery</span></span>
<span data-ttu-id="f960a-124">Para configurar la integración de Zscaler Two en Azure AD, deberá agregar Zscaler Two desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="f960a-124">To configure the integration of Zscaler Two into Azure AD, you need to add Zscaler Two from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f960a-125">**Para agregar Zscaler Two desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f960a-125">**To add Zscaler Two from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f960a-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f960a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f960a-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f960a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f960a-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f960a-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="f960a-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f960a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="f960a-133">En el cuadro de búsqueda, escriba **Zscaler Two**.</span><span class="sxs-lookup"><span data-stu-id="f960a-133">In the search box, type **Zscaler Two**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_search.png)

5. <span data-ttu-id="f960a-135">En el panel de resultados, seleccione **Zscaler Two** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f960a-135">In the results panel, select **Zscaler Two**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f960a-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f960a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f960a-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Zscaler Two con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f960a-138">In this section, you configure and test Azure AD single sign-on with Zscaler Two based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f960a-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Zscaler Two para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f960a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Two is to a user in Azure AD.</span></span> <span data-ttu-id="f960a-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario asociado de Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="f960a-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Two needs to be established.</span></span>

<span data-ttu-id="f960a-141">Para establecer la relación de vínculo, en Zscaler Two, asigne el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="f960a-141">In Zscaler Two, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f960a-142">Para configurar y probar el inicio de sesión único de Azure AD con Zscaler Two, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f960a-142">To configure and test Azure AD single sign-on with Zscaler Two, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f960a-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="f960a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f960a-144">**[Configuración de las opciones del proxy](#configuring-proxy-settings)**: para definir la configuración del proxy en Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="f960a-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="f960a-145">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f960a-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="f960a-146">**[Creación de un usuario de prueba de Zscaler Two](#creating-a-zscaler-two-test-user)**: para tener un homólogo de Britta Simon en Zscaler Two vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f960a-146">**[Creating a Zscaler Two test user](#creating-a-zscaler-two-test-user)** - to have a counterpart of Britta Simon in Zscaler Two that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="f960a-147">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f960a-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="f960a-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f960a-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f960a-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f960a-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f960a-150">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="f960a-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler Two application.</span></span>

<span data-ttu-id="f960a-151">**Para configurar el inicio de sesión único de Azure AD con Zscaler Two, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f960a-151">**To configure Azure AD single sign-on with Zscaler Two, perform the following steps:**</span></span>

1. <span data-ttu-id="f960a-152">En Azure Portal, en la página de integración de la aplicación **Zscaler Two**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f960a-152">In the Azure portal, on the **Zscaler Two** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="f960a-154">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f960a-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_samlbase.png)

3. <span data-ttu-id="f960a-156">En la sección **Dominio y direcciones URL de Zscaler Two**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f960a-156">On the **Zscaler Two Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_url.png)

   <span data-ttu-id="f960a-158">En el cuadro de texto de la dirección URL de inicio de sesión, escriba la dirección URL con la que los usuarios inician sesión en la aplicación Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="f960a-158">In the Sign-on URL textbox, type the URL used by your users to sign-on to your ZScaler Two application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f960a-159">Tiene que actualizar este valor con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="f960a-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f960a-160">Póngase en contacto con el [equipo de soporte técnico de Zscaler Two](https://www.zscaler.com/company/contact) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="f960a-160">Contact [Zscaler Two Client support team](https://www.zscaler.com/company/contact) to get these values.</span></span>

4. <span data-ttu-id="f960a-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f960a-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_certificate.png) 

5. <span data-ttu-id="f960a-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f960a-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f960a-165">En la sección **Configuración de Zscaler**, haga clic en **Configurar Zscaler Two** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="f960a-165">On the **Zscaler Two Configuration** section, click **Configure Zscaler Two** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f960a-166">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="f960a-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_configure.png) 

7. <span data-ttu-id="f960a-168">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Zscaler Two como administrador.</span><span class="sxs-lookup"><span data-stu-id="f960a-168">In a different web browser window, log in to your ZScaler Two company site as an administrator.</span></span>

8. <span data-ttu-id="f960a-169">En el menú de la parte superior, haga clic en **Administration**(Administración).</span><span class="sxs-lookup"><span data-stu-id="f960a-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="f960a-170">![Administración](./media/active-directory-saas-zscaler-two-tutorial/ic800206.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="f960a-170">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="f960a-171">En **Manage Administrators & Roles (Administrar administradores y roles)** haga clic en **Manage Users & Authentication (Administrar usuarios y autenticación)**.</span><span class="sxs-lookup"><span data-stu-id="f960a-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="f960a-172">![Administración de usuarios y autenticación](./media/active-directory-saas-zscaler-two-tutorial/ic800207.png "Administración de usuarios y autenticación")</span><span class="sxs-lookup"><span data-stu-id="f960a-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-two-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="f960a-173">En la sección **Choose Authentication Options for your Organization** (Elegir opciones de autenticación para su organización), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f960a-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="f960a-174">![Autenticación](./media/active-directory-saas-zscaler-two-tutorial/ic800208.png "Autenticación")</span><span class="sxs-lookup"><span data-stu-id="f960a-174">![Authentication](./media/active-directory-saas-zscaler-two-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="f960a-175">a.</span><span class="sxs-lookup"><span data-stu-id="f960a-175">a.</span></span> <span data-ttu-id="f960a-176">Seleccione **Authenticate using SAML Single Sign-On**(Autenticarse mediante el inicio de sesión único SAML).</span><span class="sxs-lookup"><span data-stu-id="f960a-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="f960a-177">b.</span><span class="sxs-lookup"><span data-stu-id="f960a-177">b.</span></span> <span data-ttu-id="f960a-178">Haga clic en **Configure SAML Single Sign-On Parameters**(Configurar parámetros de inicio de sesión único SAML).</span><span class="sxs-lookup"><span data-stu-id="f960a-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="f960a-179">En la página de diálogo **Configure SAML Single Sign-On Parameters** (Configurar parámetros de inicio de sesión único SAML), realice estos pasos y luego haga clic en **Done** (Listo)</span><span class="sxs-lookup"><span data-stu-id="f960a-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="f960a-180">![Inicio de sesión único](./media/active-directory-saas-zscaler-two-tutorial/ic800209.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="f960a-180">![Single Sign-On](./media/active-directory-saas-zscaler-two-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="f960a-181">a.</span><span class="sxs-lookup"><span data-stu-id="f960a-181">a.</span></span> <span data-ttu-id="f960a-182">Pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML), que ha copiado de Azure Portal, en el cuadro de texto **de la dirección URL del portal de SAML al que se dirige a los usuarios para la autenticación**.</span><span class="sxs-lookup"><span data-stu-id="f960a-182">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="f960a-183">b.</span><span class="sxs-lookup"><span data-stu-id="f960a-183">b.</span></span> <span data-ttu-id="f960a-184">En el cuadro de texto **Attribute containing Login Name** (Atributo que contiene el nombre de inicio de sesión), escriba **NameID**.</span><span class="sxs-lookup"><span data-stu-id="f960a-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="f960a-185">c.</span><span class="sxs-lookup"><span data-stu-id="f960a-185">c.</span></span> <span data-ttu-id="f960a-186">Para cargar el certificado descargado, haga clic en **pem de Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="f960a-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="f960a-187">d.</span><span class="sxs-lookup"><span data-stu-id="f960a-187">d.</span></span> <span data-ttu-id="f960a-188">Seleccione **Habilitar aprovisionamiento automático de SAML**.</span><span class="sxs-lookup"><span data-stu-id="f960a-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="f960a-189">En la página del cuadro de diálogo **Configurar autenticación de usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f960a-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="f960a-190">![Administración](./media/active-directory-saas-zscaler-two-tutorial/ic800210.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="f960a-190">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="f960a-191">a.</span><span class="sxs-lookup"><span data-stu-id="f960a-191">a.</span></span> <span data-ttu-id="f960a-192">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f960a-192">Click **Save**.</span></span>

    <span data-ttu-id="f960a-193">b.</span><span class="sxs-lookup"><span data-stu-id="f960a-193">b.</span></span> <span data-ttu-id="f960a-194">Haga clic en **Activar ahora**.</span><span class="sxs-lookup"><span data-stu-id="f960a-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="f960a-195">Configuración de los valores de proxy</span><span class="sxs-lookup"><span data-stu-id="f960a-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="f960a-196">Para definir la configuración de proxy en Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="f960a-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="f960a-197">Inicie **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f960a-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="f960a-198">Seleccione **Opciones de Internet** en el menú **Herramientas** para abrir el diálogo **Opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="f960a-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="f960a-199">![Opciones de Internet](./media/active-directory-saas-zscaler-two-tutorial/ic769492.png "Opciones de Internet")</span><span class="sxs-lookup"><span data-stu-id="f960a-199">![Internet Options](./media/active-directory-saas-zscaler-two-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="f960a-200">Haga clic en la pestaña **Conexiones** .</span><span class="sxs-lookup"><span data-stu-id="f960a-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="f960a-201">![Conexiones](./media/active-directory-saas-zscaler-two-tutorial/ic769493.png "Conexiones")</span><span class="sxs-lookup"><span data-stu-id="f960a-201">![Connections](./media/active-directory-saas-zscaler-two-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="f960a-202">Haga clic en **Configuración de LAN** para abrir el diálogo **Configuración de LAN**.</span><span class="sxs-lookup"><span data-stu-id="f960a-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="f960a-203">En la sección del servidor proxy, lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f960a-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="f960a-204">![Servidor proxy](./media/active-directory-saas-zscaler-two-tutorial/ic769494.png "Servidor proxy")</span><span class="sxs-lookup"><span data-stu-id="f960a-204">![Proxy server](./media/active-directory-saas-zscaler-two-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="f960a-205">a.</span><span class="sxs-lookup"><span data-stu-id="f960a-205">a.</span></span> <span data-ttu-id="f960a-206">Seleccione **Usar un servidor proxy para la LAN**.</span><span class="sxs-lookup"><span data-stu-id="f960a-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="f960a-207">b.</span><span class="sxs-lookup"><span data-stu-id="f960a-207">b.</span></span> <span data-ttu-id="f960a-208">En el cuadro de texto Dirección, escriba **gateway.zscalertwo.net**.</span><span class="sxs-lookup"><span data-stu-id="f960a-208">In the Address textbox, type **gateway.zscalertwo.net**.</span></span>

    <span data-ttu-id="f960a-209">c.</span><span class="sxs-lookup"><span data-stu-id="f960a-209">c.</span></span> <span data-ttu-id="f960a-210">En el cuadro de texto Puerto, escriba **80**.</span><span class="sxs-lookup"><span data-stu-id="f960a-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="f960a-211">d.</span><span class="sxs-lookup"><span data-stu-id="f960a-211">d.</span></span> <span data-ttu-id="f960a-212">Seleccione **No usar servidor proxy para direcciones locales**.</span><span class="sxs-lookup"><span data-stu-id="f960a-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="f960a-213">e.</span><span class="sxs-lookup"><span data-stu-id="f960a-213">e.</span></span> <span data-ttu-id="f960a-214">Haga clic en **Aceptar** para cerrar el diálogo **Configuración de red de área local (LAN)**.</span><span class="sxs-lookup"><span data-stu-id="f960a-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="f960a-215">Haga clic en **Aceptar** para cerrar el diálogo **Opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="f960a-215">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="f960a-216">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f960a-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f960a-217">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f960a-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f960a-218">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f960a-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f960a-219">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f960a-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="f960a-220">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f960a-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="f960a-222">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="f960a-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f960a-223">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f960a-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f960a-225">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f960a-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f960a-227">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f960a-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f960a-229">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="f960a-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f960a-231">a.</span><span class="sxs-lookup"><span data-stu-id="f960a-231">a.</span></span> <span data-ttu-id="f960a-232">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f960a-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f960a-233">b.</span><span class="sxs-lookup"><span data-stu-id="f960a-233">b.</span></span> <span data-ttu-id="f960a-234">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f960a-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f960a-235">c.</span><span class="sxs-lookup"><span data-stu-id="f960a-235">c.</span></span> <span data-ttu-id="f960a-236">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f960a-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f960a-237">d.</span><span class="sxs-lookup"><span data-stu-id="f960a-237">d.</span></span> <span data-ttu-id="f960a-238">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f960a-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-two-test-user"></a><span data-ttu-id="f960a-239">Creación de un usuario de prueba de Zscaler Two</span><span class="sxs-lookup"><span data-stu-id="f960a-239">Creating a Zscaler Two test user</span></span>

<span data-ttu-id="f960a-240">Para permitir que los usuarios de Azure AD inicien sesión en Zscaler Two, deben aprovisionarse a Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="f960a-240">To enable Azure AD users to log in to ZScaler Two, they must be provisioned to ZScaler Two.</span></span> <span data-ttu-id="f960a-241">En el caso de ZScaler Two, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="f960a-241">In the case of ZScaler Two, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="f960a-242">Siga estos pasos para configurar el aprovisionamiento de usuario:</span><span class="sxs-lookup"><span data-stu-id="f960a-242">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="f960a-243">Inicie sesión en su inquilino de **Zscaler Two**.</span><span class="sxs-lookup"><span data-stu-id="f960a-243">Log in to your **Zscaler Two** tenant.</span></span>

2. <span data-ttu-id="f960a-244">Haga clic en **Administración**.</span><span class="sxs-lookup"><span data-stu-id="f960a-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="f960a-245">![Administración](./media/active-directory-saas-zscaler-two-tutorial/ic781035.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="f960a-245">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="f960a-246">Haga clic en **User Management**(Administración de usuarios).</span><span class="sxs-lookup"><span data-stu-id="f960a-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="f960a-247">![Agregar](./media/active-directory-saas-zscaler-two-tutorial/ic781036.png "Agregar")</span><span class="sxs-lookup"><span data-stu-id="f960a-247">![Add](./media/active-directory-saas-zscaler-two-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="f960a-248">En la pestaña **Usuarios**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f960a-248">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="f960a-249">![Agregar](./media/active-directory-saas-zscaler-two-tutorial/ic781037.png "Agregar")</span><span class="sxs-lookup"><span data-stu-id="f960a-249">![Add](./media/active-directory-saas-zscaler-two-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="f960a-250">En la sección Agregar usuario, lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f960a-250">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="f960a-251">![Agregar usuario](./media/active-directory-saas-zscaler-two-tutorial/ic781038.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="f960a-251">![Add User](./media/active-directory-saas-zscaler-two-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="f960a-252">a.</span><span class="sxs-lookup"><span data-stu-id="f960a-252">a.</span></span> <span data-ttu-id="f960a-253">Escriba el **identificador de usuario**, el **nombre para mostrar del usuario**, la **contraseña**, el valor de **Confirmar contraseña** y, después, seleccione **Grupos** y el valor de **Departamento** de una cuenta de Azure AD válida que quiera aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="f960a-253">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="f960a-254">b.</span><span class="sxs-lookup"><span data-stu-id="f960a-254">b.</span></span> <span data-ttu-id="f960a-255">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f960a-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="f960a-256">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Zscaler Two ofrecida por Zscaler Two para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f960a-256">You can use any other ZScaler Two user account creation tools or APIs provided by ZScaler Two to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f960a-257">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f960a-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f960a-258">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="f960a-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler Two.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="f960a-260">**Para asignar a Britta Simon a Zscaler Two, lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="f960a-260">**To assign Britta Simon to Zscaler Two, perform the following steps:**</span></span>

1. <span data-ttu-id="f960a-261">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f960a-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f960a-263">En la lista de aplicaciones, seleccione **Zscaler Two**.</span><span class="sxs-lookup"><span data-stu-id="f960a-263">In the applications list, select **Zscaler Two**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_app.png) 

3. <span data-ttu-id="f960a-265">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f960a-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="f960a-267">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f960a-267">Click **Add** button.</span></span> <span data-ttu-id="f960a-268">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f960a-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="f960a-270">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="f960a-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f960a-271">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f960a-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f960a-272">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f960a-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f960a-273">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="f960a-273">Testing single sign-on</span></span>

<span data-ttu-id="f960a-274">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f960a-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f960a-275">Al hacer clic en el icono de Zscaler Two del panel de acceso, debería iniciar sesión en la aplicación Zscaler Two automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f960a-275">When you click the Zscaler Two tile in the Access Panel, you should get automatically signed-on to your Zscaler Two application.</span></span>
<span data-ttu-id="f960a-276">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f960a-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f960a-277">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f960a-277">Additional resources</span></span>

* [<span data-ttu-id="f960a-278">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f960a-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f960a-279">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f960a-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_203.png


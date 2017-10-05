---
title: "Tutorial: integración de Azure Active Directory con ZScaler ZSCloud | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y ZScaler ZSCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 2b6eb113e5725260bc04f50e9218939bf28b1ff0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="b8634-103">Tutorial: integración de Azure Active Directory con ZScaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="b8634-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="b8634-104">En este tutorial, aprenderá a integrar ZScaler ZSCloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b8634-104">In this tutorial, you learn how to integrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b8634-105">La integración de ZScaler ZSCloud con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b8634-105">Integrating Zscaler ZSCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b8634-106">Puede controlar en Azure AD quién tiene acceso a ZScaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="b8634-106">You can control in Azure AD who has access to Zscaler ZSCloud</span></span>
- <span data-ttu-id="b8634-107">Puede permitir que los usuarios inicien sesión automáticamente en ZScaler ZSCloud (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8634-107">You can enable your users to automatically get signed-on to Zscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b8634-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b8634-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b8634-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b8634-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8634-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b8634-110">Prerequisites</span></span>

<span data-ttu-id="b8634-111">Para configurar la integración de Azure AD con ZScaler ZSCloud, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b8634-111">To configure Azure AD integration with Zscaler ZSCloud, you need the following items:</span></span>

- <span data-ttu-id="b8634-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8634-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b8634-113">Una suscripción habilitada para el inicio de sesión único en ZScaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="b8634-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b8634-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b8634-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b8634-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b8634-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b8634-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b8634-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b8634-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b8634-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b8634-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b8634-118">Scenario description</span></span>
<span data-ttu-id="b8634-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b8634-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b8634-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="b8634-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b8634-121">Incorporación de ZScaler ZSCloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="b8634-121">Adding Zscaler ZSCloud from the gallery</span></span>
2. <span data-ttu-id="b8634-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8634-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-the-gallery"></a><span data-ttu-id="b8634-123">Incorporación de ZScaler ZSCloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="b8634-123">Adding Zscaler ZSCloud from the gallery</span></span>
<span data-ttu-id="b8634-124">Para configurar la integración de ZScaler ZSCloud en Azure AD, será preciso agregar ZScaler ZSCloud desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="b8634-124">To configure the integration of Zscaler ZSCloud into Azure AD, you need to add Zscaler ZSCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b8634-125">**Para agregar ZScaler ZSCloud desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b8634-125">**To add Zscaler ZSCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b8634-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b8634-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b8634-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b8634-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b8634-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b8634-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="b8634-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8634-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="b8634-133">En el cuadro de búsqueda, escriba **ZScaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="b8634-133">In the search box, type **Zscaler ZSCloud**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. <span data-ttu-id="b8634-135">En el panel de resultados, seleccione **ZScaler ZSCloud** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b8634-135">In the results panel, select **Zscaler ZSCloud**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b8634-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8634-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b8634-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Zscaler ZSCloud con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8634-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b8634-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de ZScaler ZSCloud para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8634-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler ZSCloud is to a user in Azure AD.</span></span> <span data-ttu-id="b8634-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario asociado de ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="b8634-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler ZSCloud needs to be established.</span></span>

<span data-ttu-id="b8634-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como valor de **Nombre de usuario** en ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="b8634-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="b8634-142">Para configurar y probar el inicio de sesión único de Azure AD con ZScaler ZSCloud, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b8634-142">To configure and test Azure AD single sign-on with Zscaler ZSCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b8634-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="b8634-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b8634-144">**[Configuración de las opciones del proxy](#configuring-proxy-settings)**: para definir la configuración del proxy en Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="b8634-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
2. <span data-ttu-id="b8634-145">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8634-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b8634-146">**[Creación de un usuario de prueba de ZScaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**: para tener un homólogo de Britta Simon en ZScaler ZSCloud vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8634-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - to have a counterpart of Britta Simon in Zscaler ZSCloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b8634-147">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8634-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b8634-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="b8634-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b8634-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8634-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b8634-150">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="b8634-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="b8634-151">**Para configurar el inicio de sesión único de Azure AD con ZScaler ZSCloud, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b8634-151">**To configure Azure AD single sign-on with Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="b8634-152">En Azure Portal, en la página de integración de la aplicación **ZScaler ZSCloud**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b8634-152">In the Azure portal, on the **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="b8634-154">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b8634-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. <span data-ttu-id="b8634-156">En la sección **ZScaler ZSCloud Domain and URLs** (Dominio y direcciones URL de ZScaler ZSCloud), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b8634-156">On the **Zscaler ZSCloud Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="b8634-158">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL con la que los usuarios inician sesión en la aplicación ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="b8634-158">In the **Sign-on URL** textbox, type the URL used by your users to sign-on to your ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="b8634-159">Tiene que actualizar este valor con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="b8634-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b8634-160">Póngase en contacto con el [equipo de soporte técnico de ZScaler ZSCloud](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) para obtenerlo.</span><span class="sxs-lookup"><span data-stu-id="b8634-160">Contact [Zscaler ZSCloud Client support team](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) to get this value.</span></span> 
 
4. <span data-ttu-id="b8634-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b8634-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. <span data-ttu-id="b8634-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="b8634-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b8634-165">En la sección **ZScaler ZSCloud Configuration** (Configuración de ZScaler ZSCloud), haga clic en **Configure ZScaler ZSCloud** (Configurar ZScaler ZSCloud) para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="b8634-165">On the **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b8634-166">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="b8634-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. <span data-ttu-id="b8634-168">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de ZScaler ZSCloud como administrador.</span><span class="sxs-lookup"><span data-stu-id="b8634-168">In a different web browser window, log in to your ZScaler ZSCloud company site as an administrator.</span></span>

8. <span data-ttu-id="b8634-169">En el menú de la parte superior, haga clic en **Administration**(Administración).</span><span class="sxs-lookup"><span data-stu-id="b8634-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="b8634-170">![Administración](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="b8634-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="b8634-171">En **Manage Administrators & Roles (Administrar administradores y roles)** haga clic en **Manage Users & Authentication (Administrar usuarios y autenticación)**.</span><span class="sxs-lookup"><span data-stu-id="b8634-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="b8634-172">![Administración de usuarios y autenticación](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Administración de usuarios y autenticación")</span><span class="sxs-lookup"><span data-stu-id="b8634-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="b8634-173">En la sección **Choose Authentication Options for your Organization** (Elegir opciones de autenticación para su organización), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b8634-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="b8634-174">![Autenticación](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Autenticación")</span><span class="sxs-lookup"><span data-stu-id="b8634-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="b8634-175">a.</span><span class="sxs-lookup"><span data-stu-id="b8634-175">a.</span></span> <span data-ttu-id="b8634-176">Seleccione **Authenticate using SAML Single Sign-On**(Autenticarse mediante el inicio de sesión único SAML).</span><span class="sxs-lookup"><span data-stu-id="b8634-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="b8634-177">b.</span><span class="sxs-lookup"><span data-stu-id="b8634-177">b.</span></span> <span data-ttu-id="b8634-178">Haga clic en **Configure SAML Single Sign-On Parameters**(Configurar parámetros de inicio de sesión único SAML).</span><span class="sxs-lookup"><span data-stu-id="b8634-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="b8634-179">En la página de diálogo **Configure SAML Single Sign-On Parameters** (Configurar parámetros de inicio de sesión único SAML), realice estos pasos y luego haga clic en **Done** (Listo)</span><span class="sxs-lookup"><span data-stu-id="b8634-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="b8634-180">![Inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="b8634-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="b8634-181">a.</span><span class="sxs-lookup"><span data-stu-id="b8634-181">a.</span></span> <span data-ttu-id="b8634-182">Pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) de Azure Portal en el cuadro de texto **de la dirección URL del Portal de SAML al que se dirige a los usuarios para la autenticación**.</span><span class="sxs-lookup"><span data-stu-id="b8634-182">Paste the **SAML Single Sign-On Service URL** value into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="b8634-183">b.</span><span class="sxs-lookup"><span data-stu-id="b8634-183">b.</span></span> <span data-ttu-id="b8634-184">En el cuadro de texto **Attribute containing Login Name** (Atributo que contiene el nombre de inicio de sesión), escriba **NameID**.</span><span class="sxs-lookup"><span data-stu-id="b8634-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="b8634-185">c.</span><span class="sxs-lookup"><span data-stu-id="b8634-185">c.</span></span> <span data-ttu-id="b8634-186">Para cargar el certificado descargado, haga clic en **pem de Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="b8634-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="b8634-187">d.</span><span class="sxs-lookup"><span data-stu-id="b8634-187">d.</span></span> <span data-ttu-id="b8634-188">Seleccione **Habilitar aprovisionamiento automático de SAML**.</span><span class="sxs-lookup"><span data-stu-id="b8634-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="b8634-189">En la página del cuadro de diálogo **Configurar autenticación de usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b8634-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="b8634-190">![Administración](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="b8634-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="b8634-191">a.</span><span class="sxs-lookup"><span data-stu-id="b8634-191">a.</span></span> <span data-ttu-id="b8634-192">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b8634-192">Click **Save**.</span></span>

    <span data-ttu-id="b8634-193">b.</span><span class="sxs-lookup"><span data-stu-id="b8634-193">b.</span></span> <span data-ttu-id="b8634-194">Haga clic en **Activar ahora**.</span><span class="sxs-lookup"><span data-stu-id="b8634-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="b8634-195">Configuración de los valores de proxy</span><span class="sxs-lookup"><span data-stu-id="b8634-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="b8634-196">Para definir la configuración de proxy en Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="b8634-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="b8634-197">Inicie **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b8634-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="b8634-198">Seleccione **Opciones de Internet** en el menú **Herramientas** para abrir el diálogo **Opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="b8634-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="b8634-199">![Opciones de Internet](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Opciones de Internet")</span><span class="sxs-lookup"><span data-stu-id="b8634-199">![Internet Options](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="b8634-200">Haga clic en la pestaña **Conexiones** .</span><span class="sxs-lookup"><span data-stu-id="b8634-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="b8634-201">![Conexiones](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Conexiones")</span><span class="sxs-lookup"><span data-stu-id="b8634-201">![Connections](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="b8634-202">Haga clic en **Configuración de LAN** para abrir el diálogo **Configuración de LAN**.</span><span class="sxs-lookup"><span data-stu-id="b8634-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="b8634-203">En la sección del servidor proxy, lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b8634-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="b8634-204">![Servidor proxy](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Servidor proxy")</span><span class="sxs-lookup"><span data-stu-id="b8634-204">![Proxy server](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="b8634-205">a.</span><span class="sxs-lookup"><span data-stu-id="b8634-205">a.</span></span> <span data-ttu-id="b8634-206">Seleccione **Usar un servidor proxy para la LAN**.</span><span class="sxs-lookup"><span data-stu-id="b8634-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="b8634-207">b.</span><span class="sxs-lookup"><span data-stu-id="b8634-207">b.</span></span> <span data-ttu-id="b8634-208">En el cuadro de texto Dirección, escriba **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="b8634-208">In the Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="b8634-209">c.</span><span class="sxs-lookup"><span data-stu-id="b8634-209">c.</span></span> <span data-ttu-id="b8634-210">En el cuadro de texto Puerto, escriba **80**.</span><span class="sxs-lookup"><span data-stu-id="b8634-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="b8634-211">d.</span><span class="sxs-lookup"><span data-stu-id="b8634-211">d.</span></span> <span data-ttu-id="b8634-212">Seleccione **No usar servidor proxy para direcciones locales**.</span><span class="sxs-lookup"><span data-stu-id="b8634-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="b8634-213">e.</span><span class="sxs-lookup"><span data-stu-id="b8634-213">e.</span></span> <span data-ttu-id="b8634-214">Haga clic en **Aceptar** para cerrar el diálogo **Configuración de red de área local (LAN)**.</span><span class="sxs-lookup"><span data-stu-id="b8634-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="b8634-215">Haga clic en **Aceptar** para cerrar el diálogo **Opciones de Internet**.</span><span class="sxs-lookup"><span data-stu-id="b8634-215">Click **OK** to close the **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b8634-216">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8634-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="b8634-217">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b8634-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="b8634-219">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="b8634-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b8634-220">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b8634-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b8634-222">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b8634-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b8634-224">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8634-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b8634-226">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="b8634-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b8634-228">a.</span><span class="sxs-lookup"><span data-stu-id="b8634-228">a.</span></span> <span data-ttu-id="b8634-229">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b8634-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b8634-230">b.</span><span class="sxs-lookup"><span data-stu-id="b8634-230">b.</span></span> <span data-ttu-id="b8634-231">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8634-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b8634-232">c.</span><span class="sxs-lookup"><span data-stu-id="b8634-232">c.</span></span> <span data-ttu-id="b8634-233">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b8634-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b8634-234">d.</span><span class="sxs-lookup"><span data-stu-id="b8634-234">d.</span></span> <span data-ttu-id="b8634-235">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b8634-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="b8634-236">Creación de un usuario de prueba de ZScaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="b8634-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="b8634-237">Para permitir que los usuarios de Azure AD inicien sesión en ZScaler ZSCloud, deben aprovisionarse en ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="b8634-237">To enable Azure AD users to log in to ZScaler ZSCloud, they must be provisioned to ZScaler ZSCloud.</span></span>  
<span data-ttu-id="b8634-238">En el caso de ZScaler ZSCloud, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="b8634-238">In the case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="b8634-239">Siga estos pasos para configurar el aprovisionamiento de usuario:</span><span class="sxs-lookup"><span data-stu-id="b8634-239">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="b8634-240">Inicie sesión en su inquilino de **Zscaler** .</span><span class="sxs-lookup"><span data-stu-id="b8634-240">Log in to your **Zscaler** tenant.</span></span>

2. <span data-ttu-id="b8634-241">Haga clic en **Administración**.</span><span class="sxs-lookup"><span data-stu-id="b8634-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="b8634-242">![Administración](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="b8634-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="b8634-243">Haga clic en **User Management**(Administración de usuarios).</span><span class="sxs-lookup"><span data-stu-id="b8634-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="b8634-244">![Agregar](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Agregar")</span><span class="sxs-lookup"><span data-stu-id="b8634-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

4. <span data-ttu-id="b8634-245">En la pestaña **Usuarios**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b8634-245">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="b8634-246">![Agregar](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Agregar")</span><span class="sxs-lookup"><span data-stu-id="b8634-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="b8634-247">En la sección Agregar usuario, lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b8634-247">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="b8634-248">![Agregar usuario](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="b8634-248">![Add User](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="b8634-249">a.</span><span class="sxs-lookup"><span data-stu-id="b8634-249">a.</span></span> <span data-ttu-id="b8634-250">Escriba el **Id. de usuario**, el **Nombre para mostrar del usuario**, la **Contraseña**, **Confirmar contraseña** y después seleccione **Grupos** y el **Departamento** de una cuenta de AAD válida que quiera aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="b8634-250">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="b8634-251">b.</span><span class="sxs-lookup"><span data-stu-id="b8634-251">b.</span></span> <span data-ttu-id="b8634-252">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b8634-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="b8634-253">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de ZScaler ZSCloud ofrecida por ZScaler ZSCloud para aprovisionar cuentas de usuario de AAD.</span><span class="sxs-lookup"><span data-stu-id="b8634-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b8634-254">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8634-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b8634-255">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="b8634-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler ZSCloud.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="b8634-257">**Para asignar a Britta Simon a ZScaler ZSCloud, lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="b8634-257">**To assign Britta Simon to Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="b8634-258">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b8634-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b8634-260">En la lista de aplicaciones, seleccione **ZScaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="b8634-260">In the applications list, select **Zscaler ZSCloud**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. <span data-ttu-id="b8634-262">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b8634-262">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="b8634-264">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b8634-264">Click **Add** button.</span></span> <span data-ttu-id="b8634-265">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b8634-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="b8634-267">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="b8634-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b8634-268">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b8634-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b8634-269">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b8634-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b8634-270">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="b8634-270">Testing single sign-on</span></span>

<span data-ttu-id="b8634-271">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b8634-271">If you want to test your single sign-on settings, open the Access Panel.</span></span>

<span data-ttu-id="b8634-272">Al hacer clic en el icono de ZScaler ZSCloud del Panel de acceso, iniciará sesión en la aplicación ZScaler ZSCloud automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b8634-272">When you click the Zscaler ZSCloud tile in the Access Panel, you should get automatically signed-on to your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="b8634-273">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b8634-273">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b8634-274">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b8634-274">Additional resources</span></span>

* [<span data-ttu-id="b8634-275">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b8634-275">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b8634-276">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b8634-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png


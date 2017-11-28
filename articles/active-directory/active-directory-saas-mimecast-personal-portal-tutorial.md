---
title: "Tutorial: Integración de Azure Active Directory con Mimecast Personal Portal | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Mimecast Personal Portal."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: bf46da35a55608d7e4656c9dd3ad9d5f2253e225
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="86a66-103">Tutorial: Integración de Azure Active Directory con Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="86a66-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="86a66-104">En este tutorial, obtendrá información sobre cómo integrar Mimecast Personal Portal con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="86a66-104">In this tutorial, you learn how to integrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86a66-105">La integración de Mimecast Personal Portal con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="86a66-105">Integrating Mimecast Personal Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="86a66-106">En Azure AD puede controlar quién tiene acceso a Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="86a66-106">You can control in Azure AD who has access to Mimecast Personal Portal</span></span>
- <span data-ttu-id="86a66-107">Puede permitir que los usuarios inicien sesión automáticamente en Mimecast Personal Portal (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86a66-107">You can enable your users to automatically get signed-on to Mimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="86a66-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="86a66-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="86a66-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86a66-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86a66-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="86a66-110">Prerequisites</span></span>

<span data-ttu-id="86a66-111">Para configurar la integración de Azure AD con Mimecast Personal Portal, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="86a66-111">To configure Azure AD integration with Mimecast Personal Portal, you need the following items:</span></span>

- <span data-ttu-id="86a66-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a66-112">An Azure AD subscription</span></span>
- <span data-ttu-id="86a66-113">Un suscripción habilitada para inicio de sesión único en Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="86a66-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86a66-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="86a66-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86a66-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="86a66-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86a66-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="86a66-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86a66-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86a66-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86a66-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="86a66-118">Scenario description</span></span>
<span data-ttu-id="86a66-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="86a66-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86a66-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="86a66-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86a66-121">Incorporación de Mimecast Personal Portal desde la galería</span><span class="sxs-lookup"><span data-stu-id="86a66-121">Adding Mimecast Personal Portal from the gallery</span></span>
2. <span data-ttu-id="86a66-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a66-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-the-gallery"></a><span data-ttu-id="86a66-123">Incorporación de Mimecast Personal Portal desde la galería</span><span class="sxs-lookup"><span data-stu-id="86a66-123">Adding Mimecast Personal Portal from the gallery</span></span>
<span data-ttu-id="86a66-124">Para configurar la integración de Mimecast Personal Portal en Azure AD, deberá agregar esta solución desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="86a66-124">To configure the integration of Mimecast Personal Portal into Azure AD, you need to add Mimecast Personal Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="86a66-125">**Para agregar Mimecast Personal Portal desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="86a66-125">**To add Mimecast Personal Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="86a66-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="86a66-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="86a66-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="86a66-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="86a66-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="86a66-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="86a66-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="86a66-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="86a66-133">En el cuadro de búsqueda, escriba **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="86a66-133">In the search box, type **Mimecast Personal Portal**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="86a66-135">En el panel de resultados, seleccione **Mimecast Personal Portal** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="86a66-135">In the results panel, select **Mimecast Personal Portal**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="86a66-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a66-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="86a66-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Mimecast Personal Portal con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="86a66-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="86a66-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Mimecast Personal Portal para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86a66-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Personal Portal is to a user in Azure AD.</span></span> <span data-ttu-id="86a66-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="86a66-140">In other words, a link relationship between an Azure AD user and the related user in Mimecast Personal Portal needs to be established.</span></span>

<span data-ttu-id="86a66-141">Para establecer la relación de vínculo, en Mimecast Personal Portal, asigne el valor del **nombre de usuario** en Azure AD como el valor del **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="86a66-141">In Mimecast Personal Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="86a66-142">Para configurar y probar el inicio de sesión único de Azure AD con Mimecast Personal Portal, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="86a66-142">To configure and test Azure AD single sign-on with Mimecast Personal Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="86a66-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="86a66-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="86a66-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86a66-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="86a66-145">**[Creación de un usuario de prueba de Mimecast Personal Portal](#creating-a-mimecast-personal-portal-test-user)**: para tener un homólogo de Britta Simon en Mimecast Personal Portal que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86a66-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - to have a counterpart of Britta Simon in Mimecast Personal Portal that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="86a66-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86a66-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="86a66-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="86a66-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="86a66-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a66-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="86a66-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="86a66-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="86a66-150">**Para configurar el inicio de sesión único de Azure AD con Mimecast Personal Portal, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="86a66-150">**To configure Azure AD single sign-on with Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="86a66-151">En la página de integración de la aplicación **Mimecast Personal Portal** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="86a66-151">In the Azure portal, on the **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="86a66-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="86a66-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="86a66-155">En la sección **Dominio y direcciones URL de Mimecast Personal Portal**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="86a66-155">On the **Mimecast Personal Portal Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="86a66-157">a.</span><span class="sxs-lookup"><span data-stu-id="86a66-157">a.</span></span> <span data-ttu-id="86a66-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="86a66-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="86a66-159">b.</span><span class="sxs-lookup"><span data-stu-id="86a66-159">b.</span></span> <span data-ttu-id="86a66-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="86a66-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="86a66-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="86a66-161">These values are not real.</span></span> <span data-ttu-id="86a66-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="86a66-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="86a66-163">Póngase en contacto con el [equipo de soporte de cliente de Mimecast Personal Portal](https://www.mimecast.com/customer-success/technical-support/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="86a66-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) to get these values.</span></span> 
 


4. <span data-ttu-id="86a66-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="86a66-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="86a66-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="86a66-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="86a66-168">En la sección **Configuración de Mimecast Personal Portal**, haga clic en **Configurar Mimecast Personal Portal** para abrir la ventana **Configurar el inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="86a66-168">On the **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** to open **Configure sign-on** window.</span></span> <span data-ttu-id="86a66-169">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="86a66-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="86a66-171">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="86a66-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="86a66-172">Vaya a **Servicios \> Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="86a66-172">Go to **Services \> Applications**.</span></span>
   
    <span data-ttu-id="86a66-173">![Aplicaciones](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="86a66-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="86a66-174">Haga clic en **Authentication Profiles**(Perfiles de autenticación).</span><span class="sxs-lookup"><span data-stu-id="86a66-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="86a66-175">![Authentication Profiles (Perfiles de autenticación)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles (Perfiles de autenticación)")</span><span class="sxs-lookup"><span data-stu-id="86a66-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="86a66-176">Haga clic en **New Authentication Profile**(Nuevo perfil de autenticación).</span><span class="sxs-lookup"><span data-stu-id="86a66-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="86a66-177">![New Authentication Profile (Nuevo perfil de autenticación)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile (Nuevo perfil de autenticación)")</span><span class="sxs-lookup"><span data-stu-id="86a66-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="86a66-178">En la sección **Authentication Profile** (Perfil de autenticación), realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="86a66-178">In the **Authentication Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="86a66-179">![Authentication Profile (Perfil de autenticación)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile (Perfil de autenticación)")</span><span class="sxs-lookup"><span data-stu-id="86a66-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="86a66-180">a.</span><span class="sxs-lookup"><span data-stu-id="86a66-180">a.</span></span> <span data-ttu-id="86a66-181">En el cuadro de texto **Description** (Descripción), escriba un nombre para la configuración.</span><span class="sxs-lookup"><span data-stu-id="86a66-181">In the **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="86a66-182">b.</span><span class="sxs-lookup"><span data-stu-id="86a66-182">b.</span></span> <span data-ttu-id="86a66-183">Seleccione **Aplicar la autenticación SAML a Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="86a66-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="86a66-184">c.</span><span class="sxs-lookup"><span data-stu-id="86a66-184">c.</span></span> <span data-ttu-id="86a66-185">Como **Provider** (Proveedor), seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="86a66-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="86a66-186">d.</span><span class="sxs-lookup"><span data-stu-id="86a66-186">d.</span></span> <span data-ttu-id="86a66-187">En el cuadro de texto **Dirección URL del emisor**, pegue el valor de **SAML Entity ID** (Identificador de entidad de SAML) que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="86a66-187">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="86a66-188">e.</span><span class="sxs-lookup"><span data-stu-id="86a66-188">e.</span></span> <span data-ttu-id="86a66-189">En el cuadro de texto **Dirección URL de inicio de sesión**, pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="86a66-189">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="86a66-190">f.</span><span class="sxs-lookup"><span data-stu-id="86a66-190">f.</span></span> <span data-ttu-id="86a66-191">En el cuadro de texto **Dirección URL de cierre de sesión**, pegue el valor de **Dirección URL de cierre de sesión** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="86a66-191">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="86a66-192">g.</span><span class="sxs-lookup"><span data-stu-id="86a66-192">g.</span></span> <span data-ttu-id="86a66-193">Abra el certificado codificado en **base 64** descargado de Azure Portal en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Certificado de proveedor de identidades (metadatos)**.</span><span class="sxs-lookup"><span data-stu-id="86a66-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="86a66-194">h.</span><span class="sxs-lookup"><span data-stu-id="86a66-194">h.</span></span> <span data-ttu-id="86a66-195">Seleccione **Permitir inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="86a66-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="86a66-196">i.</span><span class="sxs-lookup"><span data-stu-id="86a66-196">i.</span></span> <span data-ttu-id="86a66-197">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="86a66-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="86a66-198">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="86a66-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="86a66-199">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="86a66-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="86a66-200">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="86a66-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="86a66-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a66-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="86a66-202">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="86a66-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="86a66-204">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="86a66-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="86a66-205">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="86a66-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="86a66-207">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="86a66-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="86a66-209">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="86a66-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="86a66-211">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="86a66-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="86a66-213">a.</span><span class="sxs-lookup"><span data-stu-id="86a66-213">a.</span></span> <span data-ttu-id="86a66-214">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86a66-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86a66-215">b.</span><span class="sxs-lookup"><span data-stu-id="86a66-215">b.</span></span> <span data-ttu-id="86a66-216">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86a66-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="86a66-217">c.</span><span class="sxs-lookup"><span data-stu-id="86a66-217">c.</span></span> <span data-ttu-id="86a66-218">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="86a66-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="86a66-219">d.</span><span class="sxs-lookup"><span data-stu-id="86a66-219">d.</span></span> <span data-ttu-id="86a66-220">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="86a66-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="86a66-221">Creación de un usuario de prueba de Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="86a66-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="86a66-222">Para permitir que los usuarios de Azure AD inicien sesión en Mimecast Personal Portal, deben aprovisionarse en Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="86a66-222">In order to enable Azure AD users to log into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="86a66-223">En el caso de Mimecast Personal Portal, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="86a66-223">In the case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="86a66-224">Deberá registrar un dominio para poder crear los usuarios.</span><span class="sxs-lookup"><span data-stu-id="86a66-224">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="86a66-225">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="86a66-225">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="86a66-226">Inicie sesión en **Mimecast Personal Portal** como administrador.</span><span class="sxs-lookup"><span data-stu-id="86a66-226">Sign on to your **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="86a66-227">Vaya a **Directorios\> Interno**.</span><span class="sxs-lookup"><span data-stu-id="86a66-227">Go to **Directories \> Internal**.</span></span>
   
    <span data-ttu-id="86a66-228">![Directories (Directorios)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories (Directorios)")</span><span class="sxs-lookup"><span data-stu-id="86a66-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="86a66-229">Haga clic en **Register New Domain**(Registrar nuevo dominio).</span><span class="sxs-lookup"><span data-stu-id="86a66-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="86a66-230">![Register New Domain (Registrar nuevo dominio)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain (Registrar nuevo dominio)")</span><span class="sxs-lookup"><span data-stu-id="86a66-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="86a66-231">Una vez creado el nuevo dominio, haga clic en **New Address**(Nueva dirección).</span><span class="sxs-lookup"><span data-stu-id="86a66-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="86a66-232">![New Address (Nueva dirección)](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address (Nueva dirección)")</span><span class="sxs-lookup"><span data-stu-id="86a66-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="86a66-233">En el cuadro de diálogo de dirección nueva, lleve a cabo los pasos siguientes para la cuenta de Azure AD válida que desea aprovisionar:</span><span class="sxs-lookup"><span data-stu-id="86a66-233">In the new address dialog, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="86a66-234">![Guardar](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Guardar")</span><span class="sxs-lookup"><span data-stu-id="86a66-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="86a66-235">a.</span><span class="sxs-lookup"><span data-stu-id="86a66-235">a.</span></span> <span data-ttu-id="86a66-236">En el cuadro de texto **Dirección de correo electrónico**, escriba la **dirección de correo electrónico** del usuario, en este caso **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="86a66-236">In the **Email Address** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="86a66-237">b.</span><span class="sxs-lookup"><span data-stu-id="86a66-237">b.</span></span> <span data-ttu-id="86a66-238">En el cuadro de texto **Nombre global**, escriba el **nombre de usuario** como **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86a66-238">In the **Global Name** textbox, type the **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="86a66-239">c.</span><span class="sxs-lookup"><span data-stu-id="86a66-239">c.</span></span> <span data-ttu-id="86a66-240">En los cuadros de texto **Contraseña** y **Confirmar contraseña**, escriba la **contraseña** del usuario.</span><span class="sxs-lookup"><span data-stu-id="86a66-240">In the **Password**, and **Confirm Password** textboxes, type the **Password** of the user.</span></span>
   
    <span data-ttu-id="86a66-241">b.</span><span class="sxs-lookup"><span data-stu-id="86a66-241">b.</span></span> <span data-ttu-id="86a66-242">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="86a66-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="86a66-243">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Mimecast Personal Portal ofrecida por Mimecast Personal Portal para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86a66-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="86a66-244">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a66-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="86a66-245">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="86a66-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Personal Portal.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="86a66-247">**Para asignar Britta Simon a Mimecast Personal Portal, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="86a66-247">**To assign Britta Simon to Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="86a66-248">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="86a66-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="86a66-250">En la lista de aplicaciones, seleccione **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="86a66-250">In the applications list, select **Mimecast Personal Portal**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="86a66-252">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="86a66-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="86a66-254">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="86a66-254">Click **Add** button.</span></span> <span data-ttu-id="86a66-255">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="86a66-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="86a66-257">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="86a66-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="86a66-258">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="86a66-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86a66-259">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="86a66-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="86a66-260">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="86a66-260">Testing single sign-on</span></span>
<span data-ttu-id="86a66-261">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="86a66-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="86a66-262">Al hacer clic en el icono de Mimecast Personal Portal en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="86a66-262">When you click the Mimecast Personal Portal tile in the Access Panel, you should get automatically signed-on to your Mimecast Personal Portal application.</span></span> <span data-ttu-id="86a66-263">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="86a66-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="86a66-264">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="86a66-264">Additional resources</span></span>

* [<span data-ttu-id="86a66-265">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86a66-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="86a66-266">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="86a66-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png


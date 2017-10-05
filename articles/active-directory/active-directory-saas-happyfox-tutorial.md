---
title: "Tutorial: integración de Azure Active Directory con HappyFox | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y HappyFox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 8b5ad750d7849e4037ed7ee93c48b5645c68e799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="326fc-103">Tutorial: integración de Azure Active Directory con HappyFox</span><span class="sxs-lookup"><span data-stu-id="326fc-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="326fc-104">En este tutorial, aprenderá a integrar HappyFox con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="326fc-104">In this tutorial, you learn how to integrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="326fc-105">La integración de HappyFox con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="326fc-105">Integrating HappyFox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="326fc-106">Puede controlar en Azure AD quién tiene acceso a HappyFox.</span><span class="sxs-lookup"><span data-stu-id="326fc-106">You can control in Azure AD who has access to HappyFox</span></span>
- <span data-ttu-id="326fc-107">Puede permitir que los usuarios inicien sesión automáticamente en HappyFox (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="326fc-107">You can enable your users to automatically get signed-on to HappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="326fc-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="326fc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="326fc-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="326fc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="326fc-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="326fc-110">Prerequisites</span></span>

<span data-ttu-id="326fc-111">Para configurar la integración de Azure AD con HappyFox, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="326fc-111">To configure Azure AD integration with HappyFox, you need the following items:</span></span>

- <span data-ttu-id="326fc-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="326fc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="326fc-113">Una suscripción habilitada para inicio de sesión único en HappyFox</span><span class="sxs-lookup"><span data-stu-id="326fc-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="326fc-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="326fc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="326fc-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="326fc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="326fc-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="326fc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="326fc-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="326fc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="326fc-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="326fc-118">Scenario description</span></span>
<span data-ttu-id="326fc-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="326fc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="326fc-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="326fc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="326fc-121">Incorporación de HappyFox desde la galería</span><span class="sxs-lookup"><span data-stu-id="326fc-121">Adding HappyFox from the gallery</span></span>
2. <span data-ttu-id="326fc-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="326fc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-the-gallery"></a><span data-ttu-id="326fc-123">Incorporación de HappyFox desde la galería</span><span class="sxs-lookup"><span data-stu-id="326fc-123">Adding HappyFox from the gallery</span></span>
<span data-ttu-id="326fc-124">Para configurar la integración de HappyFox en Azure AD, será preciso que lo agregue desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="326fc-124">To configure the integration of HappyFox into Azure AD, you need to add HappyFox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="326fc-125">**Para agregar HappyFox desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="326fc-125">**To add HappyFox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="326fc-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="326fc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="326fc-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="326fc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="326fc-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="326fc-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="326fc-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="326fc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="326fc-133">En el cuadro de búsqueda, escriba **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="326fc-133">In the search box, type **HappyFox**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_search.png)

5. <span data-ttu-id="326fc-135">En el panel de resultados, seleccione **HappyFox** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="326fc-135">In the results panel, select **HappyFox**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="326fc-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="326fc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="326fc-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con HappyFox con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="326fc-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="326fc-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de HappyFox para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="326fc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HappyFox is to a user in Azure AD.</span></span> <span data-ttu-id="326fc-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario asociado de HappyFox.</span><span class="sxs-lookup"><span data-stu-id="326fc-140">In other words, a link relationship between an Azure AD user and the related user in HappyFox needs to be established.</span></span>

<span data-ttu-id="326fc-141">Para establecer la relación de vínculo, en HappyFox, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="326fc-141">In HappyFox, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="326fc-142">Para configurar y probar el inicio de sesión único de Azure AD con HappyFox, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="326fc-142">To configure and test Azure AD single sign-on with HappyFox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="326fc-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="326fc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="326fc-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="326fc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="326fc-145">**[Creación de un usuario de prueba de HappyFox](#creating-a-happyfox-test-user)**: para tener un homólogo de Britta Simon en HappyFox vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="326fc-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - to have a counterpart of Britta Simon in HappyFox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="326fc-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="326fc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="326fc-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="326fc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="326fc-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="326fc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="326fc-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación HappyFox.</span><span class="sxs-lookup"><span data-stu-id="326fc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="326fc-150">**Para configurar el inicio de sesión único de Azure AD con HappyFox, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="326fc-150">**To configure Azure AD single sign-on with HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="326fc-151">En Azure Portal, en la página de integración de la aplicación **HappyFox**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="326fc-151">In the Azure portal, on the **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="326fc-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="326fc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_samlbase.png)

3. <span data-ttu-id="326fc-155">En la sección **HappyFox Domain and URLs** (Dominio y direcciones URL de HappyFox), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="326fc-155">On the **HappyFox Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="326fc-157">a.</span><span class="sxs-lookup"><span data-stu-id="326fc-157">a.</span></span> <span data-ttu-id="326fc-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.happyfox.com/`.</span><span class="sxs-lookup"><span data-stu-id="326fc-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="326fc-159">b.</span><span class="sxs-lookup"><span data-stu-id="326fc-159">b.</span></span> <span data-ttu-id="326fc-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="326fc-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="326fc-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="326fc-161">These values are not real.</span></span> <span data-ttu-id="326fc-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="326fc-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="326fc-163">Póngase en contacto con el [equipo de soporte de cliente de HappyFox](https://support.happyfox.com/home) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="326fc-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) to get these values.</span></span> 
 
4. <span data-ttu-id="326fc-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="326fc-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_certificate.png) 

5. <span data-ttu-id="326fc-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="326fc-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="326fc-168">En la sección **HappyFox Configuration** (Configuración de HappyFox), haga clic en **Configure HappyFox** (Configurar HappyFox) para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="326fc-168">On the **HappyFox Configuration** section, click **Configure HappyFox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="326fc-169">Copie el valor de **SAML Single Sign-On Service URL** (URL del servicio de inicio de sesión único de SAML) de la sección de **referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="326fc-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_configure.png) 

7. <span data-ttu-id="326fc-171">Inicie sesión en el portal del personal de HappyFox y vaya a **Manage** (Administrar), haga clic en la pestaña **Integrations** (Integraciones).</span><span class="sxs-lookup"><span data-stu-id="326fc-171">Sign on to your HappyFox staff portal and navigate to **Manage**, Click on **Integrations** tab.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/header.png) 

8. <span data-ttu-id="326fc-173">En la pestaña de integraciones, haga clic en **Configure** (Configurar) en **SAML Integration** (Integración de SAML) para abrir la configuración del inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="326fc-173">In the Integrations tab, Click **Configure** under **SAML Integration** to open the Single Sign On Settings.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/configure.png) 

9. <span data-ttu-id="326fc-175">En la sección de configuración de SAML, pegue el valor de **SAML Single Sign-On Service URL** (URL del servicio de inicio de sesión único de SAML) que ha copiado de Azure Portal en el cuadro de texto **SSO Target URL** (Dirección URL de destino de SSO).</span><span class="sxs-lookup"><span data-stu-id="326fc-175">Inside SAML configuration section, paste the **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/targeturl.png)

10. <span data-ttu-id="326fc-177">Abra el certificado descargado desde Azure Portal en el bloc de notas y pegue el contenido en la sección**IdP Signature** (Firma del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="326fc-177">Open the certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/cert.png)

11. <span data-ttu-id="326fc-179">Haga clic en el botón **Guardar configuración**.</span><span class="sxs-lookup"><span data-stu-id="326fc-179">Click **Save Settings** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="326fc-181">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="326fc-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="326fc-182">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="326fc-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="326fc-183">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="326fc-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="326fc-184">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="326fc-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="326fc-185">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="326fc-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="326fc-187">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="326fc-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="326fc-188">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="326fc-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="326fc-190">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="326fc-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="326fc-192">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="326fc-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="326fc-194">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="326fc-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="326fc-196">a.</span><span class="sxs-lookup"><span data-stu-id="326fc-196">a.</span></span> <span data-ttu-id="326fc-197">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="326fc-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="326fc-198">b.</span><span class="sxs-lookup"><span data-stu-id="326fc-198">b.</span></span> <span data-ttu-id="326fc-199">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="326fc-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="326fc-200">c.</span><span class="sxs-lookup"><span data-stu-id="326fc-200">c.</span></span> <span data-ttu-id="326fc-201">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="326fc-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="326fc-202">d.</span><span class="sxs-lookup"><span data-stu-id="326fc-202">d.</span></span> <span data-ttu-id="326fc-203">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="326fc-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="326fc-204">Creación de un usuario de prueba de HappyFox</span><span class="sxs-lookup"><span data-stu-id="326fc-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="326fc-205">La aplicación admite aprovisionamiento de usuarios Just-In-Time y, tras la autenticación, los usuarios se crean automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="326fc-205">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="326fc-206">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="326fc-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="326fc-207">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a HappyFox.</span><span class="sxs-lookup"><span data-stu-id="326fc-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HappyFox.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="326fc-209">**Para asignar a Britta Simon a HappyFox, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="326fc-209">**To assign Britta Simon to HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="326fc-210">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="326fc-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="326fc-212">En la lista de aplicaciones, seleccione **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="326fc-212">In the applications list, select **HappyFox**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_app.png) 

3. <span data-ttu-id="326fc-214">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="326fc-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="326fc-216">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="326fc-216">Click **Add** button.</span></span> <span data-ttu-id="326fc-217">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="326fc-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="326fc-219">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="326fc-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="326fc-220">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="326fc-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="326fc-221">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="326fc-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="326fc-222">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="326fc-222">Testing single sign-on</span></span>

<span data-ttu-id="326fc-223">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="326fc-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="326fc-224">Al hacer clic en el icono de HappyFox del Panel de acceso, debería entrar en la página de inicio de sesión de la aplicación HappyFox.</span><span class="sxs-lookup"><span data-stu-id="326fc-224">When you click the HappyFox tile in the Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="326fc-225">Debería ver el botón **"SAML"** en la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="326fc-225">You should see the **‘SAML’** button on the sign-in page.</span></span>

    ![Complemento](./media/active-directory-saas-happyfox-tutorial/saml.png) 

2. <span data-ttu-id="326fc-227">Haga clic en el botón **"SAML"** para iniciar sesión en HappyFox con su cuenta de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="326fc-227">Click the **‘SAML’** button to log in to HappyFox using your Azure AD account.</span></span>

<span data-ttu-id="326fc-228">Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="326fc-228">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="326fc-229">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="326fc-229">Additional resources</span></span>

* [<span data-ttu-id="326fc-230">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="326fc-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="326fc-231">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="326fc-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_203.png


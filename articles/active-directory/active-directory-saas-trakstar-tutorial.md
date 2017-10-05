---
title: "Tutorial: Integración de Azure Active Directory con Trakstar | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Trakstar."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411cb8c3-95c6-4138-acf2-ffc7f663e89a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 757429aa187e6536489b6636a0a11d122c7f9378
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trakstar"></a><span data-ttu-id="4e2c7-103">Tutorial: integración de Azure Active Directory con Trakstar</span><span class="sxs-lookup"><span data-stu-id="4e2c7-103">Tutorial: Azure Active Directory integration with Trakstar</span></span>

<span data-ttu-id="4e2c7-104">En este tutorial, aprenderá a integrar Trakstar con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4e2c7-104">In this tutorial, you learn how to integrate Trakstar with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4e2c7-105">La integración de Trakstar con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4e2c7-105">Integrating Trakstar with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4e2c7-106">Puede controlar en Azure AD quién tiene acceso a Trakstar.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-106">You can control in Azure AD who has access to Trakstar</span></span>
- <span data-ttu-id="4e2c7-107">Puede permitir que los usuarios inicien sesión automáticamente en Trakstar (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-107">You can enable your users to automatically get signed-on to Trakstar (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4e2c7-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4e2c7-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4e2c7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e2c7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4e2c7-110">Prerequisites</span></span>

<span data-ttu-id="4e2c7-111">Para configurar la integración de Azure AD con Trakstar, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4e2c7-111">To configure Azure AD integration with Trakstar, you need the following items:</span></span>

- <span data-ttu-id="4e2c7-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e2c7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4e2c7-113">Una suscripción habilitada para el inicio de sesión único en Trakstar</span><span class="sxs-lookup"><span data-stu-id="4e2c7-113">A Trakstar single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4e2c7-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4e2c7-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4e2c7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4e2c7-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4e2c7-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4e2c7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4e2c7-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4e2c7-118">Scenario description</span></span>
<span data-ttu-id="4e2c7-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4e2c7-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="4e2c7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4e2c7-121">Adición de Trakstar desde la galería</span><span class="sxs-lookup"><span data-stu-id="4e2c7-121">Adding Trakstar from the gallery</span></span>
2. <span data-ttu-id="4e2c7-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e2c7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakstar-from-the-gallery"></a><span data-ttu-id="4e2c7-123">Adición de Trakstar desde la galería</span><span class="sxs-lookup"><span data-stu-id="4e2c7-123">Adding Trakstar from the gallery</span></span>
<span data-ttu-id="4e2c7-124">Para configurar la integración de Trakstar en Azure AD, será preciso que agregue Trakstar desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-124">To configure the integration of Trakstar into Azure AD, you need to add Trakstar from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4e2c7-125">**Para agregar Trakstar desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4e2c7-125">**To add Trakstar from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4e2c7-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4e2c7-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4e2c7-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="4e2c7-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="4e2c7-133">En el cuadro de búsqueda, escriba **Trakstar**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-133">In the search box, type **Trakstar**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_search.png)

5. <span data-ttu-id="4e2c7-135">En el panel de resultados, seleccione **Trakstar** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-135">In the results panel, select **Trakstar**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4e2c7-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e2c7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4e2c7-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Trakstar con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-138">In this section, you configure and test Azure AD single sign-on with Trakstar based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4e2c7-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Trakstar para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trakstar is to a user in Azure AD.</span></span> <span data-ttu-id="4e2c7-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Trakstar.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-140">In other words, a link relationship between an Azure AD user and the related user in Trakstar needs to be established.</span></span>

<span data-ttu-id="4e2c7-141">Para establecer la relación de vínculo, en Trakstar, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-141">In Trakstar, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4e2c7-142">Para configurar y probar el inicio de sesión único de Azure AD con Trakstar, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4e2c7-142">To configure and test Azure AD single sign-on with Trakstar, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4e2c7-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4e2c7-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4e2c7-145">**[Creación de un usuario de prueba de Trakstar](#creating-a-trakstar-test-user)** : para tener un homólogo de Britta Simon en Trakstar vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-145">**[Creating a Trakstar test user](#creating-a-trakstar-test-user)** - to have a counterpart of Britta Simon in Trakstar that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4e2c7-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4e2c7-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4e2c7-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e2c7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4e2c7-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Trakstar.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trakstar application.</span></span>

<span data-ttu-id="4e2c7-150">**Para configurar el inicio de sesión único de Azure AD con Trakstar, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4e2c7-150">**To configure Azure AD single sign-on with Trakstar, perform the following steps:**</span></span>

1. <span data-ttu-id="4e2c7-151">En Azure Portal, en la página de integración de la aplicación **Trakstar**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-151">In the Azure portal, on the **Trakstar** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="4e2c7-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_samlbase.png)

3. <span data-ttu-id="4e2c7-155">En la sección **Trakstar Domain and URLs** (Dominio y direcciones URL de Trakstar), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4e2c7-155">On the **Trakstar Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_url.png)

    <span data-ttu-id="4e2c7-157">a.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-157">a.</span></span> <span data-ttu-id="4e2c7-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://app.trakstar.com/auth/saml/callback?namespace=<NAMESPACE>`.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.trakstar.com/auth/saml/callback?namespace=<NAMESPACE>`</span></span>

    <span data-ttu-id="4e2c7-159">b.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-159">b.</span></span> <span data-ttu-id="4e2c7-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.trakstar.com`</span><span class="sxs-lookup"><span data-stu-id="4e2c7-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.trakstar.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4e2c7-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-161">These values are not real.</span></span> <span data-ttu-id="4e2c7-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4e2c7-163">Póngase en contacto con el [equipo de soporte técnico de Trakstar](mailto:integrations@trakstar.com) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-163">Contact [Trakstar Client support team](mailto:integrations@trakstar.com) to get these values.</span></span> 
 
4. <span data-ttu-id="4e2c7-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_certificate.png) 

5. <span data-ttu-id="4e2c7-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="4e2c7-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trakstar-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4e2c7-168">En la sección **Trakstar Configuration** (Configuración de Trakstar), haga clic en **Configure Trakstar** (Configurar Trakstar) para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-168">On the **Trakstar Configuration** section, click **Configure Trakstar** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4e2c7-169">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_configure.png) 

7. <span data-ttu-id="4e2c7-171">Para configurar el inicio de sesión único en **Trakstar**, es preciso enviar el **Certificado (Base64)** descargado, la **dirección URL de cierre de sesión, el identificador de identidad de SAML y la dirección URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de Trakstar](mailto:integrations@trakstar.com).</span><span class="sxs-lookup"><span data-stu-id="4e2c7-171">To configure single sign-on on **Trakstar** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Trakstar support team](mailto:integrations@trakstar.com).</span></span> 

> [!TIP]
> <span data-ttu-id="4e2c7-172">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4e2c7-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4e2c7-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4e2c7-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4e2c7-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e2c7-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="4e2c7-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4e2c7-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="4e2c7-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="4e2c7-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4e2c7-179">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trakstar-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4e2c7-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trakstar-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4e2c7-183">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trakstar-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4e2c7-185">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="4e2c7-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trakstar-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4e2c7-187">a.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-187">a.</span></span> <span data-ttu-id="4e2c7-188">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4e2c7-189">b.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-189">b.</span></span> <span data-ttu-id="4e2c7-190">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4e2c7-191">c.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-191">c.</span></span> <span data-ttu-id="4e2c7-192">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4e2c7-193">d.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-193">d.</span></span> <span data-ttu-id="4e2c7-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-194">Click **Create**.</span></span>
 
### <a name="creating-a-trakstar-test-user"></a><span data-ttu-id="4e2c7-195">Crear un usuario de prueba de Trakstar</span><span class="sxs-lookup"><span data-stu-id="4e2c7-195">Creating a Trakstar test user</span></span>

<span data-ttu-id="4e2c7-196">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Trakstar.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-196">The objective of this section is to create a user called Britta Simon in Trakstar.</span></span> <span data-ttu-id="4e2c7-197">Trabaje con el [equipo de soporte técnico de Trakstar](mailto:integrations@trakstar.com) para agregar los usuarios en la cuenta de Trakstar.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-197">Work with [Trakstar support team](mailto:integrations@trakstar.com) to add the users in the Trakstar account.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4e2c7-198">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e2c7-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4e2c7-199">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Trakstar.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trakstar.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="4e2c7-201">**Para asignar a Britta Simon a Trakstar, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="4e2c7-201">**To assign Britta Simon to Trakstar, perform the following steps:**</span></span>

1. <span data-ttu-id="4e2c7-202">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4e2c7-204">En la lista de aplicaciones, seleccione **@Trakstar**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-204">In the applications list, select **Trakstar**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_app.png) 

3. <span data-ttu-id="4e2c7-206">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="4e2c7-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-208">Click **Add** button.</span></span> <span data-ttu-id="4e2c7-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="4e2c7-211">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4e2c7-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4e2c7-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4e2c7-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="4e2c7-214">Testing single sign-on</span></span>

<span data-ttu-id="4e2c7-215">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="4e2c7-216">Al hacer clic en el icono de Trakstar en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Trakstar.</span><span class="sxs-lookup"><span data-stu-id="4e2c7-216">When you click the Trakstar tile in the Access Panel, you should get automatically signed-on to your Trakstar application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4e2c7-217">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4e2c7-217">Additional resources</span></span>

* [<span data-ttu-id="4e2c7-218">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4e2c7-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4e2c7-219">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4e2c7-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_203.png


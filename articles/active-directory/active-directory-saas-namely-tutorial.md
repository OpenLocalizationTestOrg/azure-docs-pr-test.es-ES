---
title: "Tutorial: Integración de Azure Active Directory con Namely | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Namely."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 1d7e8fbcfc757853ab909bbb05522f3dc387715d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="195ed-103">Tutorial: Integración de Azure Active Directory con Namely</span><span class="sxs-lookup"><span data-stu-id="195ed-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="195ed-104">En este tutorial, aprenderá a integrar Namely con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="195ed-104">In this tutorial, you learn how to integrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="195ed-105">La integración de Namely con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="195ed-105">Integrating Namely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="195ed-106">Puede controlar en Azure AD quién tiene acceso a Namely.</span><span class="sxs-lookup"><span data-stu-id="195ed-106">You can control in Azure AD who has access to Namely</span></span>
- <span data-ttu-id="195ed-107">Puede permitir que los usuarios inicien sesión automáticamente en Namely (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="195ed-107">You can enable your users to automatically get signed-on to Namely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="195ed-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="195ed-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="195ed-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="195ed-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="195ed-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="195ed-110">Prerequisites</span></span>

<span data-ttu-id="195ed-111">Para configurar la integración de Azure AD con Namely, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="195ed-111">To configure Azure AD integration with Namely, you need the following items:</span></span>

- <span data-ttu-id="195ed-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="195ed-112">An Azure AD subscription</span></span>
- <span data-ttu-id="195ed-113">Una suscripción habilitada para el inicio de sesión único en Namely</span><span class="sxs-lookup"><span data-stu-id="195ed-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="195ed-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="195ed-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="195ed-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="195ed-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="195ed-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="195ed-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="195ed-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="195ed-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="195ed-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="195ed-118">Scenario description</span></span>
<span data-ttu-id="195ed-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="195ed-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="195ed-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="195ed-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="195ed-121">Adición de Namely desde la galería</span><span class="sxs-lookup"><span data-stu-id="195ed-121">Adding Namely from the gallery</span></span>
2. <span data-ttu-id="195ed-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="195ed-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-the-gallery"></a><span data-ttu-id="195ed-123">Adición de Namely desde la galería</span><span class="sxs-lookup"><span data-stu-id="195ed-123">Adding Namely from the gallery</span></span>
<span data-ttu-id="195ed-124">Para configurar la integración de Namely en Azure AD, es preciso agregar Namely desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="195ed-124">To configure the integration of Namely into Azure AD, you need to add Namely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="195ed-125">**Para agregar Namely desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="195ed-125">**To add Namely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="195ed-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="195ed-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="195ed-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="195ed-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="195ed-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="195ed-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="195ed-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="195ed-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="195ed-133">En el cuadro de búsqueda, escriba **Namely**.</span><span class="sxs-lookup"><span data-stu-id="195ed-133">In the search box, type **Namely**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="195ed-135">En el panel de resultados, seleccione **Namely** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="195ed-135">In the results panel, select **Namely**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="195ed-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="195ed-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="195ed-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Namely con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="195ed-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="195ed-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Namely para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="195ed-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Namely is to a user in Azure AD.</span></span> <span data-ttu-id="195ed-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Namely.</span><span class="sxs-lookup"><span data-stu-id="195ed-140">In other words, a link relationship between an Azure AD user and the related user in Namely needs to be established.</span></span>

<span data-ttu-id="195ed-141">Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de Namely.</span><span class="sxs-lookup"><span data-stu-id="195ed-141">In Namely, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="195ed-142">Para configurar y probar el inicio de sesión único de Azure AD con Namely, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="195ed-142">To configure and test Azure AD single sign-on with Namely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="195ed-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="195ed-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="195ed-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="195ed-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="195ed-145">**[Creación de un usuario de prueba de Namely](#creating-a-namely-test-user)**: el objetivo es tener un homólogo de Britta Simon en Namely que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="195ed-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - to have a counterpart of Britta Simon in Namely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="195ed-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="195ed-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="195ed-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="195ed-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="195ed-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="195ed-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="195ed-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Namely.</span><span class="sxs-lookup"><span data-stu-id="195ed-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="195ed-150">**Para configurar el inicio de sesión único de Azure AD con Namely, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="195ed-150">**To configure Azure AD single sign-on with Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="195ed-151">En la página de integración de la aplicación **Namely** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="195ed-151">In the Azure portal, on the **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="195ed-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="195ed-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="195ed-155">En la sección **Dominio y direcciones URL de Namely**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="195ed-155">On the **Namely Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="195ed-157">a.</span><span class="sxs-lookup"><span data-stu-id="195ed-157">a.</span></span> <span data-ttu-id="195ed-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.namely.com`.</span><span class="sxs-lookup"><span data-stu-id="195ed-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="195ed-159">b.</span><span class="sxs-lookup"><span data-stu-id="195ed-159">b.</span></span> <span data-ttu-id="195ed-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="195ed-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="195ed-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="195ed-161">These values are not real.</span></span> <span data-ttu-id="195ed-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="195ed-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="195ed-163">Póngase en contacto con el [equipo de atención al cliente de Namely](https://www.namely.com/contact/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="195ed-163">Contact [Namely Client support team](https://www.namely.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="195ed-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="195ed-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="195ed-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="195ed-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="195ed-168">En la sección **Configuración de Namely**, haga clic en **Configurar Namely** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="195ed-168">On the **Namely Configuration** section, click **Configure Namely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="195ed-169">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="195ed-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="195ed-171">En otra ventana del explorador, inicie sesión en su sitio de la compañía de Namely como administrador.</span><span class="sxs-lookup"><span data-stu-id="195ed-171">In another browser window, sign on to your Namely company site as an administrator.</span></span>

8. <span data-ttu-id="195ed-172">En la barra de herramientas de la parte superior, haga clic en **Company**(Empresa).</span><span class="sxs-lookup"><span data-stu-id="195ed-172">In the toolbar on the top, click **Company**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="195ed-174">Haga clic en la pestaña **Configuración** .</span><span class="sxs-lookup"><span data-stu-id="195ed-174">Click the **Settings** tab.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="195ed-176">Haga clic en **SAML**.</span><span class="sxs-lookup"><span data-stu-id="195ed-176">Click **SAML**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="195ed-178">En la página **SAML Settings** (Configuración de SAML), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="195ed-178">On the **SAML Settings** page, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="195ed-180">a.</span><span class="sxs-lookup"><span data-stu-id="195ed-180">a.</span></span> <span data-ttu-id="195ed-181">Haga clic en **Enable SAML**(Habilitar SAML).</span><span class="sxs-lookup"><span data-stu-id="195ed-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="195ed-182">b.</span><span class="sxs-lookup"><span data-stu-id="195ed-182">b.</span></span> <span data-ttu-id="195ed-183">En el cuadro de texto **Identity provider SSO url** (Dirección URL de inicio de sesión único del proveedor de identidades), pegue el valor de **dirección URL del servicio de inicio de sesión único de SAML**, que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="195ed-183">In the **Identity provider SSO url** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="195ed-184">c.</span><span class="sxs-lookup"><span data-stu-id="195ed-184">c.</span></span> <span data-ttu-id="195ed-185">Abra el certificado descargado en el Bloc de notas, copie el contenido y péguelo en el cuadro de texto **Certificado de proveedor de identidades** .</span><span class="sxs-lookup"><span data-stu-id="195ed-185">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="195ed-186">d.</span><span class="sxs-lookup"><span data-stu-id="195ed-186">d.</span></span> <span data-ttu-id="195ed-187">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="195ed-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="195ed-188">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="195ed-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="195ed-189">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="195ed-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="195ed-190">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="195ed-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="195ed-191">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="195ed-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="195ed-192">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="195ed-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="195ed-194">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="195ed-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="195ed-195">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="195ed-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="195ed-197">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="195ed-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="195ed-199">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="195ed-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="195ed-201">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="195ed-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="195ed-203">a.</span><span class="sxs-lookup"><span data-stu-id="195ed-203">a.</span></span> <span data-ttu-id="195ed-204">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="195ed-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="195ed-205">b.</span><span class="sxs-lookup"><span data-stu-id="195ed-205">b.</span></span> <span data-ttu-id="195ed-206">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="195ed-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="195ed-207">c.</span><span class="sxs-lookup"><span data-stu-id="195ed-207">c.</span></span> <span data-ttu-id="195ed-208">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="195ed-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="195ed-209">d.</span><span class="sxs-lookup"><span data-stu-id="195ed-209">d.</span></span> <span data-ttu-id="195ed-210">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="195ed-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="195ed-211">Creación de un usuario de prueba en Namely</span><span class="sxs-lookup"><span data-stu-id="195ed-211">Creating a Namely test user</span></span>

<span data-ttu-id="195ed-212">El objetivo de esta sección es crear un usuario llamado Britta Simon en Namely.</span><span class="sxs-lookup"><span data-stu-id="195ed-212">The objective of this section is to create a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="195ed-213">**Para crear un usuario llamado Britta Simon en Namely, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="195ed-213">**To create a user called Britta Simon in Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="195ed-214">Inicie sesión en su sitio de la compañía de Namely como administrador.</span><span class="sxs-lookup"><span data-stu-id="195ed-214">Sign-on to your Namely company site as an administrator.</span></span>

2. <span data-ttu-id="195ed-215">En la barra de herramientas de la parte superior, haga clic en **People**(Gente).</span><span class="sxs-lookup"><span data-stu-id="195ed-215">In the toolbar on the top, click **People**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="195ed-217">Haga clic en la pestaña **Directory** (Directorio).</span><span class="sxs-lookup"><span data-stu-id="195ed-217">Click the **Directory** tab.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="195ed-219">Haga clic en **Agregar nueva persona**.</span><span class="sxs-lookup"><span data-stu-id="195ed-219">Click **Add New Person**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="195ed-221">En el cuadro de diálogo **Agregar nueva persona** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="195ed-221">On the **Add New Person** dialog, perform the following steps:</span></span>

    <span data-ttu-id="195ed-222">a.</span><span class="sxs-lookup"><span data-stu-id="195ed-222">a.</span></span> <span data-ttu-id="195ed-223">En el cuadro de texto **Nombre**, escriba **Britta**.</span><span class="sxs-lookup"><span data-stu-id="195ed-223">In the **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="195ed-224">b.</span><span class="sxs-lookup"><span data-stu-id="195ed-224">b.</span></span> <span data-ttu-id="195ed-225">En el cuadro de texto **Apellidos**, escriba **Simon**.</span><span class="sxs-lookup"><span data-stu-id="195ed-225">In the **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="195ed-226">c.</span><span class="sxs-lookup"><span data-stu-id="195ed-226">c.</span></span> <span data-ttu-id="195ed-227">En el cuadro de texto **Correo electrónico**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="195ed-227">In the **Email** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="195ed-228">d.</span><span class="sxs-lookup"><span data-stu-id="195ed-228">d.</span></span> <span data-ttu-id="195ed-229">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="195ed-229">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="195ed-230">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="195ed-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="195ed-231">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Namely.</span><span class="sxs-lookup"><span data-stu-id="195ed-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Namely.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="195ed-233">**Para asignar Britta Simon a Namely, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="195ed-233">**To assign Britta Simon to Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="195ed-234">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="195ed-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="195ed-236">En la lista de aplicaciones, seleccione **Namely**.</span><span class="sxs-lookup"><span data-stu-id="195ed-236">In the applications list, select **Namely**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="195ed-238">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="195ed-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="195ed-240">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="195ed-240">Click **Add** button.</span></span> <span data-ttu-id="195ed-241">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="195ed-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="195ed-243">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="195ed-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="195ed-244">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="195ed-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="195ed-245">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="195ed-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="195ed-246">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="195ed-246">Testing single sign-on</span></span>

<span data-ttu-id="195ed-247">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="195ed-247">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="195ed-248">Al hacer clic en el icono de Namely en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Namely.</span><span class="sxs-lookup"><span data-stu-id="195ed-248">When you click the Namely tile in the Access Panel, you should get automatically signed-on to your Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="195ed-249">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="195ed-249">Additional resources</span></span>

* [<span data-ttu-id="195ed-250">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="195ed-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="195ed-251">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="195ed-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png


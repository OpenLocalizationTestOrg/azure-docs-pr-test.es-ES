---
title: "Tutorial: Integración de Azure Active Directory con eDigitalResearch | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y eDigitalResearch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: f877a1dd844c40c913f3121e5288952653c312cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a><span data-ttu-id="1fc1d-103">Tutorial: integración de Azure Active Directory con eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="1fc1d-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span></span>

<span data-ttu-id="1fc1d-104">En este tutorial, obtendrá información sobre cómo integrar eDigitalResearch con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1fc1d-104">In this tutorial, you learn how to integrate eDigitalResearch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1fc1d-105">La integración de eDigitalResearch con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="1fc1d-105">Integrating eDigitalResearch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1fc1d-106">Puede controlar en Azure AD quién tiene acceso a eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-106">You can control in Azure AD who has access to eDigitalResearch.</span></span>
- <span data-ttu-id="1fc1d-107">Puede permitir que los usuarios inicien sesión automáticamente en eDigitalResearch (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-107">You can enable your users to automatically get signed-on to eDigitalResearch (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1fc1d-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="1fc1d-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1fc1d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fc1d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1fc1d-110">Prerequisites</span></span>

<span data-ttu-id="1fc1d-111">Para configurar la integración de Azure AD con eDigitalResearch, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1fc1d-111">To configure Azure AD integration with eDigitalResearch, you need the following items:</span></span>

- <span data-ttu-id="1fc1d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fc1d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1fc1d-113">Una suscripción habilitada para el inicio de sesión único en eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="1fc1d-113">A eDigitalResearch single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1fc1d-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1fc1d-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="1fc1d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1fc1d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1fc1d-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1fc1d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1fc1d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="1fc1d-118">Scenario description</span></span>
<span data-ttu-id="1fc1d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1fc1d-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="1fc1d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1fc1d-121">Incorporación de eDigitalResearch desde la galería</span><span class="sxs-lookup"><span data-stu-id="1fc1d-121">Adding eDigitalResearch from the gallery</span></span>
2. <span data-ttu-id="1fc1d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fc1d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-edigitalresearch-from-the-gallery"></a><span data-ttu-id="1fc1d-123">Incorporación de eDigitalResearch desde la galería</span><span class="sxs-lookup"><span data-stu-id="1fc1d-123">Adding eDigitalResearch from the gallery</span></span>
<span data-ttu-id="1fc1d-124">Para configurar la integración de eDigitalResearch en Azure AD, deberá agregar eDigitalResearch desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-124">To configure the integration of eDigitalResearch into Azure AD, you need to add eDigitalResearch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1fc1d-125">**Para agregar eDigitalResearch desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1fc1d-125">**To add eDigitalResearch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1fc1d-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="1fc1d-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1fc1d-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="1fc1d-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="1fc1d-133">En el cuadro de búsqueda, escriba **eDigitalResearch**, seleccione **eDigitalResearch** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-133">In the search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button to add the application.</span></span>

    ![eDigitalResearch en la lista de resultados](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1fc1d-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fc1d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1fc1d-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con eDigitalResearch con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1fc1d-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1fc1d-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de eDigitalResearch para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in eDigitalResearch is to a user in Azure AD.</span></span> <span data-ttu-id="1fc1d-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-138">In other words, a link relationship between an Azure AD user and the related user in eDigitalResearch needs to be established.</span></span>

<span data-ttu-id="1fc1d-139">Para establecer la relación de vínculo, en eDigitalResearch asigne el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-139">In eDigitalResearch, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1fc1d-140">Para configurar y probar el inicio de sesión único de Azure AD con eDigitalResearch, se deben completar los siguientes pasos preliminares:</span><span class="sxs-lookup"><span data-stu-id="1fc1d-140">To configure and test Azure AD single sign-on with eDigitalResearch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1fc1d-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1fc1d-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1fc1d-143">**[Creación de un usuario de prueba de eDigitalResearch](#create-a-edigitalresearch-test-user)**: para tener un homólogo de Britta Simon en eDigitalResearch que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - to have a counterpart of Britta Simon in eDigitalResearch that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1fc1d-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1fc1d-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-145">**[Test single sign-on](#test-single-sign-on)**  to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1fc1d-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fc1d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1fc1d-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eDigitalResearch application.</span></span>

<span data-ttu-id="1fc1d-148">**Para configurar el inicio de sesión único de Azure AD con eDigitalResearch, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1fc1d-148">**To configure Azure AD single sign-on with eDigitalResearch, perform the following steps:**</span></span>

1. <span data-ttu-id="1fc1d-149">En la página de integración de la aplicación **eDigitalResearch** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-149">In the Azure portal, on the **eDigitalResearch** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="1fc1d-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

3. <span data-ttu-id="1fc1d-153">En la sección **Dominio y direcciones URL de eDigitalResearch**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1fc1d-153">On the **eDigitalResearch Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    <span data-ttu-id="1fc1d-155">a.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-155">a.</span></span> <span data-ttu-id="1fc1d-156">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<company-name>.edigitalresearch.com`</span><span class="sxs-lookup"><span data-stu-id="1fc1d-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com`</span></span>

    <span data-ttu-id="1fc1d-157">b.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-157">b.</span></span> <span data-ttu-id="1fc1d-158">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<company-name>.edigitalresearch.com/login/consume`.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1fc1d-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-159">These values are not real.</span></span> <span data-ttu-id="1fc1d-160">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="1fc1d-161">Póngase en contacto con el [equipo de soporte técnico de eDigitalResearch](http://www.maruedr.com/contact) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) to get these values.</span></span>
 


4. <span data-ttu-id="1fc1d-162">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-162">On the **SAML Signing Certificate** section, click **Certificate Base(64)** and then save the certificate file on your computer.</span></span>

    <span data-ttu-id="1fc1d-163">!</span><span class="sxs-lookup"><span data-stu-id="1fc1d-163">!</span></span>![Vínculo de descarga del certificado](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

5. <span data-ttu-id="1fc1d-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="1fc1d-165">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1fc1d-167">En la sección **Configuración de eDigitalResearch**, haga clic en **Configurar eDigitalResearch** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-167">On the **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1fc1d-168">Copie los valores de **Sign-Out URL, SAML Entity ID** (Dirección URL de cierre de sesión, Identificador de entidad de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-168">Copy the **Sign-Out URL, SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configuración de eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

7. <span data-ttu-id="1fc1d-170">Para configurar el inicio de sesión único en **eDigitalResearch**, es preciso enviar los valores descargados de **Certificado (Base64)**, **SAML Entity ID** (Identificador de entidad de SAML) y **Sign-Out URL** (Dirección URL de cierre de sesión) al [equipo de soporte técnico de eDigitalResearch](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="1fc1d-170">To configure single sign-on on **eDigitalResearch** side, you need to send the downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** to [eDigitalResearch support team](http://www.maruedr.com/contact).</span></span> <span data-ttu-id="1fc1d-171">El equipo de soporte técnico lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1fc1d-172">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1fc1d-173">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1fc1d-174">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1fc1d-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1fc1d-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fc1d-175">Create an Azure AD test user</span></span>

<span data-ttu-id="1fc1d-176">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1fc1d-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="1fc1d-178">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="1fc1d-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1fc1d-179">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1fc1d-181">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1fc1d-183">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1fc1d-185">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1fc1d-185">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1fc1d-187">a.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-187">a.</span></span> <span data-ttu-id="1fc1d-188">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1fc1d-189">b.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-189">b.</span></span> <span data-ttu-id="1fc1d-190">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="1fc1d-191">c.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-191">c.</span></span> <span data-ttu-id="1fc1d-192">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="1fc1d-193">d.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-193">d.</span></span> <span data-ttu-id="1fc1d-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-194">Click **Create**.</span></span>
  
### <a name="create-a-edigitalresearch-test-user"></a><span data-ttu-id="1fc1d-195">Creación de un usuario de prueba de eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="1fc1d-195">Create a eDigitalResearch test user</span></span>

<span data-ttu-id="1fc1d-196">El objetivo de esta sección es crear un usuario llamado Britta Simon en eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-196">The objective of this section is to create a user called Britta Simon in eDigitalResearch.</span></span> 

<span data-ttu-id="1fc1d-197">Trabaje con el [equipo de soporte técnico de eDigitalResearch](http://www.maruedr.com/contact) para crear los usuarios.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-197">Work with the [eDigitalResearch support team](http://www.maruedr.com/contact) to get users created.</span></span>     
    
 > [!NOTE]
 > <span data-ttu-id="1fc1d-198">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo y seguirá un vínculo para confirmar su cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-198">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1fc1d-199">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1fc1d-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="1fc1d-200">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eDigitalResearch.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="1fc1d-202">**Para asignar Britta Simon a eDigitalResearch, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="1fc1d-202">**To assign Britta Simon to eDigitalResearch, perform the following steps:**</span></span>

1. <span data-ttu-id="1fc1d-203">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="1fc1d-205">En la lista de aplicaciones, seleccione **eDigitalResearch**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-205">In the applications list, select **eDigitalResearch**.</span></span>

    ![Vínculo a eDigitalResearch en la lista de aplicaciones](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

3. <span data-ttu-id="1fc1d-207">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="1fc1d-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-209">Click **Add** button.</span></span> <span data-ttu-id="1fc1d-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="1fc1d-212">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1fc1d-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1fc1d-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1fc1d-215">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="1fc1d-215">Test single sign-on</span></span>

<span data-ttu-id="1fc1d-216">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1fc1d-217">Al hacer clic en el icono de eDigitalResearch en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="1fc1d-217">When you click the eDigitalResearch tile in the Access Panel, you should get automatically signed-on to your eDigitalResearch application.</span></span>
<span data-ttu-id="1fc1d-218">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1fc1d-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1fc1d-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1fc1d-219">Additional resources</span></span>

* [<span data-ttu-id="1fc1d-220">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1fc1d-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1fc1d-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1fc1d-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_203.png


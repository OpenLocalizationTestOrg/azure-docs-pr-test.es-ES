---
title: "Tutorial: integración de Azure Active Directory con Nomadic | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Nomadic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 13d02b1c-d98a-40b1-824f-afa45a2deb6a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 1817a1395c2ffa7268abfff268d9d041f7f21a57
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nomadic"></a><span data-ttu-id="b5b29-103">Tutorial: Integración de Azure Active Directory con Nomadic</span><span class="sxs-lookup"><span data-stu-id="b5b29-103">Tutorial: Azure Active Directory integration with Nomadic</span></span>

<span data-ttu-id="b5b29-104">En este tutorial, obtendrá información sobre cómo integrar Nomadic con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b5b29-104">In this tutorial, you learn how to integrate Nomadic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b5b29-105">La integración de Nomadic con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b5b29-105">Integrating Nomadic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b5b29-106">Puede controlar en Azure AD quién tiene acceso a Nomadic.</span><span class="sxs-lookup"><span data-stu-id="b5b29-106">You can control in Azure AD who has access to Nomadic.</span></span>
- <span data-ttu-id="b5b29-107">Puede permitir que los usuarios inicien sesión automáticamente en Nomadic (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5b29-107">You can enable your users to automatically get signed-on to Nomadic (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b5b29-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b5b29-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b5b29-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b5b29-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5b29-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b5b29-110">Prerequisites</span></span>

<span data-ttu-id="b5b29-111">Para configurar la integración de Azure AD con Nomadic, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b5b29-111">To configure Azure AD integration with Nomadic, you need the following items:</span></span>

- <span data-ttu-id="b5b29-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5b29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b5b29-113">Una suscripción habilitada para el inicio de sesión único en Nomadic</span><span class="sxs-lookup"><span data-stu-id="b5b29-113">A Nomadic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b5b29-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b5b29-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b5b29-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b5b29-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b5b29-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b5b29-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b5b29-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una [versión de evaluación de un mes aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b5b29-117">If you don't have an Azure AD trial environment, you can [get a one-month trial here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b5b29-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b5b29-118">Scenario description</span></span>
<span data-ttu-id="b5b29-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b5b29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b5b29-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="b5b29-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b5b29-121">Agregar Nomadic desde la galería</span><span class="sxs-lookup"><span data-stu-id="b5b29-121">Add Nomadic from the gallery</span></span>
2. <span data-ttu-id="b5b29-122">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5b29-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-nomadic-from-the-gallery"></a><span data-ttu-id="b5b29-123">Agregar Nomadic desde la galería</span><span class="sxs-lookup"><span data-stu-id="b5b29-123">Add Nomadic from the gallery</span></span>
<span data-ttu-id="b5b29-124">Para configurar la integración de Nomadic en Azure AD, deberá agregar Nomadic desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="b5b29-124">To configure the integration of Nomadic into Azure AD, you need to add Nomadic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b5b29-125">**Para agregar Nomadic desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b5b29-125">**To add Nomadic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b5b29-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="b5b29-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b5b29-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="b5b29-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b5b29-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="b5b29-133">En el cuadro de búsqueda, escriba **Nomadic**, seleccione **Nomadic** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b5b29-133">In the search box, type **Nomadic**, select **Nomadic** from result panel then click **Add** button to add the application.</span></span>

    ![Nomadic en la lista de resultados](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b5b29-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5b29-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b5b29-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Nomadic con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b5b29-136">In this section, you configure and test Azure AD single sign-on with Nomadic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b5b29-137">Para que el inicio de sesión único funcione, Azure AD necesita saber cuál es el usuario homólogo de Nomadic para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5b29-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Nomadic is to a user in Azure AD.</span></span> <span data-ttu-id="b5b29-138">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Nomadic.</span><span class="sxs-lookup"><span data-stu-id="b5b29-138">In other words, a link relationship between an Azure AD user and the related user in Nomadic needs to be established.</span></span>

<span data-ttu-id="b5b29-139">Para establecer la relación de vínculo, en Nomadic, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-139">In Nomadic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b5b29-140">Para configurar y probar el inicio de sesión único de Azure AD con Nomadic, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b5b29-140">To configure and test Azure AD single sign-on with Nomadic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b5b29-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="b5b29-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b5b29-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b5b29-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5b29-143">**[Creación de un usuario de prueba de Nomadic](#create-a-nomadic-test-user)**: para tener un homólogo de Britta Simon en Nomadic que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5b29-143">**[Create a Nomadic test user](#create-a-nomadic-test-user)** - to have a counterpart of Britta Simon in Nomadic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b5b29-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5b29-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5b29-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="b5b29-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b5b29-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5b29-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b5b29-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Nomadic.</span><span class="sxs-lookup"><span data-stu-id="b5b29-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nomadic application.</span></span>

<span data-ttu-id="b5b29-148">**Para configurar el inicio de sesión único de Azure AD con Nomadic, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b5b29-148">**To configure Azure AD single sign-on with Nomadic, perform the following steps:**</span></span>

1. <span data-ttu-id="b5b29-149">En Azure Portal, en la página de integración de la aplicación **Nomadic**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-149">In the Azure portal, on the **Nomadic** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="b5b29-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b5b29-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_samlbase.png)

3. <span data-ttu-id="b5b29-153">En la sección **Dominio y direcciones URL de Nomadic**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b5b29-153">On the **Nomadic Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Nomadic](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_url.png)

    <span data-ttu-id="b5b29-155">a.</span><span class="sxs-lookup"><span data-stu-id="b5b29-155">a.</span></span> <span data-ttu-id="b5b29-156">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<company name>.nomadic.fm/signin`.</span><span class="sxs-lookup"><span data-stu-id="b5b29-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/signin`</span></span>

    <span data-ttu-id="b5b29-157">b.</span><span class="sxs-lookup"><span data-stu-id="b5b29-157">b.</span></span> <span data-ttu-id="b5b29-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<company name>.nomadic.fm/auth/saml2/sp`, `https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span><span class="sxs-lookup"><span data-stu-id="b5b29-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.nomadic.fm/auth/saml2/sp`, `https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b5b29-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="b5b29-159">These values are not real.</span></span> <span data-ttu-id="b5b29-160">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="b5b29-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b5b29-161">Póngase en contacto con el [equipo de soporte técnico de Nomadic](mailto:help@nomadic.fm) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="b5b29-161">Contact [Nomadic Client support team](mailto:help@nomadic.fm) to get these values.</span></span> 
 


4. <span data-ttu-id="b5b29-162">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b5b29-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_certificate.png) 

5. <span data-ttu-id="b5b29-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="b5b29-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-nomadic-tutorial/tutorial_general_400.png)

6.  <span data-ttu-id="b5b29-166">Para configurar SSO para su aplicación, póngase en contacto con el [equipo de soporte técnico de Nomadic](mailto:help@nomadic.fm) y proporcione los **metadatos** descargados.</span><span class="sxs-lookup"><span data-stu-id="b5b29-166">To get SSO configured for your application, contact [Nomadic support team](mailto:help@nomadic.fm) and provide them with the downloaded **metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="b5b29-167">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b5b29-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b5b29-168">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="b5b29-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b5b29-169">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b5b29-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b5b29-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5b29-170">Create an Azure AD test user</span></span>

<span data-ttu-id="b5b29-171">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b5b29-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="b5b29-173">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="b5b29-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b5b29-174">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-nomadic-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b5b29-176">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-nomadic-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b5b29-178">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-nomadic-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b5b29-180">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b5b29-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-nomadic-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b5b29-182">a.</span><span class="sxs-lookup"><span data-stu-id="b5b29-182">a.</span></span> <span data-ttu-id="b5b29-183">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b5b29-184">b.</span><span class="sxs-lookup"><span data-stu-id="b5b29-184">b.</span></span> <span data-ttu-id="b5b29-185">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b5b29-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b5b29-186">c.</span><span class="sxs-lookup"><span data-stu-id="b5b29-186">c.</span></span> <span data-ttu-id="b5b29-187">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b5b29-188">d.</span><span class="sxs-lookup"><span data-stu-id="b5b29-188">d.</span></span> <span data-ttu-id="b5b29-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-189">Click **Create**.</span></span>
 
### <a name="create-a-nomadic-test-user"></a><span data-ttu-id="b5b29-190">Creación de un usuario de prueba de Nomadic</span><span class="sxs-lookup"><span data-stu-id="b5b29-190">Create a Nomadic test user</span></span>

<span data-ttu-id="b5b29-191">En esta sección, creará un usuario llamado Britta Simon en Nomadic.</span><span class="sxs-lookup"><span data-stu-id="b5b29-191">In this section, you create a user called Britta Simon in Nomadic.</span></span> <span data-ttu-id="b5b29-192">Colabore con el [equipo de soporte técnico de Nomadic](mailto:help@nomadic.fm) para agregar los usuarios en la plataforma de Nomadic.</span><span class="sxs-lookup"><span data-stu-id="b5b29-192">Please work with [Nomadic support team](mailto:help@nomadic.fm) to add the users in the Nomadic platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b5b29-193">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5b29-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="b5b29-194">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Nomadic.</span><span class="sxs-lookup"><span data-stu-id="b5b29-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nomadic.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="b5b29-196">**Para asignar Britta Simon a Nomadic, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b5b29-196">**To assign Britta Simon to Nomadic, perform the following steps:**</span></span>

1. <span data-ttu-id="b5b29-197">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b5b29-199">En la lista de aplicaciones, seleccione **Nomadic**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-199">In the applications list, select **Nomadic**.</span></span>

    ![Vínculo a Nomadic en la lista de aplicaciones](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_app.png)  

3. <span data-ttu-id="b5b29-201">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="b5b29-203">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-203">Click **Add** button.</span></span> <span data-ttu-id="b5b29-204">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="b5b29-206">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="b5b29-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b5b29-207">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5b29-208">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b5b29-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b5b29-209">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="b5b29-209">Test single sign-on</span></span>

<span data-ttu-id="b5b29-210">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b5b29-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b5b29-211">Al hacer clic en el icono de Nomadic en el panel de acceso, debería iniciar sesión automáticamente en la aplicación Nomadic.</span><span class="sxs-lookup"><span data-stu-id="b5b29-211">When you click the Nomadic tile in the Access Panel, you should get automatically signed-on to your Nomadic application.</span></span>
<span data-ttu-id="b5b29-212">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b5b29-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b5b29-213">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b5b29-213">Additional resources</span></span>

* [<span data-ttu-id="b5b29-214">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b5b29-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5b29-215">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b5b29-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_203.png


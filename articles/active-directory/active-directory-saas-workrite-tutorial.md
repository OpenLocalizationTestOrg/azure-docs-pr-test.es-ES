---
title: "Tutorial: Integración de Azure Active Directory con Workrite | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Workrite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2a5c2956-a011-4d5c-877b-80679b6587b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4358c4c621634c17cbbd7fa1c72f12746b8e4a2a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workrite"></a><span data-ttu-id="63b7f-103">Tutorial: Integración de Azure Active Directory con Workrite</span><span class="sxs-lookup"><span data-stu-id="63b7f-103">Tutorial: Azure Active Directory integration with Workrite</span></span>

<span data-ttu-id="63b7f-104">En este tutorial, aprenderá a integrar Workrite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="63b7f-104">In this tutorial, you learn how to integrate Workrite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="63b7f-105">La integración de Workrite con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="63b7f-105">Integrating Workrite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="63b7f-106">Puede controlar en Azure AD quién tiene acceso a Workrite.</span><span class="sxs-lookup"><span data-stu-id="63b7f-106">You can control in Azure AD who has access to Workrite.</span></span>
- <span data-ttu-id="63b7f-107">Puede permitir que los usuarios inicien sesión automáticamente en Workrite (Inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63b7f-107">You can enable your users to automatically get signed-on to Workrite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="63b7f-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="63b7f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="63b7f-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="63b7f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63b7f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="63b7f-110">Prerequisites</span></span>

<span data-ttu-id="63b7f-111">Para configurar la integración de Azure AD con Workrite, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="63b7f-111">To configure Azure AD integration with Workrite, you need the following items:</span></span>

- <span data-ttu-id="63b7f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63b7f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="63b7f-113">Una suscripción habilitada para el inicio de sesión único en Workrite</span><span class="sxs-lookup"><span data-stu-id="63b7f-113">A Workrite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="63b7f-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="63b7f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="63b7f-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="63b7f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="63b7f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="63b7f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="63b7f-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63b7f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="63b7f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="63b7f-118">Scenario description</span></span>
<span data-ttu-id="63b7f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="63b7f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="63b7f-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="63b7f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="63b7f-121">Agregar Workrite desde la galería</span><span class="sxs-lookup"><span data-stu-id="63b7f-121">Adding Workrite from the gallery</span></span>
2. <span data-ttu-id="63b7f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63b7f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workrite-from-the-gallery"></a><span data-ttu-id="63b7f-123">Agregar Workrite desde la galería</span><span class="sxs-lookup"><span data-stu-id="63b7f-123">Adding Workrite from the gallery</span></span>
<span data-ttu-id="63b7f-124">Para configurar la integración de Workrite en Azure AD, deberá agregar Workrite desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="63b7f-124">To configure the integration of Workrite into Azure AD, you need to add Workrite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="63b7f-125">**Para agregar Workrite desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="63b7f-125">**To add Workrite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="63b7f-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="63b7f-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="63b7f-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="63b7f-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="63b7f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="63b7f-133">En el cuadro de búsqueda, escriba **Workrite**, seleccione **Workrite** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="63b7f-133">In the search box, type **Workrite**, select **Workrite** from result panel then click **Add** button to add the application.</span></span>

    ![Workrite en la lista de resultados](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="63b7f-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="63b7f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="63b7f-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Workrite con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="63b7f-136">In this section, you configure and test Azure AD single sign-on with Workrite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="63b7f-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Workrite para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63b7f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workrite is to a user in Azure AD.</span></span> <span data-ttu-id="63b7f-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Workrite.</span><span class="sxs-lookup"><span data-stu-id="63b7f-138">In other words, a link relationship between an Azure AD user and the related user in Workrite needs to be established.</span></span>

<span data-ttu-id="63b7f-139">En Workrite, para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-139">In Workrite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="63b7f-140">Para configurar y probar el inicio de sesión único de Azure AD con Workrite, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="63b7f-140">To configure and test Azure AD single sign-on with Workrite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="63b7f-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="63b7f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="63b7f-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63b7f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="63b7f-143">**[Creación de un usuario de prueba de Workrite](#create-a-workrite-test-user)**: para tener un homólogo de Britta Simon en Workrite que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63b7f-143">**[Create a Workrite test user](#create-a-workrite-test-user)** - to have a counterpart of Britta Simon in Workrite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="63b7f-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63b7f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="63b7f-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="63b7f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="63b7f-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63b7f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="63b7f-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Workrite.</span><span class="sxs-lookup"><span data-stu-id="63b7f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workrite application.</span></span>

<span data-ttu-id="63b7f-148">**Para configurar el inicio de sesión único de Azure AD con Workrite, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="63b7f-148">**To configure Azure AD single sign-on with Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="63b7f-149">En Azure Portal, en la página de integración de la aplicación **Workrite**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-149">In the Azure portal, on the **Workrite** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="63b7f-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="63b7f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_samlbase.png)

3. <span data-ttu-id="63b7f-153">En la sección **Dominio y direcciones URL de Workrite**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="63b7f-153">On the **Workrite Domain and URLs** section, perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_url.png)

    <span data-ttu-id="63b7f-155">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`.</span><span class="sxs-lookup"><span data-stu-id="63b7f-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="63b7f-156">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="63b7f-156">This value is not real.</span></span> <span data-ttu-id="63b7f-157">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="63b7f-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="63b7f-158">Póngase en contacto con el [equipo de soporte al cliente de Workrite](mailto:support@workrite.co.uk) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="63b7f-158">Contact [Workrite Client support team](mailto:support@workrite.co.uk) to get this value.</span></span>

4. <span data-ttu-id="63b7f-159">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="63b7f-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_certificate.png) 

5. <span data-ttu-id="63b7f-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="63b7f-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-workrite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="63b7f-163">En la sección **Configuración de Workrite**, haga clic en **Configurar Workrite** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-163">On the **Workrite Configuration** section, click **Configure Workrite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="63b7f-164">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_configure.png) 

7. <span data-ttu-id="63b7f-166">Para configurar el inicio de sesión único en **Workrite**, es preciso enviar los datos descargados de **Certificado (Base64), Sign-Out URL (Dirección URL de cierre de sesión), SAML Entity ID (Identificador de identidad de SAML) y SAML Single Sign-On Service (Dirección URL del servicio de inicio de sesión único de SAML)** al [equipo de soporte técnico de Workrite](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="63b7f-166">To configure single sign-on on **Workrite** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workrite support team](mailto:support@workrite.co.uk).</span></span>

> [!TIP]
> <span data-ttu-id="63b7f-167">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="63b7f-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="63b7f-168">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="63b7f-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="63b7f-169">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="63b7f-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="63b7f-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63b7f-170">Create an Azure AD test user</span></span>

<span data-ttu-id="63b7f-171">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="63b7f-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="63b7f-173">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="63b7f-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="63b7f-174">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-workrite-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="63b7f-176">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-workrite-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="63b7f-178">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-workrite-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="63b7f-180">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="63b7f-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-workrite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="63b7f-182">a.</span><span class="sxs-lookup"><span data-stu-id="63b7f-182">a.</span></span> <span data-ttu-id="63b7f-183">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="63b7f-184">b.</span><span class="sxs-lookup"><span data-stu-id="63b7f-184">b.</span></span> <span data-ttu-id="63b7f-185">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63b7f-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="63b7f-186">c.</span><span class="sxs-lookup"><span data-stu-id="63b7f-186">c.</span></span> <span data-ttu-id="63b7f-187">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="63b7f-188">d.</span><span class="sxs-lookup"><span data-stu-id="63b7f-188">d.</span></span> <span data-ttu-id="63b7f-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-189">Click **Create**.</span></span>
 
### <a name="create-a-workrite-test-user"></a><span data-ttu-id="63b7f-190">Creación de un usuario de prueba de Workrite</span><span class="sxs-lookup"><span data-stu-id="63b7f-190">Create a Workrite test user</span></span>

<span data-ttu-id="63b7f-191">El objetivo de esta sección es crear una usuaria de prueba llamada Britta Simon en Workrite.</span><span class="sxs-lookup"><span data-stu-id="63b7f-191">The objective of this section is to create a user called Britta Simon in Workrite.</span></span>

<span data-ttu-id="63b7f-192">**Para crear una usuaria llamada Britta Simon en Workrite, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="63b7f-192">**To create a user called Britta Simon in Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="63b7f-193">Inicie sesión en su sitio de la compañía de Workrite como administrador.</span><span class="sxs-lookup"><span data-stu-id="63b7f-193">Sign on to your workrite company site as administrator.</span></span>

2. <span data-ttu-id="63b7f-194">En el panel de navegación, haga clic en **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-194">In the navigation pane, click **Admin**.</span></span>
   
    ![Control de administración][400]

3. <span data-ttu-id="63b7f-196">Vaya a Vínculos rápidos y, a continuación, haga clic en **Crear un usuario**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-196">Go to Quick Links, and then click **Create a User**.</span></span>
   
    ![Sección Crear usuario][401]

4. <span data-ttu-id="63b7f-198">En el cuadro de diálogo **Crear usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="63b7f-198">On the **Create User** dialog, perform the following steps:</span></span>
   
    ![Cuadro de diálogo Crear usuario][402]
    
    <span data-ttu-id="63b7f-200">a.</span><span class="sxs-lookup"><span data-stu-id="63b7f-200">a.</span></span> <span data-ttu-id="63b7f-201">En el cuadro de texto **Correo electrónico**, escriba la dirección de correo electrónico de un usuario, por ejemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="63b7f-201">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="63b7f-202">b.</span><span class="sxs-lookup"><span data-stu-id="63b7f-202">b.</span></span> <span data-ttu-id="63b7f-203">En el cuadro de texto **Nombre**, escriba el nombre del usuario, en este caso, Britta.</span><span class="sxs-lookup"><span data-stu-id="63b7f-203">In the **First Name** textbox, type the firstname of user like Britta.</span></span>

    <span data-ttu-id="63b7f-204">c.</span><span class="sxs-lookup"><span data-stu-id="63b7f-204">c.</span></span> <span data-ttu-id="63b7f-205">En el cuadro de texto **Apellidos**, escriba los apellidos del usuario, en este caso, Simon.</span><span class="sxs-lookup"><span data-stu-id="63b7f-205">In the **Surname** textbox, type the surname of user like Simon.</span></span>
    
    <span data-ttu-id="63b7f-206">d.</span><span class="sxs-lookup"><span data-stu-id="63b7f-206">d.</span></span> <span data-ttu-id="63b7f-207">Seleccione **Administrador de cliente** como **Elegir rol**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-207">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="63b7f-208">e.</span><span class="sxs-lookup"><span data-stu-id="63b7f-208">e.</span></span> <span data-ttu-id="63b7f-209">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-209">Click **Save**.</span></span>   

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="63b7f-210">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63b7f-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="63b7f-211">En esta sección, concederá acceso a Brita Simon a Wokrite para permitirle que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="63b7f-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workrite.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="63b7f-213">**Para asignar a Britta Simon a Workrite, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="63b7f-213">**To assign Britta Simon to Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="63b7f-214">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="63b7f-216">En la lista de aplicaciones, seleccione **Workrite**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-216">In the applications list, select **Workrite**.</span></span>

    ![Vínculo a Workrite en la lista de aplicaciones](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_app.png)  

3. <span data-ttu-id="63b7f-218">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="63b7f-220">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-220">Click **Add** button.</span></span> <span data-ttu-id="63b7f-221">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="63b7f-223">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="63b7f-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="63b7f-224">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="63b7f-225">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="63b7f-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="63b7f-226">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="63b7f-226">Test single sign-on</span></span>

<span data-ttu-id="63b7f-227">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="63b7f-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="63b7f-228">Al hacer clic en el icono de Workrite en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Workrite.</span><span class="sxs-lookup"><span data-stu-id="63b7f-228">When you click the Workrite tile in the Access Panel, you should get automatically signed-on to your Workrite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="63b7f-229">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="63b7f-229">Additional resources</span></span>

* [<span data-ttu-id="63b7f-230">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63b7f-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="63b7f-231">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="63b7f-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_400.png
[401]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_401.png
[402]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_402.png


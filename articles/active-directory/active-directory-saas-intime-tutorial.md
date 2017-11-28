---
title: "Tutorial: integración de Azure Active Directory con InTime | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory e InTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d4e2c6e1-ae5d-4d2c-8ffc-1b24534d376a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jeedes
ms.openlocfilehash: 4bb22c92ad7f6963be6ca15073f7f01da99ba2bb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intime"></a><span data-ttu-id="81e4b-103">Tutorial: integración de Azure Active Directory con InTime</span><span class="sxs-lookup"><span data-stu-id="81e4b-103">Tutorial: Azure Active Directory integration with InTime</span></span>

<span data-ttu-id="81e4b-104">En este tutorial, obtendrá información sobre cómo integrar InTime con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="81e4b-104">In this tutorial, you learn how to integrate InTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81e4b-105">La integración de InTime con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="81e4b-105">Integrating InTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="81e4b-106">Puede controlar en Azure AD quién tiene acceso a InTime.</span><span class="sxs-lookup"><span data-stu-id="81e4b-106">You can control in Azure AD who has access to InTime.</span></span>
- <span data-ttu-id="81e4b-107">Puede permitir que los usuarios inicien sesión automáticamente en InTime (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81e4b-107">You can enable your users to automatically get signed-on to InTime (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="81e4b-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="81e4b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="81e4b-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81e4b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81e4b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="81e4b-110">Prerequisites</span></span>

<span data-ttu-id="81e4b-111">Para configurar la integración de Azure AD con InTime, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="81e4b-111">To configure Azure AD integration with InTime, you need the following items:</span></span>

- <span data-ttu-id="81e4b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81e4b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81e4b-113">Una suscripción habilitada para el inicio de sesión único en InTime</span><span class="sxs-lookup"><span data-stu-id="81e4b-113">A InTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81e4b-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="81e4b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81e4b-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="81e4b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81e4b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="81e4b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81e4b-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81e4b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81e4b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="81e4b-118">Scenario description</span></span>
<span data-ttu-id="81e4b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="81e4b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81e4b-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="81e4b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81e4b-121">Adición de InTime desde la galería</span><span class="sxs-lookup"><span data-stu-id="81e4b-121">Adding InTime from the gallery</span></span>
2. <span data-ttu-id="81e4b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81e4b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intime-from-the-gallery"></a><span data-ttu-id="81e4b-123">Adición de InTime desde la galería</span><span class="sxs-lookup"><span data-stu-id="81e4b-123">Adding InTime from the gallery</span></span>
<span data-ttu-id="81e4b-124">Para configurar la integración de InTime en Azure AD, será preciso agregar InTime desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="81e4b-124">To configure the integration of InTime into Azure AD, you need to add InTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="81e4b-125">**Para agregar InTime desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="81e4b-125">**To add InTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="81e4b-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="81e4b-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="81e4b-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="81e4b-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81e4b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="81e4b-133">En el cuadro de búsqueda, escriba **InTime**, seleccione **InTime** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="81e4b-133">In the search box, type **InTime**, select **InTime** from result panel then click **Add** button to add the application.</span></span>

    ![InTime en la lista de resultados](./media/active-directory-saas-intime-tutorial/tutorial_intime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="81e4b-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="81e4b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="81e4b-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con InTime con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="81e4b-136">In this section, you configure and test Azure AD single sign-on with InTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="81e4b-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de InTime para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81e4b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in InTime is to a user in Azure AD.</span></span> <span data-ttu-id="81e4b-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de InTime.</span><span class="sxs-lookup"><span data-stu-id="81e4b-138">In other words, a link relationship between an Azure AD user and the related user in InTime needs to be established.</span></span>

<span data-ttu-id="81e4b-139">Para establecer la relación de vínculo, en InTime, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-139">In InTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="81e4b-140">Para configurar y probar el inicio de sesión único de Azure AD con InTime, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="81e4b-140">To configure and test Azure AD single sign-on with InTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="81e4b-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="81e4b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="81e4b-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81e4b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81e4b-143">**[Creación de un usuario de prueba de InTime](#create-a-intime-test-user)** : para tener un homólogo de Britta Simon en InTime que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81e4b-143">**[Create a InTime test user](#create-a-intime-test-user)** - to have a counterpart of Britta Simon in InTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="81e4b-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81e4b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81e4b-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="81e4b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="81e4b-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81e4b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="81e4b-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en su aplicación InTime.</span><span class="sxs-lookup"><span data-stu-id="81e4b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your InTime application.</span></span>

<span data-ttu-id="81e4b-148">**Para configurar el inicio de sesión único de Azure AD con InTime, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="81e4b-148">**To configure Azure AD single sign-on with InTime, perform the following steps:**</span></span>

1. <span data-ttu-id="81e4b-149">En Azure Portal, en la página de integración de la aplicación **InTime**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-149">In the Azure portal, on the **InTime** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="81e4b-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="81e4b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-intime-tutorial/tutorial_intime_samlbase.png)

3. <span data-ttu-id="81e4b-153">En la sección **Dominio y direcciones URL de InTime**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="81e4b-153">On the **InTime Domain and URLs** section, perform the following steps:</span></span>

    ![Información sobre dominio y direcciones URL de inicio de sesión único de InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_url.png)

    <span data-ttu-id="81e4b-155">a.</span><span class="sxs-lookup"><span data-stu-id="81e4b-155">a.</span></span> <span data-ttu-id="81e4b-156">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span><span class="sxs-lookup"><span data-stu-id="81e4b-156">In the **Sign-on URL** textbox, type the URL: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span></span>

    <span data-ttu-id="81e4b-157">b.</span><span class="sxs-lookup"><span data-stu-id="81e4b-157">b.</span></span> <span data-ttu-id="81e4b-158">En el cuadro de texto **Identificador**, escriba la dirección URL: `https://auth.intimesoft.com/auth/realms/master`</span><span class="sxs-lookup"><span data-stu-id="81e4b-158">In the **Identifier** textbox, type the URL: `https://auth.intimesoft.com/auth/realms/master`</span></span>

4. <span data-ttu-id="81e4b-159">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="81e4b-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-intime-tutorial/tutorial_intime_certificate.png) 

5. <span data-ttu-id="81e4b-161">La aplicación InTime espera las aserciones de SAML en un formato específico, que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos del token SAML.</span><span class="sxs-lookup"><span data-stu-id="81e4b-161">Your InTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="81e4b-162">La siguiente captura de pantalla le muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="81e4b-162">The following screenshot shows an example for this.</span></span> <span data-ttu-id="81e4b-163">El valor predeterminado de **Identificador de usuario** es **user.userprincipalname**, pero InTime espera que este valor se asigne a la dirección de correo electrónico del usuario.</span><span class="sxs-lookup"><span data-stu-id="81e4b-163">The default value of **User Identifier** is **user.userprincipalname** but InTime expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="81e4b-164">Para ello, puede usar el atributo **user.mail** de la lista o usar el valor de atributo correspondiente en función de la configuración de su organización.</span><span class="sxs-lookup"><span data-stu-id="81e4b-164">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration</span></span> 

    ![Configuración del Atributo](./media/active-directory-saas-intime-tutorial/tutorial_intime_attribute.png)

6. <span data-ttu-id="81e4b-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="81e4b-166">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-intime-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="81e4b-168">En la sección **Configuración de InTime**, haga clic en **Configurar InTime** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-168">On the **InTime Configuration** section, click **Configure InTime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="81e4b-169">Copie los valores **Sign-Out URL y SAML Single Sign-On Service URL** (Dirección URL de cierre de sesión y Dirección URL del servicio de inicio de sesión único de SAML) de la **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_configure.png) 

8. <span data-ttu-id="81e4b-171">Para configurar el inicio de sesión único en **InTime**, es preciso enviar los valores descargados de **XML de metadatos**, **URL de cierre de sesión y URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de InTime](mailto:hdollard@intimesoft.com).</span><span class="sxs-lookup"><span data-stu-id="81e4b-171">To configure single sign-on on **InTime** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, and SAML Single Sign-On Service URL** to [InTime support team](mailto:hdollard@intimesoft.com).</span></span> <span data-ttu-id="81e4b-172">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="81e4b-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="81e4b-173">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="81e4b-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="81e4b-174">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="81e4b-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="81e4b-175">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="81e4b-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="81e4b-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81e4b-176">Create an Azure AD test user</span></span>

<span data-ttu-id="81e4b-177">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="81e4b-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="81e4b-179">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="81e4b-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="81e4b-180">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-180">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-intime-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="81e4b-182">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-182">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-intime-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="81e4b-184">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-184">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-intime-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="81e4b-186">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="81e4b-186">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-intime-tutorial/create_aaduser_04.png)

    <span data-ttu-id="81e4b-188">a.</span><span class="sxs-lookup"><span data-stu-id="81e4b-188">a.</span></span> <span data-ttu-id="81e4b-189">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-189">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81e4b-190">b.</span><span class="sxs-lookup"><span data-stu-id="81e4b-190">b.</span></span> <span data-ttu-id="81e4b-191">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81e4b-191">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="81e4b-192">c.</span><span class="sxs-lookup"><span data-stu-id="81e4b-192">c.</span></span> <span data-ttu-id="81e4b-193">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-193">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="81e4b-194">d.</span><span class="sxs-lookup"><span data-stu-id="81e4b-194">d.</span></span> <span data-ttu-id="81e4b-195">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-195">Click **Create**.</span></span>
 
### <a name="create-a-intime-test-user"></a><span data-ttu-id="81e4b-196">Creación de un usuario de prueba de InTime</span><span class="sxs-lookup"><span data-stu-id="81e4b-196">Create a InTime test user</span></span>

<span data-ttu-id="81e4b-197">En esta sección, creará un usuario llamado Britta Simon en InTime.</span><span class="sxs-lookup"><span data-stu-id="81e4b-197">In this section, you create a user called Britta Simon in InTime.</span></span> <span data-ttu-id="81e4b-198">Trabaje con el [equipo de soporte técnico de InTime](mailto:hdollard@intimesoft.com) para agregar los usuarios a la plataforma de InTime.</span><span class="sxs-lookup"><span data-stu-id="81e4b-198">Work with [InTime support team](mailto:hdollard@intimesoft.com) to add the users in the InTime platform.</span></span> <span data-ttu-id="81e4b-199">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="81e4b-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="81e4b-200">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81e4b-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="81e4b-201">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a InTime.</span><span class="sxs-lookup"><span data-stu-id="81e4b-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to InTime.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="81e4b-203">**Para asignar a Britta Simon a InTime, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="81e4b-203">**To assign Britta Simon to InTime, perform the following steps:**</span></span>

1. <span data-ttu-id="81e4b-204">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="81e4b-206">En la lista de aplicaciones, seleccione **InTime**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-206">In the applications list, select **InTime**.</span></span>

    ![Vínculo a InTime en la lista de aplicaciones](./media/active-directory-saas-intime-tutorial/tutorial_intime_app.png)  

3. <span data-ttu-id="81e4b-208">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="81e4b-210">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-210">Click **Add** button.</span></span> <span data-ttu-id="81e4b-211">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="81e4b-213">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="81e4b-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="81e4b-214">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81e4b-215">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="81e4b-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="81e4b-216">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="81e4b-216">Test single sign-on</span></span>

<span data-ttu-id="81e4b-217">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="81e4b-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="81e4b-218">Al hacer clic en el icono de InTime del Panel de acceso, debería entrar en la página de inicio de sesión de la aplicación InTime.</span><span class="sxs-lookup"><span data-stu-id="81e4b-218">When you click the InTime tile in the Access Panel, you should get the login page of your InTime application.</span></span> <span data-ttu-id="81e4b-219">Haga clic en el botón de **inicio de sesión**. Se mostrará una serie de proveedores de identidades en una lista de botones.</span><span class="sxs-lookup"><span data-stu-id="81e4b-219">Click the **Login** button, then a series of IdPs will be displayed on a list of buttons.</span></span> <span data-ttu-id="81e4b-220">Haga clic en **Nombre del IDP** proporcionado por el [equipo de soporte técnico de InTime](mailto:hdollard@intimesoft.com) para iniciar sesión en la aplicación InTime.</span><span class="sxs-lookup"><span data-stu-id="81e4b-220">click **IDP name** given by [InTime support team](mailto:hdollard@intimesoft.com) to login into your InTime application.</span></span> <span data-ttu-id="81e4b-221">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="81e4b-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="81e4b-222">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="81e4b-222">Additional resources</span></span>

* [<span data-ttu-id="81e4b-223">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81e4b-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81e4b-224">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="81e4b-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-intime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intime-tutorial/tutorial_general_203.png


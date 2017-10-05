---
title: "Tutorial: Integración de Azure Active Directory con vxMaintain | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y vxMaintain."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: ad87534af448356b8cc80d8ddd278bfb8a9165e7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="f255a-103">Tutorial: Integración de Azure Active Directory con vxMaintain</span><span class="sxs-lookup"><span data-stu-id="f255a-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="f255a-104">En este tutorial, obtendrá información sobre cómo integrar vxMaintain con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f255a-104">In this tutorial, you learn how to integrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f255a-105">Esta integración proporciona varias ventajas importantes.</span><span class="sxs-lookup"><span data-stu-id="f255a-105">This integration provides several important benefits.</span></span> <span data-ttu-id="f255a-106">Puede:</span><span class="sxs-lookup"><span data-stu-id="f255a-106">You can:</span></span>

- <span data-ttu-id="f255a-107">Controlar en Azure AD quién tiene acceso a vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="f255a-107">Control in Azure AD who has access to vxMaintain.</span></span>
- <span data-ttu-id="f255a-108">Permitir que los usuarios inicien sesión automáticamente en vxMaintain mediante inicio de sesión único (SSO) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f255a-108">Enable your users to automatically sign in to vxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="f255a-109">Administrar sus cuentas en una ubicación central, Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f255a-109">Manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="f255a-110">Para más información sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f255a-110">To learn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f255a-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f255a-111">Prerequisites</span></span>

<span data-ttu-id="f255a-112">Para configurar la integración de Azure AD con vxMaintain, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f255a-112">To configure Azure AD integration with vxMaintain, you need the following items:</span></span>

- <span data-ttu-id="f255a-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f255a-113">An Azure AD subscription</span></span>
- <span data-ttu-id="f255a-114">Una suscripción de inicio de sesión único de vxMaintain habilitada</span><span class="sxs-lookup"><span data-stu-id="f255a-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f255a-115">No se recomienda usar un entorno de producción para probar los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f255a-115">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="f255a-116">Para probar los pasos de este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f255a-116">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="f255a-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f255a-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f255a-118">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f255a-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f255a-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f255a-119">Scenario description</span></span>
<span data-ttu-id="f255a-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f255a-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="f255a-121">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="f255a-121">The scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="f255a-122">Agregar vxMaintain desde la galería</span><span class="sxs-lookup"><span data-stu-id="f255a-122">Adding vxMaintain from the gallery</span></span>
* <span data-ttu-id="f255a-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f255a-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-the-gallery"></a><span data-ttu-id="f255a-124">Adición de vxMaintain desde la galería</span><span class="sxs-lookup"><span data-stu-id="f255a-124">Add vxMaintain from the gallery</span></span>
<span data-ttu-id="f255a-125">Para configurar la integración de vxMaintain con Azure AD, deberá agregar vxMaintain desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="f255a-125">To configure the integration of vxMaintain with Azure AD, you need to add vxMaintain from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f255a-126">Para agregar vxMaintain desde la galería, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f255a-126">To add vxMaintain from the gallery, do the following:</span></span>

1. <span data-ttu-id="f255a-127">En el panel izquierdo de [Azure Portal](https://portal.azure.com), seleccione el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f255a-127">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** button.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="f255a-129">Seleccione **Aplicaciones empresariales** > **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f255a-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Panel "Aplicaciones empresariales"][2]
    
3. <span data-ttu-id="f255a-131">Para agregar una aplicación, en el cuadro de diálogo **Todas las aplicaciones**, seleccione **Nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="f255a-131">To add an application, in the **All applications** dialog box, select **New application**.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="f255a-133">En el cuadro de búsqueda, escriba **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="f255a-133">In the search box, type **vxMaintain**.</span></span>

    ![Lista desplegable de "Modo de inicio de sesión único"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="f255a-135">En la lista de resultados, seleccione **vxMaintain**y, a continuación, seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f255a-135">In the results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![El vínculo a vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f255a-137">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="f255a-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="f255a-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con vxMaintain con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f255a-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f255a-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo en vxMaintain para el usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f255a-139">For SSO to work, Azure AD needs to know the vxMaintain counterpart to the Azure AD user.</span></span> <span data-ttu-id="f255a-140">Es decir, debe establecer una relación de vínculo entre el usuario de Azure AD y el usuario correspondiente de vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="f255a-140">That is, you must establish a link relationship between the Azure AD user and the corresponding vxMaintain user.</span></span>

<span data-ttu-id="f255a-141">Para establecer la relación de vínculo, asigne el valor **nombre de usuario** de vxMaintain como valor de **nombre de usuario** de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f255a-141">To establish the link relationship, assign the vxMaintain **user name** value as the Azure AD **Username** value.</span></span>

<span data-ttu-id="f255a-142">Para configurar y probar el inicio de sesión único de Azure AD con vxMaintain, complete los siguientes bloques de creación.</span><span class="sxs-lookup"><span data-stu-id="f255a-142">To configure and test Azure AD SSO by using vxMaintain, complete the following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="f255a-143">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f255a-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="f255a-144">En esta sección, puede habilitar el inicio de sesión único de Azure AD en Azure Portal y configurar el inicio de sesión único en la aplicación vxMaintain de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="f255a-144">In this section, you can both enable Azure AD SSO in the Azure portal and configure SSO in your vxMaintain application by doing the following:</span></span>

1. <span data-ttu-id="f255a-145">En Azure Portal, en la página de integración de la aplicación **vxMaintain**, seleccione **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f255a-145">In the Azure portal, on the **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![Comando "Inicio de sesión único"][4]

2. <span data-ttu-id="f255a-147">Para habilitar el inicio de sesión único, en la lista desplegable **Modo de inicio de sesión único**, seleccione **Inicio de sesión basado en SAML**.</span><span class="sxs-lookup"><span data-stu-id="f255a-147">To enable SSO, in the **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![Comando "Inicio de sesión basado en SAML"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="f255a-149">En **Dominio y direcciones URL de vxMaintain**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f255a-149">Under **vxMaintain Domain and URLs**, do the following:</span></span>

    ![Sección Dominio y direcciones URL de vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="f255a-151">a.</span><span class="sxs-lookup"><span data-stu-id="f255a-151">a.</span></span> <span data-ttu-id="f255a-152">En el cuadro de texto **Identificador**, escriba una dirección URL que tenga la siguiente sintaxis: `https://<company name>.verisae.com`.</span><span class="sxs-lookup"><span data-stu-id="f255a-152">In the **Identifier** box, type a URL that has the following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="f255a-153">b.</span><span class="sxs-lookup"><span data-stu-id="f255a-153">b.</span></span> <span data-ttu-id="f255a-154">En el cuadro **URL de respuesta**, escriba una dirección URL que tenga la siguiente sintaxis: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="f255a-154">In the **Reply URL** box, type a URL that has the following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f255a-155">Los valores anteriores no son reales.</span><span class="sxs-lookup"><span data-stu-id="f255a-155">The preceding values are not real.</span></span> <span data-ttu-id="f255a-156">Actualícelos con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="f255a-156">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="f255a-157">Para obtener los valores, póngase en contacto con el [equipo de soporte técnico de vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="f255a-157">To obtain the values, contact the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="f255a-158">En la sección **Certificado de firma de SAML**, seleccione **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f255a-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file to your computer.</span></span>

    ![Sección "Certificado de firma SAML"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="f255a-160">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f255a-160">Select **Save**.</span></span>

    ![Botón Guardar](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f255a-162">Para configurar el inicio de sesión único de **vxMaintain**, envíe el archivo **XML de metadatos** al [equipo de soporte técnico de vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="f255a-162">To configure **vxMaintain** SSO, send the downloaded **Metadata XML** file to the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="f255a-163">Cuando configure la aplicación, puede leer una versión concisa de las instrucciones anteriores en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f255a-163">As you set up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f255a-164">Después de agregar la aplicación desde la sección **Active Directory** > **Aplicaciones empresariales**, seleccione la pestaña **Inicio de sesión único** y, a continuación, acceda a la documentación incrustada en la sección **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="f255a-164">After you add the app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation from the **Configuration** section.</span></span> 
>
><span data-ttu-id="f255a-165">Para más información sobre la característica de documentación incrustada, consulte [Administración de inicio de sesión único para aplicaciones empresariales](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="f255a-165">To learn more about the embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f255a-166">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f255a-166">Create an Azure AD test user</span></span>
<span data-ttu-id="f255a-167">En esta sección, creará el usuario de prueba Britta Simon en Azure Portal siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f255a-167">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Usuario de prueba de Azure AD][100]

1. <span data-ttu-id="f255a-169">En el panel izquierdo de **Azure Portal**, seleccione el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f255a-169">In the **Azure portal**, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![Botón "Azure Active Directory"](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f255a-171">Para mostrar una lista de usuarios, vaya a **Usuarios y grupos** > **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f255a-171">To display a list of users, go to **Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="f255a-172">![Vínculo "Todos los usuarios"](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="f255a-172">![The "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="f255a-173">Se abre el cuadro de diálogo **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f255a-173">The **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="f255a-174">Para abrir el cuadro de diálogo **Usuario**, seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f255a-174">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Botón Agregar](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f255a-176">En el cuadro de diálogo **Usuario**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f255a-176">In the **User** dialog box, do the following:</span></span>
 
    ![Cuadro de diálogo Usuario](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f255a-178">a.</span><span class="sxs-lookup"><span data-stu-id="f255a-178">a.</span></span> <span data-ttu-id="f255a-179">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f255a-179">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f255a-180">b.</span><span class="sxs-lookup"><span data-stu-id="f255a-180">b.</span></span> <span data-ttu-id="f255a-181">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario de prueba Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f255a-181">In the **User name** box, type the email address of test user Britta Simon.</span></span>

    <span data-ttu-id="f255a-182">c.</span><span class="sxs-lookup"><span data-stu-id="f255a-182">c.</span></span> <span data-ttu-id="f255a-183">Seleccione la casilla **Mostrar contraseña** y, después , anote el valor que se generó en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f255a-183">Select the **Show Password** check box, and then note the value that was generated in the **Password** box.</span></span>

    <span data-ttu-id="f255a-184">d.</span><span class="sxs-lookup"><span data-stu-id="f255a-184">d.</span></span> <span data-ttu-id="f255a-185">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f255a-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="f255a-186">Creación de un usuario de prueba de vxMaintain</span><span class="sxs-lookup"><span data-stu-id="f255a-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="f255a-187">En esta sección, creará una usuaria de prueba llamada Britta Simon en vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="f255a-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="f255a-188">Trabaje con el [equipo de soporte técnico de vxMaintain](http://www.verisae.com/contact-us) para agregar usuarios a la plataforma de vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="f255a-188">To add users in the vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="f255a-189">Antes de usar el inicio de sesión único, cree y active los usuarios.</span><span class="sxs-lookup"><span data-stu-id="f255a-189">Before you use SSO, create and activate the users.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f255a-190">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f255a-190">Assign the Azure AD test user</span></span>

<span data-ttu-id="f255a-191">En esta sección, permitirá que la usuaria de prueba Britta Simon use el inicio de sesión único (SSO) de Azure, para lo cual le concederá acceso a vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="f255a-191">In this section, you enable test user Britta Simon to use Azure SSO by granting access to vxMaintain.</span></span> <span data-ttu-id="f255a-192">Para ello, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f255a-192">To do so, do the following:</span></span>

![Usuario de prueba en la lista Nombre para mostrar][200] 

1. <span data-ttu-id="f255a-194">En la vista **Aplicaciones** de Azure Portal, vaya a la vista **Directorio** > **Aplicaciones empresariales** > **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f255a-194">In the Azure portal **Applications** view, go to **Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![Vínculo "Todas las aplicaciones"][201] 

2. <span data-ttu-id="f255a-196">En la lista **Aplicaciones**, seleccione **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="f255a-196">In the **Applications** list, select **vxMaintain**.</span></span>

    ![El vínculo a vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="f255a-198">En el panel izquierdo, seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f255a-198">In the left pane, select **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202] 

4. <span data-ttu-id="f255a-200">Seleccione **Agregar** y, después, en el panel **Agregar asignación**, seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f255a-200">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][203]

5. <span data-ttu-id="f255a-202">En el cuadro de diálogo **Usuarios y grupos**, en la lista **Usuarios** seleccione **Britta Simon** y, después, el botón **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="f255a-202">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**, and then select the **Select** button.</span></span>

7. <span data-ttu-id="f255a-203">En el cuadro de diálogo **Agregar asignación**, seleccione **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="f255a-203">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="f255a-204">Prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f255a-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="f255a-205">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f255a-205">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="f255a-206">Al seleccionar el icono de **vxMaintain** en el panel de acceso, debería iniciar sesión automáticamente en su aplicación vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="f255a-206">Selecting the **vxMaintain** tile in the Access Panel should sign you in to your vxMaintain application automatically.</span></span>

<span data-ttu-id="f255a-207">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f255a-207">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f255a-208">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f255a-208">Next steps</span></span>

* [<span data-ttu-id="f255a-209">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f255a-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f255a-210">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f255a-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png


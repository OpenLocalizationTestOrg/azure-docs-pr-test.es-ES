---
title: "Tutorial: Integración de Azure Active Directory con Help Scout | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Help Scout."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 84cee39c28a0f7e6b9878441e504131795673020
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="71ba6-103">Tutorial: integración de Azure Active Directory con Help Scout</span><span class="sxs-lookup"><span data-stu-id="71ba6-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="71ba6-104">En este tutorial, obtendrá información sobre cómo integrar Help Scout con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="71ba6-104">In this tutorial, you learn how to integrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="71ba6-105">La integración de Help Scout con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="71ba6-105">You get the following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="71ba6-106">En Azure AD puede controlar quién tiene acceso a Help Scout.</span><span class="sxs-lookup"><span data-stu-id="71ba6-106">In Azure AD, you can control who has access to Help Scout.</span></span>
- <span data-ttu-id="71ba6-107">Puede iniciar sesión automáticamente con los usuarios de Help Scout mediante un inicio de sesión único y una cuenta de Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="71ba6-107">You can automatically sign in your users to Help Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="71ba6-108">Puede administrar sus cuentas en una única ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="71ba6-108">You can manage your accounts in one, central location, the Azure portal.</span></span>

<span data-ttu-id="71ba6-109">Para más información sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="71ba6-109">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71ba6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="71ba6-110">Prerequisites</span></span>

<span data-ttu-id="71ba6-111">Para configurar la integración de Azure AD con Help Scout, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="71ba6-111">To set up Azure AD integration with Help Scout, you need the following items:</span></span>

- <span data-ttu-id="71ba6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="71ba6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="71ba6-113">Una suscripción de Help Scout, con inicio de sesión único activado</span><span class="sxs-lookup"><span data-stu-id="71ba6-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="71ba6-114">Si va a probar los pasos de este tutorial, no se recomienda hacerlo en un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="71ba6-114">If you test the steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="71ba6-115">Recomendaciones para probar los pasos de este tutorial:</span><span class="sxs-lookup"><span data-stu-id="71ba6-115">Recommendations for testing the steps in this tutorial:</span></span>

- <span data-ttu-id="71ba6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="71ba6-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="71ba6-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba gratuita durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="71ba6-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="71ba6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="71ba6-118">Scenario description</span></span>
<span data-ttu-id="71ba6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="71ba6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="71ba6-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="71ba6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="71ba6-121">Incorporación de Help Scout desde la galería.</span><span class="sxs-lookup"><span data-stu-id="71ba6-121">Add Help Scout from the gallery.</span></span>
2. <span data-ttu-id="71ba6-122">Configuración y prueba del inicio de sesión único en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71ba6-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-the-gallery"></a><span data-ttu-id="71ba6-123">Incorporación de Help Scout desde la galería</span><span class="sxs-lookup"><span data-stu-id="71ba6-123">Add Help Scout from the gallery</span></span>
<span data-ttu-id="71ba6-124">Para configurar la integración de Help Scout con Azure AD, en la galería, agréguelo a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="71ba6-124">To set up the integration of Help Scout with Azure AD, in the gallery, add Help Scout to your list of managed SaaS apps.</span></span>

<span data-ttu-id="71ba6-125">Para agregar Help Scout desde la galería:</span><span class="sxs-lookup"><span data-stu-id="71ba6-125">To add Help Scout from the gallery:</span></span>

1. <span data-ttu-id="71ba6-126">En el menú izquierdo de [Azure Portal](https://portal.azure.com), seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-126">In the [Azure portal](https://portal.azure.com), in the left menu, select **Azure Active Directory**.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="71ba6-128">Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Página Aplicaciones empresariales][2]
    
3. <span data-ttu-id="71ba6-130">Para agregar una nueva aplicación, seleccione **Nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-130">To add a new application, select **New application**.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="71ba6-132">En el cuadro de búsqueda, escriba **Help Scout**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-132">In the search box, enter **Help Scout**.</span></span> <span data-ttu-id="71ba6-133">En los resultados de búsqueda, seleccione **Help Scout** y, luego, **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-133">In the search results, select **Help Scout**, and then select **Add**.</span></span>

    ![Help Scout en la lista de resultados](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="71ba6-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="71ba6-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="71ba6-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Help Scout mediante un usuario de prueba llamado *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="71ba6-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="71ba6-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Azure AD en Help Scout.</span><span class="sxs-lookup"><span data-stu-id="71ba6-137">For single sign-on to work, Azure AD needs to know the Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="71ba6-138">Es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Help Scout.</span><span class="sxs-lookup"><span data-stu-id="71ba6-138">A link relationship between an Azure AD user and the related user in Help Scout must be established.</span></span>

<span data-ttu-id="71ba6-139">Para establecer la relación de vínculo, en Help Scout, asigne el valor de **nombre de usuario** como valor de **nombre de usuario** de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71ba6-139">To establish the link relationship, in Help Scout, for **Username**, assign the value of the **user name** in Azure AD.</span></span>

<span data-ttu-id="71ba6-140">Para configurar y probar el inicio de sesión único de Azure AD con Help Scout, es preciso completar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="71ba6-140">To configure and test Azure AD single sign-on with Help Scout, complete the following tasks:</span></span>

1. <span data-ttu-id="71ba6-141">[Configuración del inicio de sesión único de Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="71ba6-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="71ba6-142">Configura un usuario para usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="71ba6-142">Sets up a user to use this feature.</span></span>
2. <span data-ttu-id="71ba6-143">[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="71ba6-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="71ba6-144">Prueba un inicio de sesión único de Azure AD con el usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="71ba6-144">Tests Azure AD single sign-on with the user Britta Simon.</span></span>
3. <span data-ttu-id="71ba6-145">[Creación de un usuario de prueba de Help Scout](#create-a-help-scout-test-user).</span><span class="sxs-lookup"><span data-stu-id="71ba6-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="71ba6-146">Crea un homólogo de Britta Simon en Help Scout que está vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71ba6-146">Creates a counterpart of Britta Simon in Help Scout that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="71ba6-147">[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="71ba6-147">[Assign the Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="71ba6-148">Configura Britta Simon para usar un inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71ba6-148">Sets up Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="71ba6-149">[Prueba de inicio de sesión único](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="71ba6-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="71ba6-150">Comprueba que la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="71ba6-150">Verifies that the configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="71ba6-151">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="71ba6-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="71ba6-152">En esta sección, configura el inicio de sesión único de Azure AD en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="71ba6-152">In this section, you set up Azure AD single sign-on in the Azure portal.</span></span> <span data-ttu-id="71ba6-153">A continuación, configura el inicio de sesión único en la aplicación Help Scout.</span><span class="sxs-lookup"><span data-stu-id="71ba6-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="71ba6-154">Para configurar el inicio de sesión único en Azure AD con Help Scout:</span><span class="sxs-lookup"><span data-stu-id="71ba6-154">To set up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="71ba6-155">En Azure Portal, en la página de integración de la aplicación **Help Scout**, seleccione **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-155">In the Azure portal, on the **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![Configuración de vínculo de inicio de sesión único][4]

2. <span data-ttu-id="71ba6-157">En la página **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-157">On the **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="71ba6-159">En **Dominio y direcciones URL de Help Scout**, si quiere configurar la aplicación en el modo iniciado por IDP, complete los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="71ba6-159">Under **Help Scout Domain and URLs**, if you want to set up the application in IDP-initiated mode, complete the following steps:</span></span>

    1. <span data-ttu-id="71ba6-160">En el cuadro **Identificador**, escriba una dirección URL con el siguiente formato: `urn:auth0:helpscout:<instancename>`</span><span class="sxs-lookup"><span data-stu-id="71ba6-160">In the **Identifier** box, enter a URL that has the following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="71ba6-161">En el cuadro **URL de respuesta**, escriba una dirección URL con el siguiente formato: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span><span class="sxs-lookup"><span data-stu-id="71ba6-161">In the **Reply URL** box, enter a URL that has the following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="71ba6-163">Si desea configurar la aplicación con el modo SP iniciado, seleccione la casilla **Mostrar configuración avanzada de URL** y haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="71ba6-163">If you want to set up the application in SP-initiated mode, select the **Show advanced URL settings** check box, and then do the following:</span></span>

    * <span data-ttu-id="71ba6-164">En el cuadro **URL de inicio de sesión**, escriba una dirección URL con el siguiente formato: `https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="71ba6-164">In the **Sign on URL** box, enter a URL that has the following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="71ba6-166">Los valores de estas direcciones URL se muestran solo con fines demostrativos.</span><span class="sxs-lookup"><span data-stu-id="71ba6-166">The values in these URLs are for demonstration only.</span></span> <span data-ttu-id="71ba6-167">Actualice los valores con las direcciones URL reales de identificador y de respuesta.</span><span class="sxs-lookup"><span data-stu-id="71ba6-167">Update the values with the actual identifier URL and reply URL.</span></span> <span data-ttu-id="71ba6-168">Para obtener estos valores, póngase en contacto con el [equipo de soporte técnico de Help Scout](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="71ba6-168">To get these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="71ba6-169">En la sección **Certificado de firma de SAML**, seleccione **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="71ba6-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="71ba6-171">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-171">Select **Save**.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="71ba6-173">Para configurar un inicio de sesión único en Help Scout, envíe el archivo XML de metadatos descargado al [equipo de soporte técnico de Help Scout](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="71ba6-173">To set up single sign-on on the Help Scout side, send the downloaded metadata XML file to the [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="71ba6-174">El equipo de soporte técnico de Help Scout aplica esta configuración para que la conexión de inicio de sesión único de SAML esté correctamente configurada en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="71ba6-174">The Help Scout support team applies this setting so that the SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="71ba6-175">Puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="71ba6-175">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="71ba6-176">Después de agregar la aplicación seleccionando **Active Directory** > **Aplicaciones empresariales**, elija la pestaña **Inicio de sesión único**. Puede acceder a la documentación insertada en la sección **Configuración** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="71ba6-176">After you add the app by selecting **Active Directory** > **Enterprise Applications**, select the **Single Sign-On** tab. You can access the embedded documentation in the **Configuration** section, at the bottom of the page.</span></span> <span data-ttu-id="71ba6-177">Para más información, consulte la [documentación insertada de Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="71ba6-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="71ba6-178">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="71ba6-178">Create an Azure AD test user</span></span>

<span data-ttu-id="71ba6-179">En esta sección, en Azure Portal, creará un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="71ba6-179">In this section, in the Azure portal, you create a test user named Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="71ba6-181">Para crear un usuario de prueba en Azure AD:</span><span class="sxs-lookup"><span data-stu-id="71ba6-181">To create a test user in Azure AD:</span></span>

1. <span data-ttu-id="71ba6-182">En el menú izquierdo de Azure Portal, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-182">In the Azure portal, in the left menu, select **Azure Active Directory**.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="71ba6-184">Para mostrar la lista de usuarios, seleccione **Usuarios y grupos** y, luego, **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-184">To display the list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![Seleccionar Usuarios y grupos y, luego, Todos los usuarios](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="71ba6-186">Para abrir el cuadro de diálogo **Usuario**, en la parte superior de la página **Todos los usuarios**, seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-186">To open the **User** dialog box, at the top of the **All Users** page, select **Add**.</span></span>

    ![Botón Agregar](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="71ba6-188">En el cuadro de diálogo **Usuario**, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="71ba6-188">In the **User** dialog box, complete the following steps:</span></span>

    1. <span data-ttu-id="71ba6-189">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-189">In the **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="71ba6-190">En el cuadro **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="71ba6-190">In the **User name** box, enter the email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="71ba6-191">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    4. <span data-ttu-id="71ba6-192">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-192">Select **Create**.</span></span>

        ![Cuadro de diálogo Usuario](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="71ba6-194">Creación de un usuario de prueba de Help Scout</span><span class="sxs-lookup"><span data-stu-id="71ba6-194">Create a Help Scout test user</span></span>

<span data-ttu-id="71ba6-195">El objeto de esta sección es crear un usuario llamado Britta Simon en Help Scout.</span><span class="sxs-lookup"><span data-stu-id="71ba6-195">The object of this section is to create a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="71ba6-196">Help Scout admite el aprovisionamiento Just-In-Time (JIT), que está activado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="71ba6-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="71ba6-197">En esta sección, no hay ninguna acción o tarea que completar.</span><span class="sxs-lookup"><span data-stu-id="71ba6-197">In this section, there's no action or task to complete.</span></span> <span data-ttu-id="71ba6-198">Si el usuario no existe en Help Scout, se crea uno nuevo cuando se intenta acceder a Help Scout.</span><span class="sxs-lookup"><span data-stu-id="71ba6-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt to access Help Scout.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="71ba6-199">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="71ba6-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="71ba6-200">En esta sección, habilitará al usuario Britta Simon para que use el inicio de sesión único de Azure AD concediéndole acceso de cuenta de usuario a Help Scout.</span><span class="sxs-lookup"><span data-stu-id="71ba6-200">In this section, you allow the user Britta Simon to use Azure AD single sign-on by granting the user account access to Help Scout.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="71ba6-202">Para asignar a Britta Simon a Help Scout:</span><span class="sxs-lookup"><span data-stu-id="71ba6-202">To assign Britta Simon to Help Scout:</span></span>

1. <span data-ttu-id="71ba6-203">En Azure Portal, abra la vista de aplicaciones y vaya a la vista de directorio.</span><span class="sxs-lookup"><span data-stu-id="71ba6-203">In the Azure portal, open the applications view, and then go to the directory view.</span></span> <span data-ttu-id="71ba6-204">Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="71ba6-206">En la lista de aplicaciones, seleccione **Help Scout**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-206">In the applications list, select **Help Scout**.</span></span>

    ![Vínculo a Help Scout en la lista de aplicaciones](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="71ba6-208">En el menú de la izquierda, seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-208">In the left menu, select **Users and groups**.</span></span>

    ![Vínculo Usuarios y grupos][202]

4. <span data-ttu-id="71ba6-210">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-210">Select **Add**.</span></span> <span data-ttu-id="71ba6-211">Después, en la página **Agregar asignación**, seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-211">Then, on the **Add Assignment** page, select **Users and groups**.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="71ba6-213">En la página **Usuarios y grupos**, en la lista de usuarios, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-213">On the **Users and groups** page, in the list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="71ba6-214">En la página **Usuarios y grupos**, seleccione **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-214">On the **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="71ba6-215">En la página **Agregar asignación**, seleccione **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="71ba6-215">On the **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="71ba6-216">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="71ba6-216">Test single sign-on</span></span>

<span data-ttu-id="71ba6-217">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="71ba6-217">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="71ba6-218">Al seleccionar el icono de Help Scout en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Help Scout.</span><span class="sxs-lookup"><span data-stu-id="71ba6-218">When you select the Help Scout tile in the access panel, you should be automatically signed in to your Help Scout application.</span></span>

<span data-ttu-id="71ba6-219">Para más información sobre el panel de acceso, consulte [Introducción al panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="71ba6-219">For more information about the access panel, see [Introduction to the access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="71ba6-220">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="71ba6-220">Additional resources</span></span>

* [<span data-ttu-id="71ba6-221">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71ba6-221">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="71ba6-222">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="71ba6-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png


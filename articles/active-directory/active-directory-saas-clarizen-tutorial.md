---
title: "Tutorial: integración de Azure Active Directory con Clarizen | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Clarizen."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 574c6877bddac8be7d6d541bfabbdc10f6be3101
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="29df0-103">Tutorial: integración de Azure Active Directory con Clarizen</span><span class="sxs-lookup"><span data-stu-id="29df0-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="29df0-104">En este tutorial, aprenderá a integrar Azure Active Directory (Azure AD) con Clarizen.</span><span class="sxs-lookup"><span data-stu-id="29df0-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="29df0-105">Esta integración ofrece las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="29df0-105">This integration gives you the following benefits:</span></span>

- <span data-ttu-id="29df0-106">Puede controlar en Azure AD quién tiene acceso a Clarizen.</span><span class="sxs-lookup"><span data-stu-id="29df0-106">You can control, in Azure AD, who has access to Clarizen.</span></span>
- <span data-ttu-id="29df0-107">Puede permitir que los usuarios inicien sesión automáticamente en Clarizen (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29df0-107">You can enable your users to be automatically signed in to Clarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="29df0-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="29df0-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="29df0-109">El escenario de este tutorial consta de dos tareas principales:</span><span class="sxs-lookup"><span data-stu-id="29df0-109">The scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="29df0-110">Incorporación de Clarizen desde la galería.</span><span class="sxs-lookup"><span data-stu-id="29df0-110">Add Clarizen from the gallery.</span></span>
2. <span data-ttu-id="29df0-111">Configuración y prueba del inicio de sesión único en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29df0-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="29df0-112">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29df0-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29df0-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="29df0-113">Prerequisites</span></span>
<span data-ttu-id="29df0-114">Para configurar la integración de Azure AD con Clarizen, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="29df0-114">To configure Azure AD integration with Clarizen, you need the following items:</span></span>

- <span data-ttu-id="29df0-115">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="29df0-115">An Azure AD subscription</span></span>
- <span data-ttu-id="29df0-116">Una suscripción de Clarizen con inicio de sesión único habilitado</span><span class="sxs-lookup"><span data-stu-id="29df0-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="29df0-117">Para probar los pasos de este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="29df0-117">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="29df0-118">Pruebe el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="29df0-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29df0-119">No use su entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="29df0-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="29df0-120">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29df0-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-the-gallery"></a><span data-ttu-id="29df0-121">Incorporación de Clarizen desde la galería</span><span class="sxs-lookup"><span data-stu-id="29df0-121">Add Clarizen from the gallery</span></span>
<span data-ttu-id="29df0-122">Para configurar la integración de Clarizen en Azure AD, debe agregar Clarizen desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="29df0-122">To configure the integration of Clarizen into Azure AD, add Clarizen from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="29df0-123">En el panel izquierdo de [Azure Portal](https://portal.azure.com), haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29df0-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Icono de Azure Active Directory][1]

2. <span data-ttu-id="29df0-125">Haga clic en **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="29df0-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="29df0-126">A continuación, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="29df0-126">Then click **All applications**.</span></span>

    ![Clic en "Aplicaciones empresariales" y "Todas las aplicaciones"][2]

3. <span data-ttu-id="29df0-128">Haga clic en el botón **Agregar** situado en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="29df0-128">Click the **Add** button at the top of the dialog box.</span></span>

    ![Botón "Agregar"][3]

4. <span data-ttu-id="29df0-130">En el cuadro de búsqueda, escriba **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="29df0-130">In the search box, type **Clarizen**.</span></span>

    ![Escribir "Clarizen" en el cuadro de búsqueda](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="29df0-132">En el panel de resultados, seleccione **Clarizen** y luego haga clic en **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="29df0-132">In the results pane, select **Clarizen**, and then click **Add** to add the application.</span></span>

    ![Selección de Clarizen en el panel de resultados](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="29df0-134">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="29df0-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="29df0-135">En las secciones siguientes, va a configurar y probar el inicio de sesión único de Azure AD con Clarizen con el usuario de prueba Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29df0-135">In the following sections, you configure and test Azure AD single sign-on with Clarizen based on the test user Britta Simon.</span></span>

<span data-ttu-id="29df0-136">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Clarizen para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29df0-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Clarizen is to a user in Azure AD.</span></span> <span data-ttu-id="29df0-137">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Clarizen.</span><span class="sxs-lookup"><span data-stu-id="29df0-137">In other words, a link relationship between an Azure AD user and the related user in Clarizen needs to be established.</span></span> <span data-ttu-id="29df0-138">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Clarizen.</span><span class="sxs-lookup"><span data-stu-id="29df0-138">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Clarizen.</span></span>

<span data-ttu-id="29df0-139">Para configurar y probar el inicio de sesión único de Azure AD con Clarizen, complete los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="29df0-139">To configure and test Azure AD single sign-on with Clarizen, complete the following building blocks:</span></span>

1. <span data-ttu-id="29df0-140">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**, para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="29df0-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** to enable your users to use this feature.</span></span>
2. <span data-ttu-id="29df0-141">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**, para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29df0-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29df0-142">**[Creación de un usuario de prueba de Clarizen](#create-a-clarizen-test-user)**, para tener un homólogo de Britta Simon en Clarizen que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29df0-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** to have a counterpart of Britta Simon in Clarizen that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="29df0-143">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**, para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29df0-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29df0-144">**[Prueba del inicio de sesión único](#test-single-sign-on)**, para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="29df0-144">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="29df0-145">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="29df0-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="29df0-146">Habilite el inicio de sesión único de Azure AD en Azure Portal y configure el inicio de sesión único en la aplicación Clarizen.</span><span class="sxs-lookup"><span data-stu-id="29df0-146">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="29df0-147">En Azure Portal, en la página de integración de la aplicación **Clarizen**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="29df0-147">In the Azure portal, on the **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Clic en "Inicio de sesión único"][4]

2. <span data-ttu-id="29df0-149">En el cuadro de diálogo **Inicio de sesión único**, en **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="29df0-149">In the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Selección de "Inicio de sesión basado en SAML"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="29df0-151">En la sección **Dominio y direcciones URL de Clarizen**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="29df0-151">In the **Clarizen Domain and URLs** section, perform the following steps:</span></span>

    ![Cuadros de identificador y dirección URL de respuesta](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="29df0-153">a.</span><span class="sxs-lookup"><span data-stu-id="29df0-153">a.</span></span> <span data-ttu-id="29df0-154">En el cuadro **Identificador**, escriba el valor: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="29df0-154">In the **Identifier** box, type the value as: **Clarizen**</span></span>

    <span data-ttu-id="29df0-155">b.</span><span class="sxs-lookup"><span data-stu-id="29df0-155">b.</span></span> <span data-ttu-id="29df0-156">En el cuadro **URL de respuesta**, escriba la dirección URL según este patrón: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="29df0-156">In the **Reply URL** box, type a URL by using the following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="29df0-157">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="29df0-157">These are not the real values.</span></span> <span data-ttu-id="29df0-158">Tiene que usar el identificador y la dirección URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="29df0-158">You have to use the actual identifier and reply URL.</span></span> <span data-ttu-id="29df0-159">Aquí se recomienda que utilice el valor de cadena único en el identificador.</span><span class="sxs-lookup"><span data-stu-id="29df0-159">Here we suggest that you use the unique value of a string as the identifier.</span></span> <span data-ttu-id="29df0-160">Para obtener los valores reales, póngase en contacto con el [equipo de soporte técnico de Clarizen](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="29df0-160">To get the actual values, contact the [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="29df0-161">En la sección **Certificado de firma de SAML**, haga clic en **Crear nuevo certificado**.</span><span class="sxs-lookup"><span data-stu-id="29df0-161">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Clic en "Crear un nuevo certificado"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="29df0-163">En el cuadro de diálogo **Crear nuevo certificado**, haga clic en el icono del calendario y seleccione una fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="29df0-163">In the **Create New Certificate** dialog box, click the calendar icon and select an expiry date.</span></span> <span data-ttu-id="29df0-164">A continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="29df0-164">Then click **Save**.</span></span>

    ![Seleccionar y guardar una fecha de expiración](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="29df0-166">En la sección **Certificado de firma de SAML**, seleccione **Activar el certificado nuevo** y haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="29df0-166">In the **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Selección de la casilla para activar el nuevo certificado](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="29df0-168">En el cuadro de diálogo **Certificado de sustitución**, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="29df0-168">In the **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Clic en "Aceptar" para confirmar que desea activar el certificado](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="29df0-170">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="29df0-170">In the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Clic en "Certificado (Base64)" para iniciar la descarga](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="29df0-172">En la sección **Configuración de Clarizen**, haga clic en **Configurar Clarizen** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="29df0-172">In the **Clarizen Configuration** section, click **Configure Clarizen** to open the **Configure sign-on** window.</span></span>

    ![Clic en "Configurar Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Ventana "Configurar inicio de sesión", incluidos los archivos y las direcciones URL](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="29df0-175">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Clarizen como administrador.</span><span class="sxs-lookup"><span data-stu-id="29df0-175">In a different web browser window, sign in to your Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="29df0-176">Haga clic en el nombre de usuario y luego haga clic en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="29df0-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="29df0-177">![Clic en "Settings" (Configuración) debajo del nombre de usuario](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="29df0-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="29df0-178">Haga clic en la pestaña **Global Settings** (Configuración global).</span><span class="sxs-lookup"><span data-stu-id="29df0-178">Click the **Global Settings** tab.</span></span> <span data-ttu-id="29df0-179">A continuación, junto a **Federated Authentication** (Autenticación federada), haga clic en **edit** (Editar).</span><span class="sxs-lookup"><span data-stu-id="29df0-179">Then, next to **Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="29df0-180">![Pestaña "Global Settings"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span><span class="sxs-lookup"><span data-stu-id="29df0-180">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="29df0-181">En el cuadro de diálogo **Federated Authentication** (Autenticación federada), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="29df0-181">In the **Federated Authentication** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="29df0-182">![Cuadro de diálogo "Federated Authentication"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span><span class="sxs-lookup"><span data-stu-id="29df0-182">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="29df0-183">a.</span><span class="sxs-lookup"><span data-stu-id="29df0-183">a.</span></span> <span data-ttu-id="29df0-184">Seleccione **Habilitar autenticación federada**.</span><span class="sxs-lookup"><span data-stu-id="29df0-184">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="29df0-185">b.</span><span class="sxs-lookup"><span data-stu-id="29df0-185">b.</span></span> <span data-ttu-id="29df0-186">Para cargar el certificado descargado, haga clic en **Cargar** .</span><span class="sxs-lookup"><span data-stu-id="29df0-186">Click **Upload** to upload your downloaded certificate.</span></span>

    <span data-ttu-id="29df0-187">c.</span><span class="sxs-lookup"><span data-stu-id="29df0-187">c.</span></span> <span data-ttu-id="29df0-188">En el cuadro **URL de inicio de sesión**, coloque el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) en la ventana de configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29df0-188">In the **Sign-in URL** box, enter the value of **SAML Single Sign-On Service URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="29df0-189">d.</span><span class="sxs-lookup"><span data-stu-id="29df0-189">d.</span></span> <span data-ttu-id="29df0-190">En el cuadro **Sign-out URL** (URL de cierre de sesión), coloque el valor de **Sign-out URL** (URL de cierre de sesión) en la ventana de configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29df0-190">In the **Sign-out URL** box, enter the value of **Sign-Out URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="29df0-191">e.</span><span class="sxs-lookup"><span data-stu-id="29df0-191">e.</span></span> <span data-ttu-id="29df0-192">Seleccione **Usar POST**.</span><span class="sxs-lookup"><span data-stu-id="29df0-192">Select **Use POST**.</span></span>

    <span data-ttu-id="29df0-193">f.</span><span class="sxs-lookup"><span data-stu-id="29df0-193">f.</span></span> <span data-ttu-id="29df0-194">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="29df0-194">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="29df0-195">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="29df0-195">Create an Azure AD test user</span></span>
<span data-ttu-id="29df0-196">En Azure Portal, cree un usuario de prueba denominado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29df0-196">In the Azure portal, create a test user called Britta Simon.</span></span>

![Nombre y dirección de correo electrónico del usuario de prueba de Azure AD][100]

1. <span data-ttu-id="29df0-198">En el panel izquierdo de Azure Portal, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29df0-198">In the Azure portal, in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Icono de Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="29df0-200">Haga clic en **Usuarios y grupos** y luego en **Todos los usuarios** para mostrar la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="29df0-200">Click **Users and groups**, and then click **All users** to display the list of users.</span></span>

    ![Clic en "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="29df0-202">En la parte superior del cuadro de diálogo, haga clic en **Agregar** para abrir el cuadro de diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="29df0-202">At the top of the dialog box, click **Add** to open the **User** dialog box.</span></span>

    ![Botón "Agregar"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="29df0-204">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="29df0-204">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo "Usuario" con los campos nombre, dirección de correo electrónico y contraseña cumplimentados](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="29df0-206">a.</span><span class="sxs-lookup"><span data-stu-id="29df0-206">a.</span></span> <span data-ttu-id="29df0-207">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29df0-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29df0-208">b.</span><span class="sxs-lookup"><span data-stu-id="29df0-208">b.</span></span> <span data-ttu-id="29df0-209">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico de la cuenta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29df0-209">In the **User name** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="29df0-210">c.</span><span class="sxs-lookup"><span data-stu-id="29df0-210">c.</span></span> <span data-ttu-id="29df0-211">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="29df0-211">Select **Show Password** and write down the value of **Password**.</span></span>

    <span data-ttu-id="29df0-212">d.</span><span class="sxs-lookup"><span data-stu-id="29df0-212">d.</span></span> <span data-ttu-id="29df0-213">Haga clic en **Create**(Crear).</span><span class="sxs-lookup"><span data-stu-id="29df0-213">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="29df0-214">Creación de un usuario de prueba de Clarizen</span><span class="sxs-lookup"><span data-stu-id="29df0-214">Create a Clarizen test user</span></span>
<span data-ttu-id="29df0-215">Para permitir que los usuarios de Azure AD inicien sesión en Clarizen, debe aprovisionar las cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="29df0-215">To enable Azure AD users to sign in to Clarizen, you must provision user accounts.</span></span> <span data-ttu-id="29df0-216">En el caso de Clarizen, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="29df0-216">In the case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="29df0-217">Inicie sesión en el sitio de la compañía de Clarizen como administrador.</span><span class="sxs-lookup"><span data-stu-id="29df0-217">Sign in to your Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="29df0-218">Haga clic en **Contactos**.</span><span class="sxs-lookup"><span data-stu-id="29df0-218">Click **People**.</span></span>

    <span data-ttu-id="29df0-219">![Clic en "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span><span class="sxs-lookup"><span data-stu-id="29df0-219">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="29df0-220">Haga clic en **Invitar a usuario**.</span><span class="sxs-lookup"><span data-stu-id="29df0-220">Click **Invite User**.</span></span>

    <span data-ttu-id="29df0-221">![Botón "Invite User"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span><span class="sxs-lookup"><span data-stu-id="29df0-221">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="29df0-222">En el cuadro de diálogo **Invite People** (Invitar a personas), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="29df0-222">In the **Invite People** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="29df0-223">![Cuadro de diálogo "Invite People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span><span class="sxs-lookup"><span data-stu-id="29df0-223">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="29df0-224">a.</span><span class="sxs-lookup"><span data-stu-id="29df0-224">a.</span></span> <span data-ttu-id="29df0-225">En el cuadro **Email** (Correo electrónico), escriba la dirección de correo electrónico de la cuenta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29df0-225">In the **Email** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="29df0-226">b.</span><span class="sxs-lookup"><span data-stu-id="29df0-226">b.</span></span> <span data-ttu-id="29df0-227">Haga clic en **Invitar**.</span><span class="sxs-lookup"><span data-stu-id="29df0-227">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="29df0-228">El titular de la cuenta de Azure Active Directory recibirá un mensaje de correo y seguirá un vínculo para confirmar su cuenta antes de que se active.</span><span class="sxs-lookup"><span data-stu-id="29df0-228">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="29df0-229">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="29df0-229">Assign the Azure AD test user</span></span>
<span data-ttu-id="29df0-230">Habilite a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Clarizen.</span><span class="sxs-lookup"><span data-stu-id="29df0-230">Enable Britta Simon to use Azure single sign-on by granting her access to Clarizen.</span></span>

![Usuario de prueba asignado][200]

1. <span data-ttu-id="29df0-232">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y haga clic en **Aplicaciones empresariales**. Después, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="29df0-232">In the Azure portal, open the applications view, browse to the directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Clic en "Aplicaciones empresariales" y "Todas las aplicaciones"][201]

2. <span data-ttu-id="29df0-234">En la lista de aplicaciones, seleccione **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="29df0-234">In the applications list, select **Clarizen**.</span></span>

    ![Selección de Clarizen en la lista](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="29df0-236">En el panel izquierdo, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="29df0-236">In the left pane, click **Users and groups**.</span></span>

    ![Clic en "Usuarios y grupos"][202]

4. <span data-ttu-id="29df0-238">Haga clic en el botón **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="29df0-238">Click the **Add** button.</span></span> <span data-ttu-id="29df0-239">Después, en el cuadro de diálogo **Agregar asignación**, seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="29df0-239">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Botón "Agregar" y cuadro de diálogo "Agregar asignación"][203]

5. <span data-ttu-id="29df0-241">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="29df0-241">In the **Users and groups** dialog box, select **Britta Simon** in the list of users.</span></span>

6. <span data-ttu-id="29df0-242">En el cuadro de diálogo **Usuarios y grupos**, haga clic en el botón **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="29df0-242">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="29df0-243">En el cuadro de diálogo **Agregar asignación**, haga clic en el botón **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="29df0-243">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="29df0-244">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="29df0-244">Test single sign-on</span></span>
<span data-ttu-id="29df0-245">Pruebe la configuración de inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="29df0-245">Test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="29df0-246">Al hacer clic en el icono de Clarizen en el panel de acceso, debería iniciar sesión automáticamente en la aplicación Clarizen.</span><span class="sxs-lookup"><span data-stu-id="29df0-246">When you click the Clarizen tile in the Access Panel, you should be automatically signed in to your Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="29df0-247">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="29df0-247">Additional resources</span></span>

* [<span data-ttu-id="29df0-248">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29df0-248">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29df0-249">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="29df0-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png

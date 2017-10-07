---
title: "Tutorial: integración de Azure Active Directory con Clarizen | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Clarizen."
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
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="6afa8-103">Tutorial: integración de Azure Active Directory con Clarizen</span><span class="sxs-lookup"><span data-stu-id="6afa8-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="6afa8-104">En este tutorial, aprenderá cómo toointegrate Azure Active Directory (Azure AD) con Clarizen.</span><span class="sxs-lookup"><span data-stu-id="6afa8-104">In this tutorial, you learn how toointegrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="6afa8-105">Esto proporciona integración Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="6afa8-105">This integration gives you hello following benefits:</span></span>

- <span data-ttu-id="6afa8-106">Puede controlar, en Azure AD, que tiene acceso tooClarizen.</span><span class="sxs-lookup"><span data-stu-id="6afa8-106">You can control, in Azure AD, who has access tooClarizen.</span></span>
- <span data-ttu-id="6afa8-107">Puede habilitar la toobe usuarios tooClarizen (inicio de sesión único) con sus cuentas de Azure AD inicia sesión automáticamente.</span><span class="sxs-lookup"><span data-stu-id="6afa8-107">You can enable your users toobe automatically signed in tooClarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6afa8-108">Puede administrar las cuentas en una ubicación central, Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6afa8-108">You can manage your accounts in one central location, hello Azure portal.</span></span>

<span data-ttu-id="6afa8-109">escenario de Hello en este tutorial consta de dos tareas principales:</span><span class="sxs-lookup"><span data-stu-id="6afa8-109">hello scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="6afa8-110">Agregar Clarizen de hello Galería.</span><span class="sxs-lookup"><span data-stu-id="6afa8-110">Add Clarizen from hello gallery.</span></span>
2. <span data-ttu-id="6afa8-111">Configuración y prueba del inicio de sesión único en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6afa8-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="6afa8-112">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6afa8-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6afa8-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6afa8-113">Prerequisites</span></span>
<span data-ttu-id="6afa8-114">integración de Azure AD con Clarizen tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="6afa8-114">tooconfigure Azure AD integration with Clarizen, you need hello following items:</span></span>

- <span data-ttu-id="6afa8-115">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6afa8-115">An Azure AD subscription</span></span>
- <span data-ttu-id="6afa8-116">Una suscripción de Clarizen con inicio de sesión único habilitado</span><span class="sxs-lookup"><span data-stu-id="6afa8-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="6afa8-117">pasos de hello tootest en este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="6afa8-117">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="6afa8-118">Pruebe el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="6afa8-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6afa8-119">No use su entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6afa8-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="6afa8-120">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6afa8-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-hello-gallery"></a><span data-ttu-id="6afa8-121">Agregar Clarizen de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="6afa8-121">Add Clarizen from hello gallery</span></span>
<span data-ttu-id="6afa8-122">integración de hello tooconfigure de Clarizen en Azure AD, agregue Clarizen de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="6afa8-122">tooconfigure hello integration of Clarizen into Azure AD, add Clarizen from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="6afa8-123">Hola [portal de Azure](https://portal.azure.com), en Hola panel izquierdo, haga clic en hello **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="6afa8-123">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Icono de Azure Active Directory][1]

2. <span data-ttu-id="6afa8-125">Haga clic en **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="6afa8-126">A continuación, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-126">Then click **All applications**.</span></span>

    ![Clic en "Aplicaciones empresariales" y "Todas las aplicaciones"][2]

3. <span data-ttu-id="6afa8-128">Haga clic en hello **agregar** situado en la parte superior de Hola Hola del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6afa8-128">Click hello **Add** button at hello top of hello dialog box.</span></span>

    ![botón de "Agregar" Hello][3]

4. <span data-ttu-id="6afa8-130">En el cuadro de búsqueda de hello, escriba **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-130">In hello search box, type **Clarizen**.</span></span>

    ![Escriba "Clarizen" en el cuadro de búsqueda de Hola](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="6afa8-132">En el panel de resultados de hello, seleccione **Clarizen**y, a continuación, haga clic en **agregar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6afa8-132">In hello results pane, select **Clarizen**, and then click **Add** tooadd hello application.</span></span>

    ![Seleccionar Clarizen en el panel de resultados de Hola](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6afa8-134">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="6afa8-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="6afa8-135">En las secciones siguientes de hello, configurar y probar el inicio de sesión único en Azure AD con Clarizen en función de usuario de prueba de hello Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6afa8-135">In hello following sections, you configure and test Azure AD single sign-on with Clarizen based on hello test user Britta Simon.</span></span>

<span data-ttu-id="6afa8-136">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Clarizen es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6afa8-136">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clarizen is tooa user in Azure AD.</span></span> <span data-ttu-id="6afa8-137">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Clarizen debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="6afa8-137">In other words, a link relationship between an Azure AD user and hello related user in Clarizen needs toobe established.</span></span> <span data-ttu-id="6afa8-138">Establecer esta relación de vínculo asignando el valor de Hola de **nombre de usuario** en Azure AD como valor de Hola de **nombre de usuario** en Clarizen.</span><span class="sxs-lookup"><span data-stu-id="6afa8-138">You establish this link relationship by assigning hello value of **user name** in Azure AD as hello value of **Username** in Clarizen.</span></span>

<span data-ttu-id="6afa8-139">tooconfigure y prueba de inicio de sesión único en Azure AD con Clarizen, Hola completa después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="6afa8-139">tooconfigure and test Azure AD single sign-on with Clarizen, complete hello following building blocks:</span></span>

1. <span data-ttu-id="6afa8-140">**[Configurar inicio de sesión único en Azure AD](#configure-azure-ad-single-sign-on)**  tooenable su toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="6afa8-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6afa8-141">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  tootest inicio de sesión único en Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6afa8-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6afa8-142">**[Crear un usuario de prueba de Clarizen](#create-a-clarizen-test-user)**  toohave un equivalente de Britta Simon en Clarizen que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="6afa8-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** toohave a counterpart of Britta Simon in Clarizen that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="6afa8-143">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6afa8-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6afa8-144">**[Probar el inicio de sesión único](#test-single-sign-on)**  tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="6afa8-144">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6afa8-145">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6afa8-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="6afa8-146">Habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Clarizen.</span><span class="sxs-lookup"><span data-stu-id="6afa8-146">Enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="6afa8-147">En el portal de Azure, en Hola Hola **Clarizen** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-147">In hello Azure portal, on hello **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Clic en "Inicio de sesión único"][4]

2. <span data-ttu-id="6afa8-149">Hola **inicio de sesión único** cuadro de diálogo para **modo**, seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6afa8-149">In hello **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Selección de "Inicio de sesión basado en SAML"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="6afa8-151">Hola **Clarizen dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6afa8-151">In hello **Clarizen Domain and URLs** section, perform hello following steps:</span></span>

    ![Cuadros de identificador y dirección URL de respuesta](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="6afa8-153">a.</span><span class="sxs-lookup"><span data-stu-id="6afa8-153">a.</span></span> <span data-ttu-id="6afa8-154">Hola **identificador** cuadro de valor de tipo hello como: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="6afa8-154">In hello **Identifier** box, type hello value as: **Clarizen**</span></span>

    <span data-ttu-id="6afa8-155">b.</span><span class="sxs-lookup"><span data-stu-id="6afa8-155">b.</span></span> <span data-ttu-id="6afa8-156">Hola **dirección URL de respuesta** , escriba una dirección URL mediante el uso de hello siguiente patrón: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="6afa8-156">In hello **Reply URL** box, type a URL by using hello following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="6afa8-157">Estas no son valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="6afa8-157">These are not hello real values.</span></span> <span data-ttu-id="6afa8-158">Ha identificador real de toouse hello y dirección URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="6afa8-158">You have toouse hello actual identifier and reply URL.</span></span> <span data-ttu-id="6afa8-159">Aquí se recomienda usar valor de una cadena única de hello como Hola identificador.</span><span class="sxs-lookup"><span data-stu-id="6afa8-159">Here we suggest that you use hello unique value of a string as hello identifier.</span></span> <span data-ttu-id="6afa8-160">tooget Hola valores reales, póngase en contacto con hello [equipo de soporte técnico de Clarizen](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="6afa8-160">tooget hello actual values, contact hello [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="6afa8-161">En hello **el certificado de firma de SAML** sección, haga clic en **crear un nuevo certificado**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-161">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Clic en "Crear un nuevo certificado"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="6afa8-163">Hola **crear nuevo certificado** diálogo cuadro, haga clic en el icono del calendario de Hola y seleccione una fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="6afa8-163">In hello **Create New Certificate** dialog box, click hello calendar icon and select an expiry date.</span></span> <span data-ttu-id="6afa8-164">A continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-164">Then click **Save**.</span></span>

    ![Seleccionar y guardar una fecha de expiración](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="6afa8-166">Hola **el certificado de firma de SAML** sección, seleccione **activar el nuevo certificado**y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-166">In hello **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Activar casilla de verificación de Hola para hacer que el nuevo certificado de hello active](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="6afa8-168">Hola **el certificado de sustitución** cuadro de diálogo, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-168">In hello **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Al hacer clic en "Aceptar" tooconfirm que desea toomake Hola certificado activo](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="6afa8-170">Hola **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6afa8-170">In hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Haga clic en descarga de hello toostart "Certificado (Base64)"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="6afa8-172">Hola **configuración de Clarizen** sección, haga clic en **configurar Clarizen** tooopen hello **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="6afa8-172">In hello **Clarizen Configuration** section, click **Configure Clarizen** tooopen hello **Configure sign-on** window.</span></span>

    ![Clic en "Configurar Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Ventana "Configurar inicio de sesión", incluidos los archivos y las direcciones URL](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="6afa8-175">En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía Clarizen tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="6afa8-175">In a different web browser window, sign in tooyour Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="6afa8-176">Haga clic en el nombre de usuario y luego haga clic en **Settings** (Configuración).</span><span class="sxs-lookup"><span data-stu-id="6afa8-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="6afa8-177">![Clic en "Settings" (Configuración) debajo del nombre de usuario](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="6afa8-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="6afa8-178">Haga clic en hello **configuración Global** ficha. A continuación, siguiente demasiado**autenticación federada**, haga clic en **editar**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-178">Click hello **Global Settings** tab. Then, next too**Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="6afa8-179">![Pestaña "Global Settings"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span><span class="sxs-lookup"><span data-stu-id="6afa8-179">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="6afa8-180">Hola **autenticación federada** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6afa8-180">In hello **Federated Authentication** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="6afa8-181">![Cuadro de diálogo "Federated Authentication"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span><span class="sxs-lookup"><span data-stu-id="6afa8-181">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="6afa8-182">a.</span><span class="sxs-lookup"><span data-stu-id="6afa8-182">a.</span></span> <span data-ttu-id="6afa8-183">Seleccione **Habilitar autenticación federada**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-183">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="6afa8-184">b.</span><span class="sxs-lookup"><span data-stu-id="6afa8-184">b.</span></span> <span data-ttu-id="6afa8-185">Haga clic en **cargar** tooupload el certificado descargado.</span><span class="sxs-lookup"><span data-stu-id="6afa8-185">Click **Upload** tooupload your downloaded certificate.</span></span>

    <span data-ttu-id="6afa8-186">c.</span><span class="sxs-lookup"><span data-stu-id="6afa8-186">c.</span></span> <span data-ttu-id="6afa8-187">Hola **dirección URL de inicio de sesión** cuadro, escriba el valor de Hola de **SAML Single Sign-On dirección URL del servicio** desde la ventana de configuración de aplicación hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6afa8-187">In hello **Sign-in URL** box, enter hello value of **SAML Single Sign-On Service URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="6afa8-188">d.</span><span class="sxs-lookup"><span data-stu-id="6afa8-188">d.</span></span> <span data-ttu-id="6afa8-189">Hola **dirección URL de cierre de sesión** cuadro, escriba el valor de Hola de **dirección URL de cierre de sesión** desde la ventana de configuración de aplicación hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6afa8-189">In hello **Sign-out URL** box, enter hello value of **Sign-Out URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="6afa8-190">e.</span><span class="sxs-lookup"><span data-stu-id="6afa8-190">e.</span></span> <span data-ttu-id="6afa8-191">Seleccione **Usar POST**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-191">Select **Use POST**.</span></span>

    <span data-ttu-id="6afa8-192">f.</span><span class="sxs-lookup"><span data-stu-id="6afa8-192">f.</span></span> <span data-ttu-id="6afa8-193">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-193">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6afa8-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6afa8-194">Create an Azure AD test user</span></span>
<span data-ttu-id="6afa8-195">Hola portal de Azure, cree un usuario de prueba llamado a Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6afa8-195">In hello Azure portal, create a test user called Britta Simon.</span></span>

![Nombre y direcciones de correo del usuario de prueba de hello Azure AD][100]

1. <span data-ttu-id="6afa8-197">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="6afa8-197">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Icono de Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6afa8-199">Haga clic en **usuarios y grupos**y, a continuación, haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="6afa8-199">Click **Users and groups**, and then click **All users** toodisplay hello list of users.</span></span>

    ![Clic en "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6afa8-201">En la parte superior de Hola Hola del cuadro de diálogo, haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6afa8-201">At hello top of hello dialog box, click **Add** tooopen hello **User** dialog box.</span></span>

    ![botón de "Agregar" Hello](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6afa8-203">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6afa8-203">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Cuadro de diálogo "Usuario" con los campos nombre, dirección de correo electrónico y contraseña cumplimentados](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6afa8-205">a.</span><span class="sxs-lookup"><span data-stu-id="6afa8-205">a.</span></span> <span data-ttu-id="6afa8-206">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-206">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6afa8-207">b.</span><span class="sxs-lookup"><span data-stu-id="6afa8-207">b.</span></span> <span data-ttu-id="6afa8-208">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello de hello cuenta Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6afa8-208">In hello **User name** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="6afa8-209">c.</span><span class="sxs-lookup"><span data-stu-id="6afa8-209">c.</span></span> <span data-ttu-id="6afa8-210">Seleccione **Mostrar contraseña** y anote el valor de Hola de **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-210">Select **Show Password** and write down hello value of **Password**.</span></span>

    <span data-ttu-id="6afa8-211">d.</span><span class="sxs-lookup"><span data-stu-id="6afa8-211">d.</span></span> <span data-ttu-id="6afa8-212">Haga clic en **Create**(Crear).</span><span class="sxs-lookup"><span data-stu-id="6afa8-212">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="6afa8-213">Creación de un usuario de prueba de Clarizen</span><span class="sxs-lookup"><span data-stu-id="6afa8-213">Create a Clarizen test user</span></span>
<span data-ttu-id="6afa8-214">tooenable toosign de los usuarios de Azure AD en tooClarizen, debe aprovisionar las cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="6afa8-214">tooenable Azure AD users toosign in tooClarizen, you must provision user accounts.</span></span> <span data-ttu-id="6afa8-215">En caso de hello de Clarizen, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="6afa8-215">In hello case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="6afa8-216">Inicie sesión en tooyour Clarizen sitio de su compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="6afa8-216">Sign in tooyour Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="6afa8-217">Haga clic en **Contactos**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-217">Click **People**.</span></span>

    <span data-ttu-id="6afa8-218">![Clic en "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span><span class="sxs-lookup"><span data-stu-id="6afa8-218">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="6afa8-219">Haga clic en **Invitar a usuario**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-219">Click **Invite User**.</span></span>

    <span data-ttu-id="6afa8-220">![Botón "Invite User"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span><span class="sxs-lookup"><span data-stu-id="6afa8-220">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="6afa8-221">Hola **invitar personas** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6afa8-221">In hello **Invite People** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="6afa8-222">![Cuadro de diálogo "Invite People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span><span class="sxs-lookup"><span data-stu-id="6afa8-222">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="6afa8-223">a.</span><span class="sxs-lookup"><span data-stu-id="6afa8-223">a.</span></span> <span data-ttu-id="6afa8-224">Hola **correo electrónico** cuadro de dirección de correo electrónico de tipo hello de hello cuenta Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6afa8-224">In hello **Email** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="6afa8-225">b.</span><span class="sxs-lookup"><span data-stu-id="6afa8-225">b.</span></span> <span data-ttu-id="6afa8-226">Haga clic en **Invitar**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-226">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6afa8-227">titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico y seguir un vínculo tooconfirm su cuenta antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="6afa8-227">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6afa8-228">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6afa8-228">Assign hello Azure AD test user</span></span>
<span data-ttu-id="6afa8-229">Habilitar Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooClarizen de acceso.</span><span class="sxs-lookup"><span data-stu-id="6afa8-229">Enable Britta Simon toouse Azure single sign-on by granting her access tooClarizen.</span></span>

![Usuario de prueba asignado][200]

1. <span data-ttu-id="6afa8-231">Hola portal de Azure, abrir vista de aplicaciones de hello, examinar vista del directorio toohello, haga clic en **aplicaciones empresariales**y, a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-231">In hello Azure portal, open hello applications view, browse toohello directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Clic en "Aplicaciones empresariales" y "Todas las aplicaciones"][201]

2. <span data-ttu-id="6afa8-233">En la lista de aplicaciones de hello, seleccione **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-233">In hello applications list, select **Clarizen**.</span></span>

    ![Al seleccionar Clarizen en lista de Hola](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="6afa8-235">En el panel izquierdo de hello, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-235">In hello left pane, click **Users and groups**.</span></span>

    ![Clic en "Usuarios y grupos"][202]

4. <span data-ttu-id="6afa8-237">Haga clic en hello **agregar** botón.</span><span class="sxs-lookup"><span data-stu-id="6afa8-237">Click hello **Add** button.</span></span> <span data-ttu-id="6afa8-238">A continuación, en hello **Agregar asignación** cuadro de diálogo, seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6afa8-238">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![botón de "Agregar" Hello y cuadro de diálogo "Agregar asignación" hello][203]

5. <span data-ttu-id="6afa8-240">Hola **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="6afa8-240">In hello **Users and groups** dialog box, select **Britta Simon** in hello list of users.</span></span>

6. <span data-ttu-id="6afa8-241">Hola **usuarios y grupos** diálogo cuadro, haga clic en hello **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="6afa8-241">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="6afa8-242">Hola **Agregar asignación** diálogo cuadro, haga clic en hello **asignar** botón.</span><span class="sxs-lookup"><span data-stu-id="6afa8-242">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="6afa8-243">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="6afa8-243">Test single sign-on</span></span>
<span data-ttu-id="6afa8-244">Probar la configuración de inicio de sesión única de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="6afa8-244">Test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="6afa8-245">Al hacer clic en icono de Clarizen Hola Hola Panel de acceso, debería firmar automáticamente en tooyour aplicación Clarizen.</span><span class="sxs-lookup"><span data-stu-id="6afa8-245">When you click hello Clarizen tile in hello Access Panel, you should be automatically signed in tooyour Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6afa8-246">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="6afa8-246">Additional resources</span></span>

* [<span data-ttu-id="6afa8-247">Lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6afa8-247">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6afa8-248">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6afa8-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

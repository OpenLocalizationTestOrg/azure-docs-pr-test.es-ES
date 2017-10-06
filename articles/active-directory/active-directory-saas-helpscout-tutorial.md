---
title: "Tutorial: Integración de Azure Active Directory con Help Scout | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ayudar a Scout."
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
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="bbf17-103">Tutorial: integración de Azure Active Directory con Help Scout</span><span class="sxs-lookup"><span data-stu-id="bbf17-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="bbf17-104">En este tutorial, aprenderá cómo toointegrate ayuda Asesor de destinos con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bbf17-104">In this tutorial, you learn how toointegrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bbf17-105">Obtener Hola siguientes ventajas de integrar ayuda Scout con Azure AD:</span><span class="sxs-lookup"><span data-stu-id="bbf17-105">You get hello following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="bbf17-106">En Azure AD, puede controlar quién tiene acceso tooHelp Scout.</span><span class="sxs-lookup"><span data-stu-id="bbf17-106">In Azure AD, you can control who has access tooHelp Scout.</span></span>
- <span data-ttu-id="bbf17-107">Puede firmar automáticamente en su tooHelp usuarios Scout mediante el inicio de sesión único y una cuenta de usuario Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbf17-107">You can automatically sign in your users tooHelp Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="bbf17-108">Puede administrar las cuentas en una ubicación central, Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf17-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="bbf17-109">toolearn más información acerca del software como una integración de aplicaciones de servicio (SaaS) con Azure AD, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bbf17-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbf17-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bbf17-110">Prerequisites</span></span>

<span data-ttu-id="bbf17-111">tooset la integración de Azure AD con Scout ayuda, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bbf17-111">tooset up Azure AD integration with Help Scout, you need hello following items:</span></span>

- <span data-ttu-id="bbf17-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbf17-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bbf17-113">Una suscripción de Help Scout, con inicio de sesión único activado</span><span class="sxs-lookup"><span data-stu-id="bbf17-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="bbf17-114">Si prueba a pasos de hello en este tutorial, se recomienda que no probarlas en un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="bbf17-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="bbf17-115">Recomendaciones para probar los pasos de hello en este tutorial:</span><span class="sxs-lookup"><span data-stu-id="bbf17-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="bbf17-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bbf17-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="bbf17-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba gratuita durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbf17-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bbf17-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="bbf17-118">Scenario description</span></span>
<span data-ttu-id="bbf17-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="bbf17-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="bbf17-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="bbf17-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bbf17-121">Agregar a ayuda Scout de hello Galería.</span><span class="sxs-lookup"><span data-stu-id="bbf17-121">Add Help Scout from hello gallery.</span></span>
2. <span data-ttu-id="bbf17-122">Configuración y prueba del inicio de sesión único en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbf17-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-hello-gallery"></a><span data-ttu-id="bbf17-123">Agregar a ayuda Scout de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="bbf17-123">Add Help Scout from hello gallery</span></span>
<span data-ttu-id="bbf17-124">tooset la integración de Hola de ayuda Scout con Azure AD, en la Galería de hello, agregue la lista de tooyour de ayuda Scout de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="bbf17-124">tooset up hello integration of Help Scout with Azure AD, in hello gallery, add Help Scout tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bbf17-125">tooadd ayuda Scout de galería de hello:</span><span class="sxs-lookup"><span data-stu-id="bbf17-125">tooadd Help Scout from hello gallery:</span></span>

1. <span data-ttu-id="bbf17-126">Hola [portal de Azure](https://portal.azure.com), en el menú de la izquierda de Hola, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="bbf17-128">Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![página de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="bbf17-130">tooadd una nueva aplicación, seleccione **nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-130">tooadd a new application, select **New application**.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="bbf17-132">En el cuadro de búsqueda de hello, escriba **ayuda Scout**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-132">In hello search box, enter **Help Scout**.</span></span> <span data-ttu-id="bbf17-133">En los resultados de la búsqueda de hello, seleccione **ayuda Scout**y, a continuación, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-133">In hello search results, select **Help Scout**, and then select **Add**.</span></span>

    ![Ayuda Scout en la lista de resultados de Hola](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bbf17-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbf17-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="bbf17-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Help Scout mediante un usuario de prueba llamado *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="bbf17-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="bbf17-137">Para toowork de inicio de sesión único, Azure AD necesita usuario de equivalente de Azure AD tooknow hello en Scout ayuda.</span><span class="sxs-lookup"><span data-stu-id="bbf17-137">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="bbf17-138">Se debe establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Scout ayuda.</span><span class="sxs-lookup"><span data-stu-id="bbf17-138">A link relationship between an Azure AD user and hello related user in Help Scout must be established.</span></span>

<span data-ttu-id="bbf17-139">Hola tooestablish vincular relación en Scout ayuda, para **nombre de usuario**, asignar un valor de Hola de hello **nombre de usuario** en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbf17-139">tooestablish hello link relationship, in Help Scout, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="bbf17-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Scout ayuda, Hola completa después de tareas:</span><span class="sxs-lookup"><span data-stu-id="bbf17-140">tooconfigure and test Azure AD single sign-on with Help Scout, complete hello following tasks:</span></span>

1. <span data-ttu-id="bbf17-141">[Configuración del inicio de sesión único de Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="bbf17-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="bbf17-142">Configura un toouse de usuario de esta característica.</span><span class="sxs-lookup"><span data-stu-id="bbf17-142">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="bbf17-143">[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="bbf17-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="bbf17-144">Pruebas AD Azure inicio de sesión único con usuario hello Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbf17-144">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="bbf17-145">[Creación de un usuario de prueba de Help Scout](#create-a-help-scout-test-user).</span><span class="sxs-lookup"><span data-stu-id="bbf17-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="bbf17-146">Crea a un equivalente de Britta Simon en Scout ayuda que está vinculado toohello representación de Azure AD del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="bbf17-146">Creates a counterpart of Britta Simon in Help Scout that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="bbf17-147">[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="bbf17-147">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="bbf17-148">Configura Britta Simon toouse inicio de sesión único en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbf17-148">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bbf17-149">[Prueba de inicio de sesión único](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="bbf17-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="bbf17-150">Comprueba que la configuración de hello funciona.</span><span class="sxs-lookup"><span data-stu-id="bbf17-150">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="bbf17-151">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbf17-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="bbf17-152">En esta sección, configurar inicio de sesión único en Azure AD en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf17-152">In this section, you set up Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="bbf17-153">A continuación, configura el inicio de sesión único en la aplicación Help Scout.</span><span class="sxs-lookup"><span data-stu-id="bbf17-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="bbf17-154">tooset de inicio de sesión único en Azure AD con Scout ayuda:</span><span class="sxs-lookup"><span data-stu-id="bbf17-154">tooset up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="bbf17-155">En el portal de Azure, en Hola Hola **ayuda Scout** página de integración de aplicaciones, seleccione **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-155">In hello Azure portal, on hello **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![Configuración de vínculo de inicio de sesión único][4]

2. <span data-ttu-id="bbf17-157">En hello **inicio de sesión único** página, para **modo**, seleccione **sesión basado en SAML**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-157">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="bbf17-159">En **ayuda Scout dominio y las direcciones URL**si desea tooset una aplicación hello en el modo iniciado por IDP, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="bbf17-159">Under **Help Scout Domain and URLs**, if you want tooset up hello application in IDP-initiated mode, complete hello following steps:</span></span>

    1. <span data-ttu-id="bbf17-160">Hola **identificador** cuadro, escriba una dirección URL con hello siguiente patrón:`urn:auth0:helpscout:<instancename>`</span><span class="sxs-lookup"><span data-stu-id="bbf17-160">In hello **Identifier** box, enter a URL that has hello following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="bbf17-161">Hola **dirección URL de respuesta** cuadro, escriba una dirección URL con hello siguiente patrón:`https://helpscout.auth0.com/login/callback?connection=<instancename>`</span><span class="sxs-lookup"><span data-stu-id="bbf17-161">In hello **Reply URL** box, enter a URL that has hello following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="bbf17-163">Si desea tooset una aplicación hello en modo iniciado en SP, seleccione hello **mostrar avanzadas de configuración de direcciones URL** casilla de verificación y, a continuación, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="bbf17-163">If you want tooset up hello application in SP-initiated mode, select hello **Show advanced URL settings** check box, and then do hello following:</span></span>

    * <span data-ttu-id="bbf17-164">Hola **dirección URL de inicio de sesión** cuadro, escriba una dirección URL con hello siguiendo el formato:`https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="bbf17-164">In hello **Sign on URL** box, enter a URL that has hello following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="bbf17-166">los valores de Hello en estas direcciones URL son únicamente como demostración.</span><span class="sxs-lookup"><span data-stu-id="bbf17-166">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="bbf17-167">Actualizar valores de hello con la dirección URL de identificación real de Hola y la dirección URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="bbf17-167">Update hello values with hello actual identifier URL and reply URL.</span></span> <span data-ttu-id="bbf17-168">tooget estos valores, póngase en contacto con [equipo de soporte técnico de ayuda Scout](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="bbf17-168">tooget these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="bbf17-169">En **el certificado de firma de SAML**, seleccione **Metadata XML**y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="bbf17-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="bbf17-171">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-171">Select **Save**.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="bbf17-173">tooset una sola sesión en el lado de ayuda Scout hello, enviar Hola descargar metadatos XML archivo toohello [equipo de soporte técnico de ayuda Scout](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="bbf17-173">tooset up single sign-on on hello Help Scout side, send hello downloaded metadata XML file toohello [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="bbf17-174">equipo de soporte técnico de Hello ayuda Scout aplica esta configuración Hola SAML único inicio de sesión de conexión se establece correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="bbf17-174">hello Help Scout support team applies this setting so that hello SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="bbf17-175">Puede leer una versión concisa de estas instrucciones en hello [portal de Azure](https://portal.azure.com), mientras que va a configurar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bbf17-175">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="bbf17-176">Después de agregar la aplicación hello seleccionando **Active Directory** > **aplicaciones empresariales**, seleccione hello **Single Sign-On** ficha. Puede tener acceso a la documentación de hello incrustado en hello **configuración** sección final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="bbf17-176">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="bbf17-177">Para más información, consulte la [documentación insertada de Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="bbf17-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bbf17-178">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbf17-178">Create an Azure AD test user</span></span>

<span data-ttu-id="bbf17-179">En esta sección, en hello portal de Azure, cree un usuario de prueba denominado a Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbf17-179">In this section, in hello Azure portal, you create a test user named Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="bbf17-181">toocreate un usuario de prueba en Azure AD:</span><span class="sxs-lookup"><span data-stu-id="bbf17-181">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="bbf17-182">En el portal de Azure, en el menú de la izquierda, Hola Hola seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-182">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="bbf17-184">lista de hello toodisplay de usuarios, seleccionados **usuarios y grupos**y, a continuación, seleccione **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-184">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![Seleccionar Usuarios y grupos y, luego, Todos los usuarios](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="bbf17-186">Hola tooopen **usuario** cuadro de diálogo, en parte superior de Hola de hello **todos los usuarios** página, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-186">tooopen hello **User** dialog box, at hello top of hello **All Users** page, select **Add**.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="bbf17-188">Hola **usuario** cuadro de diálogo, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="bbf17-188">In hello **User** dialog box, complete hello following steps:</span></span>

    1. <span data-ttu-id="bbf17-189">Hola **nombre** cuadro, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-189">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="bbf17-190">Hola **nombre de usuario** cuadro, escriba la dirección de correo electrónico de saludo del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbf17-190">In hello **User name** box, enter hello email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="bbf17-191">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="bbf17-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="bbf17-192">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-192">Select **Create**.</span></span>

        ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="bbf17-194">Creación de un usuario de prueba de Help Scout</span><span class="sxs-lookup"><span data-stu-id="bbf17-194">Create a Help Scout test user</span></span>

<span data-ttu-id="bbf17-195">objeto de Hola de esta sección es toocreate un usuario denominado a Britta Simon en Scout ayuda.</span><span class="sxs-lookup"><span data-stu-id="bbf17-195">hello object of this section is toocreate a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="bbf17-196">Help Scout admite el aprovisionamiento Just-In-Time (JIT), que está activado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bbf17-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="bbf17-197">En esta sección, no hay ningún toocomplete acción o tarea.</span><span class="sxs-lookup"><span data-stu-id="bbf17-197">In this section, there's no action or task toocomplete.</span></span> <span data-ttu-id="bbf17-198">Si un usuario ya no existe en Scout ayuda, se crea uno nuevo si intentas tooaccess Scout ayuda.</span><span class="sxs-lookup"><span data-stu-id="bbf17-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt tooaccess Help Scout.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="bbf17-199">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbf17-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="bbf17-200">En esta sección, que permita que a Hola usuario Britta Simon toouse Azure AD inicio de sesión único mediante la concesión de tooHelp de acceso de cuenta de usuario de hello Scout.</span><span class="sxs-lookup"><span data-stu-id="bbf17-200">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooHelp Scout.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="bbf17-202">tooassign Britta Simon tooHelp Scout:</span><span class="sxs-lookup"><span data-stu-id="bbf17-202">tooassign Britta Simon tooHelp Scout:</span></span>

1. <span data-ttu-id="bbf17-203">Hola portal de Azure, abrir vista de aplicaciones de hello y, haga clic en la vista de directorio toohello.</span><span class="sxs-lookup"><span data-stu-id="bbf17-203">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="bbf17-204">Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="bbf17-206">En la lista de aplicaciones de hello, seleccione **ayuda Scout**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-206">In hello applications list, select **Help Scout**.</span></span>

    ![vínculo de ayuda Scout Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="bbf17-208">En el menú de la izquierda hello, seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-208">In hello left menu, select **Users and groups**.</span></span>

    ![Hola a los usuarios y grupos de vínculo][202]

4. <span data-ttu-id="bbf17-210">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-210">Select **Add**.</span></span> <span data-ttu-id="bbf17-211">A continuación, en hello **Agregar asignación** página, seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-211">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="bbf17-213">En hello **usuarios y grupos** página, en la lista de Hola de usuarios, seleccionados **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-213">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="bbf17-214">En hello **usuarios y grupos** página, seleccione **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-214">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="bbf17-215">En hello **Agregar asignación** página, seleccione **asignar**.</span><span class="sxs-lookup"><span data-stu-id="bbf17-215">On hello **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bbf17-216">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="bbf17-216">Test single sign-on</span></span>

<span data-ttu-id="bbf17-217">En esta sección, probará la configuración de inicio de sesión única de Azure AD mediante el panel de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="bbf17-217">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="bbf17-218">Cuando se selecciona icono de ayuda Scout hello en el panel de acceso hello, se debe sesión automáticamente en tooyour aplicación Scout ayuda.</span><span class="sxs-lookup"><span data-stu-id="bbf17-218">When you select hello Help Scout tile in hello access panel, you should be automatically signed in tooyour Help Scout application.</span></span>

<span data-ttu-id="bbf17-219">Para obtener más información sobre el panel de acceso, consulte [panel de acceso de introducción toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bbf17-219">For more information about the access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bbf17-220">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bbf17-220">Additional resources</span></span>

* [<span data-ttu-id="bbf17-221">Lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbf17-221">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bbf17-222">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bbf17-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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


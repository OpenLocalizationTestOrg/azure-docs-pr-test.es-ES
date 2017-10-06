---
title: "Tutorial: Integración de Azure Active Directory con vxMaintain | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y vxMaintain."
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
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="5180c-103">Tutorial: Integración de Azure Active Directory con vxMaintain</span><span class="sxs-lookup"><span data-stu-id="5180c-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="5180c-104">En este tutorial, aprenderá cómo toointegrate vxMaintain con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5180c-104">In this tutorial, you learn how toointegrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5180c-105">Esta integración proporciona varias ventajas importantes.</span><span class="sxs-lookup"><span data-stu-id="5180c-105">This integration provides several important benefits.</span></span> <span data-ttu-id="5180c-106">Puede:</span><span class="sxs-lookup"><span data-stu-id="5180c-106">You can:</span></span>

- <span data-ttu-id="5180c-107">Control de Azure AD que tenga acceso a toovxMaintain.</span><span class="sxs-lookup"><span data-stu-id="5180c-107">Control in Azure AD who has access toovxMaintain.</span></span>
- <span data-ttu-id="5180c-108">Habilitar el inicio de sesión de los usuarios tooautomatically en toovxMaintain con inicio de sesión único (SSO) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5180c-108">Enable your users tooautomatically sign in toovxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="5180c-109">Administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5180c-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="5180c-110">toolearn más información acerca de la integración de aplicaciones de SaaS con Azure AD, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5180c-110">toolearn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5180c-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5180c-111">Prerequisites</span></span>

<span data-ttu-id="5180c-112">integración de Azure AD con vxMaintain tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="5180c-112">tooconfigure Azure AD integration with vxMaintain, you need hello following items:</span></span>

- <span data-ttu-id="5180c-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5180c-113">An Azure AD subscription</span></span>
- <span data-ttu-id="5180c-114">Una suscripción de inicio de sesión único de vxMaintain habilitada</span><span class="sxs-lookup"><span data-stu-id="5180c-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5180c-115">Cuando se prueba pasos hello en este tutorial, se recomienda que no use un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="5180c-115">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="5180c-116">pasos de hello tootest en este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="5180c-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="5180c-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5180c-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5180c-118">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5180c-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5180c-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="5180c-119">Scenario description</span></span>
<span data-ttu-id="5180c-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="5180c-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="5180c-121">escenario de Hola que se describe en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="5180c-121">hello scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="5180c-122">Agregar vxMaintain desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="5180c-122">Adding vxMaintain from hello gallery</span></span>
* <span data-ttu-id="5180c-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5180c-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-hello-gallery"></a><span data-ttu-id="5180c-124">Agregar vxMaintain de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="5180c-124">Add vxMaintain from hello gallery</span></span>
<span data-ttu-id="5180c-125">integración de hello tooconfigure de vxMaintain con Azure AD, deberá tooadd vxMaintain de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="5180c-125">tooconfigure hello integration of vxMaintain with Azure AD, you need tooadd vxMaintain from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5180c-126">tooadd vxMaintain de galería de hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="5180c-126">tooadd vxMaintain from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="5180c-127">Hola [portal de Azure](https://portal.azure.com), en Hola panel izquierdo, seleccione hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="5180c-127">In hello [Azure portal](https://portal.azure.com), in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="5180c-129">Seleccione **Aplicaciones empresariales** > **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5180c-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![panel de "Aplicaciones empresariales" Hello][2]
    
3. <span data-ttu-id="5180c-131">una aplicación Hola tooadd **todas las aplicaciones** cuadro de diálogo, seleccione **nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="5180c-131">tooadd an application, in hello **All applications** dialog box, select **New application**.</span></span>

    ![Hola "Nueva aplicación" botón][3]

4. <span data-ttu-id="5180c-133">En el cuadro de búsqueda de hello, escriba **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="5180c-133">In hello search box, type **vxMaintain**.</span></span>

    ![lista de desplegable de "Inicio de sesión en modo simple" Hola](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="5180c-135">En la lista de resultados de hello, seleccione **vxMaintain**y, a continuación, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="5180c-135">In hello results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![vínculo de Hello vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5180c-137">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="5180c-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="5180c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con vxMaintain con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5180c-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5180c-139">Para toowork SSO, Azure AD necesita usuario de Azure AD tooknow hello vxMaintain homólogo toohello.</span><span class="sxs-lookup"><span data-stu-id="5180c-139">For SSO toowork, Azure AD needs tooknow hello vxMaintain counterpart toohello Azure AD user.</span></span> <span data-ttu-id="5180c-140">Es decir, debe establecer una relación de vínculo entre el usuario vxMaintain correspondiente de Hola y Hola Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5180c-140">That is, you must establish a link relationship between hello Azure AD user and hello corresponding vxMaintain user.</span></span>

<span data-ttu-id="5180c-141">relación de vínculo de tooestablish hello, asignar Hola vxMaintain **nombre de usuario** valor como hello Azure AD **nombre de usuario** valor.</span><span class="sxs-lookup"><span data-stu-id="5180c-141">tooestablish hello link relationship, assign hello vxMaintain **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="5180c-142">tooconfigure y SSO de Azure AD mediante el uso de vxMaintain, Hola completa después de bloques de creación de la prueba.</span><span class="sxs-lookup"><span data-stu-id="5180c-142">tooconfigure and test Azure AD SSO by using vxMaintain, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="5180c-143">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5180c-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="5180c-144">En esta sección, puede habilitar el SSO de AD de Azure en hello portal de Azure y configurar SSO en la aplicación vxMaintain haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="5180c-144">In this section, you can both enable Azure AD SSO in hello Azure portal and configure SSO in your vxMaintain application by doing hello following:</span></span>

1. <span data-ttu-id="5180c-145">En el portal de Azure, en Hola Hola **vxMaintain** página de integración de aplicaciones, seleccione **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="5180c-145">In hello Azure portal, on hello **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![Hola "Inicio de sesión único" comando][4]

2. <span data-ttu-id="5180c-147">tooenable SSO, Hola **modo de inicio de sesión único** lista desplegable, seleccione **sesión basado en SAML**.</span><span class="sxs-lookup"><span data-stu-id="5180c-147">tooenable SSO, in hello **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![Hola "basado en SAML Sign-on" comando](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="5180c-149">En **vxMaintain dominio y las direcciones URL**, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="5180c-149">Under **vxMaintain Domain and URLs**, do hello following:</span></span>

    ![Hola vxMaintain sección de dominio y las direcciones URL](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="5180c-151">a.</span><span class="sxs-lookup"><span data-stu-id="5180c-151">a.</span></span> <span data-ttu-id="5180c-152">Hola **identificador** cuadro, escriba una dirección URL que ha Hola según la sintaxis:`https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="5180c-152">In hello **Identifier** box, type a URL that has hello following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="5180c-153">b.</span><span class="sxs-lookup"><span data-stu-id="5180c-153">b.</span></span> <span data-ttu-id="5180c-154">Hola **dirección URL de respuesta** cuadro, escriba una dirección URL que ha Hola según la sintaxis:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="5180c-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5180c-155">Hello valores anteriores no son reales.</span><span class="sxs-lookup"><span data-stu-id="5180c-155">hello preceding values are not real.</span></span> <span data-ttu-id="5180c-156">Actualizarlas con el identificador real de Hola o dirección URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="5180c-156">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="5180c-157">valores de hello tooobtain, Hola contacto [equipo de soporte técnico de vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="5180c-157">tooobtain hello values, contact hello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="5180c-158">En **el certificado de firma de SAML**, seleccione **Metadata XML**y, a continuación, guarde el equipo de tooyour de archivo de metadatos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5180c-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file tooyour computer.</span></span>

    ![Hola sección "Certificado de firma de SAML"](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="5180c-160">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5180c-160">Select **Save**.</span></span>

    ![botón Guardar de Hola](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5180c-162">tooconfigure **vxMaintain** SSO, Hola envío descargado **Metadata XML** archivo toohello [equipo de soporte técnico de vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="5180c-162">tooconfigure **vxMaintain** SSO, send hello downloaded **Metadata XML** file toohello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="5180c-163">Como configurar la aplicación hello, puede leer una versión concisa de hello precede a instrucciones de hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5180c-163">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5180c-164">Después de Agregar aplicación hello de hello **Active Directory** > **aplicaciones empresariales** sección, seleccione hello **Single Sign-On** ficha y, a continuación, Hola de acceso incrusta la documentación de hello **configuración** sección.</span><span class="sxs-lookup"><span data-stu-id="5180c-164">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab, and then access hello embedded documentation from hello **Configuration** section.</span></span> 
>
><span data-ttu-id="5180c-165">toolearn más información acerca de la característica de documentación de embedded hello, consulte [administración de inicio de sesión único para aplicaciones empresariales](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="5180c-165">toolearn more about hello embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5180c-166">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5180c-166">Create an Azure AD test user</span></span>
<span data-ttu-id="5180c-167">En esta sección, para crear el usuario de prueba Britta Simon Hola portal de Azure, llevando a cabo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="5180c-167">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![usuario de prueba de Hello Azure AD][100]

1. <span data-ttu-id="5180c-169">Hola **portal de Azure**, en Hola panel izquierdo, seleccione hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="5180c-169">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![botón de "Azure Active Directory" Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5180c-171">toodisplay una lista de usuarios, vaya demasiado**usuarios y grupos** > **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5180c-171">toodisplay a list of users, go too**Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="5180c-172">![vínculo de Hello "Todos los usuarios"](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="5180c-172">![hello "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="5180c-173">Hola **todos los usuarios** abre el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5180c-173">hello **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="5180c-174">Hola tooopen **usuario** cuadro de diálogo, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="5180c-174">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![botón de agregar Hola](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5180c-176">Hola **usuario** diálogo cuadro, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="5180c-176">In hello **User** dialog box, do hello following:</span></span>
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5180c-178">a.</span><span class="sxs-lookup"><span data-stu-id="5180c-178">a.</span></span> <span data-ttu-id="5180c-179">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5180c-179">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5180c-180">b.</span><span class="sxs-lookup"><span data-stu-id="5180c-180">b.</span></span> <span data-ttu-id="5180c-181">Hola **nombre de usuario** cuadro de dirección de correo electrónico de Hola de tipo de usuario de prueba Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5180c-181">In hello **User name** box, type hello email address of test user Britta Simon.</span></span>

    <span data-ttu-id="5180c-182">c.</span><span class="sxs-lookup"><span data-stu-id="5180c-182">c.</span></span> <span data-ttu-id="5180c-183">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, valor de hello tenga en cuenta que se generó en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="5180c-183">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="5180c-184">d.</span><span class="sxs-lookup"><span data-stu-id="5180c-184">d.</span></span> <span data-ttu-id="5180c-185">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5180c-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="5180c-186">Creación de un usuario de prueba de vxMaintain</span><span class="sxs-lookup"><span data-stu-id="5180c-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="5180c-187">En esta sección, creará una usuaria de prueba llamada Britta Simon en vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="5180c-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="5180c-188">los usuarios de tooadd en la plataforma de vxMaintain hello, trabajar con el [equipo de soporte técnico de vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="5180c-188">tooadd users in hello vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="5180c-189">Antes de usar SSO, crear y activar los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="5180c-189">Before you use SSO, create and activate hello users.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5180c-190">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5180c-190">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5180c-191">En esta sección, se habilita el usuario de prueba Britta Simon toouse Azure SSO concediendo acceso toovxMaintain.</span><span class="sxs-lookup"><span data-stu-id="5180c-191">In this section, you enable test user Britta Simon toouse Azure SSO by granting access toovxMaintain.</span></span> <span data-ttu-id="5180c-192">por lo tanto, toodo Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="5180c-192">toodo so, do hello following:</span></span>

![Usuario de prueba en la lista de nombre para mostrar de Hola][200] 

1. <span data-ttu-id="5180c-194">En el portal de Azure hello **aplicaciones** ver, vaya demasiado**directorio** Vista > **aplicaciones empresariales** > **detodaslasaplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="5180c-194">In hello Azure portal **Applications** view, go too**Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![vínculo de Hello "Todas las aplicaciones"][201] 

2. <span data-ttu-id="5180c-196">Hola **aplicaciones** lista, seleccione **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="5180c-196">In hello **Applications** list, select **vxMaintain**.</span></span>

    ![vínculo de Hello vxMaintain](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="5180c-198">En el panel izquierdo de hello, seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5180c-198">In hello left pane, select **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. <span data-ttu-id="5180c-200">Seleccione **agregar** y, a continuación, en hello **Agregar asignación** panel, seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="5180c-200">Select **Add** and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][203]

5. <span data-ttu-id="5180c-202">Hola **usuarios y grupos** cuadro de diálogo hello **usuarios** lista, seleccione **Britta Simon**y, a continuación, seleccione hello **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="5180c-202">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**, and then select hello **Select** button.</span></span>

7. <span data-ttu-id="5180c-203">Hola **Agregar asignación** cuadro de diálogo, seleccione **asignar**.</span><span class="sxs-lookup"><span data-stu-id="5180c-203">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="5180c-204">Prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5180c-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="5180c-205">En esta sección, probará la configuración de SSO de Azure AD mediante el uso de hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="5180c-205">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="5180c-206">Seleccionar hello **vxMaintain** icono en el Panel de acceso de hello debe iniciar sesión en tooyour vxMaintain aplicación automáticamente.</span><span class="sxs-lookup"><span data-stu-id="5180c-206">Selecting hello **vxMaintain** tile in hello Access Panel should sign you in tooyour vxMaintain application automatically.</span></span>

<span data-ttu-id="5180c-207">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5180c-207">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5180c-208">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5180c-208">Next steps</span></span>

* [<span data-ttu-id="5180c-209">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5180c-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5180c-210">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5180c-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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


---
title: "Tutorial: Integración de Azure Active Directory con IBM Kenexa Survey Enterprise | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Enterprise de encuesta de Kenexa de IBM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="a6b89-103">Tutorial: Integración de Azure Active Directory con IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="a6b89-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="a6b89-104">En este tutorial, aprenderá cómo toointegrate IBM Kenexa encuesta Enterprise con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a6b89-104">In this tutorial, you learn how toointegrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a6b89-105">Integración de IBM Kenexa encuesta Enterprise con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a6b89-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a6b89-106">Puede controlar en Azure AD que tenga acceso tooIBM Kenexa encuesta Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a6b89-106">You can control in Azure AD who has access tooIBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="a6b89-107">Puede habilitar el inicio de sesión de los usuarios tooautomatically en tooIBM Kenexa encuesta Enterprise mediante el inicio de sesión único (SSO) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6b89-107">You can enable your users tooautomatically sign in tooIBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a6b89-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a6b89-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="a6b89-109">Si desea más información acerca del software tooknow como una integración de aplicaciones de servicio (SaaS) con Azure AD, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a6b89-109">If you want tooknow more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6b89-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a6b89-110">Prerequisites</span></span>

<span data-ttu-id="a6b89-111">tooconfigure integración de Azure AD con IBM Kenexa encuesta Enterprise, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a6b89-111">tooconfigure Azure AD integration with IBM Kenexa Survey Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="a6b89-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6b89-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a6b89-113">Una suscripción habilitada para el inicio de sesión único en IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="a6b89-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a6b89-114">Cuando se prueba pasos hello en este tutorial, se recomienda que no use un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a6b89-114">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="a6b89-115">pasos de hello tootest en este tutorial, siga estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a6b89-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="a6b89-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a6b89-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a6b89-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a6b89-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a6b89-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="a6b89-118">Scenario description</span></span>
<span data-ttu-id="a6b89-119">En este tutorial, puede probar el inicio de sesión único (SSO) de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a6b89-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="a6b89-120">escenario de Hello descrito en hello tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="a6b89-120">hello scenario outlined in hello tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="a6b89-121">Agregar IBM Kenexa encuesta Enterprise desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="a6b89-121">Adding IBM Kenexa Survey Enterprise from hello gallery</span></span>
* <span data-ttu-id="a6b89-122">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6b89-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a><span data-ttu-id="a6b89-123">Agregar IBM Kenexa encuesta Enterprise de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="a6b89-123">Add IBM Kenexa Survey Enterprise from hello gallery</span></span>
<span data-ttu-id="a6b89-124">integración de hello tooconfigure de IBM Kenexa encuesta Enterprise en Azure AD, agregue IBM Kenexa encuesta Enterprise de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="a6b89-124">tooconfigure hello integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a6b89-125">tooadd IBM Kenexa encuesta Enterprise desde la Galería de Hola Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="a6b89-125">tooadd IBM Kenexa Survey Enterprise from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="a6b89-126">Hola [portal de Azure](https://portal.azure.com), en Hola panel izquierdo, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="a6b89-126">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** button.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="a6b89-128">Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a6b89-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="a6b89-130">tooadd una aplicación, haga clic en hello **nueva aplicación** botón.</span><span class="sxs-lookup"><span data-stu-id="a6b89-130">tooadd an application, click hello **New application** button.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="a6b89-132">En el cuadro de búsqueda de hello, escriba **IBM Kenexa encuesta Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="a6b89-132">In hello search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="a6b89-134">En la lista de resultados de hello, seleccione **IBM Kenexa encuesta Enterprise**y, a continuación, haga clic en hello **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a6b89-134">In hello results list, select **IBM Kenexa Survey Enterprise**, and then click hello **Add** button tooadd hello application.</span></span>

    ![Lista de resultados de la empresa de encuesta de Kenexa de IBM en hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a6b89-136">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6b89-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a6b89-137">En esta sección, configurará y probará el inicio de sesión único de Azure AD con IBM Kenexa Survey Enterprise con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a6b89-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a6b89-138">Para toowork SSO, Azure AD necesita a equivalente de usuario de tooidentify Hola IBM Kenexa encuesta Enterprise en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6b89-138">For SSO toowork, Azure AD needs tooidentify hello IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="a6b89-139">Es decir, Azure AD debe establecer una relación de vínculo entre un usuario de Azure AD y un usuario relacionado de IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a6b89-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="a6b89-140">relación de vínculo de tooestablish hello, asignar Hola valo hello **nombre de usuario** de empresa de encuesta de IBM Kenexa como valor de Hola de hello **nombre de usuario** en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6b89-140">tooestablish hello link relationship, assign hello value of hello **user name** in IBM Kenexa Survey Enterprise as hello value of hello **Username** in Azure AD.</span></span>

<span data-ttu-id="a6b89-141">prueba SSO de Azure AD con IBM Kenexa encuesta Enterprise, completa y tooconfigure Hola bloques de creación de hello las dos secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="a6b89-141">tooconfigure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete hello building blocks in hello next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="a6b89-142">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6b89-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="a6b89-143">En esta sección, habilitar SSO de Azure AD en hello portal de Azure y configurar SSO en la aplicación empresarial de IBM Kenexa encuesta haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="a6b89-143">In this section, you enable Azure AD SSO in hello Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing hello following:</span></span>

1. <span data-ttu-id="a6b89-144">En el portal de Azure, en Hola Hola **IBM Kenexa encuesta Enterprise** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a6b89-144">In hello Azure portal, on hello **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo de inicio de sesión único de IBM Kenexa Survey Enterprise][4]

2. <span data-ttu-id="a6b89-146">Hola **inicio de sesión único** cuadro de diálogo hello **modo** cuadro, seleccione **sesión basado en SAML** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="a6b89-146">In hello **Single sign-on** dialog box, in hello **Mode** box, select **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="a6b89-148">Hola **IBM Kenexa encuesta Enterprise dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a6b89-148">In hello **IBM Kenexa Survey Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="a6b89-150">a.</span><span class="sxs-lookup"><span data-stu-id="a6b89-150">a.</span></span> <span data-ttu-id="a6b89-151">Hola **identificador** cuadro de texto, escriba una dirección URL con hello sigue el patrón:`https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="a6b89-151">In hello **Identifier** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="a6b89-152">b.</span><span class="sxs-lookup"><span data-stu-id="a6b89-152">b.</span></span> <span data-ttu-id="a6b89-153">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL con hello sigue el patrón:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="a6b89-153">In hello **Reply URL** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a6b89-154">Hello valores anteriores no son reales.</span><span class="sxs-lookup"><span data-stu-id="a6b89-154">hello preceding values are not real.</span></span> <span data-ttu-id="a6b89-155">Actualizarlas con el identificador real de Hola o dirección URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="a6b89-155">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="a6b89-156">tooobtain Hola valores reales, póngase en contacto con hello [equipo de soporte técnico de IBM Kenexa encuesta Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="a6b89-156">tooobtain hello actual values, contact hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="a6b89-157">En **el certificado de firma de SAML**, haga clic en **certificado (Base64)**y, a continuación, guarde el equipo de tooyour de archivo de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b89-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save hello certificate file tooyour computer.</span></span>

    ![vínculo de descarga del certificado (Base64) Hola](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="a6b89-159">Hola aplicación empresarial de encuesta de IBM Kenexa espera las aserciones de lenguaje de marcado de aserciones de seguridad (SAML) de hello tooreceive en un formato específico, lo que requiere tooadd atributo personalizado toohello configuración de asignaciones de los atributos de token de SAML.</span><span class="sxs-lookup"><span data-stu-id="a6b89-159">hello IBM Kenexa Survey Enterprise application expects tooreceive hello Security Assertions Markup Language (SAML) assertions in a specific format, which requires you tooadd custom attribute mappings toohello configuration of your SAML token attributes.</span></span> <span data-ttu-id="a6b89-160">Hello valor de notificación de identificador de usuario de Hola en respuesta Hola debe coincidir con Id. de SSO configurado en el sistema de Kenexa Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b89-160">hello value of hello user-identifier claim in hello response must match hello SSO ID that's configured in hello Kenexa system.</span></span> <span data-ttu-id="a6b89-161">toomap Hola identificador de usuario correspondiente en su organización como protocolo de datagramas de Internet SSO (IDP), trabajar con hello [equipo de soporte técnico de IBM Kenexa encuesta Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="a6b89-161">toomap hello appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="a6b89-162">De forma predeterminada, AD de Azure establece el identificador de usuario de hello como valor de nombre principal (UPN) del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b89-162">By default, Azure AD sets hello user identifier as hello user principal name (UPN) value.</span></span> <span data-ttu-id="a6b89-163">Puede cambiar este valor en hello **atributo** ficha, tal y como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b89-163">You can change this value on hello **Attribute** tab, as shown in hello following screenshot.</span></span> <span data-ttu-id="a6b89-164">integración de Hello funciona sólo después de haber completado correctamente la asignación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a6b89-164">hello integration works only after you've completed hello mapping correctly.</span></span>
    
    ![cuadro de diálogo de atributos de usuario de Hola](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. <span data-ttu-id="a6b89-166">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a6b89-166">Click **Save**.</span></span>

    ![Hola configurar inicio de sesión único botón Guardar](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a6b89-168">Hola tooopen **configurar inicio de sesión** ventana, en **configuración de la empresa de encuesta de IBM Kenexa**, haga clic en **configurar IBM Kenexa encuesta Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="a6b89-168">tooopen hello **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![vínculo de Hello configurar IBM Kenexa encuesta Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="a6b89-170">Hola copia **dirección URL de cierre de sesión**, **Id. de entidad SAML**, y **SAML single sign-on dirección URL del servicio** valores de hello **referencia rápida** sección.</span><span class="sxs-lookup"><span data-stu-id="a6b89-170">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from hello **Quick Reference** section.</span></span>

8. <span data-ttu-id="a6b89-171">Hola **configurar inicio de sesión** ventana, en **referencia rápida**, Hola copia **dirección URL de cierre de sesión**, **Id. de entidad SAML**, y  **SAML single sign-on dirección URL del servicio** valores.</span><span class="sxs-lookup"><span data-stu-id="a6b89-171">In hello **Configure sign-on** window, under **Quick Reference**, copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="a6b89-172">tooconfigure SSO en hello **IBM Kenexa encuesta Enterprise** cara, enviar Hola descargado **certificado (Base64)**, **dirección URL de cierre de sesión**, **Id. de entidad SAML**, y **SAML single sign-on dirección URL del servicio** valores toohello [equipo de soporte técnico de IBM Kenexa encuesta Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="a6b89-172">tooconfigure SSO on hello **IBM Kenexa Survey Enterprise** side, send hello downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values toohello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="a6b89-173">Se puede hacer referencia tooa versión concisa de estas instrucciones en hello [portal de Azure](https://portal.azure.com) mientras está configurando la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a6b89-173">You can refer tooa concise version of these instructions in hello [Azure portal](https://portal.azure.com) while you are setting up hello app.</span></span> <span data-ttu-id="a6b89-174">Después de Agregar aplicación hello de hello **Active Directory** > **aplicaciones empresariales** sección, simplemente haga clic en hello **inicio de sesión único** ficha y, a continuación, obtener acceso a Hola incrustado documentación a través de hello **configuración** sección Hola final.</span><span class="sxs-lookup"><span data-stu-id="a6b89-174">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, simply click hello **single sign-on** tab, and then access hello embedded documentation through hello **Configuration** section at hello end.</span></span> <span data-ttu-id="a6b89-175">toolearn más información acerca de la característica de documentación de embedded hello, consulte [Azure AD incrustado documentación](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a6b89-175">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a6b89-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6b89-176">Create an Azure AD test user</span></span>
<span data-ttu-id="a6b89-177">En esta sección, para crear el usuario de prueba Britta Simon Hola portal de Azure, llevando a cabo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="a6b89-177">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![Creación de un usuario de prueba de Azure AD][100]

1. <span data-ttu-id="a6b89-179">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="a6b89-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a6b89-181">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a6b89-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a6b89-183">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a6b89-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![botón de agregar Hola](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a6b89-185">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a6b89-185">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a6b89-187">a.</span><span class="sxs-lookup"><span data-stu-id="a6b89-187">a.</span></span> <span data-ttu-id="a6b89-188">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a6b89-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a6b89-189">b.</span><span class="sxs-lookup"><span data-stu-id="a6b89-189">b.</span></span> <span data-ttu-id="a6b89-190">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6b89-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="a6b89-191">c.</span><span class="sxs-lookup"><span data-stu-id="a6b89-191">c.</span></span> <span data-ttu-id="a6b89-192">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="a6b89-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="a6b89-193">d.</span><span class="sxs-lookup"><span data-stu-id="a6b89-193">d.</span></span> <span data-ttu-id="a6b89-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a6b89-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="a6b89-195">Creación de un usuario de prueba de IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="a6b89-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="a6b89-196">En esta sección, creará un usuario llamado Britta Simon en IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a6b89-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="a6b89-197">los usuarios de toocreate en Hola sistema IBM Kenexa encuesta Enterprise y mapa Hola Id. de SSO para ellos, puede trabajar con hello [equipo de soporte técnico de IBM Kenexa encuesta Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="a6b89-197">toocreate users in hello IBM Kenexa Survey Enterprise system and map hello SSO ID for them, you can work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="a6b89-198">Este valor de Id. de SSO también debe estar asignado el valor de identificador de usuario toohello de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6b89-198">This SSO ID value should also be mapped toohello user identifier value from Azure AD.</span></span> <span data-ttu-id="a6b89-199">Puede cambiar esta configuración predeterminada en hello **atributo** ficha.</span><span class="sxs-lookup"><span data-stu-id="a6b89-199">You can change this default setting on hello **Attribute** tab.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a6b89-200">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6b89-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a6b89-201">En esta sección, se habilita a usuario Britta Simon toouse Azure SSO concediendo acceso tooIBM Kenexa encuesta Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a6b89-201">In this section, you enable user Britta Simon toouse Azure SSO by granting access tooIBM Kenexa Survey Enterprise.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="a6b89-203">usuario tooassign Britta Simon tooIBM Kenexa encuesta Enterprise, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="a6b89-203">tooassign user Britta Simon tooIBM Kenexa Survey Enterprise, do hello following:</span></span>

1. <span data-ttu-id="a6b89-204">Hola portal de Azure, abra hello **aplicaciones** ver, vaya toohello **directorio** visualizarla, seleccione **aplicaciones empresariales**y, a continuación, haga clic en **todos los aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a6b89-204">In hello Azure portal, open hello **Applications** view, go toohello **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![Hola "Aplicaciones empresariales" y los vínculos de "Todas las aplicaciones"][201] 

2. <span data-ttu-id="a6b89-206">Hola **aplicaciones** lista, seleccione **IBM Kenexa encuesta Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="a6b89-206">In hello **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![vínculo de IBM Kenexa encuesta Enterprise Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="a6b89-208">En el panel izquierdo de hello, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a6b89-208">In hello left pane, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. <span data-ttu-id="a6b89-210">Haga clic en hello **agregar** botón y, a continuación, en hello **Agregar asignación** panel, seleccione **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a6b89-210">Click hello **Add** button and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="a6b89-212">Hola **usuarios y grupos** cuadro de diálogo hello **usuarios** lista, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a6b89-212">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="a6b89-213">Hola **usuarios y grupos** diálogo cuadro, haga clic en hello **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="a6b89-213">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="a6b89-214">Hola **Agregar asignación** diálogo cuadro, haga clic en hello **asignar** botón.</span><span class="sxs-lookup"><span data-stu-id="a6b89-214">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a6b89-215">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="a6b89-215">Test single sign-on</span></span>

<span data-ttu-id="a6b89-216">En esta sección, probará la configuración de SSO de Azure AD mediante el uso de hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a6b89-216">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="a6b89-217">Al hacer clic en hello **IBM Kenexa encuesta Enterprise** Hola de mosaico en el Panel de acceso, debe iniciar sesión automáticamente en tooyour aplicación empresarial de encuesta de Kenexa de IBM.</span><span class="sxs-lookup"><span data-stu-id="a6b89-217">When you click hello **IBM Kenexa Survey Enterprise** tile in hello Access Panel, you should be automatically signed in tooyour IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a6b89-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a6b89-218">Additional resources</span></span>

* [<span data-ttu-id="a6b89-219">Lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6b89-219">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a6b89-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a6b89-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 

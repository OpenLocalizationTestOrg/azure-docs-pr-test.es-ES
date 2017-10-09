---
title: "Tutorial: Integración de Azure Active Directory con Symantec Web Security Service (WSS) | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el servicio de seguridad de Web (WSS) de Symantec."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="39788-103">Tutorial: Integración de Azure Active Directory con Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="39788-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="39788-104">En este tutorial, obtendrá información sobre cómo toointegrate su servicio de seguridad de Web de Symantec (WSS) cuenta con su cuenta de Azure Active Directory (Azure AD) para que WSS puede autenticar un usuario final que se aprovisiona en hello Azure AD mediante la autenticación de SAML y aplicar el usuario o reglas de nivel de directiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="39788-104">In this tutorial, you will learn how toointegrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in hello Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="39788-105">Integración de servicios de seguridad Web de Symantec (WSS) con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="39788-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="39788-106">Administre todos los usuarios finales de Hola y grupos usados por su cuenta WSS desde el portal de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39788-106">Manage all of hello end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="39788-107">Permitir tooauthenticate de los usuarios finales de Hola a sí mismos en WSS con sus credenciales de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39788-107">Allow hello end users tooauthenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="39788-108">Activar aplicación Hola a nivel de usuario y grupo de reglas de nivel de directiva definidas en su cuenta WSS.</span><span class="sxs-lookup"><span data-stu-id="39788-108">Enable hello enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="39788-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="39788-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39788-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="39788-110">Prerequisites</span></span>

<span data-ttu-id="39788-111">tooconfigure integración de Azure AD con el servicio de seguridad Web de Symantec (WSS), necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="39788-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="39788-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="39788-112">An Azure AD subscription</span></span>
- <span data-ttu-id="39788-113">Una cuenta de Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="39788-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="39788-114">Hola tootest los pasos de este tutorial, no se recomienda con una cuenta WSS que se está usando actualmente para el propósito de producción.</span><span class="sxs-lookup"><span data-stu-id="39788-114">tootest hello steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="39788-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="39788-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="39788-116">No use una cuenta de WSS que se esté usando actualmente en producción para esta prueba a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="39788-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="39788-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="39788-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="39788-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="39788-118">Scenario description</span></span>
<span data-ttu-id="39788-119">En este tutorial, va a configurar su Azure AD tooenable único inicio de sesión tooWSS con credenciales de usuario final de hello definidas en su cuenta de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39788-119">In this tutorial, you will configure your Azure AD tooenable single sign-on tooWSS using hello end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="39788-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="39788-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="39788-121">Agregar aplicación de servicio de seguridad de Web (WSS) de Symantec hello desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="39788-121">Adding hello Symantec Web Security Service (WSS) app from hello gallery</span></span>
2. <span data-ttu-id="39788-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="39788-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="39788-123">Agregar servicio de seguridad de Web de Symantec (WSS) desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="39788-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="39788-124">integración de hello tooconfigure de Symantec Web seguridad Service (WSS) en Azure AD, deberá tooadd Symantec Web seguridad Service (WSS) de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="39788-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="39788-125">**tooadd Symantec Web seguridad Service (WSS) de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="39788-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="39788-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="39788-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="39788-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="39788-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="39788-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="39788-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="39788-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="39788-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="39788-133">En el cuadro de búsqueda de hello, escriba **Symantec Web seguridad Service (WSS)**, seleccione **Symantec Web seguridad Service (WSS)** desde el panel de resultados, a continuación, haga clic en **agregar** hello tooadd de botón aplicación.</span><span class="sxs-lookup"><span data-stu-id="39788-133">In hello search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Servicio de seguridad Web de Symantec (WSS) en la lista de resultados de Hola](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="39788-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="39788-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="39788-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Symantec Web Security Service (WSS) con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="39788-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="39788-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el servicio de seguridad Web de Symantec (WSS) es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39788-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="39788-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el servicio de seguridad Web de Symantec (WSS) debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="39788-138">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="39788-139">En el servicio de seguridad de Web de Symantec (WSS), asignar un valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="39788-139">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="39788-140">tooconfigure y prueba de inicio de sesión único en Azure AD con el servicio de seguridad Web de Symantec (WSS), deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="39788-140">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="39788-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="39788-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="39788-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39788-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="39788-143">**[Crear un usuario de prueba de servicio de seguridad de Web (WSS) de Symantec](#create-a-symantec-web-security-service-wss-test-user)**  -toohave un equivalente de Britta Simon en Symantec Web seguridad Service (WSS) que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="39788-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="39788-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="39788-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="39788-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="39788-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="39788-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="39788-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="39788-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de servicio de seguridad de Web (WSS) de Symantec.</span><span class="sxs-lookup"><span data-stu-id="39788-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="39788-148">**tooconfigure inicio de sesión único en Azure AD con el servicio de seguridad de Web de Symantec (WSS), lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="39788-148">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="39788-149">En el portal de Azure, en Hola Hola **Symantec Web seguridad Service (WSS)** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="39788-149">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="39788-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="39788-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="39788-153">En hello **dominio del servicio (WSS) de seguridad de Web de Symantec y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="39788-153">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Symantec Web Security Service (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="39788-155">a.</span><span class="sxs-lookup"><span data-stu-id="39788-155">a.</span></span> <span data-ttu-id="39788-156">Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="39788-156">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="39788-157">b.</span><span class="sxs-lookup"><span data-stu-id="39788-157">b.</span></span> <span data-ttu-id="39788-158">Hola **dirección URL de respuesta** cuadro de texto, escriba la dirección URL hello:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="39788-158">In hello **Reply URL** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="39788-159">Póngase en contacto con hello [equipo de soporte técnico de cliente de servicio de seguridad de Web (WSS) de Symantec](https://www.symantec.com/contact-us) si Hola valores de hello **identificador** y **dirección URL de respuesta** por algún motivo no funcionan.</span><span class="sxs-lookup"><span data-stu-id="39788-159">Please contact hello [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if hello values for hello **Identifier** and **Reply URL** are not working for some reason.</span></span>

4. <span data-ttu-id="39788-160">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="39788-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="39788-162">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="39788-162">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="39788-164">tooconfigure inicio de sesión único en hello lado de servicio de seguridad de Web (WSS) de Symantec, consulte la documentación en línea del toohello WSS.</span><span class="sxs-lookup"><span data-stu-id="39788-164">tooconfigure single sign-on on hello Symantec Web Security Service (WSS) side, refer toohello WSS online documentation.</span></span> <span data-ttu-id="39788-165">Hola descargado **Metadata XML** archivo deberá toobe importado en el portal WSS Hola.</span><span class="sxs-lookup"><span data-stu-id="39788-165">hello downloaded **Metadata XML** file will need toobe imported into hello WSS portal.</span></span> <span data-ttu-id="39788-166">Póngase en contacto con hello [equipo de soporte técnico de Symantec Web seguridad Service (WSS)](https://www.symantec.com/contact-us) si necesita ayuda con la configuración de hello en el portal WSS Hola.</span><span class="sxs-lookup"><span data-stu-id="39788-166">Contact hello [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with hello configuration on hello WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="39788-167">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="39788-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="39788-168">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="39788-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="39788-169">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="39788-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="39788-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="39788-170">Create an Azure AD test user</span></span>

<span data-ttu-id="39788-171">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="39788-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="39788-173">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="39788-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="39788-174">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="39788-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="39788-176">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="39788-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="39788-178">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="39788-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="39788-180">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="39788-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="39788-182">a.</span><span class="sxs-lookup"><span data-stu-id="39788-182">a.</span></span> <span data-ttu-id="39788-183">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="39788-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="39788-184">b.</span><span class="sxs-lookup"><span data-stu-id="39788-184">b.</span></span> <span data-ttu-id="39788-185">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39788-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="39788-186">c.</span><span class="sxs-lookup"><span data-stu-id="39788-186">c.</span></span> <span data-ttu-id="39788-187">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="39788-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="39788-188">d.</span><span class="sxs-lookup"><span data-stu-id="39788-188">d.</span></span> <span data-ttu-id="39788-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="39788-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="39788-190">Creación de un usuario de prueba de Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="39788-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="39788-191">En esta sección, creará un usuario llamado Britta Simon en Symantec Web Security Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="39788-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="39788-192">el nombre de usuario de Hello correspondiente final puede crearse manualmente en el portal WSS de Hola o puede esperar a que los usuarios o grupos de hello aprovisionados en hello Azure AD toobe sincronizado toohello WSS portal después de unos minutos (unos 15 minutos).</span><span class="sxs-lookup"><span data-stu-id="39788-192">hello corresponding end username can be manually created in hello WSS portal or you can wait for hello users/groups provisioned in hello Azure AD toobe synchronized toohello WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="39788-193">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="39788-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="39788-194">dirección IP pública de Hello del equipo del usuario final de hello, que será sitios Web toobrowse usado también necesita toobe aprovisionado en el portal de servicio de seguridad de Web (WSS) de Symantec Hola.</span><span class="sxs-lookup"><span data-stu-id="39788-194">hello public IP address of hello end user machine, which will be used toobrowse websites also need toobe provisioned in hello Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="39788-195">Por favor, [haga clic aquí](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget su equipo público de dirección IP.</span><span class="sxs-lookup"><span data-stu-id="39788-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="39788-196">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="39788-196">Assign hello Azure AD test user</span></span>

<span data-ttu-id="39788-197">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSymantec Web seguridad Service (WSS).</span><span class="sxs-lookup"><span data-stu-id="39788-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="39788-199">**tooassign Britta Simon tooSymantec Web seguridad Service (WSS), lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="39788-199">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="39788-200">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="39788-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="39788-202">En la lista de aplicaciones de hello, seleccione **Symantec Web seguridad Service (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="39788-202">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![vínculo de servicio de seguridad de Web (WSS) de Symantec Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. <span data-ttu-id="39788-204">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="39788-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="39788-206">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="39788-206">Click **Add** button.</span></span> <span data-ttu-id="39788-207">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="39788-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="39788-209">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="39788-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="39788-210">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="39788-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="39788-211">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="39788-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="39788-212">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="39788-212">Test single sign-on</span></span>

<span data-ttu-id="39788-213">En esta sección, probará funcionalidad de inicio de sesión único de hello ahora que ha configurado su toouse de cuenta WSS Azure AD para la autenticación de SAML.</span><span class="sxs-lookup"><span data-stu-id="39788-213">In this section, you'll test hello single sign-on functionality now that you've configured your WSS account toouse your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="39788-214">Después de haber configurado el tráfico de tooproxy de explorador web tooWSS, cuando abra el explorador web e intente toobrowse tooa sitio, a continuación, se va a ser redirigido toohello el inicio de sesión Azure página.</span><span class="sxs-lookup"><span data-stu-id="39788-214">After you have configured your web browser tooproxy traffic tooWSS, when you open your web browser and try toobrowse tooa site then you'll be redirected toohello Azure sign-on page.</span></span> <span data-ttu-id="39788-215">Especifique credenciales Hola Hola prueba final del usuario de que se ha aprovisionado en hello Azure AD (es decir, BrittaSimon) y los asociados de contraseña.</span><span class="sxs-lookup"><span data-stu-id="39788-215">Enter hello credentials of hello test end user that has been provisioned in hello Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="39788-216">Una vez autenticado, podrá toobrowse capaz de sitio Web de toohello que eligió.</span><span class="sxs-lookup"><span data-stu-id="39788-216">Once authenticated, you'll be able toobrowse toohello website that you chose.</span></span> <span data-ttu-id="39788-217">Debe crear una regla de directiva en hello WSS lado tooblock BrittaSimon del examen tooa sitio en particular, a continuación, debería ver Hola WSS bloquear página cuando intente toobrowse toothat sitio como usuario BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="39788-217">Should you create a policy rule on hello WSS side tooblock BrittaSimon from browsing tooa particular site then you should see hello WSS block page when you attempt toobrowse toothat site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="39788-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="39788-218">Additional resources</span></span>

* [<span data-ttu-id="39788-219">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39788-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="39788-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="39788-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png


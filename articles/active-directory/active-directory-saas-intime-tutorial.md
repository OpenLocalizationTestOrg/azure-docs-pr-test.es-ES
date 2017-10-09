---
title: "Tutorial: integración de Azure Active Directory con InTime | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y InTime."
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
ms.openlocfilehash: 63652f0f098aeac95e89a2500b46a18440e34698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intime"></a><span data-ttu-id="53f29-103">Tutorial: integración de Azure Active Directory con InTime</span><span class="sxs-lookup"><span data-stu-id="53f29-103">Tutorial: Azure Active Directory integration with InTime</span></span>

<span data-ttu-id="53f29-104">En este tutorial, aprenderá cómo toointegrate InTime con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="53f29-104">In this tutorial, you learn how toointegrate InTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="53f29-105">Integración InTime con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="53f29-105">Integrating InTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="53f29-106">Puede controlar en Azure AD que tenga acceso tooInTime.</span><span class="sxs-lookup"><span data-stu-id="53f29-106">You can control in Azure AD who has access tooInTime.</span></span>
- <span data-ttu-id="53f29-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooInTime (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53f29-107">You can enable your users tooautomatically get signed-on tooInTime (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="53f29-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="53f29-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="53f29-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="53f29-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53f29-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="53f29-110">Prerequisites</span></span>

<span data-ttu-id="53f29-111">integración de Azure AD con InTime tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="53f29-111">tooconfigure Azure AD integration with InTime, you need hello following items:</span></span>

- <span data-ttu-id="53f29-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="53f29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="53f29-113">Una suscripción habilitada para el inicio de sesión único en InTime</span><span class="sxs-lookup"><span data-stu-id="53f29-113">A InTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="53f29-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="53f29-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="53f29-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="53f29-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="53f29-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="53f29-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="53f29-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="53f29-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="53f29-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="53f29-118">Scenario description</span></span>
<span data-ttu-id="53f29-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="53f29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="53f29-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="53f29-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="53f29-121">Agregar InTime desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="53f29-121">Adding InTime from hello gallery</span></span>
2. <span data-ttu-id="53f29-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="53f29-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intime-from-hello-gallery"></a><span data-ttu-id="53f29-123">Agregar InTime desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="53f29-123">Adding InTime from hello gallery</span></span>
<span data-ttu-id="53f29-124">integración de hello tooconfigure de InTime en Azure AD, deberá tooadd InTime de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="53f29-124">tooconfigure hello integration of InTime into Azure AD, you need tooadd InTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="53f29-125">**tooadd InTime desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="53f29-125">**tooadd InTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="53f29-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="53f29-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="53f29-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="53f29-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="53f29-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="53f29-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="53f29-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="53f29-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="53f29-133">En el cuadro de búsqueda de hello, escriba **InTime**, seleccione **InTime** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="53f29-133">In hello search box, type **InTime**, select **InTime** from result panel then click **Add** button tooadd hello application.</span></span>

    ![InTime en la lista de resultados de Hola](./media/active-directory-saas-intime-tutorial/tutorial_intime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="53f29-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="53f29-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="53f29-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con InTime con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="53f29-136">In this section, you configure and test Azure AD single sign-on with InTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="53f29-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en InTime es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53f29-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in InTime is tooa user in Azure AD.</span></span> <span data-ttu-id="53f29-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en InTime debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="53f29-138">In other words, a link relationship between an Azure AD user and hello related user in InTime needs toobe established.</span></span>

<span data-ttu-id="53f29-139">En InTime, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="53f29-139">In InTime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="53f29-140">tooconfigure y prueba de inicio de sesión único en Azure AD con InTime, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="53f29-140">tooconfigure and test Azure AD single sign-on with InTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="53f29-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="53f29-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="53f29-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="53f29-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="53f29-143">**[Crear un usuario de prueba InTime](#create-a-intime-test-user)**  -toohave un equivalente de Britta Simon en InTime que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="53f29-143">**[Create a InTime test user](#create-a-intime-test-user)** - toohave a counterpart of Britta Simon in InTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="53f29-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="53f29-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="53f29-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="53f29-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="53f29-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="53f29-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="53f29-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación InTime.</span><span class="sxs-lookup"><span data-stu-id="53f29-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your InTime application.</span></span>

<span data-ttu-id="53f29-148">**inicio de sesión único en Azure AD tooconfigure con InTime, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="53f29-148">**tooconfigure Azure AD single sign-on with InTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="53f29-149">En el portal de Azure, en Hola Hola **InTime** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="53f29-149">In hello Azure portal, on hello **InTime** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="53f29-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="53f29-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-intime-tutorial/tutorial_intime_samlbase.png)

3. <span data-ttu-id="53f29-153">En hello **InTime dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="53f29-153">On hello **InTime Domain and URLs** section, perform hello following steps:</span></span>

    ![Información sobre dominio y direcciones URL de inicio de sesión único de InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_url.png)

    <span data-ttu-id="53f29-155">a.</span><span class="sxs-lookup"><span data-stu-id="53f29-155">a.</span></span> <span data-ttu-id="53f29-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:`https://intime6.intimesoft.com/mytime/login/login.xhtml`</span><span class="sxs-lookup"><span data-stu-id="53f29-156">In hello **Sign-on URL** textbox, type hello URL: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span></span>

    <span data-ttu-id="53f29-157">b.</span><span class="sxs-lookup"><span data-stu-id="53f29-157">b.</span></span> <span data-ttu-id="53f29-158">Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://auth.intimesoft.com/auth/realms/master`</span><span class="sxs-lookup"><span data-stu-id="53f29-158">In hello **Identifier** textbox, type hello URL: `https://auth.intimesoft.com/auth/realms/master`</span></span>

4. <span data-ttu-id="53f29-159">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="53f29-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-intime-tutorial/tutorial_intime_certificate.png) 

5. <span data-ttu-id="53f29-161">La aplicación InTime espera las aserciones de SAML de hello en un formato específico, lo que requiere tooadd atributo personalizado tooyour SAML atributos de token configuración de asignaciones.</span><span class="sxs-lookup"><span data-stu-id="53f29-161">Your InTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="53f29-162">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="53f29-162">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="53f29-163">Hola valor predeterminado de **identificador de usuario** es **user.userprincipalname** pero InTime espera este toobe asignado con la dirección de correo electrónico del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="53f29-163">hello default value of **User Identifier** is **user.userprincipalname** but InTime expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="53f29-164">Para que puede usar **user.mail** de atributo de la lista de Hola o usar el valor de atributo apropiado de hello según la configuración de la organización</span><span class="sxs-lookup"><span data-stu-id="53f29-164">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration</span></span> 

    ![Configuración del Atributo](./media/active-directory-saas-intime-tutorial/tutorial_intime_attribute.png)

6. <span data-ttu-id="53f29-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="53f29-166">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-intime-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="53f29-168">En hello **configuración InTime** sección, haga clic en **configurar InTime** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="53f29-168">On hello **InTime Configuration** section, click **Configure InTime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="53f29-169">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="53f29-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_configure.png) 

8. <span data-ttu-id="53f29-171">tooconfigure inicio de sesión único en **InTime** lado, necesita hello toosend descargado **Metadata XML**, **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** demasiado[Equipo de soporte técnico inTime](mailto:hdollard@intimesoft.com).</span><span class="sxs-lookup"><span data-stu-id="53f29-171">tooconfigure single sign-on on **InTime** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, and SAML Single Sign-On Service URL** too[InTime support team](mailto:hdollard@intimesoft.com).</span></span> <span data-ttu-id="53f29-172">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="53f29-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="53f29-173">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="53f29-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="53f29-174">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="53f29-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="53f29-175">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="53f29-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="53f29-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="53f29-176">Create an Azure AD test user</span></span>

<span data-ttu-id="53f29-177">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="53f29-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="53f29-179">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="53f29-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="53f29-180">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="53f29-180">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-intime-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="53f29-182">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="53f29-182">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-intime-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="53f29-184">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="53f29-184">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-intime-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="53f29-186">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="53f29-186">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-intime-tutorial/create_aaduser_04.png)

    <span data-ttu-id="53f29-188">a.</span><span class="sxs-lookup"><span data-stu-id="53f29-188">a.</span></span> <span data-ttu-id="53f29-189">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="53f29-189">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="53f29-190">b.</span><span class="sxs-lookup"><span data-stu-id="53f29-190">b.</span></span> <span data-ttu-id="53f29-191">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="53f29-191">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="53f29-192">c.</span><span class="sxs-lookup"><span data-stu-id="53f29-192">c.</span></span> <span data-ttu-id="53f29-193">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="53f29-193">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="53f29-194">d.</span><span class="sxs-lookup"><span data-stu-id="53f29-194">d.</span></span> <span data-ttu-id="53f29-195">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="53f29-195">Click **Create**.</span></span>
 
### <a name="create-a-intime-test-user"></a><span data-ttu-id="53f29-196">Creación de un usuario de prueba de InTime</span><span class="sxs-lookup"><span data-stu-id="53f29-196">Create a InTime test user</span></span>

<span data-ttu-id="53f29-197">En esta sección, creará un usuario llamado Britta Simon en InTime.</span><span class="sxs-lookup"><span data-stu-id="53f29-197">In this section, you create a user called Britta Simon in InTime.</span></span> <span data-ttu-id="53f29-198">Trabajar con [equipo de soporte técnico InTime](mailto:hdollard@intimesoft.com) a los usuarios de tooadd hello en plataforma InTime Hola.</span><span class="sxs-lookup"><span data-stu-id="53f29-198">Work with [InTime support team](mailto:hdollard@intimesoft.com) tooadd hello users in hello InTime platform.</span></span> <span data-ttu-id="53f29-199">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="53f29-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="53f29-200">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="53f29-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="53f29-201">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooInTime.</span><span class="sxs-lookup"><span data-stu-id="53f29-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInTime.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="53f29-203">**tooassign Britta Simon tooInTime, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="53f29-203">**tooassign Britta Simon tooInTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="53f29-204">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="53f29-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="53f29-206">En la lista de aplicaciones de hello, seleccione **InTime**.</span><span class="sxs-lookup"><span data-stu-id="53f29-206">In hello applications list, select **InTime**.</span></span>

    ![Hola InTime vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-intime-tutorial/tutorial_intime_app.png)  

3. <span data-ttu-id="53f29-208">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="53f29-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="53f29-210">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="53f29-210">Click **Add** button.</span></span> <span data-ttu-id="53f29-211">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="53f29-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="53f29-213">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="53f29-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="53f29-214">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="53f29-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="53f29-215">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="53f29-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="53f29-216">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="53f29-216">Test single sign-on</span></span>

<span data-ttu-id="53f29-217">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="53f29-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="53f29-218">Al hacer clic en icono InTime hello en Hola Panel de acceso, deberá obtener la página de inicio de sesión de saludo de la aplicación InTime.</span><span class="sxs-lookup"><span data-stu-id="53f29-218">When you click hello InTime tile in hello Access Panel, you should get hello login page of your InTime application.</span></span> <span data-ttu-id="53f29-219">Haga clic en hello **inicio de sesión** botón, se mostrará una serie de IdPs en una lista de botones.</span><span class="sxs-lookup"><span data-stu-id="53f29-219">Click hello **Login** button, then a series of IdPs will be displayed on a list of buttons.</span></span> <span data-ttu-id="53f29-220">Haga clic en **nombre IDP** proporcionado por [equipo de soporte técnico InTime](mailto:hdollard@intimesoft.com) toologin en la aplicación InTime.</span><span class="sxs-lookup"><span data-stu-id="53f29-220">click **IDP name** given by [InTime support team](mailto:hdollard@intimesoft.com) toologin into your InTime application.</span></span> <span data-ttu-id="53f29-221">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="53f29-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="53f29-222">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="53f29-222">Additional resources</span></span>

* [<span data-ttu-id="53f29-223">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53f29-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="53f29-224">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="53f29-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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


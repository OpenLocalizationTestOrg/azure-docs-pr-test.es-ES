---
title: "Tutorial: Integración de Azure Active Directory con 23 Video | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y vídeo 23."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 3430e4db3cd1114db62233e6699618071a3646ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="83c2b-103">Tutorial: Integración de Azure Active Directory con 23 Video</span><span class="sxs-lookup"><span data-stu-id="83c2b-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>

<span data-ttu-id="83c2b-104">En este tutorial, aprenderá cómo toointegrate 23 vídeo con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="83c2b-104">In this tutorial, you learn how toointegrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83c2b-105">Integración de 23 vídeo con Azure AD proporciona con hello siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="83c2b-105">Integrating 23 Video with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="83c2b-106">Puede controlar en Azure AD que tenga acceso too23 vídeo</span><span class="sxs-lookup"><span data-stu-id="83c2b-106">You can control in Azure AD who has access too23 Video</span></span>
- <span data-ttu-id="83c2b-107">Puede permitir a los usuarios obtener tooautomatically ha iniciado sesión con vídeo too23 (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="83c2b-107">You can enable your users tooautomatically get signed-on too23 Video (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="83c2b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="83c2b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="83c2b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="83c2b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83c2b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="83c2b-110">Prerequisites</span></span>

<span data-ttu-id="83c2b-111">integración de Azure AD con vídeo 23 tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="83c2b-111">tooconfigure Azure AD integration with 23 Video, you need hello following items:</span></span>

- <span data-ttu-id="83c2b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="83c2b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="83c2b-113">Una suscripción habilitada para inicio de sesión único en 23 Video</span><span class="sxs-lookup"><span data-stu-id="83c2b-113">A 23 Video single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83c2b-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="83c2b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="83c2b-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="83c2b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="83c2b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="83c2b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="83c2b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83c2b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83c2b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="83c2b-118">Scenario description</span></span>
<span data-ttu-id="83c2b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="83c2b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="83c2b-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="83c2b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83c2b-121">Agregar vídeo 23 de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="83c2b-121">Adding 23 Video from hello gallery</span></span>
2. <span data-ttu-id="83c2b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="83c2b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-23-video-from-hello-gallery"></a><span data-ttu-id="83c2b-123">Agregar vídeo 23 de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="83c2b-123">Adding 23 Video from hello gallery</span></span>
<span data-ttu-id="83c2b-124">integración de hello tooconfigure de vídeo 23 en Azure AD, necesita tooadd 23 vídeo desde la lista de tooyour de hello Galería de aplicaciones de SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="83c2b-124">tooconfigure hello integration of 23 Video into Azure AD, you need tooadd 23 Video from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="83c2b-125">**tooadd 23 vídeo desde la Galería de hello, realizar Hola lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="83c2b-125">**tooadd 23 Video from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="83c2b-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="83c2b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="83c2b-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="83c2b-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="83c2b-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="83c2b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="83c2b-133">En el cuadro de búsqueda de hello, escriba **vídeo 23**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-133">In hello search box, type **23 Video**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_search.png)

5. <span data-ttu-id="83c2b-135">En el panel de resultados de hello, seleccione **vídeo 23**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="83c2b-135">In hello results panel, select **23 Video**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="83c2b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="83c2b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="83c2b-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con 23 Video con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="83c2b-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="83c2b-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en vídeo 23 es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83c2b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 23 Video is tooa user in Azure AD.</span></span> <span data-ttu-id="83c2b-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en 23 Video requiere toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="83c2b-140">In other words, a link relationship between an Azure AD user and hello related user in 23 Video needs toobe established.</span></span>

<span data-ttu-id="83c2b-141">En vídeo 23, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="83c2b-141">In 23 Video, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="83c2b-142">tooconfigure y prueba de inicio de sesión único en Azure AD con vídeo 23, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="83c2b-142">tooconfigure and test Azure AD single sign-on with 23 Video, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="83c2b-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="83c2b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="83c2b-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83c2b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83c2b-145">**[Crear un usuario de prueba de vídeo 23](#creating-a-23-video-test-user)**  -toohave un equivalente de Britta Simon en vídeo 23 que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="83c2b-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - toohave a counterpart of Britta Simon in 23 Video that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="83c2b-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="83c2b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83c2b-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="83c2b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="83c2b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="83c2b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="83c2b-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de vídeo 23.</span><span class="sxs-lookup"><span data-stu-id="83c2b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 23 Video application.</span></span>

<span data-ttu-id="83c2b-150">**inicio de sesión único en tooconfigure Azure AD con vídeo 23, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="83c2b-150">**tooconfigure Azure AD single sign-on with 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="83c2b-151">En el portal de Azure, en Hola Hola **vídeo 23** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-151">In hello Azure portal, on hello **23 Video** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="83c2b-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="83c2b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-23video-tutorial/tutorial_23video_samlbase.png)

3. <span data-ttu-id="83c2b-155">En hello **23 vídeo dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="83c2b-155">On hello **23 Video Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-23video-tutorial/tutorial_23video_url.png)

    <span data-ttu-id="83c2b-157">a.</span><span class="sxs-lookup"><span data-stu-id="83c2b-157">a.</span></span> <span data-ttu-id="83c2b-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.23video.com`</span><span class="sxs-lookup"><span data-stu-id="83c2b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.23video.com`</span></span>

    <span data-ttu-id="83c2b-159">b.</span><span class="sxs-lookup"><span data-stu-id="83c2b-159">b.</span></span> <span data-ttu-id="83c2b-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.23video.com/saml/trust/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="83c2b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="83c2b-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="83c2b-161">These values are not real.</span></span> <span data-ttu-id="83c2b-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="83c2b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="83c2b-163">Póngase en contacto con [equipo de soporte técnico de cliente de vídeo 23](mailto:support@23company.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="83c2b-163">Contact [23 Video Client support team](mailto:support@23company.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="83c2b-164">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="83c2b-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-23video-tutorial/tutorial_23video_certificate.png) 

5. <span data-ttu-id="83c2b-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="83c2b-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-23video-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="83c2b-168">En hello **configuración de vídeo 23** sección, haga clic en **configurar vídeo de 23** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="83c2b-168">On hello **23 Video Configuration** section, click **Configure 23 Video** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="83c2b-169">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="83c2b-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-23video-tutorial/tutorial_23video_configure.png) 

7. <span data-ttu-id="83c2b-171">tooconfigure inicio de sesión único en **vídeo 23** lado, necesita hello toosend descargado **certificado (Base64)**, **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio**demasiado[equipo de soporte técnico de vídeo 23](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="83c2b-171">tooconfigure single sign-on on **23 Video** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[23 Video support team](mailto:support@23company.com).</span></span> 


> [!TIP]
> <span data-ttu-id="83c2b-172">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="83c2b-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="83c2b-173">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="83c2b-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="83c2b-174">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="83c2b-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="83c2b-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="83c2b-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="83c2b-176">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="83c2b-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="83c2b-178">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="83c2b-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="83c2b-179">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="83c2b-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="83c2b-181">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="83c2b-183">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="83c2b-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="83c2b-185">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="83c2b-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="83c2b-187">a.</span><span class="sxs-lookup"><span data-stu-id="83c2b-187">a.</span></span> <span data-ttu-id="83c2b-188">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="83c2b-189">b.</span><span class="sxs-lookup"><span data-stu-id="83c2b-189">b.</span></span> <span data-ttu-id="83c2b-190">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="83c2b-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="83c2b-191">c.</span><span class="sxs-lookup"><span data-stu-id="83c2b-191">c.</span></span> <span data-ttu-id="83c2b-192">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="83c2b-193">d.</span><span class="sxs-lookup"><span data-stu-id="83c2b-193">d.</span></span> <span data-ttu-id="83c2b-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-194">Click **Create**.</span></span>
 
### <a name="creating-a-23-video-test-user"></a><span data-ttu-id="83c2b-195">Creación de un usuario de prueba de 23 Video</span><span class="sxs-lookup"><span data-stu-id="83c2b-195">Creating a 23 Video test user</span></span>

<span data-ttu-id="83c2b-196">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en vídeo 23.</span><span class="sxs-lookup"><span data-stu-id="83c2b-196">hello objective of this section is toocreate a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="83c2b-197">**toocreate un usuario llamado Britta Simon en vídeo 23, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="83c2b-197">**toocreate a user called Britta Simon in 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="83c2b-198">Inicie sesión en tooyour sitio 23 de la compañía de vídeo como administrador.</span><span class="sxs-lookup"><span data-stu-id="83c2b-198">Sign on tooyour 23 Video company site as administrator.</span></span>

2. <span data-ttu-id="83c2b-199">Vaya demasiado**configuración**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-199">Go too**Settings**.</span></span>
 
3. <span data-ttu-id="83c2b-200">En la sección **Usuarios**, haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-200">In **Users** section, click **Configure**.</span></span>
   
    ![Asignar usuario][400]

4. <span data-ttu-id="83c2b-202">Haga clic en **Agregar un nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-202">Click **Add a new user**.</span></span> 
   
    ![Asignar usuario][401]

5. <span data-ttu-id="83c2b-204">Hola **invitar a alguien toojoin este sitio** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="83c2b-204">In hello **Invite someone toojoin this site** section, perform hello following steps:</span></span>
   
    ![Asignar usuario][402]

    <span data-ttu-id="83c2b-206">a.</span><span class="sxs-lookup"><span data-stu-id="83c2b-206">a.</span></span> <span data-ttu-id="83c2b-207">Hola **direcciones de correo electrónico** cuadro de texto, escriba la dirección de correo electrónico Britta Simon en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83c2b-207">In hello **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 
    <span data-ttu-id="83c2b-208">b.</span><span class="sxs-lookup"><span data-stu-id="83c2b-208">b.</span></span> <span data-ttu-id="83c2b-209">Haga clic en **Agregar usuario de hello**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-209">Click **Add hello user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="83c2b-210">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="83c2b-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="83c2b-211">En esta sección, se habilita las Britta Simon toouse un inicio de sesión único Azure concediendo acceso too23 vídeo.</span><span class="sxs-lookup"><span data-stu-id="83c2b-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too23 Video.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="83c2b-213">**tooassign Britta Simon too23 vídeo, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="83c2b-213">**tooassign Britta Simon too23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="83c2b-214">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="83c2b-216">En la lista de aplicaciones de hello, seleccione **vídeo 23**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-216">In hello applications list, select **23 Video**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-23video-tutorial/tutorial_23video_app.png) 

3. <span data-ttu-id="83c2b-218">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="83c2b-220">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-220">Click **Add** button.</span></span> <span data-ttu-id="83c2b-221">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="83c2b-223">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="83c2b-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="83c2b-224">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="83c2b-225">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="83c2b-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="83c2b-226">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="83c2b-226">Testing single sign-on</span></span>

<span data-ttu-id="83c2b-227">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="83c2b-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="83c2b-228">Al hacer clic en icono de vídeo de hello 23 en hello Panel de acceso, deberá obtener aplicaciones de vídeo automáticamente ha iniciado sesión tooyour 23.</span><span class="sxs-lookup"><span data-stu-id="83c2b-228">When you click hello 23 Video tile in hello Access Panel, you should get automatically signed-on tooyour 23 Video application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="83c2b-229">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="83c2b-229">Additional resources</span></span>

* [<span data-ttu-id="83c2b-230">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83c2b-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83c2b-231">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="83c2b-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-23video-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-23video-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-23video-tutorial/tutorial_general_203.png

[400]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_12.png

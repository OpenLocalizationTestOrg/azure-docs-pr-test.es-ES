---
title: "Tutorial: Integración de Azure Active Directory con Huddle | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Huddle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0b2f6c4d839943cdd07699a1ff95dc8f90505699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="d0c19-103">Tutorial: integración de Azure Active Directory con Huddle</span><span class="sxs-lookup"><span data-stu-id="d0c19-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="d0c19-104">En este tutorial, aprenderá cómo toointegrate Huddle con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0c19-104">In this tutorial, you learn how toointegrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0c19-105">Integración de Huddle con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d0c19-105">Integrating Huddle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d0c19-106">Puede controlar en Azure AD que tenga acceso tooHuddle</span><span class="sxs-lookup"><span data-stu-id="d0c19-106">You can control in Azure AD who has access tooHuddle</span></span>
- <span data-ttu-id="d0c19-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooHuddle (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0c19-107">You can enable your users tooautomatically get signed-on tooHuddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d0c19-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d0c19-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d0c19-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0c19-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0c19-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d0c19-110">Prerequisites</span></span>

<span data-ttu-id="d0c19-111">integración de Azure AD tooconfigure con Huddle, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d0c19-111">tooconfigure Azure AD integration with Huddle, you need hello following items:</span></span>

- <span data-ttu-id="d0c19-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0c19-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0c19-113">Una suscripción habilitada para el inicio de sesión único en Huddle</span><span class="sxs-lookup"><span data-stu-id="d0c19-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0c19-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d0c19-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0c19-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d0c19-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0c19-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d0c19-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0c19-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0c19-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0c19-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d0c19-118">Scenario description</span></span>

<span data-ttu-id="d0c19-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d0c19-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0c19-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="d0c19-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0c19-121">Agregar Huddle desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="d0c19-121">Adding Huddle from hello gallery</span></span>
2. <span data-ttu-id="d0c19-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0c19-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-hello-gallery"></a><span data-ttu-id="d0c19-123">Agregar Huddle desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="d0c19-123">Adding Huddle from hello gallery</span></span>
<span data-ttu-id="d0c19-124">integración de hello tooconfigure de Huddle en Azure AD, deberá tooadd Huddle de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="d0c19-124">tooconfigure hello integration of Huddle into Azure AD, you need tooadd Huddle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d0c19-125">**tooadd Huddle de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d0c19-125">**tooadd Huddle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c19-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="d0c19-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d0c19-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d0c19-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="d0c19-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d0c19-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="d0c19-133">En el cuadro de búsqueda de hello, escriba **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-133">In hello search box, type **Huddle**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="d0c19-135">En el panel de resultados de hello, seleccione **Huddle**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d0c19-135">In hello results panel, select **Huddle**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d0c19-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0c19-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="d0c19-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Huddle con un usuario de prueba llamado "Britta Simon"</span><span class="sxs-lookup"><span data-stu-id="d0c19-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d0c19-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Huddle es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0c19-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Huddle is tooa user in Azure AD.</span></span> <span data-ttu-id="d0c19-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Huddle necesidades toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="d0c19-140">In other words, a link relationship between an Azure AD user and hello related user in Huddle needs toobe established.</span></span>

<span data-ttu-id="d0c19-141">En Huddle, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0c19-141">In Huddle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d0c19-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Huddle, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d0c19-142">tooconfigure and test Azure AD single sign-on with Huddle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d0c19-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="d0c19-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>

2. <span data-ttu-id="d0c19-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0c19-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="d0c19-145">**[Crear un usuario de prueba de Huddle](#creating-a-huddle-test-user)**  -toohave un equivalente de Britta Simon en Huddle que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="d0c19-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - toohave a counterpart of Britta Simon in Huddle that is linked toohello Azure AD representation of user.</span></span>

4. <span data-ttu-id="d0c19-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d0c19-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>

5. <span data-ttu-id="d0c19-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="d0c19-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d0c19-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0c19-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d0c19-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Huddle.</span><span class="sxs-lookup"><span data-stu-id="d0c19-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="d0c19-150">**tooconfigure inicio de sesión único en Azure AD con Huddle, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d0c19-150">**tooconfigure Azure AD single sign-on with Huddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c19-151">En el portal de Azure, en Hola Hola **Huddle** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-151">In hello Azure portal, on hello **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="d0c19-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d0c19-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="d0c19-155">En hello **Huddle dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d0c19-155">On hello **Huddle Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="d0c19-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="d0c19-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d0c19-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="d0c19-158">This value is not real.</span></span> <span data-ttu-id="d0c19-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="d0c19-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="d0c19-160">Póngase en contacto con [equipo de soporte técnico de Huddle cliente](https://huddle.zendesk.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="d0c19-160">Contact [Huddle Client support team](https://huddle.zendesk.com) tooget this value.</span></span> 

4. <span data-ttu-id="d0c19-161">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d0c19-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="d0c19-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d0c19-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d0c19-165">En hello **Huddle configuración** sección, haga clic en **configurar Huddle** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="d0c19-165">On hello **Huddle Configuration** section, click **Configure Huddle** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d0c19-166">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="d0c19-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="d0c19-168">tooconfigure inicio de sesión único en el lado de Huddle, necesita hello toosend descargado **certificado**, **SAML Single Sign-On dirección URL del servicio**, y **Id. de entidad SAML** demasiado[Equipo de soporte técnico de huddle cliente](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="d0c19-168">tooconfigure single sign-on on Huddle side, you need toosend hello downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="d0c19-169">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="d0c19-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="d0c19-170">Inicio de sesión único debe toobe habilitada por el equipo de soporte técnico de Huddle Hola.</span><span class="sxs-lookup"><span data-stu-id="d0c19-170">Single sign-on needs toobe enabled by hello Huddle support team.</span></span> <span data-ttu-id="d0c19-171">Recibirá una notificación cuando se haya completado la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0c19-171">You get a notification when hello configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="d0c19-172">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="d0c19-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d0c19-173">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="d0c19-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d0c19-174">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d0c19-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d0c19-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0c19-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="d0c19-176">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="d0c19-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="d0c19-178">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d0c19-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c19-179">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="d0c19-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d0c19-181">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d0c19-183">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0c19-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d0c19-185">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="d0c19-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d0c19-187">a.</span><span class="sxs-lookup"><span data-stu-id="d0c19-187">a.</span></span> <span data-ttu-id="d0c19-188">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0c19-189">b.</span><span class="sxs-lookup"><span data-stu-id="d0c19-189">b.</span></span> <span data-ttu-id="d0c19-190">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d0c19-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d0c19-191">c.</span><span class="sxs-lookup"><span data-stu-id="d0c19-191">c.</span></span> <span data-ttu-id="d0c19-192">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d0c19-193">d.</span><span class="sxs-lookup"><span data-stu-id="d0c19-193">d.</span></span> <span data-ttu-id="d0c19-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="d0c19-195">Creación de un usuario de prueba de Huddle</span><span class="sxs-lookup"><span data-stu-id="d0c19-195">Creating a Huddle test user</span></span>

<span data-ttu-id="d0c19-196">toolog de los usuarios de Azure AD tooenable en tooHuddle, se les deben aprovisionar en Huddle.</span><span class="sxs-lookup"><span data-stu-id="d0c19-196">tooenable Azure AD users toolog in tooHuddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="d0c19-197">En caso de hello de Huddle, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="d0c19-197">In hello case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="d0c19-198">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d0c19-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c19-199">Inicie sesión en tooyour **Huddle** como administrador.</span><span class="sxs-lookup"><span data-stu-id="d0c19-199">Log in tooyour **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="d0c19-200">Haga clic en **Área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="d0c19-201">Haga clic en **Contactos\>Invitar a contactos**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="d0c19-202">![Personas](./media/active-directory-saas-huddle-tutorial/IC787838.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="d0c19-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="d0c19-203">Hola **crear una nueva invitación** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d0c19-203">In hello **Create a new invitation** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="d0c19-204">![Nueva invitación](./media/active-directory-saas-huddle-tutorial/IC787839.png "Nueva invitación")</span><span class="sxs-lookup"><span data-stu-id="d0c19-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="d0c19-205">a.</span><span class="sxs-lookup"><span data-stu-id="d0c19-205">a.</span></span> <span data-ttu-id="d0c19-206">Hola **elegir un toojoin de personas de equipo tooinvite** lista, seleccione **equipo**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-206">In hello **Choose a team tooinvite people toojoin** list, select **team**.</span></span>

   <span data-ttu-id="d0c19-207">b.</span><span class="sxs-lookup"><span data-stu-id="d0c19-207">b.</span></span> <span data-ttu-id="d0c19-208">Hola de tipo **dirección de correo electrónico** de un anuncio de Azure válido de la cuenta que desee tooprovision en demasiado**escriba la dirección de correo electrónico para las personas que desea que tooinvite** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="d0c19-208">Type hello **Email Address** of a valid Azure AD account you want tooprovision in too**Enter email address for people you'd like tooinvite** textbox.</span></span>

   <span data-ttu-id="d0c19-209">c.</span><span class="sxs-lookup"><span data-stu-id="d0c19-209">c.</span></span> <span data-ttu-id="d0c19-210">Haga clic en **Invitar**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="d0c19-211">Hola cuenta de Azure AD titular recibirá un correo electrónico con una cuenta de hello tooconfirm vínculo antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="d0c19-211">hello Azure AD account holder will receive an email including a link tooconfirm hello account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="d0c19-212">Puede usar cualquier otra Huddle usuario cuenta herramienta de creación o las API proporcionadas por Huddle tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0c19-212">You can use any other Huddle user account creation tools or APIs provided by Huddle tooprovision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d0c19-213">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0c19-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d0c19-214">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooHuddle.</span><span class="sxs-lookup"><span data-stu-id="d0c19-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHuddle.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="d0c19-216">**tooassign Britta Simon tooHuddle, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d0c19-216">**tooassign Britta Simon tooHuddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c19-217">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d0c19-219">En la lista de aplicaciones de hello, seleccione **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-219">In hello applications list, select **Huddle**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="d0c19-221">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="d0c19-223">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-223">Click **Add** button.</span></span> <span data-ttu-id="d0c19-224">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="d0c19-226">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="d0c19-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d0c19-227">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d0c19-228">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d0c19-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d0c19-229">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="d0c19-229">Testing single sign-on</span></span>

<span data-ttu-id="d0c19-230">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d0c19-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d0c19-231">Al hacer clic en icono de Huddle Hola Hola Panel de acceso, deberá obtener automáticamente la página de inicio de sesión de aplicación de Huddle.</span><span class="sxs-lookup"><span data-stu-id="d0c19-231">When you click hello Huddle tile in hello Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="d0c19-232">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d0c19-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d0c19-233">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d0c19-233">Additional resources</span></span>

* [<span data-ttu-id="d0c19-234">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0c19-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d0c19-235">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d0c19-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png

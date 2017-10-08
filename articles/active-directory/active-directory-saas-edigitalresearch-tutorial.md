---
title: "Tutorial: Integración de Azure Active Directory con eDigitalResearch | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y eDigitalResearch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 6dd3cafb25ef8ede3a4c16902ed8da69cb7b715f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a><span data-ttu-id="80fb9-103">Tutorial: integración de Azure Active Directory con eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="80fb9-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span></span>

<span data-ttu-id="80fb9-104">En este tutorial, aprenderá cómo toointegrate eDigitalResearch con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="80fb9-104">In this tutorial, you learn how toointegrate eDigitalResearch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="80fb9-105">Integración eDigitalResearch con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="80fb9-105">Integrating eDigitalResearch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="80fb9-106">Puede controlar en Azure AD que tenga acceso tooeDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="80fb9-106">You can control in Azure AD who has access tooeDigitalResearch.</span></span>
- <span data-ttu-id="80fb9-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooeDigitalResearch (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80fb9-107">You can enable your users tooautomatically get signed-on tooeDigitalResearch (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="80fb9-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="80fb9-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="80fb9-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="80fb9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80fb9-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="80fb9-110">Prerequisites</span></span>

<span data-ttu-id="80fb9-111">integración de Azure AD con eDigitalResearch tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="80fb9-111">tooconfigure Azure AD integration with eDigitalResearch, you need hello following items:</span></span>

- <span data-ttu-id="80fb9-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80fb9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="80fb9-113">Una suscripción habilitada para el inicio de sesión único en eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="80fb9-113">A eDigitalResearch single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="80fb9-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="80fb9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="80fb9-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="80fb9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="80fb9-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="80fb9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="80fb9-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="80fb9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="80fb9-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="80fb9-118">Scenario description</span></span>
<span data-ttu-id="80fb9-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="80fb9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="80fb9-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="80fb9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="80fb9-121">Agregar eDigitalResearch desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="80fb9-121">Adding eDigitalResearch from hello gallery</span></span>
2. <span data-ttu-id="80fb9-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80fb9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-edigitalresearch-from-hello-gallery"></a><span data-ttu-id="80fb9-123">Agregar eDigitalResearch desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="80fb9-123">Adding eDigitalResearch from hello gallery</span></span>
<span data-ttu-id="80fb9-124">integración de hello tooconfigure de eDigitalResearch en Azure AD, deberá tooadd eDigitalResearch de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="80fb9-124">tooconfigure hello integration of eDigitalResearch into Azure AD, you need tooadd eDigitalResearch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="80fb9-125">**tooadd eDigitalResearch de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="80fb9-125">**tooadd eDigitalResearch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="80fb9-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="80fb9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="80fb9-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="80fb9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="80fb9-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="80fb9-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="80fb9-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80fb9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="80fb9-133">En el cuadro de búsqueda de hello, escriba **eDigitalResearch**, seleccione **eDigitalResearch** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="80fb9-133">In hello search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button tooadd hello application.</span></span>

    ![eDigitalResearch en la lista de resultados de Hola](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="80fb9-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="80fb9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="80fb9-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con eDigitalResearch con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="80fb9-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="80fb9-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en eDigitalResearch es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80fb9-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eDigitalResearch is tooa user in Azure AD.</span></span> <span data-ttu-id="80fb9-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en eDigitalResearch debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="80fb9-138">In other words, a link relationship between an Azure AD user and hello related user in eDigitalResearch needs toobe established.</span></span>

<span data-ttu-id="80fb9-139">En eDigitalResearch, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="80fb9-139">In eDigitalResearch, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="80fb9-140">tooconfigure y prueba de inicio de sesión único en Azure AD con eDigitalResearch, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="80fb9-140">tooconfigure and test Azure AD single sign-on with eDigitalResearch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="80fb9-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="80fb9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="80fb9-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80fb9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="80fb9-143">**[Crear un usuario de prueba eDigitalResearch](#create-a-edigitalresearch-test-user)**  -toohave un equivalente de Britta Simon en eDigitalResearch que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="80fb9-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - toohave a counterpart of Britta Simon in eDigitalResearch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="80fb9-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="80fb9-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="80fb9-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="80fb9-145">**[Test single sign-on](#test-single-sign-on)**  tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="80fb9-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80fb9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="80fb9-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="80fb9-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eDigitalResearch application.</span></span>

<span data-ttu-id="80fb9-148">**inicio de sesión único en Azure AD tooconfigure con eDigitalResearch, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="80fb9-148">**tooconfigure Azure AD single sign-on with eDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="80fb9-149">En el portal de Azure, en Hola Hola **eDigitalResearch** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="80fb9-149">In hello Azure portal, on hello **eDigitalResearch** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="80fb9-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="80fb9-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

3. <span data-ttu-id="80fb9-153">En hello **eDigitalResearch dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="80fb9-153">On hello **eDigitalResearch Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    <span data-ttu-id="80fb9-155">a.</span><span class="sxs-lookup"><span data-stu-id="80fb9-155">a.</span></span> <span data-ttu-id="80fb9-156">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company-name>.edigitalresearch.com`</span><span class="sxs-lookup"><span data-stu-id="80fb9-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com`</span></span>

    <span data-ttu-id="80fb9-157">b.</span><span class="sxs-lookup"><span data-stu-id="80fb9-157">b.</span></span> <span data-ttu-id="80fb9-158">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company-name>.edigitalresearch.com/login/consume`</span><span class="sxs-lookup"><span data-stu-id="80fb9-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="80fb9-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="80fb9-159">These values are not real.</span></span> <span data-ttu-id="80fb9-160">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="80fb9-160">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="80fb9-161">Póngase en contacto con [equipo de soporte técnico de eDigitalResearch](http://www.maruedr.com/contact) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="80fb9-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) tooget these values.</span></span>
 


4. <span data-ttu-id="80fb9-162">En hello **el certificado de firma de SAML** sección, haga clic en **Base(64) certificado** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="80fb9-162">On hello **SAML Signing Certificate** section, click **Certificate Base(64)** and then save hello certificate file on your computer.</span></span>

    <span data-ttu-id="80fb9-163">!</span><span class="sxs-lookup"><span data-stu-id="80fb9-163">!</span></span>![vínculo de descarga del certificado de Hola](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

5. <span data-ttu-id="80fb9-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="80fb9-165">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="80fb9-167">En hello **eDigitalResearch configuración** sección, haga clic en **configurar eDigitalResearch** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="80fb9-167">On hello **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="80fb9-168">Hola copia **dirección URL de cierre de sesión, Id. de entidad SAML** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="80fb9-168">Copy hello **Sign-Out URL, SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configuración de eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

7. <span data-ttu-id="80fb9-170">tooconfigure inicio de sesión único en **eDigitalResearch** lado, necesita hello toosend descargado **archivo de certificado (Base64)**, **Id. de entidad SAML**, y  **Dirección URL de cierre de sesión** demasiado[equipo de soporte técnico de eDigitalResearch](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="80fb9-170">tooconfigure single sign-on on **eDigitalResearch** side, you need toosend hello downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** too[eDigitalResearch support team](http://www.maruedr.com/contact).</span></span> <span data-ttu-id="80fb9-171">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="80fb9-171">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="80fb9-172">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="80fb9-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="80fb9-173">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="80fb9-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="80fb9-174">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="80fb9-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="80fb9-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="80fb9-175">Create an Azure AD test user</span></span>

<span data-ttu-id="80fb9-176">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="80fb9-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="80fb9-178">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="80fb9-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="80fb9-179">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="80fb9-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="80fb9-181">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="80fb9-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="80fb9-183">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="80fb9-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="80fb9-185">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="80fb9-185">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_04.png)

    <span data-ttu-id="80fb9-187">a.</span><span class="sxs-lookup"><span data-stu-id="80fb9-187">a.</span></span> <span data-ttu-id="80fb9-188">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="80fb9-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="80fb9-189">b.</span><span class="sxs-lookup"><span data-stu-id="80fb9-189">b.</span></span> <span data-ttu-id="80fb9-190">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80fb9-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="80fb9-191">c.</span><span class="sxs-lookup"><span data-stu-id="80fb9-191">c.</span></span> <span data-ttu-id="80fb9-192">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="80fb9-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="80fb9-193">d.</span><span class="sxs-lookup"><span data-stu-id="80fb9-193">d.</span></span> <span data-ttu-id="80fb9-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="80fb9-194">Click **Create**.</span></span>
  
### <a name="create-a-edigitalresearch-test-user"></a><span data-ttu-id="80fb9-195">Creación de un usuario de prueba de eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="80fb9-195">Create a eDigitalResearch test user</span></span>

<span data-ttu-id="80fb9-196">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en eDigitalResearch toocreate.</span><span class="sxs-lookup"><span data-stu-id="80fb9-196">hello objective of this section is toocreate a user called Britta Simon in eDigitalResearch.</span></span> 

<span data-ttu-id="80fb9-197">Trabajar con hello [equipo de soporte técnico de eDigitalResearch](http://www.maruedr.com/contact) usuarios tooget creados.</span><span class="sxs-lookup"><span data-stu-id="80fb9-197">Work with hello [eDigitalResearch support team](http://www.maruedr.com/contact) tooget users created.</span></span>       
    
 > [!NOTE]
 > <span data-ttu-id="80fb9-198">titular de la cuenta de Hello Azure Active Directory recibe un correo electrónico y sigue un vínculo tooconfirm su cuenta antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="80fb9-198">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="80fb9-199">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="80fb9-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="80fb9-200">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooeDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="80fb9-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeDigitalResearch.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="80fb9-202">**tooassign Britta Simon tooeDigitalResearch, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="80fb9-202">**tooassign Britta Simon tooeDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="80fb9-203">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="80fb9-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="80fb9-205">En la lista de aplicaciones de hello, seleccione **eDigitalResearch**.</span><span class="sxs-lookup"><span data-stu-id="80fb9-205">In hello applications list, select **eDigitalResearch**.</span></span>

    ![Hola eDigitalResearch vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

3. <span data-ttu-id="80fb9-207">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="80fb9-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="80fb9-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="80fb9-209">Click **Add** button.</span></span> <span data-ttu-id="80fb9-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="80fb9-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="80fb9-212">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="80fb9-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="80fb9-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="80fb9-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="80fb9-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="80fb9-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="80fb9-215">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="80fb9-215">Test single sign-on</span></span>

<span data-ttu-id="80fb9-216">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="80fb9-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="80fb9-217">Al hacer clic en icono de eDigitalResearch Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour eDigitalResearch aplicación.</span><span class="sxs-lookup"><span data-stu-id="80fb9-217">When you click hello eDigitalResearch tile in hello Access Panel, you should get automatically signed-on tooyour eDigitalResearch application.</span></span>
<span data-ttu-id="80fb9-218">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="80fb9-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="80fb9-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="80fb9-219">Additional resources</span></span>

* [<span data-ttu-id="80fb9-220">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80fb9-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="80fb9-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="80fb9-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_203.png


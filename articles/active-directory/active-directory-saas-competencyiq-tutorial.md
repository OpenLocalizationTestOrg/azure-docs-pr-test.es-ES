---
title: "Tutorial: Integración de Azure Active Directory con CompetencyIQ | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y CompetencyIQ."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e262bf7e-cc7d-4d0e-aea7-861f00d8837d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: c032884b092da85684e24e98f75371475e09322d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-competencyiq"></a><span data-ttu-id="ce7ca-103">Tutorial: Integración de Azure Active Directory con CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="ce7ca-103">Tutorial: Azure Active Directory integration with CompetencyIQ</span></span>

<span data-ttu-id="ce7ca-104">En este tutorial, aprenderá cómo toointegrate CompetencyIQ con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ce7ca-104">In this tutorial, you learn how toointegrate CompetencyIQ with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce7ca-105">Integración CompetencyIQ con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ce7ca-105">Integrating CompetencyIQ with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ce7ca-106">Puede controlar en Azure AD que tenga acceso tooCompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="ce7ca-106">You can control in Azure AD who has access tooCompetencyIQ</span></span>
- <span data-ttu-id="ce7ca-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooCompetencyIQ (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce7ca-107">You can enable your users tooautomatically get signed-on tooCompetencyIQ (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ce7ca-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ce7ca-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ce7ca-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ce7ca-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce7ca-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ce7ca-110">Prerequisites</span></span>

<span data-ttu-id="ce7ca-111">integración de Azure AD con CompetencyIQ tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ce7ca-111">tooconfigure Azure AD integration with CompetencyIQ, you need hello following items:</span></span>

- <span data-ttu-id="ce7ca-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce7ca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce7ca-113">Una suscripción habilitada para el inicio de sesión único en CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="ce7ca-113">A CompetencyIQ single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ce7ca-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ce7ca-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ce7ca-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ce7ca-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ce7ca-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce7ca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ce7ca-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ce7ca-118">Scenario description</span></span>
<span data-ttu-id="ce7ca-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ce7ca-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="ce7ca-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ce7ca-121">Agregar CompetencyIQ desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ce7ca-121">Adding CompetencyIQ from hello gallery</span></span>
2. <span data-ttu-id="ce7ca-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce7ca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-competencyiq-from-hello-gallery"></a><span data-ttu-id="ce7ca-123">Agregar CompetencyIQ desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ce7ca-123">Adding CompetencyIQ from hello gallery</span></span>
<span data-ttu-id="ce7ca-124">integración de hello tooconfigure de CompetencyIQ en Azure AD, deberá tooadd CompetencyIQ de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-124">tooconfigure hello integration of CompetencyIQ into Azure AD, you need tooadd CompetencyIQ from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ce7ca-125">**tooadd CompetencyIQ de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ce7ca-125">**tooadd CompetencyIQ from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce7ca-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ce7ca-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ce7ca-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="ce7ca-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="ce7ca-133">En el cuadro de búsqueda de hello, escriba **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-133">In hello search box, type **CompetencyIQ**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_search.png)

5. <span data-ttu-id="ce7ca-135">En el panel de resultados de hello, seleccione **CompetencyIQ**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-135">In hello results panel, select **CompetencyIQ**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ce7ca-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce7ca-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ce7ca-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con CompetencyIQ con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ce7ca-138">In this section, you configure and test Azure AD single sign-on with CompetencyIQ based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ce7ca-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en CompetencyIQ es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CompetencyIQ is tooa user in Azure AD.</span></span> <span data-ttu-id="ce7ca-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en CompetencyIQ debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-140">In other words, a link relationship between an Azure AD user and hello related user in CompetencyIQ needs toobe established.</span></span>

<span data-ttu-id="ce7ca-141">En CompetencyIQ, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-141">In CompetencyIQ, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ce7ca-142">tooconfigure y prueba de inicio de sesión único en Azure AD con CompetencyIQ, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ce7ca-142">tooconfigure and test Azure AD single sign-on with CompetencyIQ, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ce7ca-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ce7ca-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ce7ca-145">**[Crear un usuario de prueba CompetencyIQ](#creating-a-competencyiq-test-user)**  -toohave un equivalente de Britta Simon en CompetencyIQ que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-145">**[Creating a CompetencyIQ test user](#creating-a-competencyiq-test-user)** - toohave a counterpart of Britta Simon in CompetencyIQ that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ce7ca-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ce7ca-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ce7ca-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce7ca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ce7ca-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CompetencyIQ application.</span></span>

<span data-ttu-id="ce7ca-150">**inicio de sesión único en Azure AD tooconfigure con CompetencyIQ, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ce7ca-150">**tooconfigure Azure AD single sign-on with CompetencyIQ, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce7ca-151">En el portal de Azure, en Hola Hola **CompetencyIQ** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-151">In hello Azure portal, on hello **CompetencyIQ** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="ce7ca-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_samlbase.png)

3. <span data-ttu-id="ce7ca-155">En hello **CompetencyIQ dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ce7ca-155">On hello **CompetencyIQ Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_url1.png)

    <span data-ttu-id="ce7ca-157">a.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-157">a.</span></span> <span data-ttu-id="ce7ca-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<customer>.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="ce7ca-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<customer>.competencyiq.com/`</span></span>
    
    <span data-ttu-id="ce7ca-159">b.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-159">b.</span></span> <span data-ttu-id="ce7ca-160">Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://www.competencyiq.com/`</span><span class="sxs-lookup"><span data-stu-id="ce7ca-160">In hello **Identifier** textbox, type hello URL: `https://www.competencyiq.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ce7ca-161">valor de dirección URL de Hello inicio de sesión es no real por lo que actualizarlo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-161">hello Sign-on URL value is not real so update this with actual Sign-On URL.</span></span> <span data-ttu-id="ce7ca-162">Póngase en contacto con [equipo de soporte técnico de cliente de CompetencyIQ](https://www.competencyiq.com/) tooget esto.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-162">Contact [CompetencyIQ Client support team](https://www.competencyiq.com/) tooget this.</span></span> 
 
4. <span data-ttu-id="ce7ca-163">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_certificate.png) 

5. <span data-ttu-id="ce7ca-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="ce7ca-165">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-competencyiq-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ce7ca-167">En hello **CompetencyIQ configuración** sección, haga clic en **configurar CompetencyIQ** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-167">On hello **CompetencyIQ Configuration** section, click **Configure CompetencyIQ** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ce7ca-168">Hola copia **Id. de entidad SAML**, y **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="ce7ca-168">Copy hello **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_configure.png) 

7. <span data-ttu-id="ce7ca-170">tooconfigure inicio de sesión único en **CompetencyIQ** lado, necesita hello toosend descargado **Metadata XML**, **Id. de entidad SAML** y **SAML Single Sign-On Dirección URL del servicio** demasiado[equipo de soporte técnico de CompetencyIQ](https://www.competencyiq.com/).</span><span class="sxs-lookup"><span data-stu-id="ce7ca-170">tooconfigure single sign-on on **CompetencyIQ** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[CompetencyIQ support team](https://www.competencyiq.com/).</span></span> <span data-ttu-id="ce7ca-171">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-171">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ce7ca-172">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="ce7ca-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ce7ca-173">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ce7ca-174">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ce7ca-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ce7ca-175">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce7ca-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="ce7ca-176">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="ce7ca-178">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ce7ca-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce7ca-179">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ce7ca-181">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ce7ca-183">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ce7ca-185">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="ce7ca-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-competencyiq-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ce7ca-187">a.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-187">a.</span></span> <span data-ttu-id="ce7ca-188">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce7ca-189">b.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-189">b.</span></span> <span data-ttu-id="ce7ca-190">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ce7ca-191">c.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-191">c.</span></span> <span data-ttu-id="ce7ca-192">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ce7ca-193">d.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-193">d.</span></span> <span data-ttu-id="ce7ca-194">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-194">Click **Create**.</span></span>
 
### <a name="creating-a-competencyiq-test-user"></a><span data-ttu-id="ce7ca-195">Creación de un usuario de prueba de CompetencyIQ</span><span class="sxs-lookup"><span data-stu-id="ce7ca-195">Creating a CompetencyIQ test user</span></span>

<span data-ttu-id="ce7ca-196">toolog de los usuarios de Azure AD tooenable en tooCompetencyIQ, se les deben aprovisionar en CompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-196">tooenable Azure AD users toolog in tooCompetencyIQ, they must be provisioned into CompetencyIQ.</span></span> <span data-ttu-id="ce7ca-197">Póngase en contacto con [equipo de soporte técnico de CompetencyIQ](https://www.competencyiq.com/) toocreate a los usuarios en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-197">Contact [CompetencyIQ support team](https://www.competencyiq.com/) toocreate users in hello application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ce7ca-198">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce7ca-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ce7ca-199">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCompetencyIQ.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCompetencyIQ.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="ce7ca-201">**tooassign Britta Simon tooCompetencyIQ, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ce7ca-201">**tooassign Britta Simon tooCompetencyIQ, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce7ca-202">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ce7ca-204">En la lista de aplicaciones de hello, seleccione **CompetencyIQ**.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-204">In hello applications list, select **CompetencyIQ**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-competencyiq-tutorial/tutorial_competencyiq_app.png) 

3. <span data-ttu-id="ce7ca-206">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="ce7ca-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-208">Click **Add** button.</span></span> <span data-ttu-id="ce7ca-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="ce7ca-211">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ce7ca-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ce7ca-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ce7ca-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="ce7ca-214">Testing single sign-on</span></span>

<span data-ttu-id="ce7ca-215">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ce7ca-216">Al hacer clic en icono de CompetencyIQ Hola Hola Panel de acceso, debe que se registren automáticamente en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="ce7ca-216">When you click hello CompetencyIQ tile in hello Access Panel, you should get automatically logged into hello application.</span></span>
<span data-ttu-id="ce7ca-217">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ce7ca-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ce7ca-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ce7ca-218">Additional resources</span></span>

* [<span data-ttu-id="ce7ca-219">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce7ca-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce7ca-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ce7ca-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-competencyiq-tutorial/tutorial_general_203.png


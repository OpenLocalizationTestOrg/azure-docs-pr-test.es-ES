---
title: "Tutorial: Integración de Azure Active Directory con WORKS MOBILE | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y funciona MOBILE."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 80192218a2e99a921834bb53e708d5e4fab413f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="c719d-103">Tutorial: Integración de Azure Active Directory con WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="c719d-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="c719d-104">En este tutorial, aprenderá cómo funciona la toointegrate tecnología móvil con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c719d-104">In this tutorial, you learn how toointegrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c719d-105">Integración MOBILE funciona con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c719d-105">Integrating WORKS MOBILE with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c719d-106">Puede controlar en Azure AD que tenga acceso tooWORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="c719d-106">You can control in Azure AD who has access tooWORKS MOBILE</span></span>
- <span data-ttu-id="c719d-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWORKS MOBILE (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c719d-107">You can enable your users tooautomatically get signed-on tooWORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c719d-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c719d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c719d-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c719d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c719d-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c719d-110">Prerequisites</span></span>

<span data-ttu-id="c719d-111">tooconfigure integración de Azure AD con MOBILE funciona, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c719d-111">tooconfigure Azure AD integration with WORKS MOBILE, you need hello following items:</span></span>

- <span data-ttu-id="c719d-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c719d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c719d-113">Una suscripción habilitada para el inicio de sesión único en WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="c719d-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c719d-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c719d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c719d-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c719d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c719d-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c719d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c719d-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c719d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c719d-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c719d-118">Scenario description</span></span>
<span data-ttu-id="c719d-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c719d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c719d-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c719d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c719d-121">Agregar móviles funciona de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c719d-121">Adding WORKS MOBILE from hello gallery</span></span>
2. <span data-ttu-id="c719d-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c719d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-hello-gallery"></a><span data-ttu-id="c719d-123">Agregar móviles funciona de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c719d-123">Adding WORKS MOBILE from hello gallery</span></span>
<span data-ttu-id="c719d-124">integración de hello tooconfigure de MOBILE funciona en Azure AD, deberá tooadd MOBILE funciona en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c719d-124">tooconfigure hello integration of WORKS MOBILE into Azure AD, you need tooadd WORKS MOBILE from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c719d-125">**tooadd MOBILE funciona de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c719d-125">**tooadd WORKS MOBILE from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c719d-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c719d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c719d-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c719d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c719d-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c719d-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c719d-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c719d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c719d-133">En el cuadro de búsqueda de hello, escriba **MOBILE funciona**.</span><span class="sxs-lookup"><span data-stu-id="c719d-133">In hello search box, type **WORKS MOBILE**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="c719d-135">En el panel de resultados de hello, seleccione **MOBILE funciona**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c719d-135">In hello results panel, select **WORKS MOBILE**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c719d-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c719d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c719d-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con WORKS MOBILE con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c719d-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c719d-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en MOBILE funciona es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c719d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in WORKS MOBILE is tooa user in Azure AD.</span></span> <span data-ttu-id="c719d-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en WORKS MOBILE debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c719d-140">In other words, a link relationship between an Azure AD user and hello related user in WORKS MOBILE needs toobe established.</span></span>

<span data-ttu-id="c719d-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en MOBILE funciona.</span><span class="sxs-lookup"><span data-stu-id="c719d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="c719d-142">tooconfigure y prueba de inicio de sesión único en Azure AD con MOBILE funciona, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c719d-142">tooconfigure and test Azure AD single sign-on with WORKS MOBILE, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c719d-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c719d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c719d-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c719d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c719d-145">**[Crear un usuario de prueba funciona MOBILE](#creating-a-works-mobile-test-user)**  -toohave un equivalente de Britta Simon en MOBILE WORKS que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="c719d-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - toohave a counterpart of Britta Simon in WORKS MOBILE that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c719d-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c719d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c719d-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c719d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c719d-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c719d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c719d-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación móvil funciona.</span><span class="sxs-lookup"><span data-stu-id="c719d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="c719d-150">**inicio de sesión único en tooconfigure Azure AD con MOBILE funciona, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c719d-150">**tooconfigure Azure AD single sign-on with WORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="c719d-151">En el portal de Azure, en Hola Hola **MOBILE funciona** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c719d-151">In hello Azure portal, on hello **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c719d-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c719d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="c719d-155">En hello **WORKS MOBILE dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c719d-155">On hello **WORKS MOBILE Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="c719d-157">a.</span><span class="sxs-lookup"><span data-stu-id="c719d-157">a.</span></span> <span data-ttu-id="c719d-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="c719d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="c719d-159">b.</span><span class="sxs-lookup"><span data-stu-id="c719d-159">b.</span></span> <span data-ttu-id="c719d-160">Hola **identificador** cuadro de texto, valor de tipo hello como`worksmobile.com`</span><span class="sxs-lookup"><span data-stu-id="c719d-160">In hello **Identifier** textbox, type hello value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c719d-161">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="c719d-161">This value is not real.</span></span> <span data-ttu-id="c719d-162">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="c719d-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="c719d-163">Póngase en contacto con [equipo de soporte técnico de WORKS MOBILE Client](mailto:dl_ssoinfo@worksmobile.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="c719d-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="c719d-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Raw)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c719d-164">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="c719d-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c719d-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c719d-168">En hello **WORKS MOBILE configuración** sección, haga clic en **configurar WORKS MOBILE** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="c719d-168">On hello **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c719d-169">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="c719d-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="c719d-171">tooget SSO configurado para la aplicación, póngase en contacto con [equipo de soporte técnico de WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com) y proporcionarles Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="c719d-171">tooget SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with hello following information:</span></span> 

    <span data-ttu-id="c719d-172">Hola • descargado **archivo de certificado**</span><span class="sxs-lookup"><span data-stu-id="c719d-172">• hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="c719d-173">• hello **SAML Single Sign-On dirección URL del servicio**</span><span class="sxs-lookup"><span data-stu-id="c719d-173">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="c719d-174">• hello **Id. de entidad de SAML**</span><span class="sxs-lookup"><span data-stu-id="c719d-174">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="c719d-175">• hello **dirección URL de cierre de sesión**</span><span class="sxs-lookup"><span data-stu-id="c719d-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="c719d-176">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="c719d-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c719d-177">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="c719d-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c719d-178">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c719d-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c719d-179">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c719d-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="c719d-180">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c719d-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c719d-182">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c719d-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c719d-183">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c719d-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c719d-185">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c719d-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c719d-187">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c719d-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c719d-189">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c719d-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c719d-191">a.</span><span class="sxs-lookup"><span data-stu-id="c719d-191">a.</span></span> <span data-ttu-id="c719d-192">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c719d-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c719d-193">b.</span><span class="sxs-lookup"><span data-stu-id="c719d-193">b.</span></span> <span data-ttu-id="c719d-194">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c719d-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c719d-195">c.</span><span class="sxs-lookup"><span data-stu-id="c719d-195">c.</span></span> <span data-ttu-id="c719d-196">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c719d-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c719d-197">d.</span><span class="sxs-lookup"><span data-stu-id="c719d-197">d.</span></span> <span data-ttu-id="c719d-198">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c719d-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="c719d-199">Crear un usuario de prueba de WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="c719d-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="c719d-200">En esta sección, creará un usuario llamado Britta Simon en WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="c719d-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="c719d-201">Trabaje con [equipo de soporte técnico de WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com) a los usuarios de tooadd hello en la plataforma de MOBILE funciona Hola.</span><span class="sxs-lookup"><span data-stu-id="c719d-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) tooadd hello users in hello WORKS MOBILE platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c719d-202">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c719d-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c719d-203">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="c719d-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWORKS MOBILE.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c719d-205">**tooassign Britta Simon tooWORKS MOBILE, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c719d-205">**tooassign Britta Simon tooWORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="c719d-206">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c719d-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c719d-208">En la lista de aplicaciones de hello, seleccione **MOBILE funciona**.</span><span class="sxs-lookup"><span data-stu-id="c719d-208">In hello applications list, select **WORKS MOBILE**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="c719d-210">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c719d-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c719d-212">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c719d-212">Click **Add** button.</span></span> <span data-ttu-id="c719d-213">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c719d-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c719d-215">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c719d-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c719d-216">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c719d-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c719d-217">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c719d-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c719d-218">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c719d-218">Testing single sign-on</span></span>

<span data-ttu-id="c719d-219">En esta sección, probará la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c719d-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="c719d-220">Al hacer clic en icono de MOBILE funciona Hola Hola Panel de acceso, deberá obtener aplicaciones de MOBILE funciona tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="c719d-220">When you click hello WORKS MOBILE tile in hello Access Panel, you should get automatically signed-on tooyour WORKS MOBILE application.</span></span>
<span data-ttu-id="c719d-221">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c719d-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c719d-222">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c719d-222">Additional resources</span></span>

* [<span data-ttu-id="c719d-223">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c719d-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c719d-224">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c719d-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png


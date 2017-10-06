---
title: "Tutorial: Integración de Azure Active Directory con Heroku | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Heroku."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee11db647fd385140f1dbcab2586dfafffe5d912
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="c6862-103">Tutorial: Integración de Azure Active Directory con Heroku</span><span class="sxs-lookup"><span data-stu-id="c6862-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="c6862-104">En este tutorial, aprenderá cómo toointegrate Heroku con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c6862-104">In this tutorial, you learn how toointegrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c6862-105">Integración Heroku con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c6862-105">Integrating Heroku with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c6862-106">Puede controlar en Azure AD que tenga acceso tooHeroku</span><span class="sxs-lookup"><span data-stu-id="c6862-106">You can control in Azure AD who has access tooHeroku</span></span>
- <span data-ttu-id="c6862-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooHeroku (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6862-107">You can enable your users tooautomatically get signed-on tooHeroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c6862-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c6862-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c6862-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c6862-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6862-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c6862-110">Prerequisites</span></span>

<span data-ttu-id="c6862-111">integración de Azure AD con Heroku tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c6862-111">tooconfigure Azure AD integration with Heroku, you need hello following items:</span></span>

- <span data-ttu-id="c6862-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6862-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c6862-113">Una suscripción habilitada para el inicio de sesión único en Heroku</span><span class="sxs-lookup"><span data-stu-id="c6862-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c6862-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c6862-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c6862-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c6862-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c6862-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c6862-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c6862-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c6862-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c6862-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c6862-118">Scenario description</span></span>
<span data-ttu-id="c6862-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c6862-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c6862-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c6862-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c6862-121">Agregar Heroku desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c6862-121">Adding Heroku from hello gallery</span></span>
2. <span data-ttu-id="c6862-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6862-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-hello-gallery"></a><span data-ttu-id="c6862-123">Agregar Heroku desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c6862-123">Adding Heroku from hello gallery</span></span>
<span data-ttu-id="c6862-124">integración de hello tooconfigure de Heroku en Azure AD, deberá tooadd Heroku de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c6862-124">tooconfigure hello integration of Heroku into Azure AD, you need tooadd Heroku from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c6862-125">**tooadd Heroku de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c6862-125">**tooadd Heroku from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6862-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c6862-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c6862-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c6862-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c6862-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c6862-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c6862-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c6862-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c6862-133">En el cuadro de búsqueda de hello, escriba **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="c6862-133">In hello search box, type **Heroku**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="c6862-135">En el panel de resultados de hello, seleccione **Heroku**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c6862-135">In hello results panel, select **Heroku**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c6862-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6862-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="c6862-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Heroku con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c6862-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c6862-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Heroku es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6862-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Heroku is tooa user in Azure AD.</span></span> <span data-ttu-id="c6862-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Heroku debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c6862-140">In other words, a link relationship between an Azure AD user and hello related user in Heroku needs toobe established.</span></span>

<span data-ttu-id="c6862-141">En Heroku, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6862-141">In Heroku, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c6862-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Heroku, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c6862-142">tooconfigure and test Azure AD single sign-on with Heroku, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c6862-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c6862-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c6862-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c6862-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c6862-145">**[Crear un usuario de prueba Heroku](#creating-a-heroku-test-user)**  -toohave un equivalente de Britta Simon en Heroku que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="c6862-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - toohave a counterpart of Britta Simon in Heroku that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c6862-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c6862-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c6862-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c6862-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c6862-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6862-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c6862-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Heroku.</span><span class="sxs-lookup"><span data-stu-id="c6862-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="c6862-150">**inicio de sesión único en Azure AD tooconfigure con Heroku, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c6862-150">**tooconfigure Azure AD single sign-on with Heroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6862-151">En el portal de Azure, en Hola Hola **Heroku** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c6862-151">In hello Azure portal, on hello **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c6862-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c6862-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="c6862-155">En hello **Heroku dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c6862-155">On hello **Heroku Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="c6862-157">a.</span><span class="sxs-lookup"><span data-stu-id="c6862-157">a.</span></span> <span data-ttu-id="c6862-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="c6862-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="c6862-159">b.</span><span class="sxs-lookup"><span data-stu-id="c6862-159">b.</span></span> <span data-ttu-id="c6862-160">Hola **dirección URL de identificación** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="c6862-160">In hello **Identifier URL** textbox, type a URL using hello following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="c6862-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="c6862-161">These values are not real.</span></span> <span data-ttu-id="c6862-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="c6862-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c6862-163">Estos valores se obtienen del equipo de soporte de Heroku, lo que se describe en secciones posteriores de este artículo.</span><span class="sxs-lookup"><span data-stu-id="c6862-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="c6862-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c6862-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="c6862-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c6862-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c6862-168">tooenable SSO en Heroku, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c6862-168">tooenable SSO in Heroku, perform hello following steps:</span></span>
   
    <span data-ttu-id="c6862-169">a.</span><span class="sxs-lookup"><span data-stu-id="c6862-169">a.</span></span> <span data-ttu-id="c6862-170">Inicie sesión en toohello Heroku cuenta como administrador.</span><span class="sxs-lookup"><span data-stu-id="c6862-170">Log in toohello Heroku account as an administrator.</span></span>

    <span data-ttu-id="c6862-171">b.</span><span class="sxs-lookup"><span data-stu-id="c6862-171">b.</span></span> <span data-ttu-id="c6862-172">Haga clic en hello **configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="c6862-172">Click hello **Settings** tab.</span></span>

    <span data-ttu-id="c6862-173">c.</span><span class="sxs-lookup"><span data-stu-id="c6862-173">c.</span></span> <span data-ttu-id="c6862-174">En hello **inicio de sesión único en la página**, haga clic en **cargar metadatos**.</span><span class="sxs-lookup"><span data-stu-id="c6862-174">On hello **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="c6862-175">d.</span><span class="sxs-lookup"><span data-stu-id="c6862-175">d.</span></span> <span data-ttu-id="c6862-176">Cargar archivo de metadatos de hello, que ha descargado desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c6862-176">Upload hello metadata file, which you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="c6862-177">e.</span><span class="sxs-lookup"><span data-stu-id="c6862-177">e.</span></span> <span data-ttu-id="c6862-178">Cuando el programa de instalación de hello es correcta, los administradores ver un cuadro de diálogo de confirmación y dirección URL de Hola de hello inicio de sesión de SSO para los usuarios finales se muestra.</span><span class="sxs-lookup"><span data-stu-id="c6862-178">When hello setup is successful, administrators see a confirmation dialog and hello URL of hello SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="c6862-179">f.</span><span class="sxs-lookup"><span data-stu-id="c6862-179">f.</span></span> <span data-ttu-id="c6862-180">Hola copia **dirección URL de inicio de sesión de Heroku** y **Id. de entidad Heroku** valores y retroceda demasiado**Heroku dominio y las direcciones URL** sección portal de Azure y pegue estos valores en hello **Dirección Url de inicio de sesión** y **identificador** cuadros de texto respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c6862-180">Copy hello **Heroku Login URL** and **Heroku Entity ID** values and go back too**Heroku Domain and URLs** section in Azure portal and paste these values into hello **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="c6862-182">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c6862-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="c6862-183">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="c6862-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c6862-184">Después de agregar esta aplicación de hello **Active Directory las aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="c6862-184">After adding this app from hello **Active Directory Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c6862-185">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c6862-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c6862-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6862-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="c6862-187">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c6862-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c6862-189">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c6862-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6862-190">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c6862-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c6862-192">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c6862-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c6862-194">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6862-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c6862-196">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c6862-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c6862-198">a.</span><span class="sxs-lookup"><span data-stu-id="c6862-198">a.</span></span> <span data-ttu-id="c6862-199">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c6862-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c6862-200">b.</span><span class="sxs-lookup"><span data-stu-id="c6862-200">b.</span></span> <span data-ttu-id="c6862-201">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c6862-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c6862-202">c.</span><span class="sxs-lookup"><span data-stu-id="c6862-202">c.</span></span> <span data-ttu-id="c6862-203">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c6862-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c6862-204">d.</span><span class="sxs-lookup"><span data-stu-id="c6862-204">d.</span></span> <span data-ttu-id="c6862-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c6862-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="c6862-206">Creación de un usuario de prueba de Heroku</span><span class="sxs-lookup"><span data-stu-id="c6862-206">Creating a Heroku test user</span></span>

<span data-ttu-id="c6862-207">En esta sección, creará un usuario llamado Britta Simon en Heroku.</span><span class="sxs-lookup"><span data-stu-id="c6862-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="c6862-208">Heroku admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c6862-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="c6862-209">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="c6862-209">There is no action item for you in this section.</span></span> <span data-ttu-id="c6862-210">Al tener acceso a Heroku si el usuario de hello no existe todavía, se crea un nuevo usuario.</span><span class="sxs-lookup"><span data-stu-id="c6862-210">A new user is created when accessing Heroku if hello user doesn't exist yet.</span></span> <span data-ttu-id="c6862-211">Una vez se ha aprovisionado la cuenta de hello, Hola usuario recibe un correo electrónico de comprobación y necesita el vínculo de confirmación de hello tooclick.</span><span class="sxs-lookup"><span data-stu-id="c6862-211">After hello account is provisioned, hello end user receives a verification email and needs tooclick hello acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="c6862-212">Si necesita un usuario toocreate manualmente, necesita hello toocontact [equipo de soporte técnico de Heroku cliente](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="c6862-212">If you need toocreate a user manually, you need toocontact hello [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c6862-213">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6862-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c6862-214">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooHeroku.</span><span class="sxs-lookup"><span data-stu-id="c6862-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHeroku.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c6862-216">**tooassign Britta Simon tooHeroku, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c6862-216">**tooassign Britta Simon tooHeroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6862-217">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c6862-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c6862-219">En la lista de aplicaciones de hello, seleccione **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="c6862-219">In hello applications list, select **Heroku**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="c6862-221">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c6862-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c6862-223">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c6862-223">Click **Add** button.</span></span> <span data-ttu-id="c6862-224">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c6862-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c6862-226">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c6862-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c6862-227">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c6862-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c6862-228">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c6862-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c6862-229">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c6862-229">Testing single sign-on</span></span>

<span data-ttu-id="c6862-230">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c6862-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c6862-231">Al hacer clic en icono de Heroku Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Heroku aplicación.</span><span class="sxs-lookup"><span data-stu-id="c6862-231">When you click hello Heroku tile in hello Access Panel, you should get automatically signed-on tooyour Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c6862-232">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c6862-232">Additional resources</span></span>

* [<span data-ttu-id="c6862-233">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6862-233">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c6862-234">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c6862-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png

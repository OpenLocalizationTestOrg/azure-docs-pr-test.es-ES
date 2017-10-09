---
title: "Tutorial: Integración de Azure Active Directory con &frankly | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y & sincero."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 92677b6fcd8609ca31f82a30e85c7010b7bb3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a><span data-ttu-id="cbca4-103">Tutorial: integración de Azure Active Directory con &frankly</span><span class="sxs-lookup"><span data-stu-id="cbca4-103">Tutorial: Azure Active Directory integration with &frankly</span></span>

<span data-ttu-id="cbca4-104">En este tutorial, aprenderá cómo toointegrate & sincero con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cbca4-104">In this tutorial, you learn how toointegrate &frankly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cbca4-105">Integrar & sincero con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="cbca4-105">Integrating &frankly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cbca4-106">Puede controlar en Azure AD que tenga acceso demasiado & sincero</span><span class="sxs-lookup"><span data-stu-id="cbca4-106">You can control in Azure AD who has access too&frankly</span></span>
- <span data-ttu-id="cbca4-107">Se pueden permitir a los usuarios obtener tooautomatically ha iniciado sesión demasiado & sincero (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cbca4-107">You can enable your users tooautomatically get signed-on too&frankly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cbca4-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cbca4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cbca4-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cbca4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbca4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cbca4-110">Prerequisites</span></span>

<span data-ttu-id="cbca4-111">integración de Azure AD tooconfigure con & sincero, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="cbca4-111">tooconfigure Azure AD integration with &frankly, you need hello following items:</span></span>

- <span data-ttu-id="cbca4-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cbca4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cbca4-113">Una suscripción habilitada para el inicio de sesión único en &frankly</span><span class="sxs-lookup"><span data-stu-id="cbca4-113">A &frankly single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cbca4-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="cbca4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cbca4-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="cbca4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cbca4-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cbca4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cbca4-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cbca4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cbca4-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="cbca4-118">Scenario description</span></span>
<span data-ttu-id="cbca4-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="cbca4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cbca4-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="cbca4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cbca4-121">Agregar & sincero desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cbca4-121">Adding &frankly from hello gallery</span></span>
2. <span data-ttu-id="cbca4-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cbca4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-frankly-from-hello-gallery"></a><span data-ttu-id="cbca4-123">Agregar & sincero desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cbca4-123">Adding &frankly from hello gallery</span></span>
<span data-ttu-id="cbca4-124">integración de hello tooconfigure de & sincero en Azure AD, necesita tooadd & sincero desde la lista de tooyour de hello Galería de aplicaciones de SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="cbca4-124">tooconfigure hello integration of &frankly into Azure AD, you need tooadd &frankly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cbca4-125">**tooadd & sincero desde la Galería de hello, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cbca4-125">**tooadd &frankly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbca4-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cbca4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cbca4-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cbca4-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="cbca4-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cbca4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="cbca4-133">En el cuadro de búsqueda de hello, escriba **& sincero**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-133">In hello search box, type **&frankly**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_search.png)

5. <span data-ttu-id="cbca4-135">En el panel de resultados de hello, seleccione **& sincero**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cbca4-135">In hello results panel, select **&frankly**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cbca4-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cbca4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cbca4-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con &frankly con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cbca4-138">In this section, you configure and test Azure AD single sign-on with &frankly based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cbca4-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué Hola usuario equivalente en & sincero es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cbca4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in &frankly is tooa user in Azure AD.</span></span> <span data-ttu-id="cbca4-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y usuario relacionado de hello en & sincero toobe necesidades establecida.</span><span class="sxs-lookup"><span data-stu-id="cbca4-140">In other words, a link relationship between an Azure AD user and hello related user in &frankly needs toobe established.</span></span>

<span data-ttu-id="cbca4-141">En & sincero, asignar un valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbca4-141">In &frankly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cbca4-142">tooconfigure y prueba de inicio de sesión único en Azure AD con & sincero, se necesita hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="cbca4-142">tooconfigure and test Azure AD single sign-on with &frankly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cbca4-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="cbca4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cbca4-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cbca4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cbca4-145">**[Crear una & sincero usuario de prueba](#creating-a-frankly-test-user)**  -toohave un equivalente de Britta Simon en & sincero decir vinculado toohello representación de Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="cbca4-145">**[Creating a &frankly test user](#creating-a-frankly-test-user)** - toohave a counterpart of Britta Simon in &frankly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cbca4-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cbca4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cbca4-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="cbca4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cbca4-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cbca4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cbca4-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar un inicio de sesión único en la & sincero aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cbca4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your &frankly application.</span></span>

<span data-ttu-id="cbca4-150">**tooconfigure Azure AD único inicio de sesión con & sincero, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cbca4-150">**tooconfigure Azure AD single sign-on with &frankly, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbca4-151">En el portal de Azure, en Hola Hola **& sincero** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-151">In hello Azure portal, on hello **&frankly** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="cbca4-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cbca4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_samlbase.png)

3. <span data-ttu-id="cbca4-155">En hello **& sincero dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="cbca4-155">On hello **&frankly Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url.png)

    <span data-ttu-id="cbca4-157">a.</span><span class="sxs-lookup"><span data-stu-id="cbca4-157">a.</span></span> <span data-ttu-id="cbca4-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="cbca4-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span></span>

    <span data-ttu-id="cbca4-159">b.</span><span class="sxs-lookup"><span data-stu-id="cbca4-159">b.</span></span> <span data-ttu-id="cbca4-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="cbca4-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span></span>

4. <span data-ttu-id="cbca4-161">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="cbca4-162">Si desea que aplicación de hello tooconfigure en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="cbca4-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url1.png)

    <span data-ttu-id="cbca4-164">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="cbca4-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span></span>
    > [!NOTE] 
    > <span data-ttu-id="cbca4-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="cbca4-165">These values are not real.</span></span> <span data-ttu-id="cbca4-166">Actualizar estos valores con hello identificador real, inicio de sesión y dirección URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="cbca4-166">Update these values with hello actual Identifier, Sign-on, and Reply URL.</span></span> <span data-ttu-id="cbca4-167">Póngase en contacto con [equipo de soporte técnico de andfrankly](mailto:help@andfrankly.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="cbca4-167">Contact [andfrankly support team](mailto:help@andfrankly.com) tooget these values.</span></span>

5. <span data-ttu-id="cbca4-168">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="cbca4-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_certificate.png) 

6. <span data-ttu-id="cbca4-170">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="cbca4-170">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-andfrankly-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="cbca4-172">tooconfigure inicio de sesión único en **& sincero** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de andfrankly](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="cbca4-172">tooconfigure single sign-on on **&frankly** side, you need toosend hello downloaded **Metadata XML** too[andfrankly support team](mailto:help@andfrankly.com).</span></span> 

> [!TIP]
> <span data-ttu-id="cbca4-173">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="cbca4-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cbca4-174">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="cbca4-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cbca4-175">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cbca4-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cbca4-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cbca4-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="cbca4-177">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="cbca4-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="cbca4-179">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cbca4-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbca4-180">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cbca4-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cbca4-182">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cbca4-184">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbca4-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cbca4-186">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="cbca4-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cbca4-188">a.</span><span class="sxs-lookup"><span data-stu-id="cbca4-188">a.</span></span> <span data-ttu-id="cbca4-189">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cbca4-190">b.</span><span class="sxs-lookup"><span data-stu-id="cbca4-190">b.</span></span> <span data-ttu-id="cbca4-191">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cbca4-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cbca4-192">c.</span><span class="sxs-lookup"><span data-stu-id="cbca4-192">c.</span></span> <span data-ttu-id="cbca4-193">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cbca4-194">d.</span><span class="sxs-lookup"><span data-stu-id="cbca4-194">d.</span></span> <span data-ttu-id="cbca4-195">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-195">Click **Create**.</span></span>
 
### <a name="creating-a-frankly-test-user"></a><span data-ttu-id="cbca4-196">Crear un usuario de prueba de &frankly</span><span class="sxs-lookup"><span data-stu-id="cbca4-196">Creating a &frankly test user</span></span>

<span data-ttu-id="cbca4-197">En esta sección, creará un usuario llamado Britta Simon en &frankly.</span><span class="sxs-lookup"><span data-stu-id="cbca4-197">In this section, you create a user called Britta Simon in &frankly.</span></span> <span data-ttu-id="cbca4-198">Trabajar con [equipo de soporte técnico de andfrankly](mailto:help@andfrankly.com) a los usuarios de tooadd hello en hello & sincero plataforma.</span><span class="sxs-lookup"><span data-stu-id="cbca4-198">Work with  [andfrankly support team](mailto:help@andfrankly.com) tooadd hello users in hello &frankly platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cbca4-199">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cbca4-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cbca4-200">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso demasiado & sincero.</span><span class="sxs-lookup"><span data-stu-id="cbca4-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too&frankly.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="cbca4-202">**tooassign Britta Simon demasiado & sincero, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cbca4-202">**tooassign Britta Simon too&frankly, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbca4-203">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="cbca4-205">En la lista de aplicaciones de hello, seleccione **& sincero**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-205">In hello applications list, select **&frankly**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_app.png) 

3. <span data-ttu-id="cbca4-207">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="cbca4-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-209">Click **Add** button.</span></span> <span data-ttu-id="cbca4-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="cbca4-212">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbca4-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cbca4-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cbca4-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cbca4-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cbca4-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="cbca4-215">Testing single sign-on</span></span>

<span data-ttu-id="cbca4-216">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="cbca4-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="cbca4-217">Cuando haga clic en hello & sincero disponer en mosaico en hello Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour & sincero aplicaciones</span><span class="sxs-lookup"><span data-stu-id="cbca4-217">When you click hello &frankly tile in hello Access Panel, you should get automatically signed-on tooyour &frankly application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cbca4-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="cbca4-218">Additional resources</span></span>

* [<span data-ttu-id="cbca4-219">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cbca4-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cbca4-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cbca4-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_203.png


---
title: "Tutorial: Integración de Azure Active Directory con Tableau Server | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el servidor de una plantilla."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="b16f6-103">Tutorial: Integración de Azure Active Directory con Tableau Server</span><span class="sxs-lookup"><span data-stu-id="b16f6-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="b16f6-104">En este tutorial, aprenderá cómo toointegrate Server Tableau con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b16f6-104">In this tutorial, you learn how toointegrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b16f6-105">Integración Tableau servidor con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b16f6-105">Integrating Tableau Server with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b16f6-106">Puede controlar en Azure AD que tenga acceso tooTableau Server</span><span class="sxs-lookup"><span data-stu-id="b16f6-106">You can control in Azure AD who has access tooTableau Server</span></span>
- <span data-ttu-id="b16f6-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTableau Server (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b16f6-107">You can enable your users tooautomatically get signed-on tooTableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b16f6-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b16f6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b16f6-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b16f6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b16f6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b16f6-110">Prerequisites</span></span>

<span data-ttu-id="b16f6-111">tooconfigure integración de Azure AD con el servidor de Tableau, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b16f6-111">tooconfigure Azure AD integration with Tableau Server, you need hello following items:</span></span>

- <span data-ttu-id="b16f6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b16f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b16f6-113">Una suscripción habilitada para el inicio de sesión único en Tableau Server</span><span class="sxs-lookup"><span data-stu-id="b16f6-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b16f6-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b16f6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b16f6-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b16f6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b16f6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b16f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b16f6-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b16f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b16f6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b16f6-118">Scenario description</span></span>
<span data-ttu-id="b16f6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b16f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b16f6-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="b16f6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b16f6-121">Agregar servidor de una plantilla de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="b16f6-121">Adding Tableau Server from hello gallery</span></span>
2. <span data-ttu-id="b16f6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b16f6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-hello-gallery"></a><span data-ttu-id="b16f6-123">Agregar servidor de una plantilla de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="b16f6-123">Adding Tableau Server from hello gallery</span></span>
<span data-ttu-id="b16f6-124">integración de hello tooconfigure de Tableau Server en Azure AD, deberá tooadd Server de una plantilla de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="b16f6-124">tooconfigure hello integration of Tableau Server into Azure AD, you need tooadd Tableau Server from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b16f6-125">**tooadd Tableau Server desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b16f6-125">**tooadd Tableau Server from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b16f6-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="b16f6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b16f6-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b16f6-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="b16f6-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b16f6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="b16f6-133">En el cuadro de búsqueda de hello, escriba **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-133">In hello search box, type **Tableau Server**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="b16f6-135">En el panel de resultados de hello, seleccione **Tableau Server**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b16f6-135">In hello results panel, select **Tableau Server**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b16f6-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b16f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b16f6-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Tableau Server con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b16f6-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b16f6-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el servidor de Tableau es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b16f6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Server is tooa user in Azure AD.</span></span> <span data-ttu-id="b16f6-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Tableau Server necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="b16f6-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Server needs toobe established.</span></span>

<span data-ttu-id="b16f6-141">En el servidor de Tableau, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b16f6-141">In Tableau Server, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b16f6-142">tooconfigure y prueba de inicio de sesión único en Azure AD con el servidor de una plantilla, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b16f6-142">tooconfigure and test Azure AD single sign-on with Tableau Server, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b16f6-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="b16f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b16f6-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b16f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b16f6-145">**[Crear un usuario de prueba de servidor Tableau](#creating-a-tableau-server-test-user)**  -toohave un equivalente de Britta Simon en servidor Tableau representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="b16f6-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - toohave a counterpart of Britta Simon in Tableau Server that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b16f6-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b16f6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b16f6-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="b16f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b16f6-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b16f6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b16f6-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de servidor de una plantilla.</span><span class="sxs-lookup"><span data-stu-id="b16f6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="b16f6-150">**inicio de sesión único en tooconfigure Azure AD con el servidor de Tableau, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b16f6-150">**tooconfigure Azure AD single sign-on with Tableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="b16f6-151">En el portal de Azure, en Hola Hola **Tableau Server** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-151">In hello Azure portal, on hello **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="b16f6-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b16f6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="b16f6-155">En hello **Tableau dominio del servidor y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b16f6-155">On hello **Tableau Server Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="b16f6-157">a.</span><span class="sxs-lookup"><span data-stu-id="b16f6-157">a.</span></span> <span data-ttu-id="b16f6-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="b16f6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="b16f6-159">b.</span><span class="sxs-lookup"><span data-stu-id="b16f6-159">b.</span></span> <span data-ttu-id="b16f6-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="b16f6-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="b16f6-161">c.</span><span class="sxs-lookup"><span data-stu-id="b16f6-161">c.</span></span> <span data-ttu-id="b16f6-162">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="b16f6-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="b16f6-163">Hello valores anteriores no son valores reales.</span><span class="sxs-lookup"><span data-stu-id="b16f6-163">hello preceding values are not real values.</span></span> <span data-ttu-id="b16f6-164">Posteriormente, actualizar valores de hello con dirección URL real de Hola y el identificador de página de configuración del servidor de una plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="b16f6-164">Later, you update hello values with hello actual URL and identifier from hello Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="b16f6-165">Aplicación de servidor tableau espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="b16f6-165">Tableau Server application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="b16f6-166">Configurar Hola después de notificaciones para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="b16f6-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="b16f6-167">Puede administrar valores de hello de estos atributos de hello **"Atributos de usuario"** sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b16f6-167">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="b16f6-168">Hello captura de pantalla siguiente muestra un ejemplo de Hola mismo.</span><span class="sxs-lookup"><span data-stu-id="b16f6-168">hello following screenshot shows an example for hello same.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="b16f6-170">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, configurar atributos de token de SAML como se muestra en la imagen de hello anterior y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b16f6-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="b16f6-171">Nombre del atributo</span><span class="sxs-lookup"><span data-stu-id="b16f6-171">Attribute Name</span></span> | <span data-ttu-id="b16f6-172">Valor de atributo</span><span class="sxs-lookup"><span data-stu-id="b16f6-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="b16f6-173">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="b16f6-173">username</span></span> | <span data-ttu-id="b16f6-174">*user.displayname*</span><span class="sxs-lookup"><span data-stu-id="b16f6-174">*user.displayname*</span></span> |

    <span data-ttu-id="b16f6-175">a.</span><span class="sxs-lookup"><span data-stu-id="b16f6-175">a.</span></span> <span data-ttu-id="b16f6-176">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b16f6-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="b16f6-179">b.</span><span class="sxs-lookup"><span data-stu-id="b16f6-179">b.</span></span> <span data-ttu-id="b16f6-180">Hola **nombre** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="b16f6-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b16f6-181">c.</span><span class="sxs-lookup"><span data-stu-id="b16f6-181">c.</span></span> <span data-ttu-id="b16f6-182">De hello **valor** lista, el valor de atributo de tipo hello se muestra para esa fila.</span><span class="sxs-lookup"><span data-stu-id="b16f6-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b16f6-183">d.</span><span class="sxs-lookup"><span data-stu-id="b16f6-183">d.</span></span> <span data-ttu-id="b16f6-184">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-184">Click **Ok**</span></span>


6. <span data-ttu-id="b16f6-185">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b16f6-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="b16f6-187">Haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-187">Click **Save** button.</span></span>

    <span data-ttu-id="b16f6-188">![Configuración del inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="b16f6-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="b16f6-189">tooget configurado para la aplicación de SSO, debe a inquilino de Tableau Server tooyour toosign la sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="b16f6-189">tooget SSO configured for your application, you need toosign-on tooyour Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="b16f6-190">a.</span><span class="sxs-lookup"><span data-stu-id="b16f6-190">a.</span></span> <span data-ttu-id="b16f6-191">En configuración del servidor de una plantilla de hello, haga clic en hello **SAML** ficha.</span><span class="sxs-lookup"><span data-stu-id="b16f6-191">In hello Tableau Server configuration, click hello **SAML** tab.</span></span>
  
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="b16f6-193">b.</span><span class="sxs-lookup"><span data-stu-id="b16f6-193">b.</span></span> <span data-ttu-id="b16f6-194">Casilla de Hola de **Use SAML para inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-194">Select hello checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="b16f6-195">c.</span><span class="sxs-lookup"><span data-stu-id="b16f6-195">c.</span></span> <span data-ttu-id="b16f6-196">Dirección URL de retorno de servidor tableau: Hola dirección URL que accederá los usuarios del servidor de una plantilla, por ejemplo, http://tableau_server.</span><span class="sxs-lookup"><span data-stu-id="b16f6-196">Tableau Server return URL—hello URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="b16f6-197">No se recomienda usar http://localhost.</span><span class="sxs-lookup"><span data-stu-id="b16f6-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="b16f6-198">No se permite usar una dirección URL con una barra diagonal final (por ejemplo, http://servidor_de_tableau/).</span><span class="sxs-lookup"><span data-stu-id="b16f6-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="b16f6-199">Copia **Tableau servidor la dirección URL de retorno** y péguelo tooAzure AD **dirección URL de inicio de sesión** en el cuadro de texto **Tableau dominio del servidor y las direcciones URL** sección.</span><span class="sxs-lookup"><span data-stu-id="b16f6-199">Copy **Tableau Server return URL** and paste it tooAzure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="b16f6-200">d.</span><span class="sxs-lookup"><span data-stu-id="b16f6-200">d.</span></span> <span data-ttu-id="b16f6-201">Id. de entidad SAML: Id. de entidad de hello identifica de forma única el toohello de instalación de servidor Tableau IdP.</span><span class="sxs-lookup"><span data-stu-id="b16f6-201">SAML entity ID—hello entity ID uniquely identifies your Tableau Server installation toohello IdP.</span></span> <span data-ttu-id="b16f6-202">Aquí puede especificar la dirección URL del servidor Tableau nuevo, si lo desea, pero no tiene toobe la dirección URL del servidor Tableau.</span><span class="sxs-lookup"><span data-stu-id="b16f6-202">You can enter your Tableau Server URL again here, if you like, but it does not have toobe your Tableau Server URL.</span></span> <span data-ttu-id="b16f6-203">Copia **Id. de entidad SAML** y péguelo tooAzure AD **identificador** en el cuadro de texto **Tableau dominio del servidor y las direcciones URL** sección.</span><span class="sxs-lookup"><span data-stu-id="b16f6-203">Copy **SAML entity ID** and paste it tooAzure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="b16f6-204">e.</span><span class="sxs-lookup"><span data-stu-id="b16f6-204">e.</span></span> <span data-ttu-id="b16f6-205">Haga clic en hello **Exportar archivo de metadatos** y ábralo en la aplicación de editor de texto hello.</span><span class="sxs-lookup"><span data-stu-id="b16f6-205">Click hello **Export Metadata File** and open it in hello text editor application.</span></span> <span data-ttu-id="b16f6-206">Busque la dirección URL del servicio de consumidor de aserción con Http Post y el índice 0 y copiar dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="b16f6-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy hello URL.</span></span> <span data-ttu-id="b16f6-207">Ahora pega tooAzure AD **dirección URL de respuesta** en el cuadro de texto **Tableau dominio del servidor y las direcciones URL** sección.</span><span class="sxs-lookup"><span data-stu-id="b16f6-207">Now paste it tooAzure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="b16f6-208">f.</span><span class="sxs-lookup"><span data-stu-id="b16f6-208">f.</span></span> <span data-ttu-id="b16f6-209">Busque el archivo de metadatos de federación descargado del portal de Azure y, a continuación, cargarlo en hello **archivo de metadatos de SAML Idp**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in hello **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="b16f6-210">g.</span><span class="sxs-lookup"><span data-stu-id="b16f6-210">g.</span></span> <span data-ttu-id="b16f6-211">Haga clic en hello **Aceptar** botón en la página de configuración del servidor de una plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="b16f6-211">Click hello **OK** button in hello Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="b16f6-212">Cliente tener tooupload cualquier certificado en la configuración de SSO de SAML del servidor de una plantilla de Hola y obtener omitirán Hola flujo SSO.</span><span class="sxs-lookup"><span data-stu-id="b16f6-212">Customer have tooupload any certificate in hello Tableau Server SAML SSO configuration and it will get ignored in hello SSO flow.</span></span>
    ><span data-ttu-id="b16f6-213">Si necesita ayuda para la configuración de SAML en el servidor de una plantilla, consulte el artículo de toothis [configurar SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="b16f6-213">If you need help configuring SAML on Tableau Server then please refer toothis article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="b16f6-214">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="b16f6-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b16f6-215">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="b16f6-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b16f6-216">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b16f6-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b16f6-217">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b16f6-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="b16f6-218">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="b16f6-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="b16f6-220">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b16f6-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b16f6-221">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="b16f6-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b16f6-223">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b16f6-225">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b16f6-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b16f6-227">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="b16f6-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b16f6-229">a.</span><span class="sxs-lookup"><span data-stu-id="b16f6-229">a.</span></span> <span data-ttu-id="b16f6-230">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b16f6-231">b.</span><span class="sxs-lookup"><span data-stu-id="b16f6-231">b.</span></span> <span data-ttu-id="b16f6-232">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b16f6-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b16f6-233">c.</span><span class="sxs-lookup"><span data-stu-id="b16f6-233">c.</span></span> <span data-ttu-id="b16f6-234">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b16f6-235">d.</span><span class="sxs-lookup"><span data-stu-id="b16f6-235">d.</span></span> <span data-ttu-id="b16f6-236">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="b16f6-237">Crear un usuario de prueba de Tableau Server</span><span class="sxs-lookup"><span data-stu-id="b16f6-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="b16f6-238">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en Tableau Server.</span><span class="sxs-lookup"><span data-stu-id="b16f6-238">hello objective of this section is toocreate a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="b16f6-239">Debe tooprovision todos los usuarios de hello en el servidor de una plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="b16f6-239">You need tooprovision all hello users in hello Tableau server.</span></span> 

<span data-ttu-id="b16f6-240">Ese nombre de usuario del usuario de hello debe coincidir con el valor de Hola que ha configurado en el atributo personalizado de hello Azure AD de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-240">That username of hello user should match hello value which you have configured in hello Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="b16f6-241">Con hello correcto de asignación de integración de hello debería funcionar [configurar Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="b16f6-241">With hello correct mapping hello integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="b16f6-242">Si necesita un usuario toocreate manualmente, debe toocontact hello Tableau Administrador de su organización.</span><span class="sxs-lookup"><span data-stu-id="b16f6-242">If you need toocreate a user manually, you need toocontact hello Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b16f6-243">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b16f6-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b16f6-244">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTableau Server.</span><span class="sxs-lookup"><span data-stu-id="b16f6-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Server.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="b16f6-246">**tooassign Britta Simon tooTableau servidor, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b16f6-246">**tooassign Britta Simon tooTableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="b16f6-247">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b16f6-249">En la lista de aplicaciones de hello, seleccione **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-249">In hello applications list, select **Tableau Server**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="b16f6-251">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="b16f6-253">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-253">Click **Add** button.</span></span> <span data-ttu-id="b16f6-254">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="b16f6-256">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="b16f6-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b16f6-257">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b16f6-258">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b16f6-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b16f6-259">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="b16f6-259">Testing single sign-on</span></span>

<span data-ttu-id="b16f6-260">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b16f6-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b16f6-261">Al hacer clic en icono de servidor de una plantilla de Hola Hola Panel de acceso, deberá obtener la aplicación de servidor de una plantilla de tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="b16f6-261">When you click hello Tableau Server tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Server application.</span></span>
<span data-ttu-id="b16f6-262">Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b16f6-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b16f6-263">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b16f6-263">Additional resources</span></span>

* [<span data-ttu-id="b16f6-264">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b16f6-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b16f6-265">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b16f6-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png


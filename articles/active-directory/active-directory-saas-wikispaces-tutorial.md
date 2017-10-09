---
title: "Tutorial: Integración de Azure Active Directory con Wikispaces | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Wikispaces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: eb5b72e60b415cb657b70ba530df731ae14b0425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a><span data-ttu-id="edaf1-103">Tutorial: Integración de Azure Active Directory con Wikispaces</span><span class="sxs-lookup"><span data-stu-id="edaf1-103">Tutorial: Azure Active Directory integration with Wikispaces</span></span>

<span data-ttu-id="edaf1-104">En este tutorial, aprenderá cómo toointegrate Wikispaces con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="edaf1-104">In this tutorial, you learn how toointegrate Wikispaces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="edaf1-105">Integración de Wikispaces con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="edaf1-105">Integrating Wikispaces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="edaf1-106">Puede controlar en Azure AD que tenga acceso tooWikispaces</span><span class="sxs-lookup"><span data-stu-id="edaf1-106">You can control in Azure AD who has access tooWikispaces</span></span>
- <span data-ttu-id="edaf1-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWikispaces (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="edaf1-107">You can enable your users tooautomatically get signed-on tooWikispaces (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="edaf1-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="edaf1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="edaf1-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="edaf1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edaf1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="edaf1-110">Prerequisites</span></span>

<span data-ttu-id="edaf1-111">integración de Azure AD con Wikispaces tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="edaf1-111">tooconfigure Azure AD integration with Wikispaces, you need hello following items:</span></span>

- <span data-ttu-id="edaf1-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="edaf1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="edaf1-113">Una suscripción habilitada para el inicio de sesión único en Wikispaces</span><span class="sxs-lookup"><span data-stu-id="edaf1-113">A Wikispaces single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="edaf1-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="edaf1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="edaf1-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="edaf1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="edaf1-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="edaf1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="edaf1-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="edaf1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="edaf1-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="edaf1-118">Scenario description</span></span>
<span data-ttu-id="edaf1-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="edaf1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="edaf1-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="edaf1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="edaf1-121">Agregar Wikispaces desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="edaf1-121">Adding Wikispaces from hello gallery</span></span>
2. <span data-ttu-id="edaf1-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="edaf1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wikispaces-from-hello-gallery"></a><span data-ttu-id="edaf1-123">Agregar Wikispaces desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="edaf1-123">Adding Wikispaces from hello gallery</span></span>
<span data-ttu-id="edaf1-124">integración de hello tooconfigure de Wikispaces en Azure AD, deberá tooadd Wikispaces de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="edaf1-124">tooconfigure hello integration of Wikispaces into Azure AD, you need tooadd Wikispaces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="edaf1-125">**tooadd Wikispaces de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="edaf1-125">**tooadd Wikispaces from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="edaf1-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="edaf1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="edaf1-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="edaf1-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="edaf1-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="edaf1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="edaf1-133">En el cuadro de búsqueda de hello, escriba **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-133">In hello search box, type **Wikispaces**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_search.png)

5. <span data-ttu-id="edaf1-135">En el panel de resultados de hello, seleccione **Wikispaces**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="edaf1-135">In hello results panel, select **Wikispaces**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="edaf1-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="edaf1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="edaf1-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Wikispaces con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="edaf1-138">In this section, you configure and test Azure AD single sign-on with Wikispaces based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="edaf1-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Wikispaces es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="edaf1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wikispaces is tooa user in Azure AD.</span></span> <span data-ttu-id="edaf1-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Wikispaces debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="edaf1-140">In other words, a link relationship between an Azure AD user and hello related user in Wikispaces needs toobe established.</span></span>

<span data-ttu-id="edaf1-141">En Wikispaces, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="edaf1-141">In Wikispaces, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="edaf1-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Wikispaces, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="edaf1-142">tooconfigure and test Azure AD single sign-on with Wikispaces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="edaf1-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="edaf1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="edaf1-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="edaf1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="edaf1-145">**[Crear un usuario de prueba de Wikispaces](#creating-a-wikispaces-test-user)**  -toohave un equivalente de Britta Simon en Wikispaces que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="edaf1-145">**[Creating a Wikispaces test user](#creating-a-wikispaces-test-user)** - toohave a counterpart of Britta Simon in Wikispaces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="edaf1-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="edaf1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="edaf1-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="edaf1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="edaf1-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="edaf1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="edaf1-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="edaf1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wikispaces application.</span></span>

<span data-ttu-id="edaf1-150">**inicio de sesión único en Azure AD tooconfigure con Wikispaces, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="edaf1-150">**tooconfigure Azure AD single sign-on with Wikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="edaf1-151">En el portal de Azure, en Hola Hola **Wikispaces** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-151">In hello Azure portal, on hello **Wikispaces** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="edaf1-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="edaf1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_samlbase.png)

3. <span data-ttu-id="edaf1-155">En hello **Wikispaces dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="edaf1-155">On hello **Wikispaces Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_url.png)

    <span data-ttu-id="edaf1-157">a.</span><span class="sxs-lookup"><span data-stu-id="edaf1-157">a.</span></span> <span data-ttu-id="edaf1-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.wikispaces.net`</span><span class="sxs-lookup"><span data-stu-id="edaf1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.wikispaces.net`</span></span>

    <span data-ttu-id="edaf1-159">b.</span><span class="sxs-lookup"><span data-stu-id="edaf1-159">b.</span></span> <span data-ttu-id="edaf1-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://session.wikispaces.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="edaf1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://session.wikispaces.net/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="edaf1-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="edaf1-161">These values are not real.</span></span> <span data-ttu-id="edaf1-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="edaf1-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="edaf1-163">Póngase en contacto con [equipo de soporte técnico de Wikispaces cliente](https://www.wikispaces.com/site/help) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="edaf1-163">Contact [Wikispaces Client support team](https://www.wikispaces.com/site/help) tooget these values.</span></span> 

4. <span data-ttu-id="edaf1-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="edaf1-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_certificate.png) 

5. <span data-ttu-id="edaf1-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="edaf1-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wikispaces-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="edaf1-168">inicio de sesión único en tooconfigure en **Wikispaces** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de Wikispaces](https://www.wikispaces.com/site/help).</span><span class="sxs-lookup"><span data-stu-id="edaf1-168">tooconfigure single sign-on on **Wikispaces** side, you need toosend hello downloaded **Metadata XML** too[Wikispaces support team](https://www.wikispaces.com/site/help).</span></span> <span data-ttu-id="edaf1-169">Recibirá una notificación en cuanto se ha completado la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="edaf1-169">You will get a notification as soon as hello configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="edaf1-170">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="edaf1-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="edaf1-171">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="edaf1-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="edaf1-172">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="edaf1-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="edaf1-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="edaf1-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="edaf1-174">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="edaf1-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="edaf1-176">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="edaf1-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="edaf1-177">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="edaf1-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="edaf1-179">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="edaf1-181">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="edaf1-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="edaf1-183">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="edaf1-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="edaf1-185">a.</span><span class="sxs-lookup"><span data-stu-id="edaf1-185">a.</span></span> <span data-ttu-id="edaf1-186">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="edaf1-187">b.</span><span class="sxs-lookup"><span data-stu-id="edaf1-187">b.</span></span> <span data-ttu-id="edaf1-188">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="edaf1-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="edaf1-189">c.</span><span class="sxs-lookup"><span data-stu-id="edaf1-189">c.</span></span> <span data-ttu-id="edaf1-190">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="edaf1-191">d.</span><span class="sxs-lookup"><span data-stu-id="edaf1-191">d.</span></span> <span data-ttu-id="edaf1-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-192">Click **Create**.</span></span>
 
### <a name="creating-a-wikispaces-test-user"></a><span data-ttu-id="edaf1-193">Creación de un usuario de prueba de Wikispaces</span><span class="sxs-lookup"><span data-stu-id="edaf1-193">Creating a Wikispaces test user</span></span>

<span data-ttu-id="edaf1-194">En orden tooenable toolog de los usuarios de Azure AD en tooWikispaces, se les deben aprovisionar en Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="edaf1-194">In order tooenable Azure AD users toolog in tooWikispaces, they must be provisioned into Wikispaces.</span></span> <span data-ttu-id="edaf1-195">En caso de hello de Wikispaces, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="edaf1-195">In hello case of Wikispaces, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="edaf1-196">tooprovision una cuenta de usuario, realizar Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="edaf1-196">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="edaf1-197">Inicie sesión en tooyour **Wikispaces** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="edaf1-197">Log in tooyour **Wikispaces** company site as an administrator.</span></span>

2. <span data-ttu-id="edaf1-198">Vaya demasiado**miembros**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-198">Go too**Members**.</span></span>
   
    <span data-ttu-id="edaf1-199">![Miembros](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Miembros")</span><span class="sxs-lookup"><span data-stu-id="edaf1-199">![Members](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Members")</span></span>

3. <span data-ttu-id="edaf1-200">Haga clic en hello **invitar personas**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-200">Click hello **Invite People**.</span></span>
   
    <span data-ttu-id="edaf1-201">![Invitar a personas](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invitar a personas")</span><span class="sxs-lookup"><span data-stu-id="edaf1-201">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invite People")</span></span>

4. <span data-ttu-id="edaf1-202">Hola **invitar personas** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="edaf1-202">In hello **Invite People** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="edaf1-203">![Invitar a personas](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invitar a personas")</span><span class="sxs-lookup"><span data-stu-id="edaf1-203">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invite People")</span></span>
   
    <span data-ttu-id="edaf1-204">a.</span><span class="sxs-lookup"><span data-stu-id="edaf1-204">a.</span></span> <span data-ttu-id="edaf1-205">Hola de tipo **nombres de usuario o la dirección de correo electrónico** de una cuenta válida de AAD que quiera tooprovision en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="edaf1-205">Type hello **Usernames or Email Address** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="edaf1-206">b.</span><span class="sxs-lookup"><span data-stu-id="edaf1-206">b.</span></span> <span data-ttu-id="edaf1-207">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-207">Click **Send**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="edaf1-208">titular de la cuenta de Hello Azure Active Directory recibe un correo electrónico con una cuenta de hello tooconfirm vínculo antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="edaf1-208">hello Azure Active Directory account holder receives an email including a link tooconfirm hello account before it becomes active.</span></span>
    
> [!NOTE]
> <span data-ttu-id="edaf1-209">Puede usar cualquier otra Wikispaces usuario cuenta herramienta de creación o las API proporcionadas por Wikispaces tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="edaf1-209">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="edaf1-210">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="edaf1-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="edaf1-211">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWikispaces.</span><span class="sxs-lookup"><span data-stu-id="edaf1-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWikispaces.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="edaf1-213">**tooassign Britta Simon tooWikispaces, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="edaf1-213">**tooassign Britta Simon tooWikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="edaf1-214">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="edaf1-216">En la lista de aplicaciones de hello, seleccione **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-216">In hello applications list, select **Wikispaces**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_app.png) 

3. <span data-ttu-id="edaf1-218">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="edaf1-220">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-220">Click **Add** button.</span></span> <span data-ttu-id="edaf1-221">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="edaf1-223">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="edaf1-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="edaf1-224">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="edaf1-225">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="edaf1-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="edaf1-226">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="edaf1-226">Testing single sign-on</span></span>

<span data-ttu-id="edaf1-227">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="edaf1-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="edaf1-228">Al hacer clic en hello Wikispaces disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour aplicación Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="edaf1-228">When you click hello Wikispaces tile in hello Access Panel, you should get automatically signed-on tooyour Wikispaces application.</span></span>
<span data-ttu-id="edaf1-229">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="edaf1-229">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="edaf1-230">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="edaf1-230">Additional resources</span></span>

* [<span data-ttu-id="edaf1-231">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="edaf1-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="edaf1-232">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="edaf1-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_203.png


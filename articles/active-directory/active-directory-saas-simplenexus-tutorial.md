---
title: "Tutorial: integración de Azure Active Directory con SimpleNexus | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SimpleNexus."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89821a05-88e2-4579-b144-0123b2b9cb95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 89f455d8c551045ddfcbe7234e86b13dad1140a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-simplenexus"></a><span data-ttu-id="57cbd-103">Tutorial: Integración de Azure Active Directory con SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="57cbd-103">Tutorial: Azure Active Directory integration with SimpleNexus</span></span>

<span data-ttu-id="57cbd-104">En este tutorial, aprenderá cómo toointegrate SimpleNexus con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57cbd-104">In this tutorial, you learn how toointegrate SimpleNexus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57cbd-105">Integración de SimpleNexus con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="57cbd-105">Integrating SimpleNexus with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="57cbd-106">Puede controlar en Azure AD que tenga acceso tooSimpleNexus</span><span class="sxs-lookup"><span data-stu-id="57cbd-106">You can control in Azure AD who has access tooSimpleNexus</span></span>
- <span data-ttu-id="57cbd-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSimpleNexus (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="57cbd-107">You can enable your users tooautomatically get signed-on tooSimpleNexus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57cbd-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="57cbd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="57cbd-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57cbd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57cbd-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="57cbd-110">Prerequisites</span></span>

<span data-ttu-id="57cbd-111">integración de Azure AD con SimpleNexus tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="57cbd-111">tooconfigure Azure AD integration with SimpleNexus, you need hello following items:</span></span>

- <span data-ttu-id="57cbd-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="57cbd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57cbd-113">Una suscripción habilitada para el inicio de sesión único en SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="57cbd-113">A SimpleNexus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57cbd-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="57cbd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57cbd-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="57cbd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57cbd-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="57cbd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57cbd-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57cbd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57cbd-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="57cbd-118">Scenario description</span></span>
<span data-ttu-id="57cbd-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="57cbd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57cbd-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="57cbd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57cbd-121">Agregar SimpleNexus desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="57cbd-121">Adding SimpleNexus from hello gallery</span></span>
2. <span data-ttu-id="57cbd-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="57cbd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-simplenexus-from-hello-gallery"></a><span data-ttu-id="57cbd-123">Agregar SimpleNexus desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="57cbd-123">Adding SimpleNexus from hello gallery</span></span>
<span data-ttu-id="57cbd-124">integración de hello tooconfigure de SimpleNexus en Azure AD, deberá tooadd SimpleNexus de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="57cbd-124">tooconfigure hello integration of SimpleNexus into Azure AD, you need tooadd SimpleNexus from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="57cbd-125">**tooadd SimpleNexus de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="57cbd-125">**tooadd SimpleNexus from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="57cbd-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="57cbd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="57cbd-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="57cbd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="57cbd-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="57cbd-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="57cbd-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="57cbd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="57cbd-133">En el cuadro de búsqueda de hello, escriba **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="57cbd-133">In hello search box, type **SimpleNexus**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_search.png)

5. <span data-ttu-id="57cbd-135">En el panel de resultados de hello, seleccione **SimpleNexus**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="57cbd-135">In hello results panel, select **SimpleNexus**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="57cbd-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="57cbd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="57cbd-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SimpleNexus con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="57cbd-138">In this section, you configure and test Azure AD single sign-on with SimpleNexus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="57cbd-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en SimpleNexus es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57cbd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SimpleNexus is tooa user in Azure AD.</span></span> <span data-ttu-id="57cbd-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SimpleNexus debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="57cbd-140">In other words, a link relationship between an Azure AD user and hello related user in SimpleNexus needs toobe established.</span></span>

<span data-ttu-id="57cbd-141">En SimpleNexus, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="57cbd-141">In SimpleNexus, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="57cbd-142">tooconfigure y prueba de inicio de sesión único en Azure AD con SimpleNexus, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="57cbd-142">tooconfigure and test Azure AD single sign-on with SimpleNexus, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="57cbd-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="57cbd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="57cbd-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57cbd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57cbd-145">**[Crear un usuario de prueba de SimpleNexus](#creating-a-simplenexus-test-user)**  -toohave un equivalente de Britta Simon en SimpleNexus que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="57cbd-145">**[Creating a SimpleNexus test user](#creating-a-simplenexus-test-user)** - toohave a counterpart of Britta Simon in SimpleNexus that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="57cbd-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="57cbd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57cbd-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="57cbd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="57cbd-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="57cbd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="57cbd-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="57cbd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SimpleNexus application.</span></span>

<span data-ttu-id="57cbd-150">**inicio de sesión único en Azure AD tooconfigure con SimpleNexus, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="57cbd-150">**tooconfigure Azure AD single sign-on with SimpleNexus, perform hello following steps:**</span></span>

1. <span data-ttu-id="57cbd-151">En el portal de Azure, en Hola Hola **SimpleNexus** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="57cbd-151">In hello Azure portal, on hello **SimpleNexus** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="57cbd-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="57cbd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_samlbase.png)

3. <span data-ttu-id="57cbd-155">En hello **SimpleNexus dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="57cbd-155">On hello **SimpleNexus Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_url.png)

    <span data-ttu-id="57cbd-157">a.</span><span class="sxs-lookup"><span data-stu-id="57cbd-157">a.</span></span> <span data-ttu-id="57cbd-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://simplenexus.com/<companyname>_login`</span><span class="sxs-lookup"><span data-stu-id="57cbd-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://simplenexus.com/<companyname>_login`</span></span>

    <span data-ttu-id="57cbd-159">b.</span><span class="sxs-lookup"><span data-stu-id="57cbd-159">b.</span></span> <span data-ttu-id="57cbd-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://simplenexus.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="57cbd-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://simplenexus.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="57cbd-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="57cbd-161">These values are not real.</span></span> <span data-ttu-id="57cbd-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="57cbd-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="57cbd-163">Póngase en contacto con [equipo de soporte técnico de SimpleNexus cliente](https://simplenexus.com/site/contact) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="57cbd-163">Contact [SimpleNexus Client support team](https://simplenexus.com/site/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="57cbd-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="57cbd-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_certificate.png) 

5. <span data-ttu-id="57cbd-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="57cbd-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-simplenexus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="57cbd-168">inicio de sesión único en tooconfigure en **SimpleNexus** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de SimpleNexus](https://simplenexus.com/site/contact).</span><span class="sxs-lookup"><span data-stu-id="57cbd-168">tooconfigure single sign-on on **SimpleNexus** side, you need toosend hello downloaded **Metadata XML** too[SimpleNexus support team](https://simplenexus.com/site/contact).</span></span> <span data-ttu-id="57cbd-169">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="57cbd-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="57cbd-170">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="57cbd-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="57cbd-171">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="57cbd-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="57cbd-172">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="57cbd-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="57cbd-173">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="57cbd-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="57cbd-174">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="57cbd-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="57cbd-176">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="57cbd-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="57cbd-177">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="57cbd-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57cbd-179">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="57cbd-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57cbd-181">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="57cbd-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57cbd-183">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="57cbd-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57cbd-185">a.</span><span class="sxs-lookup"><span data-stu-id="57cbd-185">a.</span></span> <span data-ttu-id="57cbd-186">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57cbd-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57cbd-187">b.</span><span class="sxs-lookup"><span data-stu-id="57cbd-187">b.</span></span> <span data-ttu-id="57cbd-188">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="57cbd-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57cbd-189">c.</span><span class="sxs-lookup"><span data-stu-id="57cbd-189">c.</span></span> <span data-ttu-id="57cbd-190">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="57cbd-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="57cbd-191">d.</span><span class="sxs-lookup"><span data-stu-id="57cbd-191">d.</span></span> <span data-ttu-id="57cbd-192">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="57cbd-192">Click **Create**.</span></span>
 
### <a name="creating-a-simplenexus-test-user"></a><span data-ttu-id="57cbd-193">Creación de un usuario de prueba de SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="57cbd-193">Creating a SimpleNexus test user</span></span>

<span data-ttu-id="57cbd-194">En orden tooenable toolog de los usuarios de Azure AD en tooSimpleNexus, se les deben aprovisionar en SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="57cbd-194">In order tooenable Azure AD users toolog in tooSimpleNexus, they must be provisioned into SimpleNexus.</span></span>

<span data-ttu-id="57cbd-195">Hola caso de SimpleNexus, el aprovisionamiento es una tarea manual realizada por el Administrador de inquilinos de Hola.</span><span class="sxs-lookup"><span data-stu-id="57cbd-195">In hello case of SimpleNexus, provisioning is a manual task performed by hello tenant administrator.</span></span>

>[!NOTE]
><span data-ttu-id="57cbd-196">Puede usar cualquier otra SimpleNexus usuario cuenta herramienta de creación o las API proporcionadas por SimpleNexus tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="57cbd-196">You can use any other SimpleNexus user account creation tools or APIs provided by SimpleNexus tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="57cbd-197">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="57cbd-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="57cbd-198">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="57cbd-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSimpleNexus.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="57cbd-200">**tooassign Britta Simon tooSimpleNexus, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="57cbd-200">**tooassign Britta Simon tooSimpleNexus, perform hello following steps:**</span></span>

1. <span data-ttu-id="57cbd-201">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="57cbd-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="57cbd-203">En la lista de aplicaciones de hello, seleccione **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="57cbd-203">In hello applications list, select **SimpleNexus**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_app.png) 

3. <span data-ttu-id="57cbd-205">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="57cbd-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="57cbd-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="57cbd-207">Click **Add** button.</span></span> <span data-ttu-id="57cbd-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="57cbd-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="57cbd-210">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="57cbd-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="57cbd-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="57cbd-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57cbd-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="57cbd-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="57cbd-213">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="57cbd-213">Testing single sign-on</span></span>

<span data-ttu-id="57cbd-214">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="57cbd-214">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="57cbd-215">Al hacer clic en hello SimpleNexus disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour aplicación SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="57cbd-215">When you click hello SimpleNexus tile in hello Access Panel, you should get automatically signed-on tooyour SimpleNexus application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="57cbd-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="57cbd-216">Additional resources</span></span>

* [<span data-ttu-id="57cbd-217">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57cbd-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57cbd-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="57cbd-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_203.png


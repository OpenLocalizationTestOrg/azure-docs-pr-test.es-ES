---
title: "Tutorial: integración de Azure Active Directory con Expensify | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Expensify."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: 141513ef27c90dae2d77a52ecab2f89c4e5a55ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="c477b-103">Tutorial: Integración de Azure Active Directory con Expensify</span><span class="sxs-lookup"><span data-stu-id="c477b-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="c477b-104">En este tutorial, aprenderá cómo toointegrate Expensify con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c477b-104">In this tutorial, you learn how toointegrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c477b-105">Integración Expensify con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c477b-105">Integrating Expensify with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c477b-106">Puede controlar en Azure AD que tenga acceso tooExpensify</span><span class="sxs-lookup"><span data-stu-id="c477b-106">You can control in Azure AD who has access tooExpensify</span></span>
- <span data-ttu-id="c477b-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooExpensify (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c477b-107">You can enable your users tooautomatically get signed-on tooExpensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c477b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c477b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c477b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c477b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c477b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c477b-110">Prerequisites</span></span>

<span data-ttu-id="c477b-111">integración de Azure AD con Expensify tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c477b-111">tooconfigure Azure AD integration with Expensify, you need hello following items:</span></span>

- <span data-ttu-id="c477b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c477b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c477b-113">Una suscripción habilitada para el inicio de sesión único en Expensify</span><span class="sxs-lookup"><span data-stu-id="c477b-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c477b-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c477b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c477b-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c477b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c477b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c477b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c477b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c477b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c477b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c477b-118">Scenario description</span></span>
<span data-ttu-id="c477b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c477b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c477b-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c477b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c477b-121">Agregar Expensify desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c477b-121">Adding Expensify from hello gallery</span></span>
2. <span data-ttu-id="c477b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c477b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-hello-gallery"></a><span data-ttu-id="c477b-123">Agregar Expensify desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c477b-123">Adding Expensify from hello gallery</span></span>
<span data-ttu-id="c477b-124">integración de hello tooconfigure de Expensify en Azure AD, deberá tooadd Expensify de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c477b-124">tooconfigure hello integration of Expensify into Azure AD, you need tooadd Expensify from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c477b-125">**tooadd Expensify de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c477b-125">**tooadd Expensify from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c477b-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c477b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c477b-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c477b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c477b-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c477b-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c477b-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c477b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c477b-133">En el cuadro de búsqueda de hello, escriba **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="c477b-133">In hello search box, type **Expensify**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="c477b-135">En el panel de resultados de hello, seleccione **Expensify**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c477b-135">In hello results panel, select **Expensify**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c477b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c477b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c477b-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Expensify con un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c477b-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c477b-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Expensify es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c477b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Expensify is tooa user in Azure AD.</span></span> <span data-ttu-id="c477b-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Expensify debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c477b-140">In other words, a link relationship between an Azure AD user and hello related user in Expensify needs toobe established.</span></span>

<span data-ttu-id="c477b-141">En Expensify, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c477b-141">In Expensify, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c477b-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Expensify, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c477b-142">tooconfigure and test Azure AD single sign-on with Expensify, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c477b-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c477b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c477b-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c477b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c477b-145">**[Creación de un usuario de prueba Expensify](#creating-an-expensify-test-user)**  -toohave un equivalente de Britta Simon en Expensify que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="c477b-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - toohave a counterpart of Britta Simon in Expensify that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c477b-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c477b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c477b-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c477b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c477b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c477b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c477b-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Expensify.</span><span class="sxs-lookup"><span data-stu-id="c477b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="c477b-150">**inicio de sesión único en Azure AD tooconfigure con Expensify, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c477b-150">**tooconfigure Azure AD single sign-on with Expensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="c477b-151">En el portal de Azure, en Hola Hola **Expensify** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c477b-151">In hello Azure portal, on hello **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c477b-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c477b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="c477b-155">En hello **Expensify dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c477b-155">On hello **Expensify Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="c477b-157">a.</span><span class="sxs-lookup"><span data-stu-id="c477b-157">a.</span></span> <span data-ttu-id="c477b-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.expensify.com/authentication/saml/login`</span><span class="sxs-lookup"><span data-stu-id="c477b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="c477b-159">b.</span><span class="sxs-lookup"><span data-stu-id="c477b-159">b.</span></span> <span data-ttu-id="c477b-160">Hola **dirección URL de identificación** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="c477b-160">In hello **Identifier URL** textbox, type a URL using hello following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="c477b-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="c477b-161">These values are not real.</span></span> <span data-ttu-id="c477b-162">Actualizar estos valores con dirección URL de inicio de sesión en la dirección URL y el identificador del real Hola.</span><span class="sxs-lookup"><span data-stu-id="c477b-162">Update these values with hello actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="c477b-163">Póngase en contacto con [equipo de soporte técnico de cliente Expensify](mailto:help@expensify.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="c477b-163">Contact [Expensify Client support team](mailto:help@expensify.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="c477b-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c477b-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="c477b-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c477b-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c477b-168">tooenable SSO en Expensify, primero debe tooenable **Control de dominio** en aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c477b-168">tooenable SSO in Expensify, you first need tooenable **Domain Control** in hello application.</span></span> <span data-ttu-id="c477b-169">Puede habilitar el Control de dominio de aplicación Hola a través de pasos de hello enumerados [aquí](http://help.expensify.com/domain-control).</span><span class="sxs-lookup"><span data-stu-id="c477b-169">You can enable Domain Control in hello application through hello steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="c477b-170">Para más información, trabaje con el [equipo de soporte técnico de cliente de Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="c477b-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="c477b-171">Una vez habilitado el control de dominio, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c477b-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="c477b-173">a.</span><span class="sxs-lookup"><span data-stu-id="c477b-173">a.</span></span> <span data-ttu-id="c477b-174">Inicie sesión en tooyour Expensify aplicación.</span><span class="sxs-lookup"><span data-stu-id="c477b-174">Sign on tooyour Expensify application.</span></span>
    
    <span data-ttu-id="c477b-175">b.</span><span class="sxs-lookup"><span data-stu-id="c477b-175">b.</span></span> <span data-ttu-id="c477b-176">En la barra de herramientas de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="c477b-176">In hello toolbar on hello top, click **Admin**.</span></span>
    
    <span data-ttu-id="c477b-177">c.</span><span class="sxs-lookup"><span data-stu-id="c477b-177">c.</span></span> <span data-ttu-id="c477b-178">En el panel izquierdo de hello, haga clic en **dominio**.</span><span class="sxs-lookup"><span data-stu-id="c477b-178">In hello left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="c477b-179">d.</span><span class="sxs-lookup"><span data-stu-id="c477b-179">d.</span></span> <span data-ttu-id="c477b-180">Haga clic en su nombre de dominio comprobado.</span><span class="sxs-lookup"><span data-stu-id="c477b-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="c477b-181">e.</span><span class="sxs-lookup"><span data-stu-id="c477b-181">e.</span></span> <span data-ttu-id="c477b-182">En el panel izquierdo de hello, haga clic en **SAML**y, a continuación, seleccione **habilitado**.</span><span class="sxs-lookup"><span data-stu-id="c477b-182">In hello left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="c477b-183">f.</span><span class="sxs-lookup"><span data-stu-id="c477b-183">f.</span></span> <span data-ttu-id="c477b-184">Hola abierto descarga los metadatos de federación de Azure AD en el Bloc de notas, Hola copiar contenido y, a continuación, péguelo en hello **metadatos del proveedor de identidades** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c477b-184">Open hello downloaded Federation Metadata from Azure AD in notepad, copy hello content, and then paste it into hello **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="c477b-185">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="c477b-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c477b-186">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="c477b-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c477b-187">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c477b-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c477b-188">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c477b-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="c477b-189">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c477b-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c477b-191">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c477b-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c477b-192">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c477b-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c477b-194">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c477b-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c477b-196">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c477b-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c477b-198">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c477b-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c477b-200">a.</span><span class="sxs-lookup"><span data-stu-id="c477b-200">a.</span></span> <span data-ttu-id="c477b-201">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c477b-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c477b-202">b.</span><span class="sxs-lookup"><span data-stu-id="c477b-202">b.</span></span> <span data-ttu-id="c477b-203">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c477b-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c477b-204">c.</span><span class="sxs-lookup"><span data-stu-id="c477b-204">c.</span></span> <span data-ttu-id="c477b-205">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c477b-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c477b-206">d.</span><span class="sxs-lookup"><span data-stu-id="c477b-206">d.</span></span> <span data-ttu-id="c477b-207">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c477b-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="c477b-208">Creación de un usuario de prueba de Expensify</span><span class="sxs-lookup"><span data-stu-id="c477b-208">Creating an Expensify test user</span></span>

<span data-ttu-id="c477b-209">En esta sección, creará un usuario denominado Britta Simon en Expensify.</span><span class="sxs-lookup"><span data-stu-id="c477b-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="c477b-210">Trabajar con [equipo de soporte técnico de Expensify cliente](mailto:help@expensify.com) a los usuarios de tooadd hello en la plataforma de Expensify Hola.</span><span class="sxs-lookup"><span data-stu-id="c477b-210">Work with [Expensify Client support team](mailto:help@expensify.com) tooadd hello users in hello Expensify platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c477b-211">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c477b-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c477b-212">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooExpensify.</span><span class="sxs-lookup"><span data-stu-id="c477b-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooExpensify.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c477b-214">**tooassign Britta Simon tooExpensify, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c477b-214">**tooassign Britta Simon tooExpensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="c477b-215">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c477b-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c477b-217">En la lista de aplicaciones de hello, seleccione **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="c477b-217">In hello applications list, select **Expensify**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="c477b-219">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c477b-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c477b-221">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c477b-221">Click **Add** button.</span></span> <span data-ttu-id="c477b-222">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c477b-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c477b-224">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c477b-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c477b-225">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c477b-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c477b-226">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c477b-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c477b-227">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c477b-227">Testing single sign-on</span></span>

<span data-ttu-id="c477b-228">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c477b-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="c477b-229">Al hacer clic en icono de Expensify Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Expensify aplicación.</span><span class="sxs-lookup"><span data-stu-id="c477b-229">When you click hello Expensify tile in hello Access Panel, you should get automatically signed-on tooyour Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c477b-230">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c477b-230">Additional resources</span></span>

* [<span data-ttu-id="c477b-231">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c477b-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c477b-232">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c477b-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png


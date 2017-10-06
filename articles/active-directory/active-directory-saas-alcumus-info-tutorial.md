---
title: "Tutorial: integración de Azure Active Directory con Alcumus Info Exchange | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Alcumus información de Exchange."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d26034b8-f0d5-4f65-aa56-0fc168ceec8c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 4ef9f4d654b6c451db44f929bdad1016304168b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-alcumus-info-exchange"></a><span data-ttu-id="cde36-103">Tutorial: Integración de Azure Active Directory con Alcumus Info Exchange</span><span class="sxs-lookup"><span data-stu-id="cde36-103">Tutorial: Azure Active Directory integration with Alcumus Info Exchange</span></span>

<span data-ttu-id="cde36-104">En este tutorial, aprenderá cómo toointegrate Alcumus información de Exchange con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cde36-104">In this tutorial, you learn how toointegrate Alcumus Info Exchange with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cde36-105">Integración de intercambio de información de Alcumus con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="cde36-105">Integrating Alcumus Info Exchange with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cde36-106">Puede controlar en Azure AD que tenga acceso tooAlcumus información de Exchange</span><span class="sxs-lookup"><span data-stu-id="cde36-106">You can control in Azure AD who has access tooAlcumus Info Exchange</span></span>
- <span data-ttu-id="cde36-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAlcumus información de Exchange (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cde36-107">You can enable your users tooautomatically get signed-on tooAlcumus Info Exchange (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cde36-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cde36-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cde36-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cde36-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cde36-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cde36-110">Prerequisites</span></span>

<span data-ttu-id="cde36-111">tooconfigure integración de Azure AD con Alcumus información de Exchange, necesitará Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="cde36-111">tooconfigure Azure AD integration with Alcumus Info Exchange, you need hello following items:</span></span>

- <span data-ttu-id="cde36-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cde36-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cde36-113">Una suscripción habilitada para inicio de sesión único en Alcumus Info Exchange</span><span class="sxs-lookup"><span data-stu-id="cde36-113">An Alcumus Info Exchange single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cde36-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="cde36-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cde36-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="cde36-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cde36-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cde36-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cde36-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cde36-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cde36-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="cde36-118">Scenario description</span></span>
<span data-ttu-id="cde36-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="cde36-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cde36-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="cde36-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cde36-121">Agregar Alcumus información de Exchange desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cde36-121">Adding Alcumus Info Exchange from hello gallery</span></span>
2. <span data-ttu-id="cde36-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cde36-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-alcumus-info-exchange-from-hello-gallery"></a><span data-ttu-id="cde36-123">Agregar Alcumus información de Exchange desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="cde36-123">Adding Alcumus Info Exchange from hello gallery</span></span>
<span data-ttu-id="cde36-124">integración de hello tooconfigure de intercambio de información de Alcumus en Azure AD, deberá tooadd Alcumus información de Exchange de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="cde36-124">tooconfigure hello integration of Alcumus Info Exchange into Azure AD, you need tooadd Alcumus Info Exchange from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cde36-125">**tooadd Alcumus información de Exchange desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cde36-125">**tooadd Alcumus Info Exchange from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cde36-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cde36-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cde36-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="cde36-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cde36-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cde36-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="cde36-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cde36-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="cde36-133">En el cuadro de búsqueda de hello, escriba **Alcumus información de Exchange**.</span><span class="sxs-lookup"><span data-stu-id="cde36-133">In hello search box, type **Alcumus Info Exchange**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_search.png)

5. <span data-ttu-id="cde36-135">En el panel de resultados de hello, seleccione **Alcumus información de Exchange**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cde36-135">In hello results panel, select **Alcumus Info Exchange**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cde36-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cde36-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cde36-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Alcumus Info Exchange con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cde36-138">In this section, you configure and test Azure AD single sign-on with Alcumus Info Exchange based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cde36-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en intercambio de información de Alcumus es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cde36-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Alcumus Info Exchange is tooa user in Azure AD.</span></span> <span data-ttu-id="cde36-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Alcumus información de Exchange debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="cde36-140">In other words, a link relationship between an Azure AD user and hello related user in Alcumus Info Exchange needs toobe established.</span></span>

<span data-ttu-id="cde36-141">En Alcumus información de Exchange, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cde36-141">In Alcumus Info Exchange, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cde36-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Alcumus información de Exchange, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="cde36-142">tooconfigure and test Azure AD single sign-on with Alcumus Info Exchange, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cde36-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="cde36-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cde36-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cde36-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cde36-145">**[Creación de un usuario de prueba de intercambio de información de Alcumus](#creating-an-alcumus-info-exchange-test-user)**  -toohave un equivalente de Britta Simon en Alcumus información de Exchange que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="cde36-145">**[Creating an Alcumus Info Exchange test user](#creating-an-alcumus-info-exchange-test-user)** - toohave a counterpart of Britta Simon in Alcumus Info Exchange that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cde36-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cde36-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cde36-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="cde36-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cde36-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cde36-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cde36-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de intercambio de información de Alcumus.</span><span class="sxs-lookup"><span data-stu-id="cde36-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Alcumus Info Exchange application.</span></span>

<span data-ttu-id="cde36-150">**tooconfigure inicio de sesión único en Azure AD con Alcumus información de Exchange, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cde36-150">**tooconfigure Azure AD single sign-on with Alcumus Info Exchange, perform hello following steps:**</span></span>

1. <span data-ttu-id="cde36-151">En el portal de Azure, en Hola Hola **Alcumus información de Exchange** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="cde36-151">In hello Azure portal, on hello **Alcumus Info Exchange** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="cde36-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cde36-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_samlbase.png)

3. <span data-ttu-id="cde36-155">En hello **Alcumus información de intercambio de dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cde36-155">On hello **Alcumus Info Exchange Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_url.png)

    <span data-ttu-id="cde36-157">a.</span><span class="sxs-lookup"><span data-stu-id="cde36-157">a.</span></span> <span data-ttu-id="cde36-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.info-exchange.com`</span><span class="sxs-lookup"><span data-stu-id="cde36-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.info-exchange.com`</span></span>

    <span data-ttu-id="cde36-159">b.</span><span class="sxs-lookup"><span data-stu-id="cde36-159">b.</span></span> <span data-ttu-id="cde36-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.info-exchange.com/Auth/`</span><span class="sxs-lookup"><span data-stu-id="cde36-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.info-exchange.com/Auth/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cde36-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="cde36-161">These values are not real.</span></span> <span data-ttu-id="cde36-162">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="cde36-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="cde36-163">Póngase en contacto con [equipo de soporte técnico de intercambio de información de Alcumus](mailto:helpdesk@alcumusgroup.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="cde36-163">Contact [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com) tooget these values.</span></span>
 
4. <span data-ttu-id="cde36-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="cde36-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_certificate.png) 

5. <span data-ttu-id="cde36-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="cde36-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cde36-168">tooconfigure inicio de sesión único en **Alcumus información de Exchange** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de intercambio de información de Alcumus](mailto:helpdesk@alcumusgroup.com).</span><span class="sxs-lookup"><span data-stu-id="cde36-168">tooconfigure single sign-on on **Alcumus Info Exchange** side, you need toosend hello downloaded **Metadata XML** too[Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com).</span></span>

> [!TIP]
> <span data-ttu-id="cde36-169">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="cde36-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cde36-170">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="cde36-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cde36-171">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cde36-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cde36-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cde36-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="cde36-173">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="cde36-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="cde36-175">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cde36-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cde36-176">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cde36-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cde36-178">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="cde36-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cde36-180">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cde36-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cde36-182">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="cde36-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cde36-184">a.</span><span class="sxs-lookup"><span data-stu-id="cde36-184">a.</span></span> <span data-ttu-id="cde36-185">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cde36-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cde36-186">b.</span><span class="sxs-lookup"><span data-stu-id="cde36-186">b.</span></span> <span data-ttu-id="cde36-187">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cde36-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cde36-188">c.</span><span class="sxs-lookup"><span data-stu-id="cde36-188">c.</span></span> <span data-ttu-id="cde36-189">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="cde36-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cde36-190">d.</span><span class="sxs-lookup"><span data-stu-id="cde36-190">d.</span></span> <span data-ttu-id="cde36-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cde36-191">Click **Create**.</span></span>
 
### <a name="creating-an-alcumus-info-exchange-test-user"></a><span data-ttu-id="cde36-192">Creación de un usuario de prueba de Alcumus Info Exchange</span><span class="sxs-lookup"><span data-stu-id="cde36-192">Creating an Alcumus Info Exchange test user</span></span>

<span data-ttu-id="cde36-193">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en Alcumus información de Exchange.</span><span class="sxs-lookup"><span data-stu-id="cde36-193">hello objective of this section is toocreate a user called Britta Simon in Alcumus Info Exchange.</span></span>

<span data-ttu-id="cde36-194">un usuario llamado Britta Simon en Alcumus información de Exchange, Hola póngase en contacto con toocreate [equipo de soporte técnico de intercambio de información de Alcumus](mailto:helpdesk@alcumusgroup.com).</span><span class="sxs-lookup"><span data-stu-id="cde36-194">toocreate a user called Britta Simon in Alcumus Info Exchange, Contact hello [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cde36-195">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cde36-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cde36-196">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAlcumus información de Exchange.</span><span class="sxs-lookup"><span data-stu-id="cde36-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAlcumus Info Exchange.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="cde36-198">**tooassign Britta Simon tooAlcumus información de Exchange, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cde36-198">**tooassign Britta Simon tooAlcumus Info Exchange, perform hello following steps:**</span></span>

1. <span data-ttu-id="cde36-199">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cde36-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="cde36-201">En la lista de aplicaciones de hello, seleccione **Alcumus información de Exchange**.</span><span class="sxs-lookup"><span data-stu-id="cde36-201">In hello applications list, select **Alcumus Info Exchange**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_app.png) 

3. <span data-ttu-id="cde36-203">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cde36-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="cde36-205">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="cde36-205">Click **Add** button.</span></span> <span data-ttu-id="cde36-206">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cde36-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="cde36-208">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="cde36-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cde36-209">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cde36-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cde36-210">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cde36-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cde36-211">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="cde36-211">Testing single sign-on</span></span>

<span data-ttu-id="cde36-212">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="cde36-212">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="cde36-213">Al hacer clic en icono de intercambio de información de Alcumus Hola Hola Panel de acceso, deberá obtener la aplicación de intercambio de información de Alcumus tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="cde36-213">When you click hello Alcumus Info Exchange tile in hello Access Panel, you should get automatically signed-on tooyour Alcumus Info Exchange application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cde36-214">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="cde36-214">Additional resources</span></span>

* [<span data-ttu-id="cde36-215">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cde36-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cde36-216">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cde36-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_203.png


---
title: "Tutorial: Integración de Azure Active Directory con Convercent | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Convercent."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: e6d09d7de52779dcf05e80215df9369ebc2ed06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="f005a-103">Tutorial: Integración de Azure Active Directory con Convercent</span><span class="sxs-lookup"><span data-stu-id="f005a-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="f005a-104">En este tutorial, aprenderá cómo toointegrate Convercent con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f005a-104">In this tutorial, you learn how toointegrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f005a-105">Integración Convercent con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f005a-105">Integrating Convercent with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f005a-106">Puede controlar en Azure AD que tenga acceso tooConvercent</span><span class="sxs-lookup"><span data-stu-id="f005a-106">You can control in Azure AD who has access tooConvercent</span></span>
- <span data-ttu-id="f005a-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooConvercent (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f005a-107">You can enable your users tooautomatically get signed-on tooConvercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f005a-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f005a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f005a-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f005a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f005a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f005a-110">Prerequisites</span></span>

<span data-ttu-id="f005a-111">integración de Azure AD con Convercent tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f005a-111">tooconfigure Azure AD integration with Convercent, you need hello following items:</span></span>

- <span data-ttu-id="f005a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f005a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f005a-113">Una suscripción habilitada para el inicio de sesión único en Convercent</span><span class="sxs-lookup"><span data-stu-id="f005a-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f005a-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f005a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f005a-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f005a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f005a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f005a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f005a-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f005a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f005a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f005a-118">Scenario description</span></span>
<span data-ttu-id="f005a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f005a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f005a-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="f005a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f005a-121">Agregar Convercent desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="f005a-121">Adding Convercent from hello gallery</span></span>
2. <span data-ttu-id="f005a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f005a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-hello-gallery"></a><span data-ttu-id="f005a-123">Agregar Convercent desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="f005a-123">Adding Convercent from hello gallery</span></span>
<span data-ttu-id="f005a-124">integración de hello tooconfigure de Convercent en Azure AD, deberá tooadd Convercent de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="f005a-124">tooconfigure hello integration of Convercent into Azure AD, you need tooadd Convercent from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f005a-125">**tooadd Convercent de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f005a-125">**tooadd Convercent from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f005a-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="f005a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f005a-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f005a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f005a-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f005a-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="f005a-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f005a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="f005a-133">En el cuadro de búsqueda de hello, escriba **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="f005a-133">In hello search box, type **Convercent**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_search.png)

5. <span data-ttu-id="f005a-135">En el panel de resultados de hello, seleccione **Convercent**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f005a-135">In hello results panel, select **Convercent**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f005a-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f005a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f005a-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Convercent con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f005a-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f005a-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Convercent es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f005a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Convercent is tooa user in Azure AD.</span></span> <span data-ttu-id="f005a-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Convercent debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="f005a-140">In other words, a link relationship between an Azure AD user and hello related user in Convercent needs toobe established.</span></span>

<span data-ttu-id="f005a-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Convercent.</span><span class="sxs-lookup"><span data-stu-id="f005a-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Convercent.</span></span>

<span data-ttu-id="f005a-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Convercent, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f005a-142">tooconfigure and test Azure AD single sign-on with Convercent, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f005a-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="f005a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f005a-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f005a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f005a-145">**[Crear un usuario de prueba Convercent](#creating-a-convercent-test-user)**  -toohave un equivalente de Britta Simon en Convercent que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="f005a-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - toohave a counterpart of Britta Simon in Convercent that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f005a-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f005a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f005a-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f005a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f005a-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f005a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f005a-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Convercent.</span><span class="sxs-lookup"><span data-stu-id="f005a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="f005a-150">**inicio de sesión único en Azure AD tooconfigure con Convercent, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f005a-150">**tooconfigure Azure AD single sign-on with Convercent, perform hello following steps:**</span></span>

1. <span data-ttu-id="f005a-151">En el portal de Azure, en Hola Hola **Convercent** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f005a-151">In hello Azure portal, on hello **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="f005a-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f005a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_samlbase.png)

3. <span data-ttu-id="f005a-155">En hello **Convercent dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado por IDP**, realizar Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="f005a-155">On hello **Convercent Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="f005a-157">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="f005a-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.convercent.com/`</span></span>
 
4. <span data-ttu-id="f005a-158">Si desea que aplicación de hello tooconfigure en **modo iniciado en SP**, en hello **Convercent dominio y las direcciones URL** sección realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="f005a-158">If you wish tooconfigure hello application in **SP initiated mode**, on hello **Convercent Domain and URLs** section perform hello following steps:</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="f005a-160">a.</span><span class="sxs-lookup"><span data-stu-id="f005a-160">a.</span></span> <span data-ttu-id="f005a-161">Haga clic en **"Mostrar configuración avanzada de URL"**.</span><span class="sxs-lookup"><span data-stu-id="f005a-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="f005a-162">b.</span><span class="sxs-lookup"><span data-stu-id="f005a-162">b.</span></span> <span data-ttu-id="f005a-163">Hola **dirección URL de inicio de sesión** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="f005a-163">In hello **Sign On URL** textbox, type hello value using hello following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="f005a-164">c.</span><span class="sxs-lookup"><span data-stu-id="f005a-164">c.</span></span> <span data-ttu-id="f005a-165">Hola **estado de retransmisión** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="f005a-165">In hello **Relay State** textbox, type hello value using hello following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f005a-166">Estos valores no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="f005a-166">These values are not hello real values.</span></span> <span data-ttu-id="f005a-167">Actualizar estos valores con hello real identificador, dirección URL de inicio de sesión y el estado de retransmisión.</span><span class="sxs-lookup"><span data-stu-id="f005a-167">Update these values with hello actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="f005a-168">Póngase en contacto con [equipo de soporte técnico de cliente de Convercent](http://support.convercent.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="f005a-168">Contact [Convercent Client support team](http://support.convercent.com) tooget these values.</span></span>

5. <span data-ttu-id="f005a-169">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f005a-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_certificate.png) 

6. <span data-ttu-id="f005a-171">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f005a-171">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-convercent-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f005a-173">tooget SSO configurado para la aplicación, póngase en contacto con [equipo de soporte técnico de Convercent](mailto:support@convercent.com) y proporcionarles Hola descargado **Metadata XML**.</span><span class="sxs-lookup"><span data-stu-id="f005a-173">tooget SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with hello downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="f005a-174">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="f005a-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f005a-175">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="f005a-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f005a-176">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f005a-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f005a-177">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f005a-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="f005a-178">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="f005a-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="f005a-180">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f005a-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f005a-181">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="f005a-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f005a-183">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f005a-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f005a-185">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f005a-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f005a-187">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="f005a-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f005a-189">a.</span><span class="sxs-lookup"><span data-stu-id="f005a-189">a.</span></span> <span data-ttu-id="f005a-190">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f005a-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f005a-191">b.</span><span class="sxs-lookup"><span data-stu-id="f005a-191">b.</span></span> <span data-ttu-id="f005a-192">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f005a-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f005a-193">c.</span><span class="sxs-lookup"><span data-stu-id="f005a-193">c.</span></span> <span data-ttu-id="f005a-194">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f005a-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f005a-195">d.</span><span class="sxs-lookup"><span data-stu-id="f005a-195">d.</span></span> <span data-ttu-id="f005a-196">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f005a-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="f005a-197">Creación de un usuario de prueba de Convercent</span><span class="sxs-lookup"><span data-stu-id="f005a-197">Creating a Convercent test user</span></span>

<span data-ttu-id="f005a-198">Trabajar con [equipo de soporte técnico de Convercent](mailto:support@convercent.com) a los usuarios de tooadd hello en la plataforma de Convercent Hola.</span><span class="sxs-lookup"><span data-stu-id="f005a-198">Work with [Convercent support team](mailto:support@convercent.com) tooadd hello users in hello Convercent platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f005a-199">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f005a-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f005a-200">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooConvercent.</span><span class="sxs-lookup"><span data-stu-id="f005a-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConvercent.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="f005a-202">**tooassign Britta Simon tooConvercent, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f005a-202">**tooassign Britta Simon tooConvercent, perform hello following steps:**</span></span>

1. <span data-ttu-id="f005a-203">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f005a-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f005a-205">En la lista de aplicaciones de hello, seleccione **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="f005a-205">In hello applications list, select **Convercent**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_app.png) 

3. <span data-ttu-id="f005a-207">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f005a-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="f005a-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f005a-209">Click **Add** button.</span></span> <span data-ttu-id="f005a-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f005a-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="f005a-212">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="f005a-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f005a-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f005a-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f005a-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f005a-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f005a-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="f005a-215">Testing single sign-on</span></span>

<span data-ttu-id="f005a-216">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f005a-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f005a-217">Al hacer clic en icono de Convercent Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Convercent aplicación.</span><span class="sxs-lookup"><span data-stu-id="f005a-217">When you click hello Convercent tile in hello Access Panel, you should get automatically signed-on tooyour Convercent application.</span></span>
<span data-ttu-id="f005a-218">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f005a-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f005a-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f005a-219">Additional resources</span></span>

* [<span data-ttu-id="f005a-220">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f005a-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f005a-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f005a-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_203.png


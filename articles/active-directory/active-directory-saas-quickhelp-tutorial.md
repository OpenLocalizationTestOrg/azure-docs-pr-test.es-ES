---
title: "Tutorial: Integración de Azure Active Directory con QuickHelp | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ayuda rápida."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: bbde5eb9bdad89680923ccd36c321b6923f91789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="0e87c-103">Tutorial: Integración de Azure Active Directory con QuickHelp</span><span class="sxs-lookup"><span data-stu-id="0e87c-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="0e87c-104">En este tutorial, aprenderá cómo toointegrate ayuda rápida con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e87c-104">In this tutorial, you learn how toointegrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e87c-105">Integrar ayuda rápida con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0e87c-105">Integrating QuickHelp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0e87c-106">Puede controlar en Azure AD que tenga acceso tooQuickHelp</span><span class="sxs-lookup"><span data-stu-id="0e87c-106">You can control in Azure AD who has access tooQuickHelp</span></span>
- <span data-ttu-id="0e87c-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooQuickHelp (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e87c-107">You can enable your users tooautomatically get signed-on tooQuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0e87c-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0e87c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0e87c-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0e87c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e87c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0e87c-110">Prerequisites</span></span>

<span data-ttu-id="0e87c-111">tooconfigure integración de Azure AD con ayuda rápida, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0e87c-111">tooconfigure Azure AD integration with QuickHelp, you need hello following items:</span></span>

- <span data-ttu-id="0e87c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e87c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e87c-113">Una suscripción habilitada para el inicio de sesión único en QuickHelp</span><span class="sxs-lookup"><span data-stu-id="0e87c-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e87c-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0e87c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e87c-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0e87c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e87c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0e87c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e87c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e87c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e87c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0e87c-118">Scenario description</span></span>
<span data-ttu-id="0e87c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0e87c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e87c-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="0e87c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e87c-121">Agregar ayuda rápida de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0e87c-121">Adding QuickHelp from hello gallery</span></span>
2. <span data-ttu-id="0e87c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e87c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-hello-gallery"></a><span data-ttu-id="0e87c-123">Agregar ayuda rápida de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0e87c-123">Adding QuickHelp from hello gallery</span></span>
<span data-ttu-id="0e87c-124">integración de hello tooconfigure de Ayuda rápida en Azure AD, deberá tooadd ayuda rápida de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="0e87c-124">tooconfigure hello integration of QuickHelp into Azure AD, you need tooadd QuickHelp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0e87c-125">**tooadd ayuda rápida de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e87c-125">**tooadd QuickHelp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e87c-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0e87c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0e87c-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0e87c-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0e87c-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0e87c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0e87c-133">En el cuadro de búsqueda de hello, escriba **ayuda rápida**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-133">In hello search box, type **QuickHelp**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="0e87c-135">En el panel de resultados de hello, seleccione **ayuda rápida**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0e87c-135">In hello results panel, select **QuickHelp**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0e87c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e87c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0e87c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con QuickHelp con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0e87c-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e87c-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Ayuda rápida es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e87c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp is tooa user in Azure AD.</span></span> <span data-ttu-id="0e87c-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Ayuda rápida necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="0e87c-140">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="0e87c-141">En la Ayuda rápida, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e87c-141">In QuickHelp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0e87c-142">tooconfigure y prueba de inicio de sesión único en Azure AD con ayuda rápida, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0e87c-142">tooconfigure and test Azure AD single sign-on with QuickHelp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0e87c-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="0e87c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0e87c-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e87c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e87c-145">**[Crear un usuario de prueba ayuda rápida](#creating-a-quickhelp-test-user)**  -toohave un equivalente de Britta Simon en Ayuda rápida que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="0e87c-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - toohave a counterpart of Britta Simon in QuickHelp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e87c-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0e87c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e87c-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0e87c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0e87c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e87c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0e87c-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Ayuda rápida.</span><span class="sxs-lookup"><span data-stu-id="0e87c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="0e87c-150">**inicio de sesión único en Azure AD tooconfigure con ayuda rápida, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e87c-150">**tooconfigure Azure AD single sign-on with QuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e87c-151">En el portal de Azure, en Hola Hola **ayuda rápida** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-151">In hello Azure portal, on hello **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0e87c-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0e87c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="0e87c-155">En hello **ayuda rápida dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0e87c-155">On hello **QuickHelp Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="0e87c-157">a.</span><span class="sxs-lookup"><span data-stu-id="0e87c-157">a.</span></span> <span data-ttu-id="0e87c-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://quickhelp.com/<instancename>/#/Login`</span><span class="sxs-lookup"><span data-stu-id="0e87c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="0e87c-159">b.</span><span class="sxs-lookup"><span data-stu-id="0e87c-159">b.</span></span> <span data-ttu-id="0e87c-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="0e87c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0e87c-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="0e87c-161">These values are not real.</span></span> <span data-ttu-id="0e87c-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="0e87c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0e87c-163">Póngase en contacto con [equipo de soporte técnico de cliente ayuda rápida](https://support.quickhelp.com/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="0e87c-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="0e87c-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0e87c-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="0e87c-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0e87c-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="0e87c-168">Sitio de empresa de Ayuda rápida tooyour inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="0e87c-168">Sign-on tooyour QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="0e87c-169">En el menú de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Configurar inicio de sesión único][21]

8. <span data-ttu-id="0e87c-171">Hola **QuickHelp Admin** menú, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-171">In hello **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Configurar inicio de sesión único][22]

9. <span data-ttu-id="0e87c-173">Haga clic en **Configuración de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="0e87c-174">En hello **configuración de autenticación** , siga los pasos de Hola</span><span class="sxs-lookup"><span data-stu-id="0e87c-174">On hello **Authentication Settings** page, perform hello following steps</span></span>
   
    ![Configurar inicio de sesión único][23]
   
    <span data-ttu-id="0e87c-176">a.</span><span class="sxs-lookup"><span data-stu-id="0e87c-176">a.</span></span> <span data-ttu-id="0e87c-177">En **Tipo de SSO**, seleccione **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="0e87c-178">b.</span><span class="sxs-lookup"><span data-stu-id="0e87c-178">b.</span></span> <span data-ttu-id="0e87c-179">tooupload el archivo de metadatos descargado de Azure, haga clic en **examinar**, navegue archivo toohello, finalizar, a continuación, haga clic en **cargar metadatos**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-179">tooupload your downloaded Azure metadata file, click **Browse**, navigate toohello file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="0e87c-180">c.</span><span class="sxs-lookup"><span data-stu-id="0e87c-180">c.</span></span> <span data-ttu-id="0e87c-181">Hola **correo electrónico** cuadro de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="0e87c-181">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="0e87c-182">d.</span><span class="sxs-lookup"><span data-stu-id="0e87c-182">d.</span></span> <span data-ttu-id="0e87c-183">Hola **nombre** cuadro de texto, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="0e87c-183">In hello **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="0e87c-184">e.</span><span class="sxs-lookup"><span data-stu-id="0e87c-184">e.</span></span> <span data-ttu-id="0e87c-185">Hola **Last Name** cuadro de texto, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="0e87c-185">In hello **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="0e87c-186">f.</span><span class="sxs-lookup"><span data-stu-id="0e87c-186">f.</span></span> <span data-ttu-id="0e87c-187">Hola **acción barra**, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-187">In hello **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0e87c-188">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="0e87c-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0e87c-189">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="0e87c-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0e87c-190">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0e87c-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0e87c-191">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e87c-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="0e87c-192">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="0e87c-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0e87c-194">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e87c-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e87c-195">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0e87c-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0e87c-197">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0e87c-199">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e87c-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0e87c-201">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0e87c-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0e87c-203">a.</span><span class="sxs-lookup"><span data-stu-id="0e87c-203">a.</span></span> <span data-ttu-id="0e87c-204">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e87c-205">b.</span><span class="sxs-lookup"><span data-stu-id="0e87c-205">b.</span></span> <span data-ttu-id="0e87c-206">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0e87c-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0e87c-207">c.</span><span class="sxs-lookup"><span data-stu-id="0e87c-207">c.</span></span> <span data-ttu-id="0e87c-208">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0e87c-209">d.</span><span class="sxs-lookup"><span data-stu-id="0e87c-209">d.</span></span> <span data-ttu-id="0e87c-210">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="0e87c-211">Creación de un usuario de prueba de QuickHelp</span><span class="sxs-lookup"><span data-stu-id="0e87c-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="0e87c-212">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en Ayuda rápida.</span><span class="sxs-lookup"><span data-stu-id="0e87c-212">hello objective of this section is toocreate a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="0e87c-213">Para toowork de inicio de sesión único, Azure AD necesita tooknow es qué usuario equivalente de hello en Ayuda rápida tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e87c-213">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp tooa user in Azure AD is.</span></span> <span data-ttu-id="0e87c-214">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Ayuda rápida necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="0e87c-214">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="0e87c-215">QuickHelp admite el aprovisionamiento Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="0e87c-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="0e87c-216">Esto significa que, si es necesario, se crea automáticamente una cuenta de usuario en la Ayuda rápida y cuenta de hello está vinculado toohello cuenta de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e87c-216">This means, if necessary, a user account is automatically created in QuickHelp and hello account is linked toohello Azure AD account.</span></span>

<span data-ttu-id="0e87c-217">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="0e87c-217">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0e87c-218">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0e87c-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0e87c-219">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooQuickHelp.</span><span class="sxs-lookup"><span data-stu-id="0e87c-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQuickHelp.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0e87c-221">**tooassign Britta Simon tooQuickHelp, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0e87c-221">**tooassign Britta Simon tooQuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="0e87c-222">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0e87c-224">En la lista de aplicaciones de hello, seleccione **ayuda rápida**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-224">In hello applications list, select **QuickHelp**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="0e87c-226">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0e87c-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-228">Click **Add** button.</span></span> <span data-ttu-id="0e87c-229">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0e87c-231">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e87c-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0e87c-232">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e87c-233">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0e87c-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0e87c-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0e87c-234">Testing single sign-on</span></span>

<span data-ttu-id="0e87c-235">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0e87c-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="0e87c-236">Al hacer clic en icono de Ayuda rápida Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour ayuda rápida aplicación.</span><span class="sxs-lookup"><span data-stu-id="0e87c-236">When you click hello QuickHelp tile in hello Access Panel, you should get automatically signed-on tooyour QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0e87c-237">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0e87c-237">Additional resources</span></span>

* [<span data-ttu-id="0e87c-238">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e87c-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e87c-239">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0e87c-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png

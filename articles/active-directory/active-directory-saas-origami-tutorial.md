---
title: "Tutorial: Integración de Azure Active Directory con Origami | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y figuras de papel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a45f2d2b8d2271cf0fc58cb8fad92f007cb5e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="642a4-103">Tutorial: Integración de Azure Active Directory con Origami</span><span class="sxs-lookup"><span data-stu-id="642a4-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="642a4-104">En este tutorial, aprenderá cómo toointegrate Origami con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="642a4-104">In this tutorial, you learn how toointegrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="642a4-105">Integración Origami con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="642a4-105">Integrating Origami with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="642a4-106">Puede controlar en Azure AD que tenga acceso tooOrigami</span><span class="sxs-lookup"><span data-stu-id="642a4-106">You can control in Azure AD who has access tooOrigami</span></span>
- <span data-ttu-id="642a4-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooOrigami (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="642a4-107">You can enable your users tooautomatically get signed-on tooOrigami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="642a4-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="642a4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="642a4-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="642a4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="642a4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="642a4-110">Prerequisites</span></span>

<span data-ttu-id="642a4-111">integración de Azure AD con Origami tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="642a4-111">tooconfigure Azure AD integration with Origami, you need hello following items:</span></span>

- <span data-ttu-id="642a4-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="642a4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="642a4-113">Una suscripción habilitada para el inicio de sesión único en Pantheon</span><span class="sxs-lookup"><span data-stu-id="642a4-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="642a4-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="642a4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="642a4-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="642a4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="642a4-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="642a4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="642a4-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="642a4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="642a4-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="642a4-118">Scenario description</span></span>
<span data-ttu-id="642a4-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="642a4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="642a4-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="642a4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="642a4-121">Agregar Origami desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="642a4-121">Adding Origami from hello gallery</span></span>
2. <span data-ttu-id="642a4-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="642a4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-hello-gallery"></a><span data-ttu-id="642a4-123">Agregar Origami desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="642a4-123">Adding Origami from hello gallery</span></span>
<span data-ttu-id="642a4-124">integración de hello tooconfigure de Origami en Azure AD, deberá tooadd Origami de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="642a4-124">tooconfigure hello integration of Origami into Azure AD, you need tooadd Origami from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="642a4-125">**tooadd Origami de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="642a4-125">**tooadd Origami from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="642a4-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="642a4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="642a4-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="642a4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="642a4-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="642a4-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="642a4-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="642a4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="642a4-133">En el cuadro de búsqueda de hello, escriba **Origami**.</span><span class="sxs-lookup"><span data-stu-id="642a4-133">In hello search box, type **Origami**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="642a4-135">En el panel de resultados de hello, seleccione **Origami**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="642a4-135">In hello results panel, select **Origami**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="642a4-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="642a4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="642a4-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Origami con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="642a4-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="642a4-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Origami es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="642a4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Origami is tooa user in Azure AD.</span></span> <span data-ttu-id="642a4-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Origami debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="642a4-140">In other words, a link relationship between an Azure AD user and hello related user in Origami needs toobe established.</span></span>

<span data-ttu-id="642a4-141">En Origami, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="642a4-141">In Origami, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="642a4-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Origami, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="642a4-142">tooconfigure and test Azure AD single sign-on with Origami, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="642a4-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="642a4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="642a4-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="642a4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="642a4-145">**[Creación de un usuario de prueba Origami](#creating-an-origami-test-user) ** -toohave un equivalente de Britta Simon en Origami que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="642a4-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - toohave a counterpart of Britta Simon in Origami that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="642a4-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="642a4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="642a4-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="642a4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="642a4-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="642a4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="642a4-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Origami.</span><span class="sxs-lookup"><span data-stu-id="642a4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="642a4-150">**inicio de sesión único en Azure AD tooconfigure con Origami, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="642a4-150">**tooconfigure Azure AD single sign-on with Origami, perform hello following steps:**</span></span>

1. <span data-ttu-id="642a4-151">En el portal de Azure, en Hola Hola **Origami** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="642a4-151">In hello Azure portal, on hello **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="642a4-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="642a4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="642a4-155">En hello **Origami dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="642a4-155">On hello **Origami Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="642a4-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="642a4-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="642a4-158">valor de Hello no es real.</span><span class="sxs-lookup"><span data-stu-id="642a4-158">hello value is not real.</span></span> <span data-ttu-id="642a4-159">Valor de Hola de actualización con Hola dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="642a4-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="642a4-160">Póngase en contacto con [equipo de soporte técnico de cliente Origami](https://wordpress.org/support/theme/origami) valor de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="642a4-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) tooget hello value.</span></span> 
 
4. <span data-ttu-id="642a4-161">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="642a4-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="642a4-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="642a4-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="642a4-165">En hello **configuración Origami** sección, haga clic en **configurar Origami** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="642a4-165">On hello **Origami Configuration** section, click **Configure Origami** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="642a4-166">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="642a4-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="642a4-168">Inicie la sesión en toohello Origami cuenta con derechos de administrador.</span><span class="sxs-lookup"><span data-stu-id="642a4-168">Log in toohello Origami account with Admin rights.</span></span>

8. <span data-ttu-id="642a4-169">En el menú de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="642a4-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="642a4-171">En la página de diálogo de inicio de sesión único en la instalación de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="642a4-171">On hello Single Sign On Setup dialog page, perform hello following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="642a4-173">a.</span><span class="sxs-lookup"><span data-stu-id="642a4-173">a.</span></span> <span data-ttu-id="642a4-174">Seleccione **Enable Single Sign On**(Habilitar el inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="642a4-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="642a4-175">b.</span><span class="sxs-lookup"><span data-stu-id="642a4-175">b.</span></span> <span data-ttu-id="642a4-176">Hola **dirección URL del proveedor de identidades de inicio de sesión página** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="642a4-176">In hello **Identity Provider's Sign-in Page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="642a4-177">c.</span><span class="sxs-lookup"><span data-stu-id="642a4-177">c.</span></span> <span data-ttu-id="642a4-178">Hola **URL de página de cierre de sesión del proveedor de identidades** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="642a4-178">In hello **Identity Provider's Sign-out Page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="642a4-179">d.</span><span class="sxs-lookup"><span data-stu-id="642a4-179">d.</span></span> <span data-ttu-id="642a4-180">Haga clic en **examinar** certificado de hello tooupload que ha descargado de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="642a4-180">Click **Browse** tooupload hello certificate you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="642a4-181">e.</span><span class="sxs-lookup"><span data-stu-id="642a4-181">e.</span></span> <span data-ttu-id="642a4-182">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="642a4-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="642a4-183">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="642a4-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="642a4-184">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="642a4-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="642a4-185">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="642a4-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="642a4-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="642a4-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="642a4-187">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="642a4-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="642a4-189">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="642a4-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="642a4-190">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="642a4-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="642a4-192">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="642a4-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="642a4-194">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="642a4-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="642a4-196">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="642a4-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="642a4-198">a.</span><span class="sxs-lookup"><span data-stu-id="642a4-198">a.</span></span> <span data-ttu-id="642a4-199">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="642a4-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="642a4-200">b.</span><span class="sxs-lookup"><span data-stu-id="642a4-200">b.</span></span> <span data-ttu-id="642a4-201">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="642a4-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="642a4-202">c.</span><span class="sxs-lookup"><span data-stu-id="642a4-202">c.</span></span> <span data-ttu-id="642a4-203">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="642a4-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="642a4-204">d.</span><span class="sxs-lookup"><span data-stu-id="642a4-204">d.</span></span> <span data-ttu-id="642a4-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="642a4-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="642a4-206">Creación de un usuario de prueba de Origami</span><span class="sxs-lookup"><span data-stu-id="642a4-206">Creating an Origami test user</span></span>

<span data-ttu-id="642a4-207">En esta sección, creará un usuario llamado Britta Simon en Origami.</span><span class="sxs-lookup"><span data-stu-id="642a4-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="642a4-208">Inicie la sesión en toohello Origami cuenta con derechos de administrador.</span><span class="sxs-lookup"><span data-stu-id="642a4-208">Log in toohello Origami account with Admin rights.</span></span>

2. <span data-ttu-id="642a4-209">En el menú de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="642a4-209">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="642a4-211">En hello **a los usuarios y la seguridad** cuadro de diálogo, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="642a4-211">On hello **Users and Security** dialog, click **Users**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="642a4-213">Haga clic en **Add New User**(Agregar nuevo usuario).</span><span class="sxs-lookup"><span data-stu-id="642a4-213">Click **Add New User**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="642a4-215">En el cuadro de diálogo de agregar nuevo usuario hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="642a4-215">On hello Add New User dialog, perform hello following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="642a4-217">a.</span><span class="sxs-lookup"><span data-stu-id="642a4-217">a.</span></span> <span data-ttu-id="642a4-218">Hola **nombre de usuario** cuadro de texto, escriba el correo electrónico de saludo del usuario como ** brittasimon@contoso.com **.</span><span class="sxs-lookup"><span data-stu-id="642a4-218">In hello **User Name** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="642a4-219">b.</span><span class="sxs-lookup"><span data-stu-id="642a4-219">b.</span></span> <span data-ttu-id="642a4-220">Hola **contraseña** cuadro de texto, escriba una contraseña.</span><span class="sxs-lookup"><span data-stu-id="642a4-220">In hello **Password** textbox, type a password.</span></span>

    <span data-ttu-id="642a4-221">c.</span><span class="sxs-lookup"><span data-stu-id="642a4-221">c.</span></span> <span data-ttu-id="642a4-222">Hola **Confirmar contraseña** cuadro de texto, escriba la contraseña de hello nuevo.</span><span class="sxs-lookup"><span data-stu-id="642a4-222">In hello **Confirm Password** textbox, type hello password again.</span></span>

    <span data-ttu-id="642a4-223">d.</span><span class="sxs-lookup"><span data-stu-id="642a4-223">d.</span></span> <span data-ttu-id="642a4-224">Hola **nombre** cuadro de texto, escriba Hola nombre de usuario como **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="642a4-224">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="642a4-225">e.</span><span class="sxs-lookup"><span data-stu-id="642a4-225">e.</span></span> <span data-ttu-id="642a4-226">Hola **Last Name** cuadro de texto, escriba Hola último nombre de usuario como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="642a4-226">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="642a4-227">f.</span><span class="sxs-lookup"><span data-stu-id="642a4-227">f.</span></span> <span data-ttu-id="642a4-228">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="642a4-228">Click **Save**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="642a4-230">Asignar **Roles de usuario** y **acceso de cliente** toohello usuario.</span><span class="sxs-lookup"><span data-stu-id="642a4-230">Assign **User Roles** and **Client Access** toohello user.</span></span> 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="642a4-232">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="642a4-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="642a4-233">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooOrigami.</span><span class="sxs-lookup"><span data-stu-id="642a4-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOrigami.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="642a4-235">**tooassign Britta Simon tooOrigami, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="642a4-235">**tooassign Britta Simon tooOrigami, perform hello following steps:**</span></span>

1. <span data-ttu-id="642a4-236">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="642a4-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="642a4-238">En la lista de aplicaciones de hello, seleccione **Origami**.</span><span class="sxs-lookup"><span data-stu-id="642a4-238">In hello applications list, select **Origami**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="642a4-240">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="642a4-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="642a4-242">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="642a4-242">Click **Add** button.</span></span> <span data-ttu-id="642a4-243">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="642a4-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="642a4-245">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="642a4-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="642a4-246">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="642a4-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="642a4-247">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="642a4-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="642a4-248">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="642a4-248">Testing single sign-on</span></span>

<span data-ttu-id="642a4-249">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="642a4-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="642a4-250">Al hacer clic en icono de Origami Hola Hola Panel de acceso, deberá obtener aplicaciones de Origami tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="642a4-250">When you click hello Origami tile in hello Access Panel, you should get automatically signed-on tooyour Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="642a4-251">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="642a4-251">Additional resources</span></span>

* [<span data-ttu-id="642a4-252">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="642a4-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="642a4-253">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="642a4-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png


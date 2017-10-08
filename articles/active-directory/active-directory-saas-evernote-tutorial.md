---
title: "Tutorial: Integración de Azure Active Directory con Evernote | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Evernote."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 4d7017e571ed12a0b155aa188c6b0ecb3c9898a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="fde23-103">Tutorial: Integración de Azure Active Directory con Evernote</span><span class="sxs-lookup"><span data-stu-id="fde23-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="fde23-104">En este tutorial, aprenderá cómo toointegrate Evernote con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fde23-104">In this tutorial, you learn how toointegrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fde23-105">Integración Evernote con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="fde23-105">Integrating Evernote with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fde23-106">Puede controlar en Azure AD que tenga acceso tooEvernote.</span><span class="sxs-lookup"><span data-stu-id="fde23-106">You can control in Azure AD who has access tooEvernote.</span></span>
- <span data-ttu-id="fde23-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooEvernote (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fde23-107">You can enable your users tooautomatically get signed-on tooEvernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fde23-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fde23-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="fde23-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fde23-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fde23-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fde23-110">Prerequisites</span></span>

<span data-ttu-id="fde23-111">integración de Azure AD con Evernote tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="fde23-111">tooconfigure Azure AD integration with Evernote, you need hello following items:</span></span>

- <span data-ttu-id="fde23-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fde23-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fde23-113">Una suscripción habilitada para el inicio de sesión único en Evernote</span><span class="sxs-lookup"><span data-stu-id="fde23-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fde23-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="fde23-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fde23-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="fde23-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fde23-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fde23-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fde23-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fde23-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fde23-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="fde23-118">Scenario description</span></span>
<span data-ttu-id="fde23-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="fde23-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fde23-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="fde23-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fde23-121">Agregar Evernote desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="fde23-121">Adding Evernote from hello gallery</span></span>
2. <span data-ttu-id="fde23-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fde23-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-hello-gallery"></a><span data-ttu-id="fde23-123">Agregar Evernote desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="fde23-123">Adding Evernote from hello gallery</span></span>
<span data-ttu-id="fde23-124">integración de hello tooconfigure de Evernote en Azure AD, deberá tooadd Evernote de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="fde23-124">tooconfigure hello integration of Evernote into Azure AD, you need tooadd Evernote from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fde23-125">**tooadd Evernote de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fde23-125">**tooadd Evernote from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fde23-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="fde23-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="fde23-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="fde23-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fde23-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fde23-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="fde23-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fde23-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="fde23-133">En el cuadro de búsqueda de hello, escriba **Evernote**, seleccione **Evernote** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="fde23-133">In hello search box, type **Evernote**, select **Evernote** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Evernote en la lista de resultados de Hola](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fde23-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="fde23-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fde23-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Evernote con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fde23-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fde23-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Evernote es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fde23-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evernote is tooa user in Azure AD.</span></span> <span data-ttu-id="fde23-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Evernote debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="fde23-138">In other words, a link relationship between an Azure AD user and hello related user in Evernote needs toobe established.</span></span>

<span data-ttu-id="fde23-139">En Evernote, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fde23-139">In Evernote, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fde23-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Evernote, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="fde23-140">tooconfigure and test Azure AD single sign-on with Evernote, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fde23-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="fde23-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fde23-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fde23-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fde23-143">**[Crear un usuario de prueba Evernote](#create-an-evernote-test-user)**  -toohave un equivalente de Britta Simon en Evernote que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="fde23-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - toohave a counterpart of Britta Simon in Evernote that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fde23-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fde23-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fde23-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="fde23-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fde23-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fde23-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fde23-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Evernote.</span><span class="sxs-lookup"><span data-stu-id="fde23-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="fde23-148">**inicio de sesión único en Azure AD tooconfigure con Evernote, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fde23-148">**tooconfigure Azure AD single sign-on with Evernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="fde23-149">En el portal de Azure, en Hola Hola **Evernote** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="fde23-149">In hello Azure portal, on hello **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="fde23-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fde23-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="fde23-153">En hello **Evernote dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea que el modo de aplicación de hello tooconfigure en IDP iniciado:</span><span class="sxs-lookup"><span data-stu-id="fde23-153">On hello **Evernote Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="fde23-155">Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="fde23-155">In hello **Identifier** textbox, type hello URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="fde23-156">Comprobar **mostrar avanzadas de configuración de direcciones URL** y realizar Hola siguiendo el paso si desea tooconfigure aplicación de hello en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="fde23-156">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="fde23-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:`https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="fde23-158">In hello **Sign on URL** textbox, type hello URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="fde23-159">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="fde23-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="fde23-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="fde23-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="fde23-163">En hello **Evernote configuración** sección, haga clic en **configurar Evernote** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="fde23-163">On hello **Evernote Configuration** section, click **Configure Evernote** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fde23-164">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="fde23-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="fde23-166">En otra ventana del explorador web, inicie sesión en el sitio de la empresa de Evernote como administrador.</span><span class="sxs-lookup"><span data-stu-id="fde23-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="fde23-167">Vaya demasiado**'Consola de administración'**</span><span class="sxs-lookup"><span data-stu-id="fde23-167">Go too**'Admin Console'**</span></span>

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="fde23-169">De hello **'Consola de administración'**, vaya demasiado**'Seguridad'** y seleccione **' Single Sign-On'**</span><span class="sxs-lookup"><span data-stu-id="fde23-169">From hello **'Admin Console'**, go too**‘Security’** and select **‘Single Sign-On’**</span></span>

    ![SSO-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="fde23-171">Configurar Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="fde23-171">Configure hello following values:</span></span>

    ![Certificate-Setting](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="fde23-173">a.</span><span class="sxs-lookup"><span data-stu-id="fde23-173">a.</span></span>  <span data-ttu-id="fde23-174">**Habilitar SSO:** SSO está habilitado de forma predeterminada (haga clic en **deshabilitar Single Sign-on** requisito de SSO de hello tooremove)</span><span class="sxs-lookup"><span data-stu-id="fde23-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** tooremove hello SSO requirement)</span></span>

    <span data-ttu-id="fde23-175">b.</span><span class="sxs-lookup"><span data-stu-id="fde23-175">b.</span></span> <span data-ttu-id="fde23-176">Pegar **el inicio de sesión único de SAML dirección URL del servicio** valor, que haya copiado desde Hola portal de Azure en hello **URL de solicitud de HTTP de SAML** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="fde23-176">Paste **SAML Single sign-on Service URL** value, which you have copied from hello Azure portal into hello **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="fde23-177">c.</span><span class="sxs-lookup"><span data-stu-id="fde23-177">c.</span></span> <span data-ttu-id="fde23-178">Abra el certificado descargado Hola de Azure AD en un contenido de hello el Bloc de notas y copie incluidos "BEGIN CERTIFICATE" y "END CERTIFICATE" y péguelo en hello **certificado X.509** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="fde23-178">Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into hello **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="fde23-179">d. Haga clic en **Guardar cambios**</span><span class="sxs-lookup"><span data-stu-id="fde23-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="fde23-180">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="fde23-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fde23-181">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="fde23-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fde23-182">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fde23-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fde23-183">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fde23-183">Create an Azure AD test user</span></span>

<span data-ttu-id="fde23-184">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="fde23-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="fde23-186">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fde23-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fde23-187">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="fde23-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fde23-189">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fde23-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fde23-191">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fde23-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fde23-193">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="fde23-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fde23-195">a.</span><span class="sxs-lookup"><span data-stu-id="fde23-195">a.</span></span> <span data-ttu-id="fde23-196">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fde23-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fde23-197">b.</span><span class="sxs-lookup"><span data-stu-id="fde23-197">b.</span></span> <span data-ttu-id="fde23-198">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fde23-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="fde23-199">c.</span><span class="sxs-lookup"><span data-stu-id="fde23-199">c.</span></span> <span data-ttu-id="fde23-200">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="fde23-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="fde23-201">d.</span><span class="sxs-lookup"><span data-stu-id="fde23-201">d.</span></span> <span data-ttu-id="fde23-202">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fde23-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="fde23-203">Creación de un usuario de prueba de Evernote</span><span class="sxs-lookup"><span data-stu-id="fde23-203">Create an Evernote test user</span></span>

<span data-ttu-id="fde23-204">En orden tooenable toolog de los usuarios de Azure AD en Evernote, se les deben aprovisionar en Evernote.</span><span class="sxs-lookup"><span data-stu-id="fde23-204">In order tooenable Azure AD users toolog into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="fde23-205">En caso de hello de Evernote, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="fde23-205">In hello case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="fde23-206">**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="fde23-206">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="fde23-207">Inicie sesión en tooyour Evernote sitio de su compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="fde23-207">Log in tooyour Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="fde23-208">Haga clic en hello **'Consola de administración'**.</span><span class="sxs-lookup"><span data-stu-id="fde23-208">Click hello **'Admin Console'**.</span></span>

    ![Admin-Console](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="fde23-210">De hello **'Consola de administración'**, vaya demasiado**'Agregar usuarios'**.</span><span class="sxs-lookup"><span data-stu-id="fde23-210">From hello **'Admin Console'**, go too**‘Add users’**.</span></span>

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="fde23-212">**Agregar miembros del equipo** en hello **correo electrónico** cuadro de texto, escriba la dirección de correo electrónico de Hola de cuenta de usuario y haga clic en **invitar.**</span><span class="sxs-lookup"><span data-stu-id="fde23-212">**Add team members** in hello **Email** textbox, type hello email address of user account and click **Invite.**</span></span>

    ![Add-testUser](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="fde23-214">Después de que se envía una invitación, titular de la cuenta de hello Azure Active Directory recibirán una invitación de correo electrónico tooaccept Hola.</span><span class="sxs-lookup"><span data-stu-id="fde23-214">After invitation is sent, hello Azure Active Directory account holder will receive an email tooaccept hello invitation.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fde23-215">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fde23-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="fde23-216">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooEvernote.</span><span class="sxs-lookup"><span data-stu-id="fde23-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvernote.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="fde23-218">**tooassign Britta Simon tooEvernote, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fde23-218">**tooassign Britta Simon tooEvernote, perform hello following steps:**</span></span>

1. <span data-ttu-id="fde23-219">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fde23-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="fde23-221">En la lista de aplicaciones de hello, seleccione **Evernote**.</span><span class="sxs-lookup"><span data-stu-id="fde23-221">In hello applications list, select **Evernote**.</span></span>

    ![vínculo de Evernote Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="fde23-223">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fde23-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="fde23-225">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fde23-225">Click **Add** button.</span></span> <span data-ttu-id="fde23-226">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fde23-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="fde23-228">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="fde23-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fde23-229">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fde23-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fde23-230">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fde23-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fde23-231">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="fde23-231">Test single sign-on</span></span>

<span data-ttu-id="fde23-232">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="fde23-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fde23-233">Al hacer clic en icono de Evernote Hola Hola Panel de acceso, deberá obtener ha iniciado sesión tooyour Evernote aplicación.</span><span class="sxs-lookup"><span data-stu-id="fde23-233">When you click hello Evernote tile in hello Access Panel, you should get signed-on tooyour Evernote application.</span></span> <span data-ttu-id="fde23-234">Con su cuenta personal podrá iniciar la sesión como una cuenta de organización pero, a continuación, la necesidad toolog.</span><span class="sxs-lookup"><span data-stu-id="fde23-234">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fde23-235">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="fde23-235">Additional resources</span></span>

* [<span data-ttu-id="fde23-236">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fde23-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fde23-237">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fde23-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png


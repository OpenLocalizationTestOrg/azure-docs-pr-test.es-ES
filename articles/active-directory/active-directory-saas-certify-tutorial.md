---
title: "Tutorial: integración de Azure Active Directory con Certify | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Certify."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b36e020-175a-4534-b341-85260739f889
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 000bef7b679a6f291b1f3cb42e10cb3ed424b25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-certify"></a><span data-ttu-id="62778-103">Tutorial: integración de Azure Active Directory con Certify</span><span class="sxs-lookup"><span data-stu-id="62778-103">Tutorial: Azure Active Directory integration with Certify</span></span>

<span data-ttu-id="62778-104">En este tutorial, aprenderá cómo toointegrate certificar con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="62778-104">In this tutorial, you learn how toointegrate Certify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62778-105">Integración Certify con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="62778-105">Integrating Certify with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="62778-106">Puede controlar en Azure AD que tenga acceso tooCertify</span><span class="sxs-lookup"><span data-stu-id="62778-106">You can control in Azure AD who has access tooCertify</span></span>
- <span data-ttu-id="62778-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooCertify (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="62778-107">You can enable your users tooautomatically get signed-on tooCertify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62778-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="62778-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="62778-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="62778-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62778-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="62778-110">Prerequisites</span></span>

<span data-ttu-id="62778-111">integración de Azure AD tooconfigure con Certify debe Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="62778-111">tooconfigure Azure AD integration with Certify, you need hello following items:</span></span>

- <span data-ttu-id="62778-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="62778-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62778-113">Una suscripción habilitada para el inicio de sesión único en Certify</span><span class="sxs-lookup"><span data-stu-id="62778-113">A Certify single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="62778-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="62778-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="62778-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="62778-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62778-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="62778-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="62778-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62778-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="62778-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="62778-118">Scenario description</span></span>
<span data-ttu-id="62778-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="62778-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62778-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="62778-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62778-121">Agregar Certify desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="62778-121">Adding Certify from hello gallery</span></span>
2. <span data-ttu-id="62778-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="62778-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-certify-from-hello-gallery"></a><span data-ttu-id="62778-123">Agregar Certify desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="62778-123">Adding Certify from hello gallery</span></span>
<span data-ttu-id="62778-124">integración de hello tooconfigure de Certify en Azure AD, deberá tooadd Certify de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="62778-124">tooconfigure hello integration of Certify into Azure AD, you need tooadd Certify from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="62778-125">**tooadd Certify desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="62778-125">**tooadd Certify from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="62778-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="62778-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="62778-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="62778-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="62778-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="62778-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="62778-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="62778-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="62778-133">En el cuadro de búsqueda de hello, escriba **Certify**.</span><span class="sxs-lookup"><span data-stu-id="62778-133">In hello search box, type **Certify**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-certify-tutorial/tutorial_certify_search.png)

5. <span data-ttu-id="62778-135">En el panel de resultados de hello, seleccione **Certify**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="62778-135">In hello results panel, select **Certify**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-certify-tutorial/tutorial_certify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62778-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="62778-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62778-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Certify con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="62778-138">In this section, you configure and test Azure AD single sign-on with Certify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="62778-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Certify es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62778-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Certify is tooa user in Azure AD.</span></span> <span data-ttu-id="62778-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Certify debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="62778-140">In other words, a link relationship between an Azure AD user and hello related user in Certify needs toobe established.</span></span>

<span data-ttu-id="62778-141">En Certify, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="62778-141">In Certify, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="62778-142">prueba Azure AD y tooconfigure inicio de sesión único con Certify debe hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="62778-142">tooconfigure and test Azure AD single sign-on with Certify, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="62778-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="62778-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="62778-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62778-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62778-145">**[Crear un usuario de prueba Certify](#creating-a-certify-test-user)**  -toohave un equivalente de Britta Simon en Certify que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="62778-145">**[Creating a Certify test user](#creating-a-certify-test-user)** - toohave a counterpart of Britta Simon in Certify that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="62778-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="62778-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62778-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="62778-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62778-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="62778-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="62778-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Certify.</span><span class="sxs-lookup"><span data-stu-id="62778-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Certify application.</span></span>

<span data-ttu-id="62778-150">**inicio de sesión único en tooconfigure Azure AD con Certify realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="62778-150">**tooconfigure Azure AD single sign-on with Certify, perform hello following steps:**</span></span>

1. <span data-ttu-id="62778-151">En el portal de Azure, en Hola Hola **Certify** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="62778-151">In hello Azure portal, on hello **Certify** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="62778-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="62778-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-certify-tutorial/tutorial_certify_samlbase.png)

3. <span data-ttu-id="62778-155">En hello **certificar dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="62778-155">On hello **Certify Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-certify-tutorial/tutorial_certify_url.png)

    <span data-ttu-id="62778-157">Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://www.certify.com`</span><span class="sxs-lookup"><span data-stu-id="62778-157">In hello **Identifier** textbox, type hello URL: `https://www.certify.com`</span></span>

4. <span data-ttu-id="62778-158">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Raw)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="62778-158">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-certify-tutorial/tutorial_certify_certificate.png) 

5. <span data-ttu-id="62778-160">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="62778-160">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-certify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="62778-162">En hello **configuración certificar** sección, haga clic en **configurar certificar** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="62778-162">On hello **Certify Configuration** section, click **Configure Certify** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="62778-163">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="62778-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-certify-tutorial/tutorial_certify_configure.png) 

7. <span data-ttu-id="62778-165">tooconfigure inicio de sesión único en **Certify** lado, necesita hello toosend descargado **Certificate(Raw)** y **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio**demasiado[equipo de soporte técnico de Certify](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="62778-165">tooconfigure single sign-on on **Certify** side, you need toosend hello downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Certify support team](mailto:support@certify.com).</span></span> <span data-ttu-id="62778-166">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="62778-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="62778-167">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="62778-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="62778-168">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="62778-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="62778-169">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="62778-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62778-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="62778-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="62778-171">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="62778-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="62778-173">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="62778-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="62778-174">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="62778-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="62778-176">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="62778-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="62778-178">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="62778-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62778-180">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="62778-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-certify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="62778-182">a.</span><span class="sxs-lookup"><span data-stu-id="62778-182">a.</span></span> <span data-ttu-id="62778-183">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="62778-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62778-184">b.</span><span class="sxs-lookup"><span data-stu-id="62778-184">b.</span></span> <span data-ttu-id="62778-185">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="62778-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="62778-186">c.</span><span class="sxs-lookup"><span data-stu-id="62778-186">c.</span></span> <span data-ttu-id="62778-187">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="62778-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="62778-188">d.</span><span class="sxs-lookup"><span data-stu-id="62778-188">d.</span></span> <span data-ttu-id="62778-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="62778-189">Click **Create**.</span></span>
 
### <a name="creating-a-certify-test-user"></a><span data-ttu-id="62778-190">Creación de un usuario de prueba de Certify</span><span class="sxs-lookup"><span data-stu-id="62778-190">Creating a Certify test user</span></span>

<span data-ttu-id="62778-191">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Certify toocreate.</span><span class="sxs-lookup"><span data-stu-id="62778-191">hello objective of this section is toocreate a user called Britta Simon in Certify.</span></span> <span data-ttu-id="62778-192">Certify admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="62778-192">Certify supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="62778-193">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="62778-193">There is no action item for you in this section.</span></span> <span data-ttu-id="62778-194">Si no existe todavía, se creará un nuevo usuario durante un tooaccess intento Certify.</span><span class="sxs-lookup"><span data-stu-id="62778-194">A new user will be created during an attempt tooaccess Certify if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="62778-195">Si necesita un usuario toocreate manualmente, necesita hello toocontact [equipo de soporte técnico de Certify](mailto:support@certify.com).</span><span class="sxs-lookup"><span data-stu-id="62778-195">If you need toocreate an user manually, you need toocontact hello [Certify support team](mailto:support@certify.com).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="62778-196">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="62778-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="62778-197">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCertify.</span><span class="sxs-lookup"><span data-stu-id="62778-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCertify.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="62778-199">**tooassign Britta Simon tooCertify, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="62778-199">**tooassign Britta Simon tooCertify, perform hello following steps:**</span></span>

1. <span data-ttu-id="62778-200">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="62778-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="62778-202">En la lista de aplicaciones de hello, seleccione **Certify**.</span><span class="sxs-lookup"><span data-stu-id="62778-202">In hello applications list, select **Certify**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-certify-tutorial/tutorial_certify_app.png) 

3. <span data-ttu-id="62778-204">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="62778-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="62778-206">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="62778-206">Click **Add** button.</span></span> <span data-ttu-id="62778-207">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="62778-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="62778-209">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="62778-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="62778-210">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="62778-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="62778-211">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="62778-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="62778-212">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="62778-212">Testing single sign-on</span></span>

<span data-ttu-id="62778-213">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="62778-213">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="62778-214">Al hacer clic en icono de Certify Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Certify aplicación.</span><span class="sxs-lookup"><span data-stu-id="62778-214">When you click hello Certify tile in hello Access Panel, you should get automatically signed-on tooyour Certify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="62778-215">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="62778-215">Additional resources</span></span>

* [<span data-ttu-id="62778-216">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62778-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62778-217">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="62778-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-certify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-certify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-certify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-certify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-certify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-certify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-certify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-certify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-certify-tutorial/tutorial_general_203.png


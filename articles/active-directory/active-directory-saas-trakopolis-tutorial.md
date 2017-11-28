---
title: "Tutorial: Integración de Azure Active Directory con Trakopolis | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Trakopolis."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 73d67c3e-4b4b-4d3b-aa58-6699ea1ccea3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 00f9b21c0a837d1d9fbbd9135367fae4b02db934
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trakopolis"></a><span data-ttu-id="24159-103">Tutorial: integración de Azure Active Directory con Trakopolis</span><span class="sxs-lookup"><span data-stu-id="24159-103">Tutorial: Azure Active Directory integration with Trakopolis</span></span>

<span data-ttu-id="24159-104">En este tutorial, aprenderá cómo toointegrate Trakopolis con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="24159-104">In this tutorial, you learn how toointegrate Trakopolis with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24159-105">Integración Trakopolis con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="24159-105">Integrating Trakopolis with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="24159-106">Puede controlar en Azure AD que tenga acceso tooTrakopolis</span><span class="sxs-lookup"><span data-stu-id="24159-106">You can control in Azure AD who has access tooTrakopolis</span></span>
- <span data-ttu-id="24159-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTrakopolis (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="24159-107">You can enable your users tooautomatically get signed-on tooTrakopolis (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="24159-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="24159-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="24159-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="24159-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24159-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="24159-110">Prerequisites</span></span>

<span data-ttu-id="24159-111">integración de Azure AD con Trakopolis tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="24159-111">tooconfigure Azure AD integration with Trakopolis, you need hello following items:</span></span>

- <span data-ttu-id="24159-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="24159-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24159-113">Una suscripción habilitada para el inicio de sesión único en Trakopolis</span><span class="sxs-lookup"><span data-stu-id="24159-113">A Trakopolis single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24159-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="24159-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24159-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="24159-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24159-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="24159-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24159-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24159-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24159-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="24159-118">Scenario description</span></span>
<span data-ttu-id="24159-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="24159-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24159-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="24159-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24159-121">Agregar Trakopolis desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="24159-121">Adding Trakopolis from hello gallery</span></span>
2. <span data-ttu-id="24159-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="24159-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakopolis-from-hello-gallery"></a><span data-ttu-id="24159-123">Agregar Trakopolis desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="24159-123">Adding Trakopolis from hello gallery</span></span>
<span data-ttu-id="24159-124">integración de hello tooconfigure de Trakopolis en Azure AD, deberá tooadd Trakopolis de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="24159-124">tooconfigure hello integration of Trakopolis into Azure AD, you need tooadd Trakopolis from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="24159-125">**tooadd Trakopolis de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="24159-125">**tooadd Trakopolis from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="24159-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="24159-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="24159-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="24159-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="24159-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="24159-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="24159-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24159-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="24159-133">En el cuadro de búsqueda de hello, escriba **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="24159-133">In hello search box, type **Trakopolis**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_search.png)

5. <span data-ttu-id="24159-135">En el panel de resultados de hello, seleccione **Trakopolis**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="24159-135">In hello results panel, select **Trakopolis**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="24159-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="24159-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="24159-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Trakopolis con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="24159-138">In this section, you configure and test Azure AD single sign-on with Trakopolis based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="24159-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Trakopolis es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24159-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Trakopolis is tooa user in Azure AD.</span></span> <span data-ttu-id="24159-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Trakopolis debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="24159-140">In other words, a link relationship between an Azure AD user and hello related user in Trakopolis needs toobe established.</span></span>

<span data-ttu-id="24159-141">En Trakopolis, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="24159-141">In Trakopolis, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="24159-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Trakopolis, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="24159-142">tooconfigure and test Azure AD single sign-on with Trakopolis, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="24159-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="24159-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="24159-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="24159-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24159-145">**[Crear un usuario de prueba Trakopolis](#creating-a-trakopolis-test-user)**  -toohave un equivalente de Britta Simon en Trakopolis que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="24159-145">**[Creating a Trakopolis test user](#creating-a-trakopolis-test-user)** - toohave a counterpart of Britta Simon in Trakopolis that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="24159-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="24159-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24159-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="24159-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="24159-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="24159-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="24159-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="24159-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Trakopolis application.</span></span>

<span data-ttu-id="24159-150">**inicio de sesión único en Azure AD tooconfigure con Trakopolis, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="24159-150">**tooconfigure Azure AD single sign-on with Trakopolis, perform hello following steps:**</span></span>

1. <span data-ttu-id="24159-151">En el portal de Azure, en Hola Hola **Trakopolis** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="24159-151">In hello Azure portal, on hello **Trakopolis** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="24159-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="24159-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_samlbase.png)

3. <span data-ttu-id="24159-155">En hello **Trakopolis dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="24159-155">On hello **Trakopolis Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_url.png)

    <span data-ttu-id="24159-157">a.</span><span class="sxs-lookup"><span data-stu-id="24159-157">a.</span></span> <span data-ttu-id="24159-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.trakopolis.com/`</span><span class="sxs-lookup"><span data-stu-id="24159-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.trakopolis.com/`</span></span>

    <span data-ttu-id="24159-159">b.</span><span class="sxs-lookup"><span data-stu-id="24159-159">b.</span></span> <span data-ttu-id="24159-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.trakopolis.com`</span><span class="sxs-lookup"><span data-stu-id="24159-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.trakopolis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="24159-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="24159-161">These values are not real.</span></span> <span data-ttu-id="24159-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="24159-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="24159-163">Póngase en contacto con [equipo de soporte técnico de cliente de Trakopolis](mailto:support@cantelematics.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="24159-163">Contact [Trakopolis Client support team](mailto:support@cantelematics.com) tooget these values.</span></span> 

4. <span data-ttu-id="24159-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="24159-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_certificate.png) 

5. <span data-ttu-id="24159-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="24159-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trakopolis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="24159-168">En hello **Trakopolis configuración** sección, haga clic en **configurar Trakopolis** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="24159-168">On hello **Trakopolis Configuration** section, click **Configure Trakopolis** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="24159-169">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="24159-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_configure.png) 

7. <span data-ttu-id="24159-171">inicio de sesión único en tooconfigure en **Trakopolis** lado, necesita hello toosend descargado **Metadata XML, dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** demasiado[Trakopolis equipo de soporte técnico](mailto:support@cantelematics.com).</span><span class="sxs-lookup"><span data-stu-id="24159-171">tooconfigure single sign-on on **Trakopolis** side, you need toosend hello downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Trakopolis support team](mailto:support@cantelematics.com).</span></span> <span data-ttu-id="24159-172">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="24159-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="24159-173">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="24159-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="24159-174">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="24159-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="24159-175">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24159-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="24159-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="24159-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="24159-177">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="24159-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="24159-179">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="24159-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="24159-180">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="24159-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="24159-182">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="24159-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="24159-184">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="24159-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="24159-186">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="24159-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-trakopolis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="24159-188">a.</span><span class="sxs-lookup"><span data-stu-id="24159-188">a.</span></span> <span data-ttu-id="24159-189">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="24159-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24159-190">b.</span><span class="sxs-lookup"><span data-stu-id="24159-190">b.</span></span> <span data-ttu-id="24159-191">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="24159-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="24159-192">c.</span><span class="sxs-lookup"><span data-stu-id="24159-192">c.</span></span> <span data-ttu-id="24159-193">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="24159-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="24159-194">d.</span><span class="sxs-lookup"><span data-stu-id="24159-194">d.</span></span> <span data-ttu-id="24159-195">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="24159-195">Click **Create**.</span></span>
 
### <a name="creating-a-trakopolis-test-user"></a><span data-ttu-id="24159-196">Creación de un usuario de prueba de Trakopolis</span><span class="sxs-lookup"><span data-stu-id="24159-196">Creating a Trakopolis test user</span></span>

<span data-ttu-id="24159-197">En esta sección, creará un usuario llamado Britta Simon en Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="24159-197">In this section, you create a user called Britta Simon in Trakopolis.</span></span> <span data-ttu-id="24159-198">Trabajar con [equipo de soporte técnico Trakopolis](mailto:support@cantelematics.com) para agregar usuarios de hello en la plataforma de Trakopolis Hola.</span><span class="sxs-lookup"><span data-stu-id="24159-198">Work with [Trakopolis support team](mailto:support@cantelematics.com) to add hello users in hello Trakopolis platform.</span></span> <span data-ttu-id="24159-199">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="24159-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="24159-200">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="24159-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="24159-201">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTrakopolis.</span><span class="sxs-lookup"><span data-stu-id="24159-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTrakopolis.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="24159-203">**tooassign Britta Simon tooTrakopolis, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="24159-203">**tooassign Britta Simon tooTrakopolis, perform hello following steps:**</span></span>

1. <span data-ttu-id="24159-204">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="24159-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="24159-206">En la lista de aplicaciones de hello, seleccione **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="24159-206">In hello applications list, select **Trakopolis**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_app.png) 

3. <span data-ttu-id="24159-208">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="24159-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="24159-210">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="24159-210">Click **Add** button.</span></span> <span data-ttu-id="24159-211">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="24159-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="24159-213">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="24159-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="24159-214">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="24159-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="24159-215">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="24159-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="24159-216">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="24159-216">Testing single sign-on</span></span>

<span data-ttu-id="24159-217">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="24159-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="24159-218">Al hacer clic en hello Trakopolis el icono Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour Trakopolis aplicación.</span><span class="sxs-lookup"><span data-stu-id="24159-218">When you click hello Trakopolis tile in hello Access Panel, you should get automatically signed-on tooyour Trakopolis application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24159-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="24159-219">Additional resources</span></span>

* [<span data-ttu-id="24159-220">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="24159-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24159-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="24159-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_203.png


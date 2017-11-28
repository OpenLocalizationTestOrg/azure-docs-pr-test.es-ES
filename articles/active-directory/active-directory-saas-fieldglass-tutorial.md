---
title: "Tutorial: Integración de Azure Active Directory con Fieldglass | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Fieldglass."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2510195f-d5b1-4684-b3da-283fb8619df2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d953996bc3bf5721b8280dae4b9992aef7934b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fieldglass"></a><span data-ttu-id="c75bd-103">Tutorial: Integración de Azure Active Directory con Fieldglass</span><span class="sxs-lookup"><span data-stu-id="c75bd-103">Tutorial: Azure Active Directory integration with Fieldglass</span></span>

<span data-ttu-id="c75bd-104">En este tutorial, aprenderá cómo toointegrate Fieldglass con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c75bd-104">In this tutorial, you learn how toointegrate Fieldglass with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c75bd-105">Integración Fieldglass con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c75bd-105">Integrating Fieldglass with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c75bd-106">Puede controlar en Azure AD que tenga acceso tooFieldglass</span><span class="sxs-lookup"><span data-stu-id="c75bd-106">You can control in Azure AD who has access tooFieldglass</span></span>
- <span data-ttu-id="c75bd-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooFieldglass (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c75bd-107">You can enable your users tooautomatically get signed-on tooFieldglass (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c75bd-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c75bd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c75bd-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c75bd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c75bd-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c75bd-110">Prerequisites</span></span>

<span data-ttu-id="c75bd-111">integración de Azure AD con Fieldglass tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c75bd-111">tooconfigure Azure AD integration with Fieldglass, you need hello following items:</span></span>

- <span data-ttu-id="c75bd-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c75bd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c75bd-113">Una suscripción habilitada para el inicio de sesión único en Fieldglass</span><span class="sxs-lookup"><span data-stu-id="c75bd-113">A Fieldglass single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c75bd-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c75bd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c75bd-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c75bd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c75bd-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c75bd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c75bd-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c75bd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c75bd-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c75bd-118">Scenario description</span></span>
<span data-ttu-id="c75bd-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c75bd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c75bd-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c75bd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c75bd-121">Agregar Fieldglass desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c75bd-121">Adding Fieldglass from hello gallery</span></span>
2. <span data-ttu-id="c75bd-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c75bd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fieldglass-from-hello-gallery"></a><span data-ttu-id="c75bd-123">Agregar Fieldglass desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c75bd-123">Adding Fieldglass from hello gallery</span></span>
<span data-ttu-id="c75bd-124">integración de hello tooconfigure de Fieldglass en Azure AD, deberá tooadd Fieldglass de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c75bd-124">tooconfigure hello integration of Fieldglass into Azure AD, you need tooadd Fieldglass from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c75bd-125">**tooadd Fieldglass de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c75bd-125">**tooadd Fieldglass from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c75bd-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c75bd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c75bd-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c75bd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c75bd-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c75bd-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c75bd-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c75bd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c75bd-133">En el cuadro de búsqueda de hello, escriba **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="c75bd-133">In hello search box, type **Fieldglass**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_search.png)

5. <span data-ttu-id="c75bd-135">En el panel de resultados de hello, seleccione **Fieldglass**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c75bd-135">In hello results panel, select **Fieldglass**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c75bd-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c75bd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c75bd-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Fieldglass con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c75bd-138">In this section, you configure and test Azure AD single sign-on with Fieldglass based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c75bd-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Fieldglass es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c75bd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fieldglass is tooa user in Azure AD.</span></span> <span data-ttu-id="c75bd-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Fieldglass debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c75bd-140">In other words, a link relationship between an Azure AD user and hello related user in Fieldglass needs toobe established.</span></span>

<span data-ttu-id="c75bd-141">En Fieldglass, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c75bd-141">In Fieldglass, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c75bd-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Fieldglass, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c75bd-142">tooconfigure and test Azure AD single sign-on with Fieldglass, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c75bd-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c75bd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c75bd-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c75bd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c75bd-145">**[Crear un usuario de prueba Fieldglass](#creating-a-fieldglass-test-user)**  -toohave un equivalente de Britta Simon en Fieldglass que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="c75bd-145">**[Creating a Fieldglass test user](#creating-a-fieldglass-test-user)** - toohave a counterpart of Britta Simon in Fieldglass that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c75bd-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c75bd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c75bd-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c75bd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c75bd-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c75bd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c75bd-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="c75bd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Fieldglass application.</span></span>

<span data-ttu-id="c75bd-150">**inicio de sesión único en Azure AD tooconfigure con Fieldglass, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c75bd-150">**tooconfigure Azure AD single sign-on with Fieldglass, perform hello following steps:**</span></span>

1. <span data-ttu-id="c75bd-151">En el portal de Azure, en Hola Hola **Fieldglass** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c75bd-151">In hello Azure portal, on hello **Fieldglass** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c75bd-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c75bd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_samlbase.png)

3. <span data-ttu-id="c75bd-155">En hello **Fieldglass dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c75bd-155">On hello **Fieldglass Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_url.png)

    <span data-ttu-id="c75bd-157">a.</span><span class="sxs-lookup"><span data-stu-id="c75bd-157">a.</span></span> <span data-ttu-id="c75bd-158">Hola **identificador** cuadro de texto, escriba una dirección URL como `https://www.fieldglass.com` o siguen el patrón de hello:`https://<company name>.fgvms.com`</span><span class="sxs-lookup"><span data-stu-id="c75bd-158">In hello **Identifier** textbox, type a URL as  `https://www.fieldglass.com` or follow hello pattern:  `https://<company name>.fgvms.com`</span></span>

    <span data-ttu-id="c75bd-159">b.</span><span class="sxs-lookup"><span data-stu-id="c75bd-159">b.</span></span> <span data-ttu-id="c75bd-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="c75bd-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://www.fieldglass.net/<company name>`|
    | `https://<company name>.fgvms.com/<company name>`|

    > [!NOTE] 
    > <span data-ttu-id="c75bd-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="c75bd-161">These values are not real.</span></span> <span data-ttu-id="c75bd-162">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="c75bd-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="c75bd-163">Póngase en contacto con [equipo de soporte técnico Fieldglass](http://www.fieldglass.com/solutions/support) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="c75bd-163">Contact [Fieldglass support team](http://www.fieldglass.com/solutions/support) tooget these values.</span></span>
 
4. <span data-ttu-id="c75bd-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c75bd-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_certificate.png) 

5. <span data-ttu-id="c75bd-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c75bd-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fieldglass-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c75bd-168">En hello **Fieldglass configuración** sección, haga clic en **configurar Fieldglass** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="c75bd-168">On hello **Fieldglass Configuration** section, click **Configure Fieldglass** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c75bd-169">Hola copia **dirección URL de cierre de sesión y el Id. de entidad SAML** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="c75bd-169">Copy hello **Sign-Out URL and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_configure.png) 

7. <span data-ttu-id="c75bd-171">tooconfigure inicio de sesión único en **Fieldglass** lado, necesita hello toosend descargado **Certificate(Base64)** y **dirección URL de cierre de sesión, Id. de entidad SAML** demasiado[ Equipo de soporte técnico Fieldglass](http://www.fieldglass.com/solutions/support).</span><span class="sxs-lookup"><span data-stu-id="c75bd-171">tooconfigure single sign-on on **Fieldglass** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID** too[Fieldglass support team](http://www.fieldglass.com/solutions/support).</span></span> <span data-ttu-id="c75bd-172">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="c75bd-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c75bd-173">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="c75bd-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c75bd-174">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="c75bd-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c75bd-175">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c75bd-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c75bd-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c75bd-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="c75bd-177">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c75bd-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c75bd-179">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c75bd-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c75bd-180">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c75bd-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c75bd-182">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c75bd-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c75bd-184">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c75bd-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c75bd-186">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c75bd-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c75bd-188">a.</span><span class="sxs-lookup"><span data-stu-id="c75bd-188">a.</span></span> <span data-ttu-id="c75bd-189">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c75bd-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c75bd-190">b.</span><span class="sxs-lookup"><span data-stu-id="c75bd-190">b.</span></span> <span data-ttu-id="c75bd-191">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c75bd-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c75bd-192">c.</span><span class="sxs-lookup"><span data-stu-id="c75bd-192">c.</span></span> <span data-ttu-id="c75bd-193">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c75bd-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c75bd-194">d.</span><span class="sxs-lookup"><span data-stu-id="c75bd-194">d.</span></span> <span data-ttu-id="c75bd-195">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c75bd-195">Click **Create**.</span></span>
 
### <a name="creating-a-fieldglass-test-user"></a><span data-ttu-id="c75bd-196">Creación de un usuario de prueba en Fieldglass</span><span class="sxs-lookup"><span data-stu-id="c75bd-196">Creating a Fieldglass test user</span></span>

<span data-ttu-id="c75bd-197">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en FieldGlass toocreate.</span><span class="sxs-lookup"><span data-stu-id="c75bd-197">hello objective of this section is toocreate a user called Britta Simon in FieldGlass.</span></span> <span data-ttu-id="c75bd-198">Trabaje con su [equipo de soporte técnico Fieldglass](http://www.fieldglass.com/solutions/support) a los usuarios de tooadd Hola Hola Fieldglass cuenta.</span><span class="sxs-lookup"><span data-stu-id="c75bd-198">Please work with your [Fieldglass support team](http://www.fieldglass.com/solutions/support) tooadd hello users in hello Fieldglass account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c75bd-199">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c75bd-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c75bd-200">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooFieldglass.</span><span class="sxs-lookup"><span data-stu-id="c75bd-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFieldglass.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c75bd-202">**tooassign Britta Simon tooFieldglass, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c75bd-202">**tooassign Britta Simon tooFieldglass, perform hello following steps:**</span></span>

1. <span data-ttu-id="c75bd-203">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c75bd-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c75bd-205">En la lista de aplicaciones de hello, seleccione **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="c75bd-205">In hello applications list, select **Fieldglass**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_app.png) 

3. <span data-ttu-id="c75bd-207">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c75bd-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c75bd-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c75bd-209">Click **Add** button.</span></span> <span data-ttu-id="c75bd-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c75bd-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c75bd-212">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c75bd-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c75bd-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c75bd-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c75bd-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c75bd-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c75bd-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c75bd-215">Testing single sign-on</span></span>

<span data-ttu-id="c75bd-216">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c75bd-216">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c75bd-217">Al hacer clic en hello Fieldglass el icono Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour Fieldglass aplicación.</span><span class="sxs-lookup"><span data-stu-id="c75bd-217">When you click hello Fieldglass tile in hello Access Panel, you should get automatically signed-on tooyour Fieldglass application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c75bd-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c75bd-218">Additional resources</span></span>

* [<span data-ttu-id="c75bd-219">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c75bd-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c75bd-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c75bd-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_203.png


---
title: "Tutorial: Integración de Azure Active Directory con Condeco | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Condeco."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4601c17d-ad93-4865-8885-b378c4bbe82b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 20c57ff0466c28d4fb69f73bc8b5a479715eba0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-condeco"></a><span data-ttu-id="d2ad0-103">Tutorial: Integración de Azure Active Directory con Condeco</span><span class="sxs-lookup"><span data-stu-id="d2ad0-103">Tutorial: Azure Active Directory integration with Condeco</span></span>

<span data-ttu-id="d2ad0-104">En este tutorial, aprenderá cómo toointegrate Condeco con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d2ad0-104">In this tutorial, you learn how toointegrate Condeco with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d2ad0-105">Integración Condeco con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d2ad0-105">Integrating Condeco with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d2ad0-106">Puede controlar en Azure AD que tenga acceso tooCondeco</span><span class="sxs-lookup"><span data-stu-id="d2ad0-106">You can control in Azure AD who has access tooCondeco</span></span>
- <span data-ttu-id="d2ad0-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooCondeco (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2ad0-107">You can enable your users tooautomatically get signed-on tooCondeco (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d2ad0-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d2ad0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d2ad0-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d2ad0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2ad0-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d2ad0-110">Prerequisites</span></span>

<span data-ttu-id="d2ad0-111">integración de Azure AD con Condeco tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d2ad0-111">tooconfigure Azure AD integration with Condeco, you need hello following items:</span></span>

- <span data-ttu-id="d2ad0-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2ad0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d2ad0-113">Una suscripción habilitada para inicio de sesión único en Condeco</span><span class="sxs-lookup"><span data-stu-id="d2ad0-113">A Condeco single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d2ad0-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d2ad0-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d2ad0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d2ad0-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d2ad0-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d2ad0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d2ad0-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d2ad0-118">Scenario description</span></span>
<span data-ttu-id="d2ad0-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d2ad0-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="d2ad0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d2ad0-121">Agregar Condeco desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="d2ad0-121">Adding Condeco from hello gallery</span></span>
2. <span data-ttu-id="d2ad0-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2ad0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-condeco-from-hello-gallery"></a><span data-ttu-id="d2ad0-123">Agregar Condeco desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="d2ad0-123">Adding Condeco from hello gallery</span></span>
<span data-ttu-id="d2ad0-124">integración de hello tooconfigure de Condeco en Azure AD, deberá tooadd Condeco de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-124">tooconfigure hello integration of Condeco into Azure AD, you need tooadd Condeco from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d2ad0-125">**tooadd Condeco de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d2ad0-125">**tooadd Condeco from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2ad0-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d2ad0-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d2ad0-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="d2ad0-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="d2ad0-133">En el cuadro de búsqueda de hello, escriba **Condeco**.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-133">In hello search box, type **Condeco**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_search.png)

5. <span data-ttu-id="d2ad0-135">En el panel de resultados de hello, seleccione **Condeco**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-135">In hello results panel, select **Condeco**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d2ad0-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2ad0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d2ad0-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Condeco con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d2ad0-138">In this section, you configure and test Azure AD single sign-on with Condeco based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d2ad0-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Condeco es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Condeco is tooa user in Azure AD.</span></span> <span data-ttu-id="d2ad0-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Condeco debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-140">In other words, a link relationship between an Azure AD user and hello related user in Condeco needs toobe established.</span></span>

<span data-ttu-id="d2ad0-141">En Condeco, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-141">In Condeco, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d2ad0-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Condeco, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d2ad0-142">tooconfigure and test Azure AD single sign-on with Condeco, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d2ad0-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d2ad0-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d2ad0-145">**[Crear un usuario de prueba Condeco](#creating-a-condeco-test-user) ** -toohave un equivalente de Britta Simon en Condeco que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-145">**[Creating a Condeco test user](#creating-a-condeco-test-user)** - toohave a counterpart of Britta Simon in Condeco that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d2ad0-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d2ad0-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d2ad0-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2ad0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d2ad0-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Condeco.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Condeco application.</span></span>

<span data-ttu-id="d2ad0-150">**inicio de sesión único en Azure AD tooconfigure con Condeco, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d2ad0-150">**tooconfigure Azure AD single sign-on with Condeco, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2ad0-151">En el portal de Azure, en Hola Hola **Condeco** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-151">In hello Azure portal, on hello **Condeco** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="d2ad0-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_samlbase.png)

3. <span data-ttu-id="d2ad0-155">En hello **Condeco dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d2ad0-155">On hello **Condeco Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_url.png)

    <span data-ttu-id="d2ad0-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.condecosoftware.com`</span><span class="sxs-lookup"><span data-stu-id="d2ad0-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.condecosoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d2ad0-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-158">This value is not real.</span></span> <span data-ttu-id="d2ad0-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="d2ad0-160">Póngase en contacto con [equipo de soporte técnico de cliente de Condeco](mailTo:supportna@condecosoftware.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-160">Contact [Condeco Client support team](mailTo:supportna@condecosoftware.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="d2ad0-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_certificate.png) 

5. <span data-ttu-id="d2ad0-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d2ad0-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-condeco-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d2ad0-165">tooconfigure inicio de sesión único en **Condeco** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de Condeco](mailTo:supportna@condecosoftware.com).</span><span class="sxs-lookup"><span data-stu-id="d2ad0-165">tooconfigure single sign-on on **Condeco** side, you need toosend hello downloaded **Metadata XML** too[Condeco support team](mailTo:supportna@condecosoftware.com).</span></span> <span data-ttu-id="d2ad0-166">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d2ad0-167">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="d2ad0-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d2ad0-168">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d2ad0-169">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d2ad0-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d2ad0-170">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2ad0-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="d2ad0-171">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="d2ad0-173">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d2ad0-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2ad0-174">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-condeco-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d2ad0-176">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-condeco-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d2ad0-178">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-condeco-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d2ad0-180">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="d2ad0-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-condeco-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d2ad0-182">a.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-182">a.</span></span> <span data-ttu-id="d2ad0-183">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d2ad0-184">b.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-184">b.</span></span> <span data-ttu-id="d2ad0-185">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d2ad0-186">c.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-186">c.</span></span> <span data-ttu-id="d2ad0-187">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d2ad0-188">d.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-188">d.</span></span> <span data-ttu-id="d2ad0-189">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-189">Click **Create**.</span></span>
 
### <a name="creating-a-condeco-test-user"></a><span data-ttu-id="d2ad0-190">Crear un usuario de prueba de Condeco</span><span class="sxs-lookup"><span data-stu-id="d2ad0-190">Creating a Condeco test user</span></span>

<span data-ttu-id="d2ad0-191">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Condeco toocreate.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-191">hello objective of this section is toocreate a user called Britta Simon in Condeco.</span></span> <span data-ttu-id="d2ad0-192">Condeco admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-192">Condeco supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="d2ad0-193">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-193">There is no action item for you in this section.</span></span> <span data-ttu-id="d2ad0-194">Se crea un nuevo usuario durante un tooaccess intento Condeco si no existe todavía.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-194">A new user is created during an attempt tooaccess Condeco if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="d2ad0-195">Si necesita un usuario toocreate manualmente, necesita hello toocontact [equipo de soporte técnico de Condeco](mailTo:supportna@condecosoftware.com).</span><span class="sxs-lookup"><span data-stu-id="d2ad0-195">If you need toocreate a user manually, you need toocontact hello [Condeco support team](mailTo:supportna@condecosoftware.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d2ad0-196">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2ad0-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d2ad0-197">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCondeco.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCondeco.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="d2ad0-199">**tooassign Britta Simon tooCondeco, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d2ad0-199">**tooassign Britta Simon tooCondeco, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2ad0-200">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d2ad0-202">En la lista de aplicaciones de hello, seleccione **Condeco**.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-202">In hello applications list, select **Condeco**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_app.png) 

3. <span data-ttu-id="d2ad0-204">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="d2ad0-206">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-206">Click **Add** button.</span></span> <span data-ttu-id="d2ad0-207">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="d2ad0-209">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d2ad0-210">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d2ad0-211">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d2ad0-212">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="d2ad0-212">Testing single sign-on</span></span>

<span data-ttu-id="d2ad0-213">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d2ad0-214">Al hacer clic en icono de Condeco Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Condeco aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2ad0-214">When you click hello Condeco tile in hello Access Panel, you should get automatically signed-on tooyour Condeco application.</span></span>
<span data-ttu-id="d2ad0-215">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d2ad0-215">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d2ad0-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d2ad0-216">Additional resources</span></span>

* [<span data-ttu-id="d2ad0-217">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d2ad0-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d2ad0-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d2ad0-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_203.png


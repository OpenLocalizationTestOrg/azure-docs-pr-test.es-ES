---
title: "Tutorial: Integración de Azure Active Directory con AppBlade | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y AppBlade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 06f3d8fcee97945c867bca6f3aebe15ecef04617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="eee77-103">Tutorial: Integración de Azure Active Directory con AppBlade</span><span class="sxs-lookup"><span data-stu-id="eee77-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>

<span data-ttu-id="eee77-104">En este tutorial, aprenderá cómo toointegrate AppBlade con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eee77-104">In this tutorial, you learn how toointegrate AppBlade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eee77-105">Integración AppBlade con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="eee77-105">Integrating AppBlade with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eee77-106">Puede controlar en Azure AD que tenga acceso tooAppBlade</span><span class="sxs-lookup"><span data-stu-id="eee77-106">You can control in Azure AD who has access tooAppBlade</span></span>
- <span data-ttu-id="eee77-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAppBlade (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eee77-107">You can enable your users tooautomatically get signed-on tooAppBlade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eee77-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="eee77-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eee77-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eee77-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eee77-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="eee77-110">Prerequisites</span></span>

<span data-ttu-id="eee77-111">integración de Azure AD con AppBlade tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="eee77-111">tooconfigure Azure AD integration with AppBlade, you need hello following items:</span></span>

- <span data-ttu-id="eee77-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eee77-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eee77-113">Una suscripción habilitada para inicio de sesión único en AppBlade</span><span class="sxs-lookup"><span data-stu-id="eee77-113">An AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eee77-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="eee77-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eee77-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="eee77-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eee77-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="eee77-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eee77-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eee77-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eee77-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="eee77-118">Scenario description</span></span>
<span data-ttu-id="eee77-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="eee77-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eee77-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="eee77-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eee77-121">Agregar AppBlade desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="eee77-121">Adding AppBlade from hello gallery</span></span>
2. <span data-ttu-id="eee77-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eee77-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-hello-gallery"></a><span data-ttu-id="eee77-123">Agregar AppBlade desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="eee77-123">Adding AppBlade from hello gallery</span></span>
<span data-ttu-id="eee77-124">integración de hello tooconfigure de AppBlade en Azure AD, deberá tooadd AppBlade de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="eee77-124">tooconfigure hello integration of AppBlade into Azure AD, you need tooadd AppBlade from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eee77-125">**tooadd AppBlade de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="eee77-125">**tooadd AppBlade from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eee77-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="eee77-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eee77-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="eee77-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eee77-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="eee77-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="eee77-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eee77-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="eee77-133">En el cuadro de búsqueda de hello, escriba **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="eee77-133">In hello search box, type **AppBlade**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_search.png)

5. <span data-ttu-id="eee77-135">En el panel de resultados de hello, seleccione **AppBlade**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="eee77-135">In hello results panel, select **AppBlade**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eee77-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eee77-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eee77-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con AppBlade con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="eee77-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eee77-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en AppBlade es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eee77-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppBlade is tooa user in Azure AD.</span></span> <span data-ttu-id="eee77-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en AppBlade debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="eee77-140">In other words, a link relationship between an Azure AD user and hello related user in AppBlade needs toobe established.</span></span>

<span data-ttu-id="eee77-141">En AppBlade, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="eee77-141">In AppBlade, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eee77-142">tooconfigure y prueba de inicio de sesión único en Azure AD con AppBlade, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="eee77-142">tooconfigure and test Azure AD single sign-on with AppBlade, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eee77-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="eee77-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eee77-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eee77-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eee77-145">**[Creación de un usuario de prueba AppBlade](#creating-an-appblade-test-user)**  -toohave un equivalente de Britta Simon en AppBlade que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="eee77-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - toohave a counterpart of Britta Simon in AppBlade that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eee77-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="eee77-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eee77-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="eee77-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eee77-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eee77-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eee77-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación AppBlade.</span><span class="sxs-lookup"><span data-stu-id="eee77-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="eee77-150">**inicio de sesión único en Azure AD tooconfigure con AppBlade, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="eee77-150">**tooconfigure Azure AD single sign-on with AppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="eee77-151">En el portal de Azure, en Hola Hola **AppBlade** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="eee77-151">In hello Azure portal, on hello **AppBlade** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="eee77-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="eee77-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_samlbase.png)

3. <span data-ttu-id="eee77-155">En hello **AppBlade dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="eee77-155">On hello **AppBlade Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_url.png)

    <span data-ttu-id="eee77-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.appblade.com/saml/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="eee77-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eee77-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="eee77-158">This value is not real.</span></span> <span data-ttu-id="eee77-159">Valor de Hola de actualización con Hola dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="eee77-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="eee77-160">Póngase en contacto con [equipo de soporte técnico de AppBlade cliente](mailto:support@appblade.com) valor de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="eee77-160">Contact [AppBlade Client support team](mailto:support@appblade.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="eee77-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="eee77-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_certificate.png) 

5. <span data-ttu-id="eee77-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="eee77-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-appblade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eee77-165">tooconfigure inicio de sesión único en **AppBlade** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="eee77-165">tooconfigure single sign-on on **AppBlade** side, you need toosend hello downloaded **Metadata XML** too[AppBlade support team](mailto:support@appblade.com).</span></span> <span data-ttu-id="eee77-166">Además, por favor, pídale hello tooconfigure **dirección URL del emisor de SSO** como `https://appblade.com/saml`.</span><span class="sxs-lookup"><span data-stu-id="eee77-166">Also, please ask them tooconfigure hello **SSO Issuer URL** as `https://appblade.com/saml`.</span></span> <span data-ttu-id="eee77-167">Esta configuración es necesaria para toowork de inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="eee77-167">This setting is required for single sign-on toowork.</span></span>


> [!TIP]
> <span data-ttu-id="eee77-168">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="eee77-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eee77-169">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="eee77-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eee77-170">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eee77-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eee77-171">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="eee77-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="eee77-172">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="eee77-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="eee77-174">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="eee77-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eee77-175">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="eee77-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eee77-177">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="eee77-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eee77-179">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="eee77-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eee77-181">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="eee77-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eee77-183">a.</span><span class="sxs-lookup"><span data-stu-id="eee77-183">a.</span></span> <span data-ttu-id="eee77-184">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eee77-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eee77-185">b.</span><span class="sxs-lookup"><span data-stu-id="eee77-185">b.</span></span> <span data-ttu-id="eee77-186">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eee77-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eee77-187">c.</span><span class="sxs-lookup"><span data-stu-id="eee77-187">c.</span></span> <span data-ttu-id="eee77-188">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="eee77-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eee77-189">d.</span><span class="sxs-lookup"><span data-stu-id="eee77-189">d.</span></span> <span data-ttu-id="eee77-190">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="eee77-190">Click **Create**.</span></span>
 
### <a name="creating-an-appblade-test-user"></a><span data-ttu-id="eee77-191">Creación de un usuario de prueba de AppBlade</span><span class="sxs-lookup"><span data-stu-id="eee77-191">Creating an AppBlade test user</span></span>

<span data-ttu-id="eee77-192">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en AppBlade toocreate.</span><span class="sxs-lookup"><span data-stu-id="eee77-192">hello objective of this section is toocreate a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="eee77-193">AppBlade admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="eee77-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="eee77-194">**Asegúrese de que el nombre de dominio está configurado con AppBlade para el aprovisionamiento de usuarios. Después de que solo Hola just-in-time aprovisionamiento de usuarios funciona.**</span><span class="sxs-lookup"><span data-stu-id="eee77-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only hello just-in-time user provisioning works.**</span></span>

<span data-ttu-id="eee77-195">Si el usuario hello tiene una dirección de correo electrónico termina con configurado por AppBlade para su cuenta de dominio de hello, a continuación, el usuario de Hola unirá automáticamente a cuenta de hello como un miembro con el nivel de permiso de hello especificado, que es uno de "Basic" (un usuario básico que solo se puede instalar las aplicaciones), "miembro del equipo (un usuario que puede cargar nuevas versiones de aplicaciones y administrar proyectos) o"Administrador"(cuenta de toohello de privilegios de administrador total).</span><span class="sxs-lookup"><span data-stu-id="eee77-195">If hello user has an email address ending with hello domain configured by AppBlade for your account, then hello user will automatically join hello account as a member with hello permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges toohello account).</span></span> <span data-ttu-id="eee77-196">Normalmente uno se elija básico y, a continuación, promocionar los usuarios manualmente a través de un inicio de sesión de administrador (AppBlade necesita tooconfigure un inicio de sesión de administración basada en correo electrónico de antemano o promocionar un usuario en nombre de cliente hello después de iniciar sesión).</span><span class="sxs-lookup"><span data-stu-id="eee77-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs tooconfigure either an email-based admin login in advance or promote a user on behalf of hello customer after login).</span></span>

<span data-ttu-id="eee77-197">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="eee77-197">There is no action item for you in this section.</span></span> <span data-ttu-id="eee77-198">Se crea un nuevo usuario durante un tooaccess intento AppBlade si no existe todavía.</span><span class="sxs-lookup"><span data-stu-id="eee77-198">A new user is created during an attempt tooaccess AppBlade if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="eee77-199">Si necesita un usuario toocreate manualmente, necesita hello toocontact [equipo de soporte técnico de AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="eee77-199">If you need toocreate a user manually, you need toocontact hello [AppBlade support team](mailto:support@appblade.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eee77-200">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="eee77-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eee77-201">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAppBlade.</span><span class="sxs-lookup"><span data-stu-id="eee77-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppBlade.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="eee77-203">**tooassign Britta Simon tooAppBlade, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="eee77-203">**tooassign Britta Simon tooAppBlade, perform hello following steps:**</span></span>

1. <span data-ttu-id="eee77-204">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="eee77-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="eee77-206">En la lista de aplicaciones de hello, seleccione **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="eee77-206">In hello applications list, select **AppBlade**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_app.png) 

3. <span data-ttu-id="eee77-208">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="eee77-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="eee77-210">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="eee77-210">Click **Add** button.</span></span> <span data-ttu-id="eee77-211">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="eee77-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="eee77-213">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="eee77-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eee77-214">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="eee77-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eee77-215">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="eee77-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eee77-216">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="eee77-216">Testing single sign-on</span></span>

<span data-ttu-id="eee77-217">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="eee77-217">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="eee77-218">Al hacer clic en icono de AppBlade Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour AppBlade aplicación.</span><span class="sxs-lookup"><span data-stu-id="eee77-218">When you click hello AppBlade tile in hello Access Panel, you should get automatically signed-on tooyour AppBlade application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="eee77-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="eee77-219">Additional resources</span></span>

* [<span data-ttu-id="eee77-220">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eee77-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eee77-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eee77-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_203.png


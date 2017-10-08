---
title: "Tutorial: integración de Azure Active Directory con Projectplace | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Projectplace."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 95d109052096161f995ff26a18f8d64f0c4a3dc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="36a07-103">Tutorial: Integración de Azure Active Directory con Projectplace</span><span class="sxs-lookup"><span data-stu-id="36a07-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="36a07-104">En este tutorial, aprenderá cómo toointegrate Projectplace con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="36a07-104">In this tutorial, you learn how toointegrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="36a07-105">Integración de Projectplace con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="36a07-105">Integrating Projectplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="36a07-106">Puede controlar en Azure AD que tenga acceso tooProjectplace</span><span class="sxs-lookup"><span data-stu-id="36a07-106">You can control in Azure AD who has access tooProjectplace</span></span>
- <span data-ttu-id="36a07-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooProjectplace (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36a07-107">You can enable your users tooautomatically get signed-on tooProjectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="36a07-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="36a07-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="36a07-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="36a07-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36a07-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="36a07-110">Prerequisites</span></span>

<span data-ttu-id="36a07-111">integración de Azure AD con Projectplace tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="36a07-111">tooconfigure Azure AD integration with Projectplace, you need hello following items:</span></span>

- <span data-ttu-id="36a07-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36a07-112">An Azure AD subscription</span></span>
- <span data-ttu-id="36a07-113">Una suscripción habilitada para el inicio de sesión único en Projectplace</span><span class="sxs-lookup"><span data-stu-id="36a07-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="36a07-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="36a07-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="36a07-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="36a07-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="36a07-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="36a07-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="36a07-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36a07-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="36a07-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="36a07-118">Scenario description</span></span>
<span data-ttu-id="36a07-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="36a07-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="36a07-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="36a07-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="36a07-121">Agregar Projectplace desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="36a07-121">Adding Projectplace from hello gallery</span></span>
2. <span data-ttu-id="36a07-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36a07-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-hello-gallery"></a><span data-ttu-id="36a07-123">Agregar Projectplace desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="36a07-123">Adding Projectplace from hello gallery</span></span>
<span data-ttu-id="36a07-124">integración de hello tooconfigure de Projectplace en Azure AD, deberá tooadd Projectplace de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="36a07-124">tooconfigure hello integration of Projectplace into Azure AD, you need tooadd Projectplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="36a07-125">**tooadd Projectplace de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="36a07-125">**tooadd Projectplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="36a07-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="36a07-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="36a07-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="36a07-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="36a07-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="36a07-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="36a07-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="36a07-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="36a07-133">En el cuadro de búsqueda de hello, escriba **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="36a07-133">In hello search box, type **Projectplace**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_search.png)

5. <span data-ttu-id="36a07-135">En el panel de resultados de hello, seleccione **Projectplace**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="36a07-135">In hello results panel, select **Projectplace**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="36a07-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36a07-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="36a07-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Projectplace con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="36a07-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="36a07-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Projectplace es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36a07-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Projectplace is tooa user in Azure AD.</span></span> <span data-ttu-id="36a07-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Projectplace debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="36a07-140">In other words, a link relationship between an Azure AD user and hello related user in Projectplace needs toobe established.</span></span>

<span data-ttu-id="36a07-141">En Projectplace, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="36a07-141">In Projectplace, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="36a07-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Projectplace, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="36a07-142">tooconfigure and test Azure AD single sign-on with Projectplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="36a07-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="36a07-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="36a07-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="36a07-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="36a07-145">**[Crear un usuario de prueba de Projectplace](#creating-a-projectplace-test-user)**  -toohave un equivalente de Britta Simon en Projectplace que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="36a07-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - toohave a counterpart of Britta Simon in Projectplace that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="36a07-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="36a07-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="36a07-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="36a07-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="36a07-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36a07-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="36a07-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Projectplace.</span><span class="sxs-lookup"><span data-stu-id="36a07-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="36a07-150">**inicio de sesión único en Azure AD tooconfigure con Projectplace, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="36a07-150">**tooconfigure Azure AD single sign-on with Projectplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="36a07-151">En el portal de Azure, en Hola Hola **Projectplace** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="36a07-151">In hello Azure portal, on hello **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="36a07-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="36a07-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_samlbase.png)

3. <span data-ttu-id="36a07-155">En hello **Projectplace dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="36a07-155">On hello **Projectplace Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="36a07-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company>.projectplace.com`</span><span class="sxs-lookup"><span data-stu-id="36a07-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="36a07-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="36a07-158">This value is not real.</span></span> <span data-ttu-id="36a07-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="36a07-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="36a07-160">Póngase en contacto con [equipo de soporte técnico de Projectplace cliente](https://success.planview.com/Projectplace/Support) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="36a07-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) tooget this value.</span></span> 
 
4. <span data-ttu-id="36a07-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="36a07-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_certificate.png) 

5. <span data-ttu-id="36a07-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="36a07-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-projectplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="36a07-165">inicio de sesión único en tooconfigure en **Projectplace** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="36a07-165">tooconfigure single sign-on on **Projectplace** side, you need toosend hello downloaded **Metadata XML** too[Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="36a07-166">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="36a07-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="36a07-167">configuración de inicio de sesión único de Hello tiene toobe realizada por hello [equipo de soporte técnico de Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="36a07-167">hello single sign-on configuration has toobe performed by hello [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="36a07-168">Recibirá una notificación en cuanto se ha completado la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="36a07-168">You will get a notification as soon as hello configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="36a07-169">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="36a07-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="36a07-170">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="36a07-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="36a07-171">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="36a07-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="36a07-172">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="36a07-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="36a07-173">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="36a07-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="36a07-175">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="36a07-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="36a07-176">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="36a07-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="36a07-178">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="36a07-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="36a07-180">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="36a07-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="36a07-182">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="36a07-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="36a07-184">a.</span><span class="sxs-lookup"><span data-stu-id="36a07-184">a.</span></span> <span data-ttu-id="36a07-185">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="36a07-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="36a07-186">b.</span><span class="sxs-lookup"><span data-stu-id="36a07-186">b.</span></span> <span data-ttu-id="36a07-187">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="36a07-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="36a07-188">c.</span><span class="sxs-lookup"><span data-stu-id="36a07-188">c.</span></span> <span data-ttu-id="36a07-189">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="36a07-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="36a07-190">d.</span><span class="sxs-lookup"><span data-stu-id="36a07-190">d.</span></span> <span data-ttu-id="36a07-191">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="36a07-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="36a07-192">Creación de un usuario de prueba de Projectplace</span><span class="sxs-lookup"><span data-stu-id="36a07-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="36a07-193">En orden tooenable toolog de los usuarios de Azure AD en Projectplace, se les deben aprovisionar en Projectplace.</span><span class="sxs-lookup"><span data-stu-id="36a07-193">In order tooenable Azure AD users toolog into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="36a07-194">En caso de hello de Projectplace, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="36a07-194">In hello case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="36a07-195">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="36a07-195">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="36a07-196">Inicie sesión en tooyour **Projectplace** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="36a07-196">Log in tooyour **Projectplace** company site as an administrator.</span></span>

2. <span data-ttu-id="36a07-197">Vaya demasiado**personas**y, a continuación, haga clic en **miembros**.</span><span class="sxs-lookup"><span data-stu-id="36a07-197">Go too**People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="36a07-198">![Personas](./media/active-directory-saas-projectplace-tutorial/ic790228.png "Personas")</span><span class="sxs-lookup"><span data-stu-id="36a07-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span></span>

3. <span data-ttu-id="36a07-199">Haga clic en **Agregar miembro**.</span><span class="sxs-lookup"><span data-stu-id="36a07-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="36a07-200">![Agregar miembros](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Agregar miembros")</span><span class="sxs-lookup"><span data-stu-id="36a07-200">![Add Members](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Add Members")</span></span>

4. <span data-ttu-id="36a07-201">Hola **Agregar miembro** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="36a07-201">In hello **Add Member** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="36a07-202">![Nuevos miembros](./media/active-directory-saas-projectplace-tutorial/ic790233.png "Nuevos miembros")</span><span class="sxs-lookup"><span data-stu-id="36a07-202">![New Members](./media/active-directory-saas-projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="36a07-203">a.</span><span class="sxs-lookup"><span data-stu-id="36a07-203">a.</span></span> <span data-ttu-id="36a07-204">Hola **nuevos miembros** cuadros de texto relacionados con el cuadro de texto, escriba Hola dirección de correo electrónico de una cuenta válida de AAD que quiera tooprovision en hello.</span><span class="sxs-lookup"><span data-stu-id="36a07-204">In hello **New Members** textbox, type hello email address of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="36a07-205">b.</span><span class="sxs-lookup"><span data-stu-id="36a07-205">b.</span></span> <span data-ttu-id="36a07-206">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="36a07-206">Click **Send**.</span></span>

   <span data-ttu-id="36a07-207">Un correo electrónico con una cuenta de hello tooconfirm vínculo antes de activarla se envía toohello titular de la cuenta de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36a07-207">An email including a link tooconfirm hello account before it becomes active is sent toohello Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="36a07-208">Puede usar cualquier otra Projectplace usuario cuenta herramienta de creación o las API proporcionadas por Projectplace tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="36a07-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="36a07-209">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="36a07-209">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="36a07-210">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooProjectplace.</span><span class="sxs-lookup"><span data-stu-id="36a07-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProjectplace.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="36a07-212">**tooassign Britta Simon tooProjectplace, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="36a07-212">**tooassign Britta Simon tooProjectplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="36a07-213">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="36a07-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="36a07-215">En la lista de aplicaciones de hello, seleccione **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="36a07-215">In hello applications list, select **Projectplace**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_app.png) 

3. <span data-ttu-id="36a07-217">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="36a07-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="36a07-219">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="36a07-219">Click **Add** button.</span></span> <span data-ttu-id="36a07-220">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="36a07-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="36a07-222">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="36a07-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="36a07-223">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="36a07-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="36a07-224">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="36a07-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="36a07-225">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="36a07-225">Testing single sign-on</span></span>

<span data-ttu-id="36a07-226">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="36a07-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="36a07-227">Al hacer clic en icono de Projectplace Hola Hola Panel de acceso, deberá obtener aplicaciones de Projectplace tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="36a07-227">When you click hello Projectplace tile in hello Access Panel, you should get automatically signed-on tooyour Projectplace application.</span></span>
<span data-ttu-id="36a07-228">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="36a07-228">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="36a07-229">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="36a07-229">Additional resources</span></span>

* [<span data-ttu-id="36a07-230">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36a07-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="36a07-231">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="36a07-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_203.png


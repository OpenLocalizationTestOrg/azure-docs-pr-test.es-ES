---
title: "Tutorial: Integración de Azure Active Directory con FM:Systems | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y FM: Systems."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 677ef74dac663a43835d65a4d4f4fd031a0078cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a><span data-ttu-id="cd00c-103">Tutorial: Integración de Azure Active Directory con FM:Systems</span><span class="sxs-lookup"><span data-stu-id="cd00c-103">Tutorial: Azure Active Directory integration with FM:Systems</span></span>

<span data-ttu-id="cd00c-104">En este tutorial, aprenderá cómo toointegrate FM: Systems con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cd00c-104">In this tutorial, you learn how toointegrate FM:Systems with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cd00c-105">Integración de FM: Systems con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="cd00c-105">Integrating FM:Systems with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cd00c-106">Puede controlar en Azure AD que tenga acceso tooFM:Systems</span><span class="sxs-lookup"><span data-stu-id="cd00c-106">You can control in Azure AD who has access tooFM:Systems</span></span>
- <span data-ttu-id="cd00c-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooFM:Systems (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd00c-107">You can enable your users tooautomatically get signed-on tooFM:Systems (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cd00c-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cd00c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cd00c-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cd00c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd00c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cd00c-110">Prerequisites</span></span>

<span data-ttu-id="cd00c-111">tooconfigure integración de Azure AD con FM: Systems, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="cd00c-111">tooconfigure Azure AD integration with FM:Systems, you need hello following items:</span></span>

- <span data-ttu-id="cd00c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd00c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cd00c-113">Una suscripción que permita el inicio de sesión único en FM:Systems</span><span class="sxs-lookup"><span data-stu-id="cd00c-113">An FM:Systems single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cd00c-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="cd00c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cd00c-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="cd00c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cd00c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="cd00c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cd00c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cd00c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cd00c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="cd00c-118">Scenario description</span></span>
<span data-ttu-id="cd00c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="cd00c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cd00c-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="cd00c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cd00c-121">Adición de FM: Systems desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="cd00c-121">Adding FM:Systems from hello gallery</span></span>
2. <span data-ttu-id="cd00c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd00c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fmsystems-from-hello-gallery"></a><span data-ttu-id="cd00c-123">Adición de FM: Systems desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="cd00c-123">Adding FM:Systems from hello gallery</span></span>
<span data-ttu-id="cd00c-124">integración de hello tooconfigure de FM: Systems en Azure AD, deberá tooadd FM: Systems en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="cd00c-124">tooconfigure hello integration of FM:Systems into Azure AD, you need tooadd FM:Systems from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cd00c-125">**tooadd FM: Systems de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cd00c-125">**tooadd FM:Systems from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd00c-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cd00c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cd00c-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cd00c-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="cd00c-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cd00c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="cd00c-133">En el cuadro de búsqueda de hello, escriba **FM: Systems**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-133">In hello search box, type **FM:Systems**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_search.png)

5. <span data-ttu-id="cd00c-135">En el panel de resultados de hello, seleccione **FM: Systems**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cd00c-135">In hello results panel, select **FM:Systems**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cd00c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd00c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cd00c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con FM:Systems con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cd00c-138">In this section, you configure and test Azure AD single sign-on with FM:Systems based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cd00c-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en FM: Systems es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd00c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FM:Systems is tooa user in Azure AD.</span></span> <span data-ttu-id="cd00c-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en FM: Systems debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="cd00c-140">In other words, a link relationship between an Azure AD user and hello related user in FM:Systems needs toobe established.</span></span>

<span data-ttu-id="cd00c-141">En FM: Systems, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd00c-141">In FM:Systems, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cd00c-142">tooconfigure y prueba de inicio de sesión único en Azure AD con FM: Systems, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="cd00c-142">tooconfigure and test Azure AD single sign-on with FM:Systems, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cd00c-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="cd00c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cd00c-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cd00c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cd00c-145">**[Creación de un usuario de prueba de FM: Systems](#creating-an-fmsystems-test-user)**  -toohave un equivalente de Britta Simon en FM: Systems que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="cd00c-145">**[Creating an FM:Systems test user](#creating-an-fmsystems-test-user)** - toohave a counterpart of Britta Simon in FM:Systems that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cd00c-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cd00c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cd00c-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="cd00c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cd00c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd00c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cd00c-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de FM: Systems.</span><span class="sxs-lookup"><span data-stu-id="cd00c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FM:Systems application.</span></span>

<span data-ttu-id="cd00c-150">**inicio de sesión único en Azure AD tooconfigure con FM: Systems, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cd00c-150">**tooconfigure Azure AD single sign-on with FM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd00c-151">En el portal de Azure, en Hola Hola **FM: Systems** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-151">In hello Azure portal, on hello **FM:Systems** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="cd00c-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="cd00c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_samlbase.png)

3. <span data-ttu-id="cd00c-155">En hello **FM: Systems dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cd00c-155">On hello **FM:Systems Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_url.png)

    <span data-ttu-id="cd00c-157">Hola **dirección URL de respuesta** cuadro de texto, escriba su FM: Systems **dirección URL de respuesta**, escriba Hola la dirección URL con hello sigue el patrón:`https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span><span class="sxs-lookup"><span data-stu-id="cd00c-157">In hello **Reply URL** textbox, type your FM:Systems **Reply URL**, type hello URL using hello following pattern: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cd00c-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="cd00c-158">This value is not real.</span></span> <span data-ttu-id="cd00c-159">Actualizar este valor con la dirección URL de respuesta real Hola.</span><span class="sxs-lookup"><span data-stu-id="cd00c-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="cd00c-160">Póngase en contacto con [equipo de soporte técnico de FM: Systems](https://fmsystems.com/ask-us/) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="cd00c-160">Contact [FM:Systems support team](https://fmsystems.com/ask-us/) tooget this value.</span></span>
 
4. <span data-ttu-id="cd00c-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="cd00c-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_certificate.png) 

5. <span data-ttu-id="cd00c-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="cd00c-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fm-systems-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cd00c-165">inicio de sesión único en tooconfigure en **FM: Systems** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de FM: Systems](https://fmsystems.com/ask-us/).</span><span class="sxs-lookup"><span data-stu-id="cd00c-165">tooconfigure single sign-on on **FM:Systems** side, you need toosend hello downloaded **Metadata XML** too[FM:Systems support team](https://fmsystems.com/ask-us/).</span></span> <span data-ttu-id="cd00c-166">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="cd00c-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span> <span data-ttu-id="cd00c-167">Cuando SSO se haya habilitado en su suscripción recibirá una notificación.</span><span class="sxs-lookup"><span data-stu-id="cd00c-167">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="cd00c-168">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="cd00c-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cd00c-169">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="cd00c-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cd00c-170">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cd00c-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cd00c-171">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd00c-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="cd00c-172">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="cd00c-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="cd00c-174">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cd00c-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd00c-175">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="cd00c-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cd00c-177">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cd00c-179">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd00c-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cd00c-181">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="cd00c-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cd00c-183">a.</span><span class="sxs-lookup"><span data-stu-id="cd00c-183">a.</span></span> <span data-ttu-id="cd00c-184">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cd00c-185">b.</span><span class="sxs-lookup"><span data-stu-id="cd00c-185">b.</span></span> <span data-ttu-id="cd00c-186">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cd00c-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cd00c-187">c.</span><span class="sxs-lookup"><span data-stu-id="cd00c-187">c.</span></span> <span data-ttu-id="cd00c-188">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cd00c-189">d.</span><span class="sxs-lookup"><span data-stu-id="cd00c-189">d.</span></span> <span data-ttu-id="cd00c-190">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-190">Click **Create**.</span></span>
 
### <a name="creating-an-fmsystems-test-user"></a><span data-ttu-id="cd00c-191">Creación de un usuario de prueba de FM: Systems</span><span class="sxs-lookup"><span data-stu-id="cd00c-191">Creating an FM:Systems test user</span></span>

1. <span data-ttu-id="cd00c-192">En una ventana del explorador web, inicie sesión en el sitio de la compañía de FM:Systems como administrador.</span><span class="sxs-lookup"><span data-stu-id="cd00c-192">In a web browser window, log into your FM:Systems company site as an administrator.</span></span>

2. <span data-ttu-id="cd00c-193">Vaya demasiado**administración del sistema \> administrar seguridad \> usuarios \> lista de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-193">Go too**System Administration \> Manage Security \> Users \> User list**.</span></span>
   
    <span data-ttu-id="cd00c-194">![Administración del sistema](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "Administración del sistema")</span><span class="sxs-lookup"><span data-stu-id="cd00c-194">![System Administration](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "System Administration")</span></span>

3. <span data-ttu-id="cd00c-195">Haga clic en **Crear nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-195">Click **Create new user**.</span></span>
   
    <span data-ttu-id="cd00c-196">![Creación de nuevos usuarios](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Creación de nuevos usuarios")</span><span class="sxs-lookup"><span data-stu-id="cd00c-196">![Create New User](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Create New User")</span></span>

4. <span data-ttu-id="cd00c-197">Hola **Create User** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="cd00c-197">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="cd00c-198">![Creación de usuarios](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Creación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="cd00c-198">![Create User](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Create User")</span></span>
   
    <span data-ttu-id="cd00c-199">a.</span><span class="sxs-lookup"><span data-stu-id="cd00c-199">a.</span></span> <span data-ttu-id="cd00c-200">Hola de tipo **nombre de usuario**, hello **contraseña**, **Confirmar contraseña**, **correo electrónico** hello y **Id. de empleado**de un Azure válida cuadros de texto relacionadas con la cuenta de Active Directory que quiera tooprovision en Hola.</span><span class="sxs-lookup"><span data-stu-id="cd00c-200">Type hello **UserName**, hello **Password**, **Confirm Password**, **E-mail** and hello **Employee ID** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="cd00c-201">b.</span><span class="sxs-lookup"><span data-stu-id="cd00c-201">b.</span></span> <span data-ttu-id="cd00c-202">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-202">Click **Next**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cd00c-203">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd00c-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cd00c-204">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooFM:Systems.</span><span class="sxs-lookup"><span data-stu-id="cd00c-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFM:Systems.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="cd00c-206">**tooassign Britta Simon tooFM:Systems, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="cd00c-206">**tooassign Britta Simon tooFM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd00c-207">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="cd00c-209">En la lista de aplicaciones de hello, seleccione **FM: Systems**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-209">In hello applications list, select **FM:Systems**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_app.png) 

3. <span data-ttu-id="cd00c-211">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="cd00c-213">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-213">Click **Add** button.</span></span> <span data-ttu-id="cd00c-214">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="cd00c-216">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd00c-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cd00c-217">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cd00c-218">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="cd00c-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cd00c-219">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="cd00c-219">Testing single sign-on</span></span>

<span data-ttu-id="cd00c-220">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="cd00c-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cd00c-221">Al hacer clic en icono de FM: Systems Hola Hola Panel de acceso, deberá obtener la aplicación de FM: Systems tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="cd00c-221">When you click hello FM:Systems tile in hello Access Panel, you should get automatically signed-on tooyour FM:Systems application.</span></span>
<span data-ttu-id="cd00c-222">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cd00c-222">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cd00c-223">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="cd00c-223">Additional resources</span></span>

* [<span data-ttu-id="cd00c-224">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd00c-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cd00c-225">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cd00c-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_203.png


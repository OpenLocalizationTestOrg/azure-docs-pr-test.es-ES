---
title: "Tutorial: Integración de Azure Active Directory con Neota Logic Studio | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Neota lógica Studio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: a479ee49618de8275132dbc2c21a8ef723d92d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="f8bbf-103">Tutorial: Integración de Azure Active Directory con Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="f8bbf-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="f8bbf-104">En este tutorial, aprenderá cómo toointegrate Neota lógica Studio con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f8bbf-104">In this tutorial, you learn how toointegrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f8bbf-105">Integración Neota lógica Studio con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f8bbf-105">Integrating Neota Logic Studio with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f8bbf-106">Puede controlar en Azure AD que tenga acceso tooNeota Studio lógica</span><span class="sxs-lookup"><span data-stu-id="f8bbf-106">You can control in Azure AD who has access tooNeota Logic Studio</span></span>
- <span data-ttu-id="f8bbf-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooNeota Studio lógica (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8bbf-107">You can enable your users tooautomatically get signed-on tooNeota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f8bbf-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f8bbf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f8bbf-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="f8bbf-110">[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="f8bbf-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8bbf-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f8bbf-111">Prerequisites</span></span>

<span data-ttu-id="f8bbf-112">integración de Azure AD con Neota lógica Studio tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f8bbf-112">tooconfigure Azure AD integration with Neota Logic Studio, you need hello following items:</span></span>

- <span data-ttu-id="f8bbf-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8bbf-113">An Azure AD subscription</span></span>
- <span data-ttu-id="f8bbf-114">Una suscripción habilitada para inicio de sesión único en Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="f8bbf-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f8bbf-115">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f8bbf-116">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f8bbf-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f8bbf-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f8bbf-118">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f8bbf-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f8bbf-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f8bbf-119">Scenario description</span></span>

<span data-ttu-id="f8bbf-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f8bbf-121">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="f8bbf-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f8bbf-122">Agregar Neota lógica Studio desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="f8bbf-122">Adding Neota Logic Studio from hello gallery</span></span>
2. <span data-ttu-id="f8bbf-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8bbf-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-hello-gallery"></a><span data-ttu-id="f8bbf-124">Agregar Neota lógica Studio desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="f8bbf-124">Adding Neota Logic Studio from hello gallery</span></span>

<span data-ttu-id="f8bbf-125">integración de hello tooconfigure de Neota lógica Studio en Azure AD, deberá tooadd Neota lógica Studio de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-125">tooconfigure hello integration of Neota Logic Studio into Azure AD, you need tooadd Neota Logic Studio from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f8bbf-126">**tooadd Neota Studio de lógica de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f8bbf-126">**tooadd Neota Logic Studio from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8bbf-127">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f8bbf-129">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f8bbf-130">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-130">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="f8bbf-132">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="f8bbf-134">En el cuadro de búsqueda de hello, escriba **Neota lógica Studio**.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-134">In hello search box, type **Neota Logic Studio**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

5. <span data-ttu-id="f8bbf-136">En el panel de resultados de hello, seleccione **Neota lógica Studio**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-136">In hello results panel, select **Neota Logic Studio**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f8bbf-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8bbf-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="f8bbf-139">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Neota Logic Studio con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f8bbf-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f8bbf-140">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Neota lógica Studio es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Neota Logic Studio is tooa user in Azure AD.</span></span> <span data-ttu-id="f8bbf-141">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Neota lógica Studio debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-141">In other words, a link relationship between an Azure AD user and hello related user in Neota Logic Studio needs toobe established.</span></span>

<span data-ttu-id="f8bbf-142">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Neota lógica Studio.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="f8bbf-143">tooconfigure y prueba de inicio de sesión único en Azure AD con Neota lógica Studio, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f8bbf-143">tooconfigure and test Azure AD single sign-on with Neota Logic Studio, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f8bbf-144">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f8bbf-145">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f8bbf-146">**[Crear un usuario de prueba Neota lógica Studio](#creating-a-neota-logic-studio-test-user)**  -toohave un equivalente de Britta Simon en Neota lógica Studio que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - toohave a counterpart of Britta Simon in Neota Logic Studio that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f8bbf-147">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f8bbf-148">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f8bbf-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8bbf-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f8bbf-150">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Neota lógica Studio.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="f8bbf-151">**tooconfigure inicio de sesión único en Azure AD con Neota lógica Studio, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f8bbf-151">**tooconfigure Azure AD single sign-on with Neota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8bbf-152">En el portal de Azure, en Hola Hola **Neota lógica Studio** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-152">In hello Azure portal, on hello **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="f8bbf-154">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

3. <span data-ttu-id="f8bbf-156">En hello **Neota lógica Studio dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="f8bbf-156">On hello **Neota Logic Studio Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="f8bbf-158">a.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-158">a.</span></span> <span data-ttu-id="f8bbf-159">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<sub domain>.neotalogic.com/a/<sub application>`</span><span class="sxs-lookup"><span data-stu-id="f8bbf-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="f8bbf-160">b.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-160">b.</span></span> <span data-ttu-id="f8bbf-161">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="f8bbf-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f8bbf-162">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-162">These values are not hello real.</span></span> <span data-ttu-id="f8bbf-163">Actualizar estos valores con hello real & identificador de dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-163">Update these values with hello actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="f8bbf-164">Aquí le sugerimos toouse Hola único valor de cadena en hello identificador.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-164">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="f8bbf-165">Póngase en contacto con [equipo de soporte técnico de Neota lógica Studio cliente](https://www.neotalogic.com/contact-us/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="f8bbf-166">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

5. <span data-ttu-id="f8bbf-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f8bbf-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f8bbf-170">tooget SSO configurado para la aplicación, póngase en contacto con [compatibilidad Neota lógica Studio](https://www.neotalogic.com/contact-us/) de equipo y proporcióneles con descargado **Metadata XML** archivo.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-170">tooget SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="f8bbf-171">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="f8bbf-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f8bbf-172">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f8bbf-173">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f8bbf-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f8bbf-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8bbf-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="f8bbf-175">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="f8bbf-177">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f8bbf-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8bbf-178">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f8bbf-180">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f8bbf-182">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f8bbf-184">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="f8bbf-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f8bbf-186">a.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-186">a.</span></span> <span data-ttu-id="f8bbf-187">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f8bbf-188">b.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-188">b.</span></span> <span data-ttu-id="f8bbf-189">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f8bbf-190">c.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-190">c.</span></span> <span data-ttu-id="f8bbf-191">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f8bbf-192">d.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-192">d.</span></span> <span data-ttu-id="f8bbf-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="f8bbf-194">Crear un usuario de prueba de Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="f8bbf-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="f8bbf-195">En esta sección, creará un usuario llamado Britta Simon en Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="f8bbf-196">trabajar con [equipo de soporte técnico de Neota lógica Studio cliente](https://www.neotalogic.com/contact-us/) para agregar usuarios de hello en plataforma de hello Neota lógica Studio.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add hello users in hello Neota Logic Studio platform.</span></span> <span data-ttu-id="f8bbf-197">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f8bbf-198">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8bbf-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f8bbf-199">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooNeota Studio lógica.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNeota Logic Studio.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="f8bbf-201">**tooassign Britta Simon tooNeota Studio lógica, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="f8bbf-201">**tooassign Britta Simon tooNeota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8bbf-202">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f8bbf-204">En la lista de aplicaciones de hello, seleccione **Neota lógica Studio**.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-204">In hello applications list, select **Neota Logic Studio**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

3. <span data-ttu-id="f8bbf-206">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="f8bbf-208">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-208">Click **Add** button.</span></span> <span data-ttu-id="f8bbf-209">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="f8bbf-211">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f8bbf-212">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f8bbf-213">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f8bbf-214">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="f8bbf-214">Testing single sign-on</span></span>

<span data-ttu-id="f8bbf-215">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f8bbf-216">Haga clic en el icono de hello Neota lógica Studio Hola Panel de acceso, será redirigido tooOrganization página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-216">Click hello Neota Logic Studio tile in hello Access Panel, you will be redirected tooOrganization sign-on page.</span></span> <span data-ttu-id="f8bbf-217">Después de iniciar sesión correctamente, podrás ha iniciado sesión tooyour aplicación Neota lógica Studio.</span><span class="sxs-lookup"><span data-stu-id="f8bbf-217">After successful login, you will be signed-on tooyour Neota Logic Studio application.</span></span> <span data-ttu-id="f8bbf-218">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="f8bbf-218">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

<span data-ttu-id="f8bbf-219">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="f8bbf-219">For more information about hello Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f8bbf-220">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f8bbf-220">Additional resources</span></span>

* [<span data-ttu-id="f8bbf-221">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8bbf-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f8bbf-222">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f8bbf-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_203.png


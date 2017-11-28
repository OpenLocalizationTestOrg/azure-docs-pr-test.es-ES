---
title: "Tutorial: integración de Azure Active Directory con HappyFox | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y HappyFox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 1190652d7d1144c7eddea339cb3f9175912407fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="43d6f-103">Tutorial: integración de Azure Active Directory con HappyFox</span><span class="sxs-lookup"><span data-stu-id="43d6f-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="43d6f-104">En este tutorial, aprenderá cómo toointegrate HappyFox con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="43d6f-104">In this tutorial, you learn how toointegrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="43d6f-105">Integración HappyFox con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="43d6f-105">Integrating HappyFox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="43d6f-106">Puede controlar en Azure AD que tenga acceso tooHappyFox</span><span class="sxs-lookup"><span data-stu-id="43d6f-106">You can control in Azure AD who has access tooHappyFox</span></span>
- <span data-ttu-id="43d6f-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooHappyFox (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="43d6f-107">You can enable your users tooautomatically get signed-on tooHappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="43d6f-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="43d6f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="43d6f-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="43d6f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43d6f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="43d6f-110">Prerequisites</span></span>

<span data-ttu-id="43d6f-111">integración de Azure AD con HappyFox tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="43d6f-111">tooconfigure Azure AD integration with HappyFox, you need hello following items:</span></span>

- <span data-ttu-id="43d6f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="43d6f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="43d6f-113">Una suscripción habilitada para inicio de sesión único en HappyFox</span><span class="sxs-lookup"><span data-stu-id="43d6f-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="43d6f-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="43d6f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="43d6f-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="43d6f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="43d6f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="43d6f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="43d6f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="43d6f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="43d6f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="43d6f-118">Scenario description</span></span>
<span data-ttu-id="43d6f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="43d6f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="43d6f-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="43d6f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="43d6f-121">Agregar HappyFox desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="43d6f-121">Adding HappyFox from hello gallery</span></span>
2. <span data-ttu-id="43d6f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="43d6f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-hello-gallery"></a><span data-ttu-id="43d6f-123">Agregar HappyFox desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="43d6f-123">Adding HappyFox from hello gallery</span></span>
<span data-ttu-id="43d6f-124">integración de hello tooconfigure de HappyFox en Azure AD, deberá tooadd HappyFox de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="43d6f-124">tooconfigure hello integration of HappyFox into Azure AD, you need tooadd HappyFox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="43d6f-125">**tooadd HappyFox de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="43d6f-125">**tooadd HappyFox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="43d6f-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="43d6f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="43d6f-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="43d6f-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="43d6f-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="43d6f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="43d6f-133">En el cuadro de búsqueda de hello, escriba **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-133">In hello search box, type **HappyFox**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_search.png)

5. <span data-ttu-id="43d6f-135">En el panel de resultados de hello, seleccione **HappyFox**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="43d6f-135">In hello results panel, select **HappyFox**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="43d6f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="43d6f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="43d6f-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con HappyFox con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43d6f-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="43d6f-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en HappyFox es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43d6f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HappyFox is tooa user in Azure AD.</span></span> <span data-ttu-id="43d6f-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en HappyFox debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="43d6f-140">In other words, a link relationship between an Azure AD user and hello related user in HappyFox needs toobe established.</span></span>

<span data-ttu-id="43d6f-141">En HappyFox, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="43d6f-141">In HappyFox, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="43d6f-142">tooconfigure y prueba de inicio de sesión único en Azure AD con HappyFox, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="43d6f-142">tooconfigure and test Azure AD single sign-on with HappyFox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="43d6f-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="43d6f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="43d6f-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43d6f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="43d6f-145">**[Crear un usuario de prueba HappyFox](#creating-a-happyfox-test-user)**  -toohave un equivalente de Britta Simon en HappyFox que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="43d6f-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - toohave a counterpart of Britta Simon in HappyFox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="43d6f-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="43d6f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="43d6f-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="43d6f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="43d6f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="43d6f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="43d6f-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación HappyFox.</span><span class="sxs-lookup"><span data-stu-id="43d6f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="43d6f-150">**inicio de sesión único en Azure AD tooconfigure con HappyFox, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="43d6f-150">**tooconfigure Azure AD single sign-on with HappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="43d6f-151">En el portal de Azure, en Hola Hola **HappyFox** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-151">In hello Azure portal, on hello **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="43d6f-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="43d6f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_samlbase.png)

3. <span data-ttu-id="43d6f-155">En hello **HappyFox dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="43d6f-155">On hello **HappyFox Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="43d6f-157">a.</span><span class="sxs-lookup"><span data-stu-id="43d6f-157">a.</span></span> <span data-ttu-id="43d6f-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.happyfox.com/`</span><span class="sxs-lookup"><span data-stu-id="43d6f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="43d6f-159">b.</span><span class="sxs-lookup"><span data-stu-id="43d6f-159">b.</span></span> <span data-ttu-id="43d6f-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="43d6f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="43d6f-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="43d6f-161">These values are not real.</span></span> <span data-ttu-id="43d6f-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="43d6f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="43d6f-163">Póngase en contacto con [equipo de soporte técnico de cliente de HappyFox](https://support.happyfox.com/home) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="43d6f-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) tooget these values.</span></span> 
 
4. <span data-ttu-id="43d6f-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="43d6f-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_certificate.png) 

5. <span data-ttu-id="43d6f-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="43d6f-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="43d6f-168">En hello **HappyFox configuración** sección, haga clic en **configurar HappyFox** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="43d6f-168">On hello **HappyFox Configuration** section, click **Configure HappyFox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="43d6f-169">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_configure.png) 

7. <span data-ttu-id="43d6f-171">Inicie sesión en el portal personal de tooyour HappyFox y navegue demasiado**administrar**, haga clic en **integraciones** ficha.</span><span class="sxs-lookup"><span data-stu-id="43d6f-171">Sign on tooyour HappyFox staff portal and navigate too**Manage**, Click on **Integrations** tab.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/header.png) 

8. <span data-ttu-id="43d6f-173">En la ficha de integraciones de hello, haga clic en **configurar** en **SAML integración** tooopen Hola inicio de sesión único en la configuración.</span><span class="sxs-lookup"><span data-stu-id="43d6f-173">In hello Integrations tab, Click **Configure** under **SAML Integration** tooopen hello Single Sign On Settings.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/configure.png) 

9. <span data-ttu-id="43d6f-175">Dentro de la sección de configuración de SAML, pegue hello **SAML Single Sign-On dirección URL del servicio** que ha copiado desde el portal de Azure en **dirección URL de destino de SSO** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="43d6f-175">Inside SAML configuration section, paste hello **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/targeturl.png)

10. <span data-ttu-id="43d6f-177">Abra el certificado Hola descargado desde el portal de Azure en el Bloc de notas y pegue su contenido en **IdP firma** sección.</span><span class="sxs-lookup"><span data-stu-id="43d6f-177">Open hello certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/cert.png)

11. <span data-ttu-id="43d6f-179">Haga clic en el botón **Guardar configuración**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-179">Click **Save Settings** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="43d6f-181">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="43d6f-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="43d6f-182">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="43d6f-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="43d6f-183">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="43d6f-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="43d6f-184">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="43d6f-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="43d6f-185">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="43d6f-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="43d6f-187">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="43d6f-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="43d6f-188">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="43d6f-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="43d6f-190">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="43d6f-192">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="43d6f-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="43d6f-194">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="43d6f-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="43d6f-196">a.</span><span class="sxs-lookup"><span data-stu-id="43d6f-196">a.</span></span> <span data-ttu-id="43d6f-197">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="43d6f-198">b.</span><span class="sxs-lookup"><span data-stu-id="43d6f-198">b.</span></span> <span data-ttu-id="43d6f-199">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="43d6f-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="43d6f-200">c.</span><span class="sxs-lookup"><span data-stu-id="43d6f-200">c.</span></span> <span data-ttu-id="43d6f-201">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="43d6f-202">d.</span><span class="sxs-lookup"><span data-stu-id="43d6f-202">d.</span></span> <span data-ttu-id="43d6f-203">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="43d6f-204">Creación de un usuario de prueba de HappyFox</span><span class="sxs-lookup"><span data-stu-id="43d6f-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="43d6f-205">Aplicación admite sólo en el aprovisionamiento de usuarios de tiempo y después de autenticar usuarios se crean automáticamente en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="43d6f-205">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="43d6f-206">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="43d6f-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="43d6f-207">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooHappyFox.</span><span class="sxs-lookup"><span data-stu-id="43d6f-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHappyFox.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="43d6f-209">**tooassign Britta Simon tooHappyFox, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="43d6f-209">**tooassign Britta Simon tooHappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="43d6f-210">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="43d6f-212">En la lista de aplicaciones de hello, seleccione **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-212">In hello applications list, select **HappyFox**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_app.png) 

3. <span data-ttu-id="43d6f-214">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="43d6f-216">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-216">Click **Add** button.</span></span> <span data-ttu-id="43d6f-217">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="43d6f-219">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="43d6f-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="43d6f-220">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="43d6f-221">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="43d6f-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="43d6f-222">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="43d6f-222">Testing single sign-on</span></span>

<span data-ttu-id="43d6f-223">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="43d6f-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="43d6f-224">Al hacer clic en icono de HappyFox Hola Hola Panel de acceso, deberá obtener la página de inicio de sesión de la aplicación HappyFox.</span><span class="sxs-lookup"><span data-stu-id="43d6f-224">When you click hello HappyFox tile in hello Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="43d6f-225">Debería ver Hola **'SAML'** botón en la página de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="43d6f-225">You should see hello **‘SAML’** button on hello sign-in page.</span></span>

    ![Complemento](./media/active-directory-saas-happyfox-tutorial/saml.png) 

2. <span data-ttu-id="43d6f-227">Haga clic en hello **'SAML'** toolog de botón en tooHappyFox con su cuenta de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43d6f-227">Click hello **‘SAML’** button toolog in tooHappyFox using your Azure AD account.</span></span>

<span data-ttu-id="43d6f-228">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="43d6f-228">For more information about hello Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="43d6f-229">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="43d6f-229">Additional resources</span></span>

* [<span data-ttu-id="43d6f-230">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="43d6f-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="43d6f-231">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="43d6f-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_203.png


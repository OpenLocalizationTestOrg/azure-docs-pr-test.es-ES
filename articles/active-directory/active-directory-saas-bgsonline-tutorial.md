---
title: "Tutorial: Integración de Azure Active Directory con BGS Online | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y BG en línea."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4fd6b29b-1b46-4fd1-9f5e-16b1c9d892cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: b728606ded7687d424a8175d0602b6b00f398497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bgs-online"></a><span data-ttu-id="63c63-103">Tutorial: Integración de Azure Active Directory con BGS Online</span><span class="sxs-lookup"><span data-stu-id="63c63-103">Tutorial: Azure Active Directory integration with BGS Online</span></span>

<span data-ttu-id="63c63-104">En este tutorial, aprenderá cómo toointegrate BG Online con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="63c63-104">In this tutorial, you learn how toointegrate BGS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="63c63-105">Integración BG Online con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="63c63-105">Integrating BGS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="63c63-106">Puede controlar en Azure AD que tenga acceso tooBGS en línea</span><span class="sxs-lookup"><span data-stu-id="63c63-106">You can control in Azure AD who has access tooBGS Online</span></span>
- <span data-ttu-id="63c63-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooBGS en línea (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63c63-107">You can enable your users tooautomatically get signed-on tooBGS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="63c63-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="63c63-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="63c63-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="63c63-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63c63-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="63c63-110">Prerequisites</span></span>

<span data-ttu-id="63c63-111">tooconfigure integración de Azure AD con BG en línea, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="63c63-111">tooconfigure Azure AD integration with BGS Online, you need hello following items:</span></span>

- <span data-ttu-id="63c63-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63c63-112">An Azure AD subscription</span></span>
- <span data-ttu-id="63c63-113">Una suscripción habilitada para el inicio de sesión único en BGS Online</span><span class="sxs-lookup"><span data-stu-id="63c63-113">A BGS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="63c63-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="63c63-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="63c63-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="63c63-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="63c63-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="63c63-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="63c63-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63c63-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="63c63-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="63c63-118">Scenario description</span></span>
<span data-ttu-id="63c63-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="63c63-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="63c63-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="63c63-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="63c63-121">Agregar BG en línea desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="63c63-121">Adding BGS Online from hello gallery</span></span>
2. <span data-ttu-id="63c63-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63c63-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bgs-online-from-hello-gallery"></a><span data-ttu-id="63c63-123">Agregar BG en línea desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="63c63-123">Adding BGS Online from hello gallery</span></span>
<span data-ttu-id="63c63-124">integración de hello tooconfigure de BG en línea en Azure AD, deberá tooadd BG en pantalla de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="63c63-124">tooconfigure hello integration of BGS Online into Azure AD, you need tooadd BGS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="63c63-125">**tooadd BG en línea desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="63c63-125">**tooadd BGS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="63c63-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="63c63-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="63c63-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="63c63-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="63c63-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="63c63-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="63c63-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="63c63-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="63c63-133">En el cuadro de búsqueda de hello, escriba **BG en línea**.</span><span class="sxs-lookup"><span data-stu-id="63c63-133">In hello search box, type **BGS Online**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_search.png)

5. <span data-ttu-id="63c63-135">En el panel de resultados de hello, seleccione **BG en línea**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="63c63-135">In hello results panel, select **BGS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="63c63-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63c63-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="63c63-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con BGS Online con un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="63c63-138">In this section, you configure and test Azure AD single sign-on with BGS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="63c63-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario homólogo Hola BG en línea es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63c63-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BGS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="63c63-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en BG en línea debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="63c63-140">In other words, a link relationship between an Azure AD user and hello related user in BGS Online needs toobe established.</span></span>

<span data-ttu-id="63c63-141">En BG Online, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="63c63-141">In BGS Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="63c63-142">tooconfigure y prueba de inicio de sesión único en Azure AD con BG en línea, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="63c63-142">tooconfigure and test Azure AD single sign-on with BGS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="63c63-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="63c63-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="63c63-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63c63-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="63c63-145">**[Crear un usuario de prueba en pantalla de BG](#creating-a-bgs-online-test-user)**  -toohave un equivalente de Britta Simon en BG Online que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="63c63-145">**[Creating a BGS Online test user](#creating-a-bgs-online-test-user)** - toohave a counterpart of Britta Simon in BGS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="63c63-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="63c63-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="63c63-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="63c63-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="63c63-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63c63-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="63c63-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación BG en línea.</span><span class="sxs-lookup"><span data-stu-id="63c63-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BGS Online application.</span></span>

<span data-ttu-id="63c63-150">**inicio de sesión único en tooconfigure Azure AD con BG Online, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="63c63-150">**tooconfigure Azure AD single sign-on with BGS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="63c63-151">En el portal de Azure, en Hola Hola **BG en línea** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="63c63-151">In hello Azure portal, on hello **BGS Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="63c63-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="63c63-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_samlbase.png)

3. <span data-ttu-id="63c63-155">En hello **BG en pantalla de dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="63c63-155">On hello **BGS Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_url.png)

    <span data-ttu-id="63c63-157">a.</span><span class="sxs-lookup"><span data-stu-id="63c63-157">a.</span></span> <span data-ttu-id="63c63-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="63c63-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="63c63-159">En el entorno de producción, use este patrón`https://<company name>.millwardbrown.report`</span><span class="sxs-lookup"><span data-stu-id="63c63-159">For production environment, use this pattern `https://<company name>.millwardbrown.report`</span></span> 

    <span data-ttu-id="63c63-160">En el entorno de prueba, use este patrón`https://millwardbrown.marketingtracker.nl/mt5/`</span><span class="sxs-lookup"><span data-stu-id="63c63-160">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/`</span></span>

    <span data-ttu-id="63c63-161">b.</span><span class="sxs-lookup"><span data-stu-id="63c63-161">b.</span></span> <span data-ttu-id="63c63-162">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="63c63-162">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    
    <span data-ttu-id="63c63-163">En el entorno de producción, use este patrón`https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="63c63-163">For production environment, use this pattern `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span></span> 
      
    <span data-ttu-id="63c63-164">En el entorno de prueba, use este patrón`https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="63c63-164">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="63c63-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="63c63-165">These values are not real.</span></span> <span data-ttu-id="63c63-166">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="63c63-166">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="63c63-167">Póngase en contacto con [equipo de soporte técnico en línea de BG](mailTo:bgsdashboardteam@millwardbrown.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="63c63-167">Contact [BGS Online support team](mailTo:bgsdashboardteam@millwardbrown.com) tooget these values.</span></span>
 

4. <span data-ttu-id="63c63-168">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="63c63-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_certificate.png) 

5. <span data-ttu-id="63c63-170">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="63c63-170">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bgsonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="63c63-172">En hello **configuración en línea de BG** sección, haga clic en **configurar BG en línea** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="63c63-172">On hello **BGS Online Configuration** section, click **Configure BGS Online** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="63c63-173">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="63c63-173">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_configure.png) 

7. <span data-ttu-id="63c63-175">tooconfigure inicio de sesión único en **BG en línea** lado, necesita hello toosend descargado **Metadata XML** y **SAML Single Sign-On dirección URL del servicio** demasiado[BG Equipo de soporte técnico en línea](mailto:bgsdashboardteam@millwardbrown.com).</span><span class="sxs-lookup"><span data-stu-id="63c63-175">tooconfigure single sign-on on **BGS Online** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com).</span></span> 


> [!TIP]
> <span data-ttu-id="63c63-176">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="63c63-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="63c63-177">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="63c63-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="63c63-178">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="63c63-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="63c63-179">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="63c63-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="63c63-180">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="63c63-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="63c63-182">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="63c63-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="63c63-183">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="63c63-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="63c63-185">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="63c63-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="63c63-187">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="63c63-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="63c63-189">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="63c63-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="63c63-191">a.</span><span class="sxs-lookup"><span data-stu-id="63c63-191">a.</span></span> <span data-ttu-id="63c63-192">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="63c63-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="63c63-193">b.</span><span class="sxs-lookup"><span data-stu-id="63c63-193">b.</span></span> <span data-ttu-id="63c63-194">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="63c63-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="63c63-195">c.</span><span class="sxs-lookup"><span data-stu-id="63c63-195">c.</span></span> <span data-ttu-id="63c63-196">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="63c63-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="63c63-197">d.</span><span class="sxs-lookup"><span data-stu-id="63c63-197">d.</span></span> <span data-ttu-id="63c63-198">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="63c63-198">Click **Create**.</span></span>
 
### <a name="creating-a-bgs-online-test-user"></a><span data-ttu-id="63c63-199">Creación de un usuario de prueba de BGS Online</span><span class="sxs-lookup"><span data-stu-id="63c63-199">Creating a BGS Online test user</span></span>

<span data-ttu-id="63c63-200">En esta sección, creará un usuario llamado Britta Simon en BGS Online.</span><span class="sxs-lookup"><span data-stu-id="63c63-200">In this section, you create a user called Britta Simon in BGS Online.</span></span> <span data-ttu-id="63c63-201">Trabajar con [equipo de soporte técnico en línea de BG](mailto:bgsdashboardteam@millwardbrown.com) a los usuarios de tooadd hello en la plataforma de Hola BG en línea.</span><span class="sxs-lookup"><span data-stu-id="63c63-201">Work with [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com) tooadd hello users in hello BGS Online platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="63c63-202">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="63c63-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="63c63-203">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooBGS en línea.</span><span class="sxs-lookup"><span data-stu-id="63c63-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBGS Online.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="63c63-205">**tooassign Britta Simon tooBGS en línea, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="63c63-205">**tooassign Britta Simon tooBGS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="63c63-206">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="63c63-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="63c63-208">En la lista de aplicaciones de hello, seleccione **BG en línea**.</span><span class="sxs-lookup"><span data-stu-id="63c63-208">In hello applications list, select **BGS Online**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_app.png) 

3. <span data-ttu-id="63c63-210">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="63c63-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="63c63-212">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="63c63-212">Click **Add** button.</span></span> <span data-ttu-id="63c63-213">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="63c63-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="63c63-215">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="63c63-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="63c63-216">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="63c63-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="63c63-217">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="63c63-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="63c63-218">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="63c63-218">Testing single sign-on</span></span>

<span data-ttu-id="63c63-219">En esta sección, probará la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="63c63-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="63c63-220">Al hacer clic en icono BG Online Hola Hola Panel de acceso, deberá obtener aplicación BG Online tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="63c63-220">When you click hello BGS Online tile in hello Access Panel, you should get automatically signed-on tooyour BGS Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="63c63-221">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="63c63-221">Additional resources</span></span>

* [<span data-ttu-id="63c63-222">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63c63-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="63c63-223">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="63c63-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_203.png


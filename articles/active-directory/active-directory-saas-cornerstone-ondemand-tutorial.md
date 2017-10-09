---
title: "Tutorial: Integración de Azure Active Directory con Cornerstone OnDemand | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Cornerstone OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f57c5fef-49b0-4591-91ef-fc0de6d654ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 85fd6eb4e93010d8f7477df236403e205e9f2d83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cornerstone-ondemand"></a><span data-ttu-id="aec61-103">Tutorial: Integración de Azure Active Directory con Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="aec61-103">Tutorial: Azure Active Directory integration with Cornerstone OnDemand</span></span>

<span data-ttu-id="aec61-104">En este tutorial, aprenderá cómo toointegrate Cornerstone OnDemand con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aec61-104">In this tutorial, you learn how toointegrate Cornerstone OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aec61-105">Integración Cornerstone OnDemand con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="aec61-105">Integrating Cornerstone OnDemand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="aec61-106">Puede controlar en Azure AD que tenga acceso tooCornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="aec61-106">You can control in Azure AD who has access tooCornerstone OnDemand</span></span>
- <span data-ttu-id="aec61-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooCornerstone OnDemand (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aec61-107">You can enable your users tooautomatically get signed-on tooCornerstone OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aec61-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="aec61-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="aec61-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aec61-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aec61-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="aec61-110">Prerequisites</span></span>

<span data-ttu-id="aec61-111">tooconfigure integración de Azure AD con Cornerstone OnDemand, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="aec61-111">tooconfigure Azure AD integration with Cornerstone OnDemand, you need hello following items:</span></span>

- <span data-ttu-id="aec61-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aec61-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aec61-113">Una suscripción habilitada para el inicio de sesión único en Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="aec61-113">A Cornerstone OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aec61-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="aec61-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aec61-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="aec61-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aec61-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="aec61-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aec61-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aec61-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aec61-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="aec61-118">Scenario description</span></span>
<span data-ttu-id="aec61-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="aec61-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aec61-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="aec61-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aec61-121">Agregar Cornerstone OnDemand desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="aec61-121">Adding Cornerstone OnDemand from hello gallery</span></span>
2. <span data-ttu-id="aec61-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aec61-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cornerstone-ondemand-from-hello-gallery"></a><span data-ttu-id="aec61-123">Agregar Cornerstone OnDemand desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="aec61-123">Adding Cornerstone OnDemand from hello gallery</span></span>
<span data-ttu-id="aec61-124">integración de hello tooconfigure de Cornerstone OnDemand en Azure AD, deberá tooadd Cornerstone OnDemand de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="aec61-124">tooconfigure hello integration of Cornerstone OnDemand into Azure AD, you need tooadd Cornerstone OnDemand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="aec61-125">**tooadd Cornerstone OnDemand de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aec61-125">**tooadd Cornerstone OnDemand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="aec61-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="aec61-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aec61-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="aec61-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="aec61-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="aec61-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="aec61-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aec61-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="aec61-133">En el cuadro de búsqueda de hello, escriba **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="aec61-133">In hello search box, type **Cornerstone OnDemand**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_search.png)

5. <span data-ttu-id="aec61-135">En el panel de resultados de hello, seleccione **Cornerstone OnDemand**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="aec61-135">In hello results panel, select **Cornerstone OnDemand**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aec61-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aec61-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aec61-138">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con Cornerstone OnDemand con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="aec61-138">In this section, you configure and test Azure AD single sign-on with Cornerstone OnDemand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="aec61-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Cornerstone OnDemand es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aec61-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cornerstone OnDemand is tooa user in Azure AD.</span></span> <span data-ttu-id="aec61-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Cornerstone OnDemand debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="aec61-140">In other words, a link relationship between an Azure AD user and hello related user in Cornerstone OnDemand needs toobe established.</span></span>

<span data-ttu-id="aec61-141">En Cornerstone OnDemand, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aec61-141">In Cornerstone OnDemand, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="aec61-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Cornerstone OnDemand, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="aec61-142">tooconfigure and test Azure AD single sign-on with Cornerstone OnDemand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="aec61-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="aec61-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="aec61-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aec61-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aec61-145">**[Crear un usuario de prueba de Cornerstone OnDemand](#creating-a-cornerstone-ondemand-test-user)**  -toohave un equivalente de Britta Simon en Cornerstone OnDemand que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="aec61-145">**[Creating a Cornerstone OnDemand test user](#creating-a-cornerstone-ondemand-test-user)** - toohave a counterpart of Britta Simon in Cornerstone OnDemand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="aec61-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="aec61-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aec61-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="aec61-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aec61-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aec61-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aec61-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="aec61-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cornerstone OnDemand application.</span></span>

<span data-ttu-id="aec61-150">**inicio de sesión único en tooconfigure Azure AD con Cornerstone OnDemand, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aec61-150">**tooconfigure Azure AD single sign-on with Cornerstone OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="aec61-151">En el portal de Azure, en Hola Hola **Cornerstone OnDemand** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="aec61-151">In hello Azure portal, on hello **Cornerstone OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="aec61-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="aec61-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_samlbase.png)

3. <span data-ttu-id="aec61-155">En hello **Cornerstone OnDemand dominio y las direcciones URL** sección, lleve a cabo Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="aec61-155">On hello **Cornerstone OnDemand Domain and URLs** section, perform hello following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_url.png)

    <span data-ttu-id="aec61-157">a.</span><span class="sxs-lookup"><span data-stu-id="aec61-157">a.</span></span> <span data-ttu-id="aec61-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="aec61-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.csod.com`</span></span>

    <span data-ttu-id="aec61-159">b.</span><span class="sxs-lookup"><span data-stu-id="aec61-159">b.</span></span> <span data-ttu-id="aec61-160">En **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="aec61-160">In **Identifier** textbox, type a URL using hello following pattern: `https://<company>.csod.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="aec61-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="aec61-161">These values are not real.</span></span> <span data-ttu-id="aec61-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="aec61-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="aec61-163">Póngase en contacto con [equipo de soporte técnico de Cornerstone OnDemand cliente](mailTo:moreinfo@csod.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="aec61-163">Contact [Cornerstone OnDemand Client support team](mailTo:moreinfo@csod.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="aec61-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="aec61-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_certificate.png) 

5. <span data-ttu-id="aec61-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="aec61-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="aec61-168">En hello **Cornerstone OnDemand configuración** sección, haga clic en **configurar Cornerstone OnDemand** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="aec61-168">On hello **Cornerstone OnDemand Configuration** section, click **Configure Cornerstone OnDemand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="aec61-169">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="aec61-169">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_configure.png) 

7. <span data-ttu-id="aec61-171">tooconfigure inicio de sesión único en **Cornerstone OnDemand** lado, necesita hello toosend descargado **certificado**, **dirección URL de cierre de sesión** y **único de SAML Dirección URL del servicio Inicio de sesión** demasiado[equipo de soporte técnico de Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="aec61-171">tooconfigure single sign-on on **Cornerstone OnDemand** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL** and **SAML Single Sign-On Service URL**  too[Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span> <span data-ttu-id="aec61-172">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="aec61-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="aec61-173">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="aec61-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="aec61-174">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="aec61-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="aec61-175">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aec61-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aec61-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aec61-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="aec61-177">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="aec61-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="aec61-179">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aec61-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="aec61-180">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="aec61-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aec61-182">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="aec61-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aec61-184">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aec61-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aec61-186">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="aec61-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aec61-188">a.</span><span class="sxs-lookup"><span data-stu-id="aec61-188">a.</span></span> <span data-ttu-id="aec61-189">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aec61-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aec61-190">b.</span><span class="sxs-lookup"><span data-stu-id="aec61-190">b.</span></span> <span data-ttu-id="aec61-191">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="aec61-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aec61-192">c.</span><span class="sxs-lookup"><span data-stu-id="aec61-192">c.</span></span> <span data-ttu-id="aec61-193">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="aec61-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="aec61-194">d.</span><span class="sxs-lookup"><span data-stu-id="aec61-194">d.</span></span> <span data-ttu-id="aec61-195">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="aec61-195">Click **Create**.</span></span>
 
### <a name="creating-a-cornerstone-ondemand-test-user"></a><span data-ttu-id="aec61-196">Creación de un usuario de prueba de Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="aec61-196">Creating a Cornerstone OnDemand test user</span></span>

<span data-ttu-id="aec61-197">En orden tooenable toolog de los usuarios de Azure AD en Cornerstone OnDemand, les deben aprovisionar en Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="aec61-197">In order tooenable Azure AD users toolog into Cornerstone OnDemand, they must be provisioned into Cornerstone OnDemand.</span></span> <span data-ttu-id="aec61-198">En caso de hello de Cornerstone OnDemand, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="aec61-198">In hello case of Cornerstone OnDemand, provisioning is a manual task.</span></span>

<span data-ttu-id="aec61-199">tooconfigure aprovisionamiento de usuario, información de envío hello (p. ej.: nombre, correo electrónico) acerca del usuario de hello Azure AD desea tooprovision toohello [equipo de soporte técnico de Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="aec61-199">tooconfigure user provisioning, send hello information (e.g.: Name, Email) about hello Azure AD user you want tooprovision toohello [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span>

>[!NOTE]
><span data-ttu-id="aec61-200">Puede usar cualquier otra Cornerstone OnDemand usuario cuenta herramienta de creación o las API proporcionadas por Cornerstone OnDemand tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="aec61-200">You can use any other Cornerstone OnDemand user account creation tools or APIs provided by Cornerstone OnDemand tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="aec61-201">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="aec61-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="aec61-202">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCornerstone a petición.</span><span class="sxs-lookup"><span data-stu-id="aec61-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCornerstone OnDemand.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="aec61-204">**tooassign Britta Simon tooCornerstone OnDemand, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aec61-204">**tooassign Britta Simon tooCornerstone OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="aec61-205">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="aec61-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="aec61-207">En la lista de aplicaciones de hello, seleccione **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="aec61-207">In hello applications list, select **Cornerstone OnDemand**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_app.png) 

3. <span data-ttu-id="aec61-209">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="aec61-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="aec61-211">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="aec61-211">Click **Add** button.</span></span> <span data-ttu-id="aec61-212">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="aec61-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="aec61-214">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="aec61-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="aec61-215">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="aec61-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aec61-216">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="aec61-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aec61-217">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="aec61-217">Testing single sign-on</span></span>

<span data-ttu-id="aec61-218">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="aec61-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="aec61-219">Al hacer clic en icono de Cornerstone OnDemand Hola Hola Panel de acceso, deberá obtener aplicaciones de Cornerstone OnDemand tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="aec61-219">When you click hello Cornerstone OnDemand tile in hello Access Panel, you should get automatically signed-on tooyour Cornerstone OnDemand application.</span></span>
<span data-ttu-id="aec61-220">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="aec61-220">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="aec61-221">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="aec61-221">Additional resources</span></span>

* [<span data-ttu-id="aec61-222">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aec61-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aec61-223">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aec61-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_203.png


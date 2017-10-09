---
title: "Tutorial: Integración de Azure Active Directory con Birst Agile Business Analytics | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y análisis de negocios Agile Birst."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 677183b1-5348-4302-88cc-5c8ab63a3c6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: f007edcec0fb8ece215ab69f7ec7ca59ca34bddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-birst-agile-business-analytics"></a><span data-ttu-id="7ad4a-103">Tutorial: Integración de Azure Active Directory con Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="7ad4a-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span></span>

<span data-ttu-id="7ad4a-104">En este tutorial, aprenderá cómo toointegrate Birst Agile análisis de negocios con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7ad4a-104">In this tutorial, you learn how toointegrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ad4a-105">Integración de análisis de negocios Agile Birst con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7ad4a-105">Integrating Birst Agile Business Analytics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7ad4a-106">Puede controlar en Azure AD que tenga acceso tooBirst Agile análisis de negocios</span><span class="sxs-lookup"><span data-stu-id="7ad4a-106">You can control in Azure AD who has access tooBirst Agile Business Analytics</span></span>
- <span data-ttu-id="7ad4a-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooBirst Agile análisis de negocios (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ad4a-107">You can enable your users tooautomatically get signed-on tooBirst Agile Business Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7ad4a-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7ad4a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7ad4a-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7ad4a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ad4a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7ad4a-110">Prerequisites</span></span>

<span data-ttu-id="7ad4a-111">integración de Azure AD con análisis de negocios Agile Birst tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7ad4a-111">tooconfigure Azure AD integration with Birst Agile Business Analytics, you need hello following items:</span></span>

- <span data-ttu-id="7ad4a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ad4a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ad4a-113">Una suscripción habilitada al inicio de sesión único de Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="7ad4a-113">A Birst Agile Business Analytics single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ad4a-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ad4a-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="7ad4a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ad4a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ad4a-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ad4a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ad4a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="7ad4a-118">Scenario description</span></span>
<span data-ttu-id="7ad4a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ad4a-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="7ad4a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ad4a-121">Agregar Birst Agile análisis de negocios desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7ad4a-121">Adding Birst Agile Business Analytics from hello gallery</span></span>
2. <span data-ttu-id="7ad4a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ad4a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-birst-agile-business-analytics-from-hello-gallery"></a><span data-ttu-id="7ad4a-123">Agregar Birst Agile análisis de negocios desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7ad4a-123">Adding Birst Agile Business Analytics from hello gallery</span></span>
<span data-ttu-id="7ad4a-124">integración de hello tooconfigure de análisis de negocios Agile Birst en Azure AD, deberá tooadd Birst Agile análisis de negocios de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-124">tooconfigure hello integration of Birst Agile Business Analytics into Azure AD, you need tooadd Birst Agile Business Analytics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7ad4a-125">**tooadd Birst Agile análisis de negocios de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7ad4a-125">**tooadd Birst Agile Business Analytics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ad4a-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7ad4a-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7ad4a-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="7ad4a-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="7ad4a-133">En el cuadro de búsqueda de hello, escriba **Birst análisis de negocios Agile**.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-133">In hello search box, type **Birst Agile Business Analytics**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_search.png)

5. <span data-ttu-id="7ad4a-135">En el panel de resultados de hello, seleccione **análisis de negocios Agile Birst**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-135">In hello results panel, select **Birst Agile Business Analytics**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7ad4a-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ad4a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7ad4a-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con Birst Agile Business ByDesign con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7ad4a-138">In this section, you configure and test Azure AD single sign-on with Birst Agile Business Analytics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7ad4a-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en análisis de negocios Agile Birst es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Birst Agile Business Analytics is tooa user in Azure AD.</span></span> <span data-ttu-id="7ad4a-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en análisis de negocios Agile Birst debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-140">In other words, a link relationship between an Azure AD user and hello related user in Birst Agile Business Analytics needs toobe established.</span></span>

<span data-ttu-id="7ad4a-141">En análisis de negocios Agile Birst, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-141">In Birst Agile Business Analytics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7ad4a-142">tooconfigure y prueba de inicio de sesión único en Azure AD con análisis de negocios Agile Birst, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="7ad4a-142">tooconfigure and test Azure AD single sign-on with Birst Agile Business Analytics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7ad4a-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7ad4a-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ad4a-145">**[Crear un usuario de prueba de análisis de negocios Agile Birst](#creating-a-birst-agile-business-analytics-test-user)**  -toohave un equivalente de Britta Simon en Agile análisis de negocios de Birst que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-145">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - toohave a counterpart of Britta Simon in Birst Agile Business Analytics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7ad4a-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ad4a-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7ad4a-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ad4a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7ad4a-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de análisis de negocios Agile Birst.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Birst Agile Business Analytics application.</span></span>

<span data-ttu-id="7ad4a-150">**tooconfigure inicio de sesión único en Azure AD con análisis de negocios Agile Birst, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7ad4a-150">**tooconfigure Azure AD single sign-on with Birst Agile Business Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ad4a-151">En el portal de Azure, en Hola Hola **análisis de negocios Agile Birst** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-151">In hello Azure portal, on hello **Birst Agile Business Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="7ad4a-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-birst-tutorial/tutorial_birst_samlbase.png)

3. <span data-ttu-id="7ad4a-155">En hello **Birst Agile Business Analytics dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7ad4a-155">On hello **Birst Agile Business Analytics Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-birst-tutorial/tutorial_birst_url.png)

     <span data-ttu-id="7ad4a-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="7ad4a-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

     <span data-ttu-id="7ad4a-158">depende de la dirección URL de Hola Hola centro de datos que se encuentra la cuenta de Birst:</span><span class="sxs-lookup"><span data-stu-id="7ad4a-158">hello URL depends on hello datacenter that your Birst account is located:</span></span> 

     * <span data-ttu-id="7ad4a-159">Para seguir el patrón de hello el uso de centro de datos de EE. UU.:`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="7ad4a-159">For US datacenter use following hello pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span> 

     * <span data-ttu-id="7ad4a-160">Para Europa centro de datos use Hola siguiente patrón:`https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="7ad4a-160">For Europe datacenter use hello following pattern: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7ad4a-161">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-161">This value is not real.</span></span> <span data-ttu-id="7ad4a-162">Valor de Hola de actualización con Hola dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-162">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="7ad4a-163">Póngase en contacto con [equipo de soporte técnico de cliente de análisis de negocios Agile Birst](mailto:info@birst.com) valor de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-163">Contact [Birst Agile Business Analytics Client support team](mailto:info@birst.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="7ad4a-164">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-birst-tutorial/tutorial_birst_certificate.png) 

5. <span data-ttu-id="7ad4a-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="7ad4a-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-birst-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7ad4a-168">En hello **configuración de análisis de negocios Agile Birst** sección, haga clic en **configurar análisis de negocios ágil de Birst** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-168">On hello **Birst Agile Business Analytics Configuration** section, click **Configure Birst Agile Business Analytics** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7ad4a-169">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="7ad4a-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-birst-tutorial/tutorial_birst_configure.png) 

7. <span data-ttu-id="7ad4a-171">tooconfigure inicio de sesión único en **análisis de negocios Agile Birst** lado, necesita hello toosend descargado **certificado (Base64)**, **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On Dirección URL del servicio** demasiado[equipo de soporte técnico de análisis de negocios Agile Birst](mailto:info@birst.com).</span><span class="sxs-lookup"><span data-stu-id="7ad4a-171">tooconfigure single sign-on on **Birst Agile Business Analytics** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Birst Agile Business Analytics support team](mailto:info@birst.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="7ad4a-172">Indique el equipo de tooBirst que esta integración debe algoritmo SHA256 (no se admiten SHA1) para que pueda establecer Hola SSO en el servidor adecuado de hello como **app2101** etcetera.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-172">Mention tooBirst team that this integration needs SHA256 Algorithm (SHA1 will not be supported) so that they can set hello SSO on hello appropriate server like **app2101** etc.</span></span>
  

> [!TIP]
> <span data-ttu-id="7ad4a-173">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="7ad4a-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7ad4a-174">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7ad4a-175">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ad4a-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7ad4a-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ad4a-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="7ad4a-177">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="7ad4a-179">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7ad4a-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ad4a-180">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7ad4a-182">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7ad4a-184">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7ad4a-186">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="7ad4a-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7ad4a-188">a.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-188">a.</span></span> <span data-ttu-id="7ad4a-189">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ad4a-190">b.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-190">b.</span></span> <span data-ttu-id="7ad4a-191">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ad4a-192">c.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-192">c.</span></span> <span data-ttu-id="7ad4a-193">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7ad4a-194">d.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-194">d.</span></span> <span data-ttu-id="7ad4a-195">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-195">Click **Create**.</span></span>
 
### <a name="creating-a-birst-agile-business-analytics-test-user"></a><span data-ttu-id="7ad4a-196">Creación de un usuario de prueba de Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="7ad4a-196">Creating a Birst Agile Business Analytics test user</span></span>

<span data-ttu-id="7ad4a-197">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en análisis de negocios Agile Birst toocreate.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-197">hello objective of this section is toocreate a user called Britta Simon in Birst Agile Business Analytics.</span></span> <span data-ttu-id="7ad4a-198">Trabajar con [equipo de soporte técnico de análisis de negocios Agile Birst](mailto:info@birst.com) a los usuarios de tooadd Hola Hola Birst cuenta.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-198">Work with [Birst Agile Business Analytics support team](mailto:info@birst.com) tooadd hello users in hello Birst account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7ad4a-199">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ad4a-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7ad4a-200">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooBirst Agile análisis de negocios.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBirst Agile Business Analytics.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="7ad4a-202">**tooassign Britta Simon tooBirst Agile análisis de negocios, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7ad4a-202">**tooassign Britta Simon tooBirst Agile Business Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ad4a-203">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7ad4a-205">En la lista de aplicaciones de hello, seleccione **Birst análisis de negocios Agile**.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-205">In hello applications list, select **Birst Agile Business Analytics**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-birst-tutorial/tutorial_birst_app.png) 

3. <span data-ttu-id="7ad4a-207">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="7ad4a-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-209">Click **Add** button.</span></span> <span data-ttu-id="7ad4a-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="7ad4a-212">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7ad4a-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ad4a-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7ad4a-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="7ad4a-215">Testing single sign-on</span></span>

<span data-ttu-id="7ad4a-216">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="7ad4a-217">Al hacer clic en hello análisis de negocios Agile Birst el icono Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación de análisis de negocios Agile Birst.</span><span class="sxs-lookup"><span data-stu-id="7ad4a-217">When you click hello Birst Agile Business Analytics tile in hello Access Panel, you should get automatically signed-on tooyour Birst Agile Business Analytics application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7ad4a-218">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7ad4a-218">Additional resources</span></span>

* [<span data-ttu-id="7ad4a-219">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ad4a-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ad4a-220">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7ad4a-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-birst-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-birst-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-birst-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-birst-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-birst-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-birst-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-birst-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-birst-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-birst-tutorial/tutorial_general_203.png


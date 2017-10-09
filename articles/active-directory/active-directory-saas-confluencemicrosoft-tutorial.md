---
title: "Tutorial: Integración de Azure Active Directory con Confluence SAML SSO by Microsoft | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SSO de SAML confluencia por Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ace23800e3908c8125052b4a2edcaae71f19935d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a><span data-ttu-id="d92b3-103">Tutorial: Integración de Azure Active Directory con Confluence SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="d92b3-103">Tutorial: Azure Active Directory integration with Confluence SAML SSO by Microsoft</span></span>

<span data-ttu-id="d92b3-104">En este tutorial, aprenderá cómo toointegrate SSO de SAML confluencia por Microsoft con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d92b3-104">In this tutorial, you learn how toointegrate Confluence SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d92b3-105">Integración de SSO de SAML confluencia por Microsoft con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d92b3-105">Integrating Confluence SAML SSO by Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d92b3-106">Puede controlar en Azure AD que tenga acceso tooConfluence SSO de SAML por Microsoft</span><span class="sxs-lookup"><span data-stu-id="d92b3-106">You can control in Azure AD who has access tooConfluence SAML SSO by Microsoft</span></span>
- <span data-ttu-id="d92b3-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooConfluence SSO de SAML por Microsoft (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d92b3-107">You can enable your users tooautomatically get signed-on tooConfluence SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d92b3-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d92b3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d92b3-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d92b3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d92b3-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d92b3-110">Prerequisites</span></span>

<span data-ttu-id="d92b3-111">tooconfigure integración de Azure AD con SSO de SAML confluencia por Microsoft, deberá Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="d92b3-111">tooconfigure Azure AD integration with Confluence SAML SSO by Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="d92b3-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d92b3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d92b3-113">Aplicación de servidor confluencia instalado en un servidor de Windows de 64 bits (local o en la infraestructura de IaaS en la nube hello)</span><span class="sxs-lookup"><span data-stu-id="d92b3-113">Confluence server application installed on a Windows 64-bit server (on premise or on hello cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="d92b3-114">El servidor de Confluence es compatible con HTTPS</span><span class="sxs-lookup"><span data-stu-id="d92b3-114">Confluence server is HTTPS enabled</span></span>
- <span data-ttu-id="d92b3-115">Tenga en cuenta Hola admitida versiones de complemento de confluencia se mencionan en por debajo de la sección.</span><span class="sxs-lookup"><span data-stu-id="d92b3-115">Note hello supported versions for Confluence Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="d92b3-116">Confluencia servidor es accesible en internet especialmente tooAzure página de inicio de sesión de AD para la autenticación y debe tooreceive capaz de Hola símbolo (token) de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d92b3-116">Confluence server is reachable on internet particularly tooAzure AD Login page for authentication and should able tooreceive hello token from Azure AD</span></span>
- <span data-ttu-id="d92b3-117">Las credenciales de administrador se configuran en Confluence</span><span class="sxs-lookup"><span data-stu-id="d92b3-117">Admin credentials are set up in Confluence</span></span>
- <span data-ttu-id="d92b3-118">WebSudo está deshabilitado en Confluence</span><span class="sxs-lookup"><span data-stu-id="d92b3-118">WebSudo is disabled in Confluence</span></span>
- <span data-ttu-id="d92b3-119">Usuario creado en la aplicación de servidor confluencia Hola de prueba</span><span class="sxs-lookup"><span data-stu-id="d92b3-119">Test user created in hello Confluence server application</span></span>

> [!NOTE]
> <span data-ttu-id="d92b3-120">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción de confluencia.</span><span class="sxs-lookup"><span data-stu-id="d92b3-120">tootest hello steps in this tutorial, we do not recommend using a production environment of Confluence.</span></span> <span data-ttu-id="d92b3-121">Probar la integración de Hola primero en el desarrollo o el entorno de aplicación hello y, a continuación, entorno de producción de hello de uso de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="d92b3-121">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="d92b3-122">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="d92b3-122">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d92b3-123">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d92b3-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d92b3-124">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de prueba de un mes: [oferta de versión de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d92b3-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-confluence"></a><span data-ttu-id="d92b3-125">Versiones compatibles de Confluence</span><span class="sxs-lookup"><span data-stu-id="d92b3-125">Supported versions of Confluence</span></span> 

<span data-ttu-id="d92b3-126">En la actualidad se admiten las siguientes versiones de Confluence:</span><span class="sxs-lookup"><span data-stu-id="d92b3-126">As of now, following versions of Confluence are supported:</span></span>

- <span data-ttu-id="d92b3-127">Confluencia: too5.10 5.0</span><span class="sxs-lookup"><span data-stu-id="d92b3-127">Confluence: 5.0 too5.10</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d92b3-128">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="d92b3-128">Scenario description</span></span>
<span data-ttu-id="d92b3-129">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="d92b3-129">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d92b3-130">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="d92b3-130">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d92b3-131">Agregar SSO de SAML confluencia por Microsoft de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="d92b3-131">Adding Confluence SAML SSO by Microsoft from hello gallery</span></span>
2. <span data-ttu-id="d92b3-132">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d92b3-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-confluence-saml-sso-by-microsoft-from-hello-gallery"></a><span data-ttu-id="d92b3-133">Agregar SSO de SAML confluencia por Microsoft de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="d92b3-133">Adding Confluence SAML SSO by Microsoft from hello gallery</span></span>
<span data-ttu-id="d92b3-134">integración de hello tooconfigure de SSO de SAML confluencia por Microsoft en Azure AD, deberá tooadd SSO de SAML confluencia por Microsoft de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="d92b3-134">tooconfigure hello integration of Confluence SAML SSO by Microsoft into Azure AD, you need tooadd Confluence SAML SSO by Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d92b3-135">**tooadd SSO de SAML confluencia por Microsoft de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d92b3-135">**tooadd Confluence SAML SSO by Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d92b3-136">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="d92b3-136">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d92b3-138">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-138">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d92b3-139">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-139">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="d92b3-141">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d92b3-141">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="d92b3-143">En el cuadro de búsqueda de hello, escriba **SSO de SAML confluencia Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-143">In hello search box, type **Confluence SAML SSO by Microsoft**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_search.png)

5. <span data-ttu-id="d92b3-145">En el panel de resultados de hello, seleccione **SSO de SAML confluencia Microsoft**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d92b3-145">In hello results panel, select **Confluence SAML SSO by Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d92b3-147">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d92b3-147">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d92b3-148">En esta sección va a configurar y probar el inicio de sesión único de Azure AD con Confluence SAML SSO by Microsoft con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d92b3-148">In this section, you configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d92b3-149">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en confluencia SSO de SAML de Microsoft es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d92b3-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Confluence SAML SSO by Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="d92b3-150">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SSO de SAML confluencia Microsoft necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="d92b3-150">In other words, a link relationship between an Azure AD user and hello related user in Confluence SAML SSO by Microsoft needs toobe established.</span></span>

<span data-ttu-id="d92b3-151">En SSO de SAML confluencia por Microsoft, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d92b3-151">In Confluence SAML SSO by Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d92b3-152">tooconfigure y prueba de inicio de sesión único en Azure AD con SSO de SAML confluencia por Microsoft, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="d92b3-152">tooconfigure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d92b3-153">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="d92b3-153">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d92b3-154">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d92b3-154">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d92b3-155">**[Crear un SSO de SAML confluencia por usuario de prueba de Microsoft](#creating-a-confluence-saml-sso-by-microsoft-test-user)**  -toohave un equivalente de Britta Simon en SSO de SAML confluencia por Microsoft que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="d92b3-155">**[Creating a Confluence SAML SSO by Microsoft test user](#creating-a-confluence-saml-sso-by-microsoft-test-user)** - toohave a counterpart of Britta Simon in Confluence SAML SSO by Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d92b3-156">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d92b3-156">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d92b3-157">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="d92b3-157">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d92b3-158">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d92b3-158">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d92b3-159">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en el SSO de SAML confluencia por aplicación de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d92b3-159">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Confluence SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="d92b3-160">**tooconfigure inicio de sesión único en Azure AD con SSO de SAML confluencia por Microsoft, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d92b3-160">**tooconfigure Azure AD single sign-on with Confluence SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="d92b3-161">En el portal de Azure, en Hola Hola **SSO de SAML confluencia Microsoft** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-161">In hello Azure portal, on hello **Confluence SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="d92b3-163">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="d92b3-163">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_samlbase.png)

3. <span data-ttu-id="d92b3-165">En hello **SSO de SAML confluencia Domain de Microsoft y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d92b3-165">On hello **Confluence SAML SSO by Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    <span data-ttu-id="d92b3-167">a.</span><span class="sxs-lookup"><span data-stu-id="d92b3-167">a.</span></span> <span data-ttu-id="d92b3-168">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="d92b3-168">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="d92b3-169">b.</span><span class="sxs-lookup"><span data-stu-id="d92b3-169">b.</span></span> <span data-ttu-id="d92b3-170">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="d92b3-170">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="d92b3-171">c.</span><span class="sxs-lookup"><span data-stu-id="d92b3-171">c.</span></span> <span data-ttu-id="d92b3-172">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="d92b3-172">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d92b3-173">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="d92b3-173">These values are not real.</span></span> <span data-ttu-id="d92b3-174">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d92b3-174">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="d92b3-175">En caso de que sea una dirección URL con nombre, el puerto es opcional.</span><span class="sxs-lookup"><span data-stu-id="d92b3-175">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="d92b3-176">Estos valores se reciben durante la configuración de Hola de complemento de confluencia, que se explica más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="d92b3-176">These values are received during hello configuration of Confluence plugin, which is explained later in hello tutorial.</span></span>
 

4. <span data-ttu-id="d92b3-177">Hola toogenerate **metadatos** dirección url, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="d92b3-177">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="d92b3-178">a.</span><span class="sxs-lookup"><span data-stu-id="d92b3-178">a.</span></span> <span data-ttu-id="d92b3-179">Haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-179">Click **App registrations**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="d92b3-181">b.</span><span class="sxs-lookup"><span data-stu-id="d92b3-181">b.</span></span> <span data-ttu-id="d92b3-182">Haga clic en **extremos** tooopen **extremos** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d92b3-182">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="d92b3-184">c.</span><span class="sxs-lookup"><span data-stu-id="d92b3-184">c.</span></span> <span data-ttu-id="d92b3-185">Haga clic en hello copia botón toocopy **documento de metadatos de federación** dirección url y péguela en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="d92b3-185">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="d92b3-187">d.</span><span class="sxs-lookup"><span data-stu-id="d92b3-187">d.</span></span> <span data-ttu-id="d92b3-188">Ahora vaya toohello página de propiedades de **SSO de SAML confluencia Microsoft** copia hello y **Id. de aplicación** con **copia** botón y péguelo en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="d92b3-188">Now go toohello property page of **Confluence SAML SSO by Microsoft** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/appid.png)

    <span data-ttu-id="d92b3-190">e.</span><span class="sxs-lookup"><span data-stu-id="d92b3-190">e.</span></span> <span data-ttu-id="d92b3-191">Generar hello **dirección URL de metadatos** con hello sigue el patrón: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` y copie este valor en el Bloc de notas como se utiliza para la configuración de Hola de complemento de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="d92b3-191">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for hello configuration of hello plugin.</span></span>

5. <span data-ttu-id="d92b3-192">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="d92b3-192">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d92b3-194">Póngase en contacto con [Microsoft](mailto:waadpartners@microsoft.com) con hello siguiente información para hello confluencia complemento.</span><span class="sxs-lookup"><span data-stu-id="d92b3-194">Contact [Microsoft](mailto:waadpartners@microsoft.com) with hello following information for hello Confluence plugin.</span></span>
    
    *   <span data-ttu-id="d92b3-195">Nombre del cliente:</span><span class="sxs-lookup"><span data-stu-id="d92b3-195">Customer Name:</span></span>
    *   <span data-ttu-id="d92b3-196">Nombre del dominio principal:</span><span class="sxs-lookup"><span data-stu-id="d92b3-196">Primary domain name:</span></span>
    *   <span data-ttu-id="d92b3-197">Azure AD Premium: Sí/No (el complemento será de tooall disponible Hola cliente Free, Basic y Premium SKU)</span><span class="sxs-lookup"><span data-stu-id="d92b3-197">Azure AD Premium: Yes/No (Plugin will be available tooall     hello customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="d92b3-198">Número de usuarios que van a usar esta integración:</span><span class="sxs-lookup"><span data-stu-id="d92b3-198">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="d92b3-199">Versión de Confluence:</span><span class="sxs-lookup"><span data-stu-id="d92b3-199">Confluence Version:</span></span>
    *   <span data-ttu-id="d92b3-200">Comentarios:</span><span class="sxs-lookup"><span data-stu-id="d92b3-200">Comments:</span></span>

7. <span data-ttu-id="d92b3-201">En una ventana del explorador web diferente, inicie sesión en la instancia de confluencia tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="d92b3-201">In a different web browser window, log in tooyour Confluence instance as an administrator.</span></span>

8. <span data-ttu-id="d92b3-202">Mantenga el mouse sobre el icono de engranaje y haga clic en hello **complementos**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-202">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="d92b3-204">En la sección de la pestaña Complementos, haga clic en **Administrar complementos**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-204">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon72.png)

10. <span data-ttu-id="d92b3-206">Cargar manualmente el complemento de hello proporcionado por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d92b3-206">Manually upload hello plugin provided by Microsoft.</span></span> <span data-ttu-id="d92b3-207">Una vez instalado el complemento de hello, aparece en **usuario instalado** sección de complementos de **administrar complemento** sección.</span><span class="sxs-lookup"><span data-stu-id="d92b3-207">Once hello plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="d92b3-208">Haga clic en **configurar** tooconfigure Hola nuevo complemento.</span><span class="sxs-lookup"><span data-stu-id="d92b3-208">Click **Configure** tooconfigure hello new plugin.</span></span>

12. <span data-ttu-id="d92b3-209">Siga estos pasos en la página de configuración:</span><span class="sxs-lookup"><span data-stu-id="d92b3-209">Perform following steps on configuration page:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="d92b3-211">a.</span><span class="sxs-lookup"><span data-stu-id="d92b3-211">a.</span></span> <span data-ttu-id="d92b3-212">En **dirección URL de metadatos** pegar hello **dirección URL de metadatos** generados a partir de Azure AD y haga clic en hello **resolver** botón.</span><span class="sxs-lookup"><span data-stu-id="d92b3-212">In **Metadata URL** paste hello **Metadata URL** generated from Azure AD and click hello **Resolve** button.</span></span> <span data-ttu-id="d92b3-213">Lee la dirección URL de metadatos de IdP de Hola y rellena toda la información de campos Hola.</span><span class="sxs-lookup"><span data-stu-id="d92b3-213">It reads hello IdP metadata URL and populates all hello fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="d92b3-214">La ubicación del Id. de usuario de SAML predeterminada es el identificador de nombre.</span><span class="sxs-lookup"><span data-stu-id="d92b3-214">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="d92b3-215">Puede cambiar esta opción de atributo tooan y escriba el nombre del atributo adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="d92b3-215">You can change this tooan attribute option and enter hello appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="d92b3-216">Asegúrese de que hay un solo certificado asignado en la aplicación hello de forma que no hay ningún error en la resolución de metadatos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d92b3-216">Ensure that there is only one certificate mapped against hello app so that there is no error in resolving hello metadata.</span></span> <span data-ttu-id="d92b3-217">Si hay varios certificados, después de resolver los metadatos de Hola, administrador obtiene un error.</span><span class="sxs-lookup"><span data-stu-id="d92b3-217">If there are multiple certificates, upon resolving hello metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="d92b3-218">b.</span><span class="sxs-lookup"><span data-stu-id="d92b3-218">b.</span></span> <span data-ttu-id="d92b3-219">Hola copia **identificador, la dirección URL de respuesta y la dirección URL de inicio de sesión** valores y péguelos en **identificador, la dirección URL de respuesta y la dirección URL de inicio de sesión** cuadros de texto respectivamente en **SSO de SAML confluencia Domain de Microsoft y las direcciones URL**  sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d92b3-219">Copy hello **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **Confluence SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="d92b3-220">c.</span><span class="sxs-lookup"><span data-stu-id="d92b3-220">c.</span></span> <span data-ttu-id="d92b3-221">En **el nombre del botón de inicio de sesión** nombre de tipo hello del botón de la organización quiere Hola usuarios toosee en pantalla de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d92b3-221">In **Login Button Name** type hello name of button your organization wants hello users toosee on login screen.</span></span>

    <span data-ttu-id="d92b3-222">d.</span><span class="sxs-lookup"><span data-stu-id="d92b3-222">d.</span></span> <span data-ttu-id="d92b3-223">En **ubicaciones de Id. de usuario de SAML** seleccione **Id. de usuario está en elemento NameIdentifier de Hola de hello instrucción Subject** o **Id. de usuario está en un elemento Attribute**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-223">In **SAML User ID Locations** select either **User ID is in hello NameIdentifier element of hello Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="d92b3-224">Este identificador tiene toobe Hola confluencia un identificador de usuario. Si no se encuentra el Id. de usuario de hello, sistema no permitirá que toolog a los usuarios en.</span><span class="sxs-lookup"><span data-stu-id="d92b3-224">This ID has toobe hello Confluence user id. If hello user id is not matched, then system will not allow users toolog in.</span></span> 
    
    <span data-ttu-id="d92b3-225">e.</span><span class="sxs-lookup"><span data-stu-id="d92b3-225">e.</span></span> <span data-ttu-id="d92b3-226">Si selecciona **Id. de usuario está en un elemento Attribute** opción, a continuación, en **nombre del atributo** cuadro de texto Nombre de Hola de tipo de atributo de Hola donde se esperaba el Id. de usuario.</span><span class="sxs-lookup"><span data-stu-id="d92b3-226">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type hello name of hello attribute where User Id is expected.</span></span> 

    <span data-ttu-id="d92b3-227">f.</span><span class="sxs-lookup"><span data-stu-id="d92b3-227">f.</span></span> <span data-ttu-id="d92b3-228">Si usas el dominio federado de hello (por ejemplo, etc. ADFS) con Azure AD, a continuación, haga clic en hello **habilitar Home Realm Discovery** opción y configure hello **nombre de dominio**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-228">If you are using hello federated domain (like ADFS etc.) with Azure AD, then click on hello **Enable Home Realm Discovery** option and configure hello **Domain Name**.</span></span>
    
    <span data-ttu-id="d92b3-229">g.</span><span class="sxs-lookup"><span data-stu-id="d92b3-229">g.</span></span> <span data-ttu-id="d92b3-230">En **nombre de dominio** escriba Hola dominio aquí el nombre en el caso de inicio de sesión de hello basada en AD FS.</span><span class="sxs-lookup"><span data-stu-id="d92b3-230">In **Domain Name** type hello domain name here in case of hello ADFS-based login.</span></span>

    <span data-ttu-id="d92b3-231">h.</span><span class="sxs-lookup"><span data-stu-id="d92b3-231">h.</span></span> <span data-ttu-id="d92b3-232">Comprobar **Habilitar cierre de sesión único** si desea toolog fuera de Azure AD cuando un usuario cierra la sesión de confluencia.</span><span class="sxs-lookup"><span data-stu-id="d92b3-232">Check **Enable Single Sign out** if you wish toolog out from Azure AD when a user logs out from Confluence.</span></span> 

    <span data-ttu-id="d92b3-233">i.</span><span class="sxs-lookup"><span data-stu-id="d92b3-233">i.</span></span> <span data-ttu-id="d92b3-234">Haga clic en **guardar** botón Configuración de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="d92b3-234">Click **Save** button toosave hello settings.</span></span>


> [!TIP]
> <span data-ttu-id="d92b3-235">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="d92b3-235">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d92b3-236">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="d92b3-236">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d92b3-237">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d92b3-237">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d92b3-238">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="d92b3-238">Creating an Azure AD test user</span></span>
<span data-ttu-id="d92b3-239">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="d92b3-239">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="d92b3-241">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d92b3-241">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d92b3-242">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="d92b3-242">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d92b3-244">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-244">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d92b3-246">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d92b3-246">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d92b3-248">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="d92b3-248">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d92b3-250">a.</span><span class="sxs-lookup"><span data-stu-id="d92b3-250">a.</span></span> <span data-ttu-id="d92b3-251">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-251">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d92b3-252">b.</span><span class="sxs-lookup"><span data-stu-id="d92b3-252">b.</span></span> <span data-ttu-id="d92b3-253">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d92b3-253">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d92b3-254">c.</span><span class="sxs-lookup"><span data-stu-id="d92b3-254">c.</span></span> <span data-ttu-id="d92b3-255">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-255">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d92b3-256">d.</span><span class="sxs-lookup"><span data-stu-id="d92b3-256">d.</span></span> <span data-ttu-id="d92b3-257">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-257">Click **Create**.</span></span>
 
### <a name="creating-a-confluence-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="d92b3-258">Creación de un usuario de prueba de Confluence SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="d92b3-258">Creating a Confluence SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="d92b3-259">toolog de los usuarios de Azure AD tooenable en tooConfluence en el servidor local, se les deben aprovisionar en SSO de SAML confluencia por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d92b3-259">tooenable Azure AD users toolog in tooConfluence on premise server, they must be provisioned into Confluence SAML SSO by Microsoft.</span></span> <span data-ttu-id="d92b3-260">Para Confluence SAML SSO by Microsoft, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="d92b3-260">For Confluence SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="d92b3-261">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d92b3-261">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="d92b3-262">Inicie sesión en tooyour confluencia en servidor local como administrador.</span><span class="sxs-lookup"><span data-stu-id="d92b3-262">Log in tooyour Confluence on premise server as an administrator.</span></span>

2. <span data-ttu-id="d92b3-263">Mantenga el mouse sobre el icono de engranaje y haga clic en hello **administración de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-263">Hover on cog and click hello **User management**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-confluencemicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="d92b3-265">En la sección Usuarios, haga clic en la pestaña **Agregar usuarios**. En hello **"Agregar usuarios"** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="d92b3-265">Under Users section, click **Add users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![Agregar empleado](./media/active-directory-saas-confluencemicrosoft-tutorial/user2.png) 

    <span data-ttu-id="d92b3-267">a.</span><span class="sxs-lookup"><span data-stu-id="d92b3-267">a.</span></span> <span data-ttu-id="d92b3-268">Hola **nombre de usuario** cuadro de texto, correo electrónico de Hola de tipo de usuario como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d92b3-268">In hello **Username** textbox, type hello email of user like Britta Simon.</span></span>

    <span data-ttu-id="d92b3-269">b.</span><span class="sxs-lookup"><span data-stu-id="d92b3-269">b.</span></span> <span data-ttu-id="d92b3-270">Hola **nombre completo** cuadro de texto, nombre completo de tipo hello del usuario como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d92b3-270">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="d92b3-271">c.</span><span class="sxs-lookup"><span data-stu-id="d92b3-271">c.</span></span> <span data-ttu-id="d92b3-272">Hola **correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="d92b3-272">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="d92b3-273">d.</span><span class="sxs-lookup"><span data-stu-id="d92b3-273">d.</span></span> <span data-ttu-id="d92b3-274">Hola **contraseña** cuadro de texto, escriba la contraseña para Britta Simon Hola.</span><span class="sxs-lookup"><span data-stu-id="d92b3-274">In hello **Password** textbox, type hello password for Britta Simon.</span></span>

    <span data-ttu-id="d92b3-275">e.</span><span class="sxs-lookup"><span data-stu-id="d92b3-275">e.</span></span> <span data-ttu-id="d92b3-276">Haga clic en **Confirmar contraseña** introducir la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="d92b3-276">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="d92b3-277">f.</span><span class="sxs-lookup"><span data-stu-id="d92b3-277">f.</span></span> <span data-ttu-id="d92b3-278">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-278">Click **Add** button.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d92b3-279">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d92b3-279">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d92b3-280">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooConfluence SSO de SAML por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d92b3-280">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConfluence SAML SSO by Microsoft.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="d92b3-282">**tooassign Britta Simon tooConfluence SSO de SAML por Microsoft, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="d92b3-282">**tooassign Britta Simon tooConfluence SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="d92b3-283">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-283">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="d92b3-285">En la lista de aplicaciones de hello, seleccione **SSO de SAML confluencia Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-285">In hello applications list, select **Confluence SAML SSO by Microsoft**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png) 

3. <span data-ttu-id="d92b3-287">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-287">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="d92b3-289">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-289">Click **Add** button.</span></span> <span data-ttu-id="d92b3-290">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-290">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="d92b3-292">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="d92b3-292">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d92b3-293">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-293">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d92b3-294">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="d92b3-294">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d92b3-295">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="d92b3-295">Testing single sign-on</span></span>

<span data-ttu-id="d92b3-296">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="d92b3-296">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d92b3-297">Al hacer clic en hello SSO de SAML confluencia por mosaico de Microsoft en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour SSO de SAML confluencia por aplicación de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d92b3-297">When you click hello Confluence SAML SSO by Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour Confluence SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="d92b3-298">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d92b3-298">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d92b3-299">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d92b3-299">Additional resources</span></span>

* [<span data-ttu-id="d92b3-300">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d92b3-300">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d92b3-301">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d92b3-301">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_203.png


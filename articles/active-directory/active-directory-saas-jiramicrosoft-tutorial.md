---
title: "Tutorial: Integración de Azure Active Directory con JIRA SAML SSO by Microsoft | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SSO de SAML JIRA por Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 178c4c040d9939bca271ac185ca5c2feb14f1247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="2fe31-103">Tutorial: Integración de Azure Active Directory con JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="2fe31-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="2fe31-104">En este tutorial, aprenderá cómo toointegrate SSO de SAML JIRA por Microsoft con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2fe31-104">In this tutorial, you learn how toointegrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2fe31-105">Integración de SSO de SAML JIRA por Microsoft con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2fe31-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2fe31-106">Puede controlar en Azure AD que tenga acceso tooJIRA SSO de SAML por Microsoft</span><span class="sxs-lookup"><span data-stu-id="2fe31-106">You can control in Azure AD who has access tooJIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="2fe31-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooJIRA SSO de SAML por Microsoft (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fe31-107">You can enable your users tooautomatically get signed-on tooJIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2fe31-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2fe31-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2fe31-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2fe31-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fe31-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2fe31-110">Prerequisites</span></span>

<span data-ttu-id="2fe31-111">tooconfigure integración de Azure AD con SSO de SAML JIRA por Microsoft, deberá Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2fe31-111">tooconfigure Azure AD integration with JIRA SAML SSO by Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="2fe31-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fe31-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2fe31-113">Aplicación de servidor JIRA instalado en un servidor de Windows de 64 bits (local o en la infraestructura de IaaS en la nube hello)</span><span class="sxs-lookup"><span data-stu-id="2fe31-113">JIRA server application installed on a Windows 64-bit server (on premise or on hello cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="2fe31-114">El servidor JIRA es compatible con HTTPS</span><span class="sxs-lookup"><span data-stu-id="2fe31-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="2fe31-115">Tenga en cuenta Hola admitida versiones de complemento de JIRA se mencionan en por debajo de la sección.</span><span class="sxs-lookup"><span data-stu-id="2fe31-115">Note hello supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="2fe31-116">JIRA servidor es accesible en internet especialmente tooAzure página de inicio de sesión de AD para la autenticación y debe tooreceive capaz de Hola símbolo (token) de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fe31-116">JIRA server is reachable on internet particularly tooAzure AD Login page for authentication and should able tooreceive hello token from Azure AD</span></span>
- <span data-ttu-id="2fe31-117">Las credenciales de administrador se configuran en JIRA</span><span class="sxs-lookup"><span data-stu-id="2fe31-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="2fe31-118">WebSudo está deshabilitado en JIRA</span><span class="sxs-lookup"><span data-stu-id="2fe31-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="2fe31-119">Usuario creado en la aplicación de servidor JIRA Hola de prueba</span><span class="sxs-lookup"><span data-stu-id="2fe31-119">Test user created in hello JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="2fe31-120">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción de JIRA.</span><span class="sxs-lookup"><span data-stu-id="2fe31-120">tootest hello steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="2fe31-121">Probar la integración de Hola primero en el desarrollo o el entorno de aplicación hello y, a continuación, entorno de producción de hello de uso de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="2fe31-121">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="2fe31-122">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2fe31-122">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2fe31-123">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2fe31-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2fe31-124">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de prueba de un mes: [oferta de versión de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2fe31-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="2fe31-125">Versiones compatibles de JIRA</span><span class="sxs-lookup"><span data-stu-id="2fe31-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="2fe31-126">En la actualidad, se admiten las siguientes versiones de JIRA:</span><span class="sxs-lookup"><span data-stu-id="2fe31-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="2fe31-127">Núcleo JIRA y Software: too7.2.0 6.0</span><span class="sxs-lookup"><span data-stu-id="2fe31-127">JIRA Core and Software: 6.0 too7.2.0</span></span>
- <span data-ttu-id="2fe31-128">JIRA departamento de servicios: too3.2 3.0</span><span class="sxs-lookup"><span data-stu-id="2fe31-128">JIRA Service Desk: 3.0 too3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2fe31-129">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2fe31-129">Scenario description</span></span>
<span data-ttu-id="2fe31-130">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2fe31-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2fe31-131">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="2fe31-131">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2fe31-132">Adición de SSO de SAML JIRA por Microsoft de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="2fe31-132">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
2. <span data-ttu-id="2fe31-133">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fe31-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-hello-gallery"></a><span data-ttu-id="2fe31-134">Adición de SSO de SAML JIRA por Microsoft de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="2fe31-134">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
<span data-ttu-id="2fe31-135">integración de hello tooconfigure de SSO de SAML JIRA por Microsoft en Azure AD, deberá tooadd SSO de SAML JIRA por Microsoft de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="2fe31-135">tooconfigure hello integration of JIRA SAML SSO by Microsoft into Azure AD, you need tooadd JIRA SAML SSO by Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2fe31-136">**tooadd JIRA SSO de SAML por Microsoft de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2fe31-136">**tooadd JIRA SAML SSO by Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2fe31-137">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="2fe31-137">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2fe31-139">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-139">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2fe31-140">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-140">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="2fe31-142">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2fe31-142">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="2fe31-144">En el cuadro de búsqueda de hello, escriba **JIRA SSO de SAML Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-144">In hello search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="2fe31-146">En el panel de resultados de hello, seleccione **JIRA SSO de SAML Microsoft**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2fe31-146">In hello results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2fe31-148">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fe31-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2fe31-149">En esta sección, va a configurar y probar el inicio de sesión único de Azure AD con JIRA SAML SSO by Microsoft con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2fe31-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2fe31-150">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en JIRA SSO de SAML de Microsoft es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2fe31-150">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in JIRA SAML SSO by Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="2fe31-151">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SSO de SAML JIRA Microsoft necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="2fe31-151">In other words, a link relationship between an Azure AD user and hello related user in JIRA SAML SSO by Microsoft needs toobe established.</span></span>

<span data-ttu-id="2fe31-152">En SSO de SAML JIRA por Microsoft, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2fe31-152">In JIRA SAML SSO by Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2fe31-153">tooconfigure y prueba de inicio de sesión único en Azure AD con SSO de SAML JIRA por Microsoft, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2fe31-153">tooconfigure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2fe31-154">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="2fe31-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2fe31-155">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2fe31-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2fe31-156">**[Crear un SSO de SAML JIRA por usuario de prueba de Microsoft](#creating-a-jira-saml-sso-by-microsoft-test-user)**  -toohave un equivalente de Britta Simon en SSO de SAML JIRA por Microsoft que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="2fe31-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - toohave a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2fe31-157">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2fe31-157">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2fe31-158">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="2fe31-158">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2fe31-159">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fe31-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2fe31-160">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en el SSO de SAML JIRA por la aplicación de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2fe31-160">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="2fe31-161">**tooconfigure inicio de sesión único en Azure AD con SSO de SAML JIRA por Microsoft, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2fe31-161">**tooconfigure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="2fe31-162">En el portal de Azure, en Hola Hola **JIRA SSO de SAML Microsoft** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-162">In hello Azure portal, on hello **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="2fe31-164">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2fe31-164">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="2fe31-166">En hello **JIRA SSO de SAML Domain de Microsoft y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2fe31-166">On hello **JIRA SAML SSO by Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="2fe31-168">a.</span><span class="sxs-lookup"><span data-stu-id="2fe31-168">a.</span></span> <span data-ttu-id="2fe31-169">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="2fe31-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="2fe31-170">b.</span><span class="sxs-lookup"><span data-stu-id="2fe31-170">b.</span></span> <span data-ttu-id="2fe31-171">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="2fe31-171">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="2fe31-172">c.</span><span class="sxs-lookup"><span data-stu-id="2fe31-172">c.</span></span> <span data-ttu-id="2fe31-173">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="2fe31-173">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2fe31-174">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="2fe31-174">These values are not real.</span></span> <span data-ttu-id="2fe31-175">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="2fe31-175">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2fe31-176">En caso de que sea una dirección URL con nombre, el puerto es opcional.</span><span class="sxs-lookup"><span data-stu-id="2fe31-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="2fe31-177">Estos valores se reciben durante la configuración de Hola de complemento de Jira, que se explica más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="2fe31-177">These values are received during hello configuration of Jira plugin, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="2fe31-178">Hola toogenerate **metadatos** dirección url, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2fe31-178">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="2fe31-179">a.</span><span class="sxs-lookup"><span data-stu-id="2fe31-179">a.</span></span> <span data-ttu-id="2fe31-180">Haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-180">Click **App registrations**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="2fe31-182">b.</span><span class="sxs-lookup"><span data-stu-id="2fe31-182">b.</span></span> <span data-ttu-id="2fe31-183">Haga clic en **extremos** tooopen **extremos** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2fe31-183">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="2fe31-185">c.</span><span class="sxs-lookup"><span data-stu-id="2fe31-185">c.</span></span> <span data-ttu-id="2fe31-186">Haga clic en hello copia botón toocopy **documento de metadatos de federación** dirección url y péguela en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="2fe31-186">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="2fe31-188">d.</span><span class="sxs-lookup"><span data-stu-id="2fe31-188">d.</span></span> <span data-ttu-id="2fe31-189">Ahora vaya toohello página de propiedades de **JIRA SSO de SAML Microsoft** copia hello y **Id. de aplicación** con **copia** botón y péguelo en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="2fe31-189">Now go toohello property page of **JIRA SAML SSO by Microsoft** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="2fe31-191">e.</span><span class="sxs-lookup"><span data-stu-id="2fe31-191">e.</span></span> <span data-ttu-id="2fe31-192">Generar hello **dirección URL de metadatos** con hello sigue el patrón: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` y copie este valor en el Bloc de notas como se utiliza para la configuración de Hola de complemento de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="2fe31-192">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for hello configuration of hello plugin.</span></span>

5. <span data-ttu-id="2fe31-193">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2fe31-193">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2fe31-195">Póngase en contacto con [Microsoft](mailto:waadpartners@microsoft.com) con hello siguiente información para hello JIRA complemento.</span><span class="sxs-lookup"><span data-stu-id="2fe31-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with hello following information for hello JIRA plugin.</span></span>
    
    *   <span data-ttu-id="2fe31-196">Nombre del cliente:</span><span class="sxs-lookup"><span data-stu-id="2fe31-196">Customer Name:</span></span>
    *   <span data-ttu-id="2fe31-197">Nombre del dominio principal:</span><span class="sxs-lookup"><span data-stu-id="2fe31-197">Primary domain name:</span></span>
    *   <span data-ttu-id="2fe31-198">Azure AD Premium: Sí/No (el complemento será de tooall disponible Hola cliente Free, Basic y Premium SKU)</span><span class="sxs-lookup"><span data-stu-id="2fe31-198">Azure AD Premium: Yes/No (Plugin will be available tooall     hello customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="2fe31-199">Número de usuarios que van a usar esta integración:</span><span class="sxs-lookup"><span data-stu-id="2fe31-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="2fe31-200">Versión de JIRA:</span><span class="sxs-lookup"><span data-stu-id="2fe31-200">JIRA Version:</span></span>
    *   <span data-ttu-id="2fe31-201">Comentarios:</span><span class="sxs-lookup"><span data-stu-id="2fe31-201">Comments:</span></span>

7. <span data-ttu-id="2fe31-202">En una ventana del explorador web diferente, inicie sesión en la instancia JIRA tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="2fe31-202">In a different web browser window, log in tooyour JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="2fe31-203">Mantenga el mouse sobre el icono de engranaje y haga clic en hello **complementos**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-203">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="2fe31-205">En la sección de la pestaña Complementos, haga clic en **Administrar complementos**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="2fe31-207">Cargar manualmente el complemento de hello proporcionado por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2fe31-207">Manually upload hello plugin provided by Microsoft.</span></span> <span data-ttu-id="2fe31-208">Una vez instalado el complemento de hello, aparece en **usuario instalado** sección de complementos de **administrar complemento** sección.</span><span class="sxs-lookup"><span data-stu-id="2fe31-208">Once hello plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="2fe31-209">Haga clic en **configurar** tooconfigure Hola nuevo complemento.</span><span class="sxs-lookup"><span data-stu-id="2fe31-209">Click **Configure** tooconfigure hello new plugin.</span></span>

12. <span data-ttu-id="2fe31-210">Siga estos pasos en la página de configuración:</span><span class="sxs-lookup"><span data-stu-id="2fe31-210">Perform following steps on configuration page:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="2fe31-212">a.</span><span class="sxs-lookup"><span data-stu-id="2fe31-212">a.</span></span> <span data-ttu-id="2fe31-213">En **dirección URL de metadatos** pegar hello **dirección URL de metadatos** generados a partir de Azure AD y haga clic en hello **resolver** botón.</span><span class="sxs-lookup"><span data-stu-id="2fe31-213">In **Metadata URL** paste hello **Metadata URL** generated from Azure AD and click hello **Resolve** button.</span></span> <span data-ttu-id="2fe31-214">Lee la dirección URL de metadatos de IdP de Hola y rellena toda la información de campos Hola.</span><span class="sxs-lookup"><span data-stu-id="2fe31-214">It reads hello IdP metadata URL and populates all hello fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="2fe31-215">La ubicación del Id. de usuario de SAML predeterminada es el identificador de nombre.</span><span class="sxs-lookup"><span data-stu-id="2fe31-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="2fe31-216">Puede cambiar esta opción de atributo tooan y escriba el nombre del atributo adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="2fe31-216">You can change this tooan attribute option and enter hello appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="2fe31-217">Asegúrese de que hay un solo certificado asignado en la aplicación hello de forma que no hay ningún error en la resolución de metadatos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2fe31-217">Ensure that there is only one certificate mapped against hello app so that there is no error in resolving hello metadata.</span></span> <span data-ttu-id="2fe31-218">Si hay varios certificados, después de resolver los metadatos de Hola, administrador obtiene un error.</span><span class="sxs-lookup"><span data-stu-id="2fe31-218">If there are multiple certificates, upon resolving hello metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="2fe31-219">b.</span><span class="sxs-lookup"><span data-stu-id="2fe31-219">b.</span></span> <span data-ttu-id="2fe31-220">Hola copia **identificador, la dirección URL de respuesta y la dirección URL de inicio de sesión** valores y péguelos en **identificador, la dirección URL de respuesta y la dirección URL de inicio de sesión** cuadros de texto respectivamente en **SSO de SAML de JIRA Domain de Microsoft y las direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2fe31-220">Copy hello **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="2fe31-221">c.</span><span class="sxs-lookup"><span data-stu-id="2fe31-221">c.</span></span> <span data-ttu-id="2fe31-222">En **el nombre del botón de inicio de sesión** nombre de tipo hello del botón de la organización quiere Hola usuarios toosee en pantalla de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="2fe31-222">In **Login Button Name** type hello name of button your organization wants hello users toosee on login screen.</span></span>

    <span data-ttu-id="2fe31-223">d.</span><span class="sxs-lookup"><span data-stu-id="2fe31-223">d.</span></span> <span data-ttu-id="2fe31-224">En **ubicaciones de Id. de usuario de SAML** seleccione **Id. de usuario está en elemento NameIdentifier de Hola de hello instrucción Subject** o **Id. de usuario está en un elemento Attribute**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-224">In **SAML User ID Locations** select either **User ID is in hello NameIdentifier element of hello Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="2fe31-225">Este identificador tiene toobe hello JIRA un identificador de usuario. Si no se encuentra el Id. de usuario de hello, sistema no permitirá que toolog a los usuarios en.</span><span class="sxs-lookup"><span data-stu-id="2fe31-225">This ID has toobe hello JIRA user id. If hello user id is not matched, then system will not allow users toolog in.</span></span> 
    
    <span data-ttu-id="2fe31-226">e.</span><span class="sxs-lookup"><span data-stu-id="2fe31-226">e.</span></span> <span data-ttu-id="2fe31-227">Si selecciona **Id. de usuario está en un elemento Attribute** opción, a continuación, en **nombre del atributo** cuadro de texto Nombre de Hola de tipo de atributo de Hola donde se esperaba el Id. de usuario.</span><span class="sxs-lookup"><span data-stu-id="2fe31-227">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type hello name of hello attribute where User Id is expected.</span></span> 

    <span data-ttu-id="2fe31-228">f.</span><span class="sxs-lookup"><span data-stu-id="2fe31-228">f.</span></span> <span data-ttu-id="2fe31-229">Si usas el dominio federado de hello (por ejemplo, etc. ADFS) con Azure AD, a continuación, haga clic en hello **habilitar Home Realm Discovery** opción y configure hello **nombre de dominio**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-229">If you are using hello federated domain (like ADFS etc.) with Azure AD, then click on hello **Enable Home Realm Discovery** option and configure hello **Domain Name**.</span></span>
    
    <span data-ttu-id="2fe31-230">g.</span><span class="sxs-lookup"><span data-stu-id="2fe31-230">g.</span></span> <span data-ttu-id="2fe31-231">En **nombre de dominio** escriba Hola dominio aquí el nombre en el caso de inicio de sesión de hello basada en AD FS.</span><span class="sxs-lookup"><span data-stu-id="2fe31-231">In **Domain Name** type hello domain name here in case of hello ADFS-based login.</span></span>

    <span data-ttu-id="2fe31-232">h.</span><span class="sxs-lookup"><span data-stu-id="2fe31-232">h.</span></span> <span data-ttu-id="2fe31-233">Comprobar **Habilitar cierre de sesión único** si desea toolog fuera de Azure AD cuando un usuario cierra la sesión de JIRA.</span><span class="sxs-lookup"><span data-stu-id="2fe31-233">Check **Enable Single Sign out** if you wish toolog out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="2fe31-234">i.</span><span class="sxs-lookup"><span data-stu-id="2fe31-234">i.</span></span> <span data-ttu-id="2fe31-235">Haga clic en **guardar** botón Configuración de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="2fe31-235">Click **Save** button toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="2fe31-236">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="2fe31-236">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2fe31-237">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="2fe31-237">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2fe31-238">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2fe31-238">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2fe31-239">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fe31-239">Creating an Azure AD test user</span></span>
<span data-ttu-id="2fe31-240">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="2fe31-240">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="2fe31-242">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2fe31-242">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2fe31-243">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="2fe31-243">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2fe31-245">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-245">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2fe31-247">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2fe31-247">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2fe31-249">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="2fe31-249">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2fe31-251">a.</span><span class="sxs-lookup"><span data-stu-id="2fe31-251">a.</span></span> <span data-ttu-id="2fe31-252">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-252">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2fe31-253">b.</span><span class="sxs-lookup"><span data-stu-id="2fe31-253">b.</span></span> <span data-ttu-id="2fe31-254">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2fe31-254">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2fe31-255">c.</span><span class="sxs-lookup"><span data-stu-id="2fe31-255">c.</span></span> <span data-ttu-id="2fe31-256">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-256">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2fe31-257">d.</span><span class="sxs-lookup"><span data-stu-id="2fe31-257">d.</span></span> <span data-ttu-id="2fe31-258">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-258">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="2fe31-259">Creación de un usuario de prueba de JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="2fe31-259">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="2fe31-260">toolog de los usuarios de Azure AD tooenable en tooJIRA el servidor local, se les deben aprovisionar en SSO de SAML JIRA por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2fe31-260">tooenable Azure AD users toolog in tooJIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="2fe31-261">Para JIRA SAML SSO by Microsoft, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="2fe31-261">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="2fe31-262">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2fe31-262">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="2fe31-263">Inicie sesión en tooyour JIRA de servidor local como administrador.</span><span class="sxs-lookup"><span data-stu-id="2fe31-263">Log in tooyour JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="2fe31-264">Mantenga el mouse sobre el icono de engranaje y haga clic en hello **administración de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-264">Hover on cog and click hello **User management**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="2fe31-266">Son tooenter de página de acceso redirigida tooAdministrator **contraseña** y haga clic en **confirmar** botón.</span><span class="sxs-lookup"><span data-stu-id="2fe31-266">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![Agregar empleado](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="2fe31-268">En la sección de la pestaña **Administración de usuarios**, haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-268">Under **User management** tab section, click **create user**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="2fe31-270">En hello **"Crear nuevo usuario"** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="2fe31-270">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Agregar empleado](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="2fe31-272">a.</span><span class="sxs-lookup"><span data-stu-id="2fe31-272">a.</span></span> <span data-ttu-id="2fe31-273">Hola **dirección de correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2fe31-273">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="2fe31-274">b.</span><span class="sxs-lookup"><span data-stu-id="2fe31-274">b.</span></span> <span data-ttu-id="2fe31-275">Hola **nombre completo** cuadro de texto, nombre completo del tipo de usuario de hello como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2fe31-275">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="2fe31-276">c.</span><span class="sxs-lookup"><span data-stu-id="2fe31-276">c.</span></span> <span data-ttu-id="2fe31-277">Hola **nombre de usuario** Hola de tipo de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2fe31-277">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="2fe31-278">d.</span><span class="sxs-lookup"><span data-stu-id="2fe31-278">d.</span></span> <span data-ttu-id="2fe31-279">Hola **contraseña** cuadro de texto, escriba la contraseña de saludo del usuario.</span><span class="sxs-lookup"><span data-stu-id="2fe31-279">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="2fe31-280">e.</span><span class="sxs-lookup"><span data-stu-id="2fe31-280">e.</span></span> <span data-ttu-id="2fe31-281">Haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-281">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2fe31-282">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2fe31-282">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2fe31-283">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooJIRA SSO de SAML por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2fe31-283">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJIRA SAML SSO by Microsoft.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="2fe31-285">**tooassign Britta Simon tooJIRA SSO de SAML por Microsoft, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2fe31-285">**tooassign Britta Simon tooJIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="2fe31-286">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-286">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2fe31-288">En la lista de aplicaciones de hello, seleccione **JIRA SSO de SAML Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-288">In hello applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="2fe31-290">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-290">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="2fe31-292">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-292">Click **Add** button.</span></span> <span data-ttu-id="2fe31-293">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-293">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="2fe31-295">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="2fe31-295">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2fe31-296">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-296">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2fe31-297">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2fe31-297">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2fe31-298">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="2fe31-298">Testing single sign-on</span></span>

<span data-ttu-id="2fe31-299">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2fe31-299">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2fe31-300">Al hacer clic en hello SSO de SAML JIRA por mosaico de Microsoft en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour SSO de SAML JIRA por la aplicación de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2fe31-300">When you click hello JIRA SAML SSO by Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="2fe31-301">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2fe31-301">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2fe31-302">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2fe31-302">Additional resources</span></span>

* [<span data-ttu-id="2fe31-303">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2fe31-303">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2fe31-304">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2fe31-304">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png


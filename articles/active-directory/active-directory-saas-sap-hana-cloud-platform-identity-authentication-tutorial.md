---
title: "Tutorial: Integración de Azure Active Directory con SAP HANA Cloud Platform Identity Authentication | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SAP HANA autenticación de la identidad de plataforma de nube."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="aa088-103">Tutorial: Integración de Azure Active Directory con SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="aa088-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="aa088-104">En este tutorial, aprenderá cómo toointegrate SAP HANA autenticación de identidades de plataforma de nube con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aa088-104">In this tutorial, you learn how toointegrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="aa088-105">Autenticación de la identidad de plataforma de nube de SAP HANA se utiliza como un proxy IdP tooaccess las aplicaciones SAP con Azure AD como Hola IdP principal.</span><span class="sxs-lookup"><span data-stu-id="aa088-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP tooaccess SAP applications using Azure AD as hello main IdP.</span></span>

<span data-ttu-id="aa088-106">Integración de autenticación de la identidad de plataforma de nube de SAP HANA con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="aa088-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="aa088-107">Puede controlar en Azure AD que tenga acceso tooSAP aplicación</span><span class="sxs-lookup"><span data-stu-id="aa088-107">You can control in Azure AD who has access tooSAP application</span></span>
- <span data-ttu-id="aa088-108">Puede habilitar los usuarios tooautomatically get tooSAP ha iniciado sesión con las aplicaciones inicio de sesión único (SSO) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa088-108">You can enable your users tooautomatically get signed-on tooSAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="aa088-109">Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="aa088-109">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="aa088-110">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aa088-110">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="aa088-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="aa088-111">Prerequisites</span></span>

<span data-ttu-id="aa088-112">tooconfigure integración de Azure AD con autenticación de la identidad de plataforma de nube de SAP HANA, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="aa088-112">tooconfigure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need hello following items:</span></span>

- <span data-ttu-id="aa088-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa088-113">An Azure AD subscription</span></span>
- <span data-ttu-id="aa088-114">Una suscripción de **SAP HANA Cloud Platform Identity Authentication** con el inicio de sesión único habilitado</span><span class="sxs-lookup"><span data-stu-id="aa088-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="aa088-115">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="aa088-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="aa088-116">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="aa088-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aa088-117">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="aa088-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="aa088-118">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aa088-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aa088-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="aa088-119">Scenario description</span></span>
<span data-ttu-id="aa088-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="aa088-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="aa088-121">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="aa088-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aa088-122">Agregar la autenticación de la identidad de plataforma de nube de SAP HANA desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="aa088-122">Adding SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
2. <span data-ttu-id="aa088-123">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa088-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="aa088-124">Antes de entrar en detalles técnicos de hello, resulta vital toounderstand conceptos de hello en que va toolook.</span><span class="sxs-lookup"><span data-stu-id="aa088-124">Before diving into hello technical details, it is vital toounderstand hello concepts you're going toolook at.</span></span> <span data-ttu-id="aa088-125">Hola federación de Active Directory de Azure y autenticación de la identidad de plataforma de nube de SAP HANA permite tooimplement SSO a través de aplicaciones o servicios protegidos por AAD (como un IdP) con aplicaciones de SAP y servicios protegidos por identidad de plataforma de nube de SAP HANA Autenticación.</span><span class="sxs-lookup"><span data-stu-id="aa088-125">hello SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you tooimplement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="aa088-126">Actualmente, autenticación de la identidad de plataforma de nube de SAP HANA actúa como un proveedor de identidades de Proxy tooSAP-aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="aa088-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider tooSAP-applications.</span></span> <span data-ttu-id="aa088-127">A su vez, Azure Active Directory actúa como Hola iniciales de proveedor de identidades en este programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="aa088-127">Azure Active Directory in turn acts as hello leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="aa088-128">Hola siguiente diagrama muestra cómo hacerlo:</span><span class="sxs-lookup"><span data-stu-id="aa088-128">hello following diagram illustrates this:</span></span>    

![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="aa088-130">Con esta configuración, su inquilino de SAP HANA Cloud Platform Identity Authentication se configurará como una aplicación de confianza en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aa088-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="aa088-131">Todas las aplicaciones de SAP y los servicios que desee tooprotect a través de esta manera se configuran posteriormente en la consola de administración de autenticación de la identidad de plataforma de nube de SAP HANA Hola!</span><span class="sxs-lookup"><span data-stu-id="aa088-131">All SAP applications and services you want tooprotect through this way are subsequently configured in hello SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="aa088-132">Esto significa que esa autorización para conceder acceso tooSAP aplicaciones y servicios necesidades tootake lugar en la autenticación de la identidad de plataforma de nube de SAP HANA para dicha configuración (como autorización tooconfiguring lugar en Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="aa088-132">This means that authorization for granting access tooSAP applications and services needs tootake place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed tooconfiguring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="aa088-133">Mediante la configuración de autenticación de la identidad de plataforma de nube de SAP HANA como una aplicación a través de hello Azure Active Directory Marketplace, no es necesario tootake atención configurar notificaciones individuales necesarios y las aserciones de SAML y transformaciones necesitan tooproduce un token de autenticación válido para las aplicaciones de SAP.</span><span class="sxs-lookup"><span data-stu-id="aa088-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through hello Azure Active Directory Marketplace, you don't need tootake care of configuring needed individual claims / SAML assertions and transformations needed tooproduce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="aa088-134">Actualmente, el SSO web solo se ha probado en ambas soluciones.</span><span class="sxs-lookup"><span data-stu-id="aa088-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="aa088-135">Aunque los flujos necesarios para establecer comunicación de aplicación a API o de API a API deberían funcionar, todavía no se han probado.</span><span class="sxs-lookup"><span data-stu-id="aa088-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="aa088-136">Sin embargo, sí que se hará en actividades posteriores.</span><span class="sxs-lookup"><span data-stu-id="aa088-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a><span data-ttu-id="aa088-137">Agregar autenticación de la identidad de plataforma de nube de SAP HANA desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="aa088-137">Add SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
<span data-ttu-id="aa088-138">integración de hello tooconfigure de autenticación de la identidad de plataforma de nube de SAP HANA en Azure AD, deberá tooadd autenticación de la identidad de plataforma de nube de SAP HANA en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="aa088-138">tooconfigure hello integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="aa088-139">**tooadd autenticación de identidad de SAP HANA en la nube plataforma desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aa088-139">**tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa088-140">Hola [ **portal de administración de Azure**](https://portal.azure.com), en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="aa088-140">In hello [**Azure Management portal**](https://portal.azure.com), on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aa088-142">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="aa088-142">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="aa088-143">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="aa088-143">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="aa088-145">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa088-145">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="aa088-147">En el cuadro de búsqueda de hello, escriba **autenticación de la identidad de plataforma de nube de SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="aa088-147">In hello search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="aa088-149">En el panel de resultados de hello, seleccione **autenticación de la identidad de plataforma de nube de SAP HANA**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="aa088-149">In hello results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="aa088-151">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa088-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="aa088-152">En esta sección, se configura y prueba el inicio de sesión único de Azure AD con SAP HANA Cloud Platform Identity Authentication con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="aa088-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aa088-153">Para toowork SSO, Azure AD necesita tooknow qué usuario equivalente de hello en autenticación de la identidad de plataforma de nube de SAP HANA es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa088-153">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA Cloud Platform Identity Authentication is tooa user in Azure AD.</span></span> <span data-ttu-id="aa088-154">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en autenticación de la identidad de plataforma de nube de SAP HANA debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="aa088-154">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA Cloud Platform Identity Authentication needs toobe established.</span></span>

<span data-ttu-id="aa088-155">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** de autenticación de la identidad de plataforma de nube de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="aa088-155">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="aa088-156">tooconfigure y prueba de Azure AD SSO con la autenticación de la identidad de plataforma de nube de SAP HANA, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="aa088-156">tooconfigure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="aa088-157">**[Configuración del inicio de sesión único en Azure AD](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="aa088-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="aa088-158">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa088-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aa088-159">**[Crear un usuario de prueba de autenticación de la identidad de plataforma de nube de SAP HANA](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave un equivalente de Britta Simon en la plataforma de identidad autenticación SAP HANA en la nube es representación toohello vinculado Azure AD de ella.</span><span class="sxs-lookup"><span data-stu-id="aa088-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - toohave a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="aa088-160">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="aa088-160">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aa088-161">**[Probar el inicio de sesión único](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="aa088-161">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="aa088-162">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa088-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="aa088-163">En esta sección, habilita el SSO de Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación de autenticación de la identidad de plataforma de nube de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="aa088-163">In this section, you enable Azure AD SSO in hello Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="aa088-164">Aplicación de autenticación de la identidad de plataforma de nube de SAP HANA espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="aa088-164">SAP HANA Cloud Platform Identity Authentication application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="aa088-165">Puede administrar valores de hello de estos atributos de Hola "**atributos de usuario**" sección en la página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="aa088-165">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="aa088-166">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="aa088-166">hello following screenshot shows an example for this.</span></span>

![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="aa088-168">**tooconfigure SSO de AD de Azure con la autenticación de identidades de plataforma de nube de SAP HANA, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aa088-168">**tooconfigure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa088-169">En el portal de administración de Azure de hello, en hello **autenticación de la identidad de plataforma de nube de SAP HANA** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="aa088-169">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="aa088-171">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="aa088-171">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único][5]

3. <span data-ttu-id="aa088-173">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo, si la aplicación SAP espera un atributo, por ejemplo "firstName".</span><span class="sxs-lookup"><span data-stu-id="aa088-173">In hello **User Attributes** section on hello **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="aa088-174">En el cuadro de diálogo de atributos de token de SAML de hello, Agregar atributo de "firstName" Hola.</span><span class="sxs-lookup"><span data-stu-id="aa088-174">On hello SAML token attributes dialog, add hello "firstName" attribute.</span></span>
 1. <span data-ttu-id="aa088-175">Haga clic en **Agregar atributo** tooopen hello **Agregar atributo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa088-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
 
    ![Configurar inicio de sesión único][6]

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="aa088-178">Hola **nombre del atributo** cuadro de texto, nombre de atributo de tipo hello "firstName".</span><span class="sxs-lookup"><span data-stu-id="aa088-178">In hello **Attribute Name** textbox, type hello attribute name "firstName".</span></span>
 3. <span data-ttu-id="aa088-179">De hello **valor del atributo** lista, el valor del atributo Hola seleccione "user.givenname".</span><span class="sxs-lookup"><span data-stu-id="aa088-179">From hello **Attribute Value** list, select hello attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="aa088-180">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="aa088-180">Click **Ok**.</span></span>

4. <span data-ttu-id="aa088-181">En hello **dominio de autenticación de la identidad de plataforma de SAP HANA en la nube y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="aa088-181">On hello **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="aa088-183">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba el inicio de sesión de Hola en dirección URL para la aplicación de SAP de hello.</span><span class="sxs-lookup"><span data-stu-id="aa088-183">In hello **Sign On URL** textbox, type hello sign on URL for hello SAP application.</span></span>
 2. <span data-ttu-id="aa088-184">Hola **identificador** cuadro de texto, valor de Hola de tipo siguiente patrón:`<entity-id>.accounts.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="aa088-184">In hello **Identifier** textbox, type hello value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="aa088-185">Si no sabe este valor, siga documentación de autenticación de la identidad de plataforma de nube de SAP HANA hello en [inquilino SAML 2.0 configuración](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span><span class="sxs-lookup"><span data-stu-id="aa088-185">If you don't know this value, please follow hello SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="aa088-186">En hello **configuración de autenticación de identidad de SAP HANA Cloud plataforma** sección, haga clic en **configurar autenticación de identidad de plataforma de SAP HANA en la nube** tooopen **configurardeiniciodesesión** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa088-186">On hello **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** tooopen **Configure sign-on** dialog.</span></span> <span data-ttu-id="aa088-187">A continuación, haga clic en **metadatos XML de SAML** y guarde el archivo hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="aa088-187">Then, click on **SAML XML Metadata** and save hello file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="aa088-190">tooget SSO configurado para la aplicación, vaya tooSAP consola de administración de la autenticación de identidad de HANA nube plataforma.</span><span class="sxs-lookup"><span data-stu-id="aa088-190">tooget SSO configured for your application, go tooSAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="aa088-191">dirección URL de Hello tiene Hola siguiente patrón:`https://<tenant-id>.accounts.ondemand.com/admin`</span><span class="sxs-lookup"><span data-stu-id="aa088-191">hello URL has hello following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="aa088-192">A continuación, siga documentación hello en autenticación de la identidad de plataforma de nube de SAP HANA demasiado[configurar Microsoft Azure AD como proveedor de identidad corporativa en autenticación de la identidad de plataforma de nube de SAP HANA](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span><span class="sxs-lookup"><span data-stu-id="aa088-192">Then, follow hello documentation on SAP HANA Cloud Platform Identity Authentication too[Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="aa088-193">En el portal de administración de Azure de hello, haga clic en **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="aa088-193">In hello Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="aa088-194">Continuar Hola siguientes pasos únicamente si desea tooadd y habilitar SSO para otra aplicación de SAP.</span><span class="sxs-lookup"><span data-stu-id="aa088-194">Continue hello following steps only if you want tooadd and enable SSO for another SAP application.</span></span> <span data-ttu-id="aa088-195">Repita los pasos en hello sección "Agregar SAP HANA nube plataforma autenticación de la identidad de la Galería de Hola" tooadd otra instancia de la autenticación de la identidad de plataforma de nube de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="aa088-195">Repeat steps under hello section “Adding SAP HANA Cloud Platform Identity Authentication from hello gallery” tooadd another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="aa088-196">En el portal de administración de Azure de hello, en hello **autenticación de la identidad de plataforma de nube de SAP HANA** página de integración de aplicaciones, haga clic en **en el inicio de sesión vinculado**.</span><span class="sxs-lookup"><span data-stu-id="aa088-196">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![Configuración del inicio de sesión vinculado](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="aa088-198">A continuación, guarde la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa088-198">Then, save hello configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="aa088-199">nueva aplicación de Hello aprovecharán la configuración de SSO de hello para la aplicación de SAP de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="aa088-199">hello new application will leverage hello SSO configuration for hello previous SAP application.</span></span> <span data-ttu-id="aa088-200">Asegúrese de que se use Hola mismo proveedores de identidad corporativa en hello consola de administración de autenticación de SAP HANA nube plataforma de identidad.</span><span class="sxs-lookup"><span data-stu-id="aa088-200">Please make sure you use hello same Corporate Identity Providers in hello SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="aa088-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa088-201">Create an Azure AD test user</span></span>
<span data-ttu-id="aa088-202">objetivo de Hola de esta sección es toocreate un usuario de prueba en el nuevo portal de hello llamado a Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa088-202">hello objective of this section is toocreate a test user in hello new portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="aa088-204">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aa088-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa088-205">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="aa088-205">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aa088-207">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="aa088-207">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aa088-209">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa088-209">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aa088-211">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="aa088-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="aa088-213">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aa088-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="aa088-214">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="aa088-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="aa088-215">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="aa088-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>
  4. <span data-ttu-id="aa088-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="aa088-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="aa088-217">Creación de un usuario de prueba de SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="aa088-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="aa088-218">No es necesario toocreate un usuario en la autenticación de la identidad de plataforma de nube de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="aa088-218">You don't need toocreate an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="aa088-219">Los usuarios que están en el almacén del usuario de hello Azure AD pueden usar la funcionalidad SSO de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa088-219">Users who are in hello Azure AD user store can use hello SSO functionality.</span></span>

<span data-ttu-id="aa088-220">Autenticación de la identidad de plataforma de nube de SAP HANA es compatible con la opción de federación de identidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa088-220">SAP HANA Cloud Platform Identity Authentication supports hello Identity Federation option.</span></span> <span data-ttu-id="aa088-221">Esta opción permite Hola aplicación toocheck si los usuarios de hello autenticados por el proveedor de identidad corporativa Hola existen en hello almacén de SAP HANA en la nube plataforma de identidad de autenticación de usuario.</span><span class="sxs-lookup"><span data-stu-id="aa088-221">This option allows hello application toocheck if hello users authenticated by hello corporate identity provider exist in hello user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="aa088-222">En la configuración predeterminada de hello, opción de federación de identidades de hello está deshabilitada.</span><span class="sxs-lookup"><span data-stu-id="aa088-222">In hello default setting, hello Identity Federation option is disabled.</span></span> <span data-ttu-id="aa088-223">Si se habilita la federación de identidades, solo los usuarios de Hola que se importan de autenticación de la identidad de plataforma de nube de SAP HANA son tooaccess capaz de aplicación de hello.</span><span class="sxs-lookup"><span data-stu-id="aa088-223">If Identity Federation is enabled, only hello users that are imported in SAP HANA Cloud Platform Identity Authentication are able tooaccess hello application.</span></span> 

<span data-ttu-id="aa088-224">Para obtener más información sobre cómo tooenable o deshabilitar la federación de identidades con autenticación de identidades de plataforma de nube de SAP HANA, vea Habilitar la federación de identidades con autenticación de identidades de plataforma de nube de SAP HANA en [Configurar federación de identidades con hello almacén de SAP HANA nube plataforma de identidad de autenticación de usuario. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span><span class="sxs-lookup"><span data-stu-id="aa088-224">For more information about how tooenable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with hello User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="aa088-225">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa088-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="aa088-226">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooSAP acceso HANA autenticación de la identidad de plataforma de nube.</span><span class="sxs-lookup"><span data-stu-id="aa088-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooSAP HANA Cloud Platform Identity Authentication.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="aa088-228">**tooassign Britta Simon tooSAP autenticación de identidades de plataforma de nube de HANA, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="aa088-228">**tooassign Britta Simon tooSAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa088-229">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="aa088-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="aa088-231">En la lista de aplicaciones de hello, seleccione **autenticación de la identidad de plataforma de nube de SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="aa088-231">In hello applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="aa088-233">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="aa088-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="aa088-235">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="aa088-235">Click **Add** button.</span></span> <span data-ttu-id="aa088-236">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="aa088-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="aa088-238">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa088-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="aa088-239">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="aa088-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aa088-240">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="aa088-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="aa088-241">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="aa088-241">Test single sign-on</span></span>

<span data-ttu-id="aa088-242">En esta sección, probará la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="aa088-242">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="aa088-243">Al hacer clic en icono de autenticación de la identidad de plataforma de nube de SAP HANA Hola Hola Panel de acceso, deberá obtener la aplicación de autenticación de la identidad de plataforma de nube de SAP HANA tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="aa088-243">When you click hello SAP HANA Cloud Platform Identity Authentication tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="aa088-244">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="aa088-244">Additional resources</span></span>

* [<span data-ttu-id="aa088-245">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa088-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aa088-246">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aa088-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png
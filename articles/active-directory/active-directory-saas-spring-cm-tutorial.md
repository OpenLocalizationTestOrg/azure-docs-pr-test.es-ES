---
title: "Tutorial: Integración de Azure Active Directory con SpringCM | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SpringCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 12c8ebe765e2c6e61115256e9343d90ec132e1f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="8af02-103">Tutorial: integración de Azure Active Directory con SprinkCM</span><span class="sxs-lookup"><span data-stu-id="8af02-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="8af02-104">En este tutorial, aprenderá cómo toointegrate SpringCM con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8af02-104">In this tutorial, you learn how toointegrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8af02-105">Integración de SpringCM con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8af02-105">Integrating SpringCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8af02-106">Puede controlar en Azure AD que tenga acceso tooSpringCM</span><span class="sxs-lookup"><span data-stu-id="8af02-106">You can control in Azure AD who has access tooSpringCM</span></span>
- <span data-ttu-id="8af02-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSpringCM (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8af02-107">You can enable your users tooautomatically get signed-on tooSpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8af02-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8af02-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8af02-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8af02-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8af02-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8af02-110">Prerequisites</span></span>

<span data-ttu-id="8af02-111">integración de Azure AD con SpringCM tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8af02-111">tooconfigure Azure AD integration with SpringCM, you need hello following items:</span></span>

- <span data-ttu-id="8af02-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8af02-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8af02-113">Una suscripción habilitada para el inicio de sesión único en SpringCM</span><span class="sxs-lookup"><span data-stu-id="8af02-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8af02-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8af02-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8af02-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8af02-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8af02-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8af02-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8af02-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8af02-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8af02-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8af02-118">Scenario description</span></span>
<span data-ttu-id="8af02-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8af02-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8af02-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="8af02-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8af02-121">Agregar SpringCM desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8af02-121">Adding SpringCM from hello gallery</span></span>
2. <span data-ttu-id="8af02-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8af02-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-hello-gallery"></a><span data-ttu-id="8af02-123">Agregar SpringCM desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8af02-123">Adding SpringCM from hello gallery</span></span>
<span data-ttu-id="8af02-124">integración de hello tooconfigure de SpringCM en Azure AD, deberá tooadd SpringCM de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="8af02-124">tooconfigure hello integration of SpringCM into Azure AD, you need tooadd SpringCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8af02-125">**tooadd SpringCM de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8af02-125">**tooadd SpringCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8af02-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8af02-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8af02-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8af02-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8af02-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8af02-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="8af02-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8af02-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="8af02-133">En el cuadro de búsqueda de hello, escriba **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="8af02-133">In hello search box, type **SpringCM**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="8af02-135">En el panel de resultados de hello, seleccione **SpringCM**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8af02-135">In hello results panel, select **SpringCM**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8af02-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8af02-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8af02-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SpringCM con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8af02-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8af02-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en SpringCM es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8af02-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SpringCM is tooa user in Azure AD.</span></span> <span data-ttu-id="8af02-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SpringCM debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="8af02-140">In other words, a link relationship between an Azure AD user and hello related user in SpringCM needs toobe established.</span></span>

<span data-ttu-id="8af02-141">En SpringCM, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8af02-141">In SpringCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8af02-142">tooconfigure y prueba de inicio de sesión único en Azure AD con SpringCM, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8af02-142">tooconfigure and test Azure AD single sign-on with SpringCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8af02-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="8af02-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8af02-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8af02-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8af02-145">**[Crear un usuario de prueba de SpringCM](#creating-a-springcm-test-user)**  -toohave un equivalente de Britta Simon en SpringCM que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="8af02-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - toohave a counterpart of Britta Simon in SpringCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8af02-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8af02-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8af02-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8af02-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8af02-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8af02-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8af02-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de SpringCM.</span><span class="sxs-lookup"><span data-stu-id="8af02-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="8af02-150">**inicio de sesión único en Azure AD tooconfigure con SpringCM, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8af02-150">**tooconfigure Azure AD single sign-on with SpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="8af02-151">En el portal de Azure, en Hola Hola **SpringCM** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8af02-151">In hello Azure portal, on hello **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8af02-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8af02-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="8af02-155">En hello **SpringCM dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8af02-155">On hello **SpringCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="8af02-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="8af02-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8af02-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="8af02-158">This value is not real.</span></span> <span data-ttu-id="8af02-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="8af02-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="8af02-160">Póngase en contacto con [equipo de soporte técnico de cliente de SpringCM](https://knowledge.springcm.com/support) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="8af02-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="8af02-161">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Raw)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8af02-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="8af02-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8af02-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8af02-165">En hello **configuración de SpringCM** sección, haga clic en **configurar SpringCM** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="8af02-165">On hello **SpringCM Configuration** section, click **Configure SpringCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8af02-166">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="8af02-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="8af02-168">En una ventana del explorador web diferente, inicie sesión en tooyour **SpringCM** como administrador.</span><span class="sxs-lookup"><span data-stu-id="8af02-168">In a different web browser window, sign on tooyour **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="8af02-169">En el menú de hello en la parte superior de hello, haga clic en **ir a**, haga clic en **preferencias**y, a continuación, en hello **preferencias de cuenta** sección, haga clic en **SSO de SAML**.</span><span class="sxs-lookup"><span data-stu-id="8af02-169">In hello menu on hello top, click **GO TO**, click **Preferences**, and then, in hello **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="8af02-170">![SSO DE SAML](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SSO DE SAML")</span><span class="sxs-lookup"><span data-stu-id="8af02-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="8af02-171">En la sección de configuración del proveedor de identidades de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8af02-171">In hello Identity Provider Configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="8af02-172">![Configuración del proveedor de identidades](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Configuración del proveedor de identidades")</span><span class="sxs-lookup"><span data-stu-id="8af02-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="8af02-173">a.</span><span class="sxs-lookup"><span data-stu-id="8af02-173">a.</span></span> <span data-ttu-id="8af02-174">tooupload el certificado descargado de Azure Active Directory, haga clic en **Seleccionar certificado de emisor** o **cambiar el certificado de emisor**.</span><span class="sxs-lookup"><span data-stu-id="8af02-174">tooupload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="8af02-175">b.</span><span class="sxs-lookup"><span data-stu-id="8af02-175">b.</span></span> <span data-ttu-id="8af02-176">Pegar **Id. de entidad SAML** valor, que ha copiado desde el portal de Azure en hello **emisor** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="8af02-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into hello **Issuer** textbox.</span></span>
    
    <span data-ttu-id="8af02-177">c.</span><span class="sxs-lookup"><span data-stu-id="8af02-177">c.</span></span> <span data-ttu-id="8af02-178">Pegar **SAML Single Sign-On dirección URL del servicio** valor, que haya copiado desde Hola portal de Azure en hello **extremo iniciado por el proveedor de servicio (SP)** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="8af02-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="8af02-179">d.</span><span class="sxs-lookup"><span data-stu-id="8af02-179">d.</span></span> <span data-ttu-id="8af02-180">Seleccione **SAML Enabled** (SAML habilitado) como **Enable** (Habilitar).</span><span class="sxs-lookup"><span data-stu-id="8af02-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="8af02-181">e.</span><span class="sxs-lookup"><span data-stu-id="8af02-181">e.</span></span> <span data-ttu-id="8af02-182">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="8af02-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="8af02-183">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="8af02-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8af02-184">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="8af02-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8af02-185">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8af02-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8af02-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8af02-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="8af02-187">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="8af02-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="8af02-189">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8af02-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8af02-190">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8af02-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8af02-192">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8af02-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8af02-194">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8af02-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8af02-196">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="8af02-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8af02-198">a.</span><span class="sxs-lookup"><span data-stu-id="8af02-198">a.</span></span> <span data-ttu-id="8af02-199">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8af02-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8af02-200">b.</span><span class="sxs-lookup"><span data-stu-id="8af02-200">b.</span></span> <span data-ttu-id="8af02-201">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8af02-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8af02-202">c.</span><span class="sxs-lookup"><span data-stu-id="8af02-202">c.</span></span> <span data-ttu-id="8af02-203">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8af02-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8af02-204">d.</span><span class="sxs-lookup"><span data-stu-id="8af02-204">d.</span></span> <span data-ttu-id="8af02-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8af02-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="8af02-206">Creación de un usuario de prueba de SpringCM</span><span class="sxs-lookup"><span data-stu-id="8af02-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="8af02-207">toolog de los usuarios de Azure Active Directory tooenable en tooSpringCM, se les deben aprovisionar en SpringCM.</span><span class="sxs-lookup"><span data-stu-id="8af02-207">tooenable Azure Active Directory users toolog in tooSpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="8af02-208">En caso de hello de SpringCM, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="8af02-208">In hello case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="8af02-209">Para obtener más información, consulte [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user) (Creación y edición de un usuario de SpringCM).</span><span class="sxs-lookup"><span data-stu-id="8af02-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="8af02-210">**tooprovision un tooSpringCM de cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8af02-210">**tooprovision a user account tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="8af02-211">Inicie sesión en tooyour **SpringCM** como administrador.</span><span class="sxs-lookup"><span data-stu-id="8af02-211">Log in tooyour **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="8af02-212">Haga clic en **GOTO** y, luego, en **ADDRESS BOOK** (LIBRETA DE DIRECCIONES).</span><span class="sxs-lookup"><span data-stu-id="8af02-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="8af02-213">![Creación de usuarios](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Creación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="8af02-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="8af02-214">Haga clic en **Crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="8af02-214">Click **Create User**.</span></span>

4. <span data-ttu-id="8af02-215">Seleccione un **Rol de usuario**.</span><span class="sxs-lookup"><span data-stu-id="8af02-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="8af02-216">Seleccione **Enviar correo electrónico de activación**.</span><span class="sxs-lookup"><span data-stu-id="8af02-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="8af02-217">Tipo hello nombre, apellido y dirección de correo electrónico de una cuenta de usuario válida de Azure Active Directory que quiera tooprovision en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="8af02-217">Type hello first name, last name, and email address of a valid Azure Active Directory user account you want tooprovision into hello related textboxes.</span></span>

7. <span data-ttu-id="8af02-218">Agregar Hola usuario tooa **grupo de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="8af02-218">Add hello user tooa **Security group**.</span></span>

8. <span data-ttu-id="8af02-219">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="8af02-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="8af02-220">Puede usar cualquier otra SpringCM usuario cuenta herramienta de creación o las API proporcionadas por SpringCM tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="8af02-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM tooprovision AAD user accounts.</span></span>  
  > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8af02-221">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8af02-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8af02-222">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSpringCM.</span><span class="sxs-lookup"><span data-stu-id="8af02-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringCM.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="8af02-224">**tooassign Britta Simon tooSpringCM, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8af02-224">**tooassign Britta Simon tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="8af02-225">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8af02-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8af02-227">En la lista de aplicaciones de hello, seleccione **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="8af02-227">In hello applications list, select **SpringCM**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="8af02-229">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8af02-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="8af02-231">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8af02-231">Click **Add** button.</span></span> <span data-ttu-id="8af02-232">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8af02-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="8af02-234">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="8af02-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8af02-235">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8af02-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8af02-236">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8af02-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8af02-237">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="8af02-237">Testing single sign-on</span></span>

<span data-ttu-id="8af02-238">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="8af02-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="8af02-239">Al hacer clic en icono de SpringCM Hola Hola Panel de acceso, deberá obtener la aplicación de SpringCM tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="8af02-239">When you click hello SpringCM tile in hello Access Panel, you should get automatically signed-on tooyour SpringCM application.</span></span>

<span data-ttu-id="8af02-240">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8af02-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8af02-241">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8af02-241">Additional resources</span></span>

* [<span data-ttu-id="8af02-242">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8af02-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8af02-243">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8af02-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png


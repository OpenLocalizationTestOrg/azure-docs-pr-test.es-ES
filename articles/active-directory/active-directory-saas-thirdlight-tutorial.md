---
title: "Tutorial: integración de Azure Active Directory con ThirdLight | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y ThirdLight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a510e514f6a8c4e89220b9a6f6db29668b451b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="3a4a8-103">Tutorial: integración de Azure Active Directory con ThirdLight</span><span class="sxs-lookup"><span data-stu-id="3a4a8-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="3a4a8-104">En este tutorial, aprenderá cómo toointegrate ThirdLight con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a4a8-104">In this tutorial, you learn how toointegrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a4a8-105">Integración ThirdLight con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3a4a8-105">Integrating ThirdLight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3a4a8-106">Puede controlar en Azure AD que tenga acceso tooThirdLight</span><span class="sxs-lookup"><span data-stu-id="3a4a8-106">You can control in Azure AD who has access tooThirdLight</span></span>
- <span data-ttu-id="3a4a8-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooThirdLight (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a4a8-107">You can enable your users tooautomatically get signed-on tooThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3a4a8-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3a4a8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3a4a8-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3a4a8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a4a8-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3a4a8-110">Prerequisites</span></span>

<span data-ttu-id="3a4a8-111">integración de Azure AD con ThirdLight tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3a4a8-111">tooconfigure Azure AD integration with ThirdLight, you need hello following items:</span></span>

- <span data-ttu-id="3a4a8-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a4a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a4a8-113">Una suscripción habilitada para el inicio de sesión único en ThirdLight</span><span class="sxs-lookup"><span data-stu-id="3a4a8-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a4a8-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a4a8-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3a4a8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a4a8-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3a4a8-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a4a8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a4a8-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3a4a8-118">Scenario description</span></span>
<span data-ttu-id="3a4a8-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a4a8-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="3a4a8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a4a8-121">Agregar ThirdLight desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3a4a8-121">Adding ThirdLight from hello gallery</span></span>
2. <span data-ttu-id="3a4a8-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a4a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-hello-gallery"></a><span data-ttu-id="3a4a8-123">Agregar ThirdLight desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3a4a8-123">Adding ThirdLight from hello gallery</span></span>
<span data-ttu-id="3a4a8-124">integración de hello tooconfigure de ThirdLight en Azure AD, deberá tooadd ThirdLight de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-124">tooconfigure hello integration of ThirdLight into Azure AD, you need tooadd ThirdLight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3a4a8-125">**tooadd ThirdLight de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3a4a8-125">**tooadd ThirdLight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a4a8-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3a4a8-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3a4a8-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3a4a8-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3a4a8-133">En el cuadro de búsqueda de hello, escriba **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-133">In hello search box, type **ThirdLight**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. <span data-ttu-id="3a4a8-135">En el panel de resultados de hello, seleccione **ThirdLight**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-135">In hello results panel, select **ThirdLight**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3a4a8-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a4a8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3a4a8-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con ThirdLight con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3a4a8-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en ThirdLight es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThirdLight is tooa user in Azure AD.</span></span> <span data-ttu-id="3a4a8-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en ThirdLight debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-140">In other words, a link relationship between an Azure AD user and hello related user in ThirdLight needs toobe established.</span></span>

<span data-ttu-id="3a4a8-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ThirdLight.</span></span>

<span data-ttu-id="3a4a8-142">tooconfigure y prueba de inicio de sesión único en Azure AD con ThirdLight, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3a4a8-142">tooconfigure and test Azure AD single sign-on with ThirdLight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3a4a8-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3a4a8-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a4a8-145">**[Crear un usuario de prueba ThirdLight](#creating-a-thirdlight-test-user)**  -toohave un equivalente de Britta Simon en ThirdLight que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - toohave a counterpart of Britta Simon in ThirdLight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3a4a8-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a4a8-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3a4a8-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a4a8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3a4a8-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="3a4a8-150">**inicio de sesión único en Azure AD tooconfigure con ThirdLight, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3a4a8-150">**tooconfigure Azure AD single sign-on with ThirdLight, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a4a8-151">En el portal de Azure, en Hola Hola **ThirdLight** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-151">In hello Azure portal, on hello **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3a4a8-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. <span data-ttu-id="3a4a8-155">En hello **ThirdLight dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3a4a8-155">On hello **ThirdLight Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="3a4a8-157">a.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-157">a.</span></span> <span data-ttu-id="3a4a8-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.thirdlight.com/`</span><span class="sxs-lookup"><span data-stu-id="3a4a8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="3a4a8-159">b.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-159">b.</span></span> <span data-ttu-id="3a4a8-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="3a4a8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3a4a8-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-161">These values are not real.</span></span> <span data-ttu-id="3a4a8-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y Identiifer.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-162">Update these values with hello actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="3a4a8-163">Póngase en contacto con [equipo de soporte técnico de cliente de ThirdLight](https://www.thirdlight.com/support) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="3a4a8-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. <span data-ttu-id="3a4a8-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3a4a8-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3a4a8-168">En una ventana del explorador web diferente, inicie sesión en el sitio de la empresa ThirdLight tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-168">In a different web browser window, log in tooyour ThirdLight company site as an administrator.</span></span>

7. <span data-ttu-id="3a4a8-169">Vaya demasiado**configuración \> administración del sistema**y, a continuación, haga clic en **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-169">Go too**Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="3a4a8-170">![Administración del sistema](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "Administración del sistema")</span><span class="sxs-lookup"><span data-stu-id="3a4a8-170">![System Administration](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "System Administration")</span></span>

8. <span data-ttu-id="3a4a8-171">En la sección de configuración de hello SAML2, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3a4a8-171">In hello SAML2 configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="3a4a8-172">![Inicio de sesión único SAML](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "Inicio de sesión único SAML")</span><span class="sxs-lookup"><span data-stu-id="3a4a8-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="3a4a8-173">a.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-173">a.</span></span> <span data-ttu-id="3a4a8-174">Seleccione **Habilitar inicio de sesión único de SAML2**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="3a4a8-175">b.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-175">b.</span></span> <span data-ttu-id="3a4a8-176">Como **Origen para los metadatos de IdP**, seleccione **Cargar metadatos de IdP desde XML**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="3a4a8-177">c.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-177">c.</span></span> <span data-ttu-id="3a4a8-178">Abrir archivo de metadatos de hello descargado, copie el contenido de hello y, a continuación, péguelo en hello **XML de metadatos de IdP** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-178">Open hello downloaded metadata file, copy hello content, and then paste it into hello **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="3a4a8-179">d.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-179">d.</span></span> <span data-ttu-id="3a4a8-180">Haga clic en **Guardar configuración de SAML2**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="3a4a8-181">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="3a4a8-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3a4a8-182">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3a4a8-183">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3a4a8-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3a4a8-184">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a4a8-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="3a4a8-185">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3a4a8-187">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3a4a8-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a4a8-188">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3a4a8-190">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3a4a8-192">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3a4a8-194">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="3a4a8-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3a4a8-196">a.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-196">a.</span></span> <span data-ttu-id="3a4a8-197">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a4a8-198">b.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-198">b.</span></span> <span data-ttu-id="3a4a8-199">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-199">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="3a4a8-200">c.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-200">c.</span></span> <span data-ttu-id="3a4a8-201">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3a4a8-202">d.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-202">d.</span></span> <span data-ttu-id="3a4a8-203">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="3a4a8-204">Creación de un usuario de prueba ThirdLight</span><span class="sxs-lookup"><span data-stu-id="3a4a8-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="3a4a8-205">toolog de los usuarios de Azure AD tooenable en tooThirdLight, se les deben aprovisionar en ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-205">tooenable Azure AD users toolog in tooThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="3a4a8-206">En caso de hello de ThirdLight, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-206">In hello case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="3a4a8-207">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3a4a8-207">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a4a8-208">Inicie sesión en tooyour **ThirdLight** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-208">Log in tooyour **ThirdLight** company site as an administrator.</span></span>

2. <span data-ttu-id="3a4a8-209">Vaya demasiado**usuarios** ficha.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-209">Go too**Users** tab.</span></span>

3. <span data-ttu-id="3a4a8-210">Seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-210">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="3a4a8-211">Haga clic en el botón **Agregar nuevo usuario** .</span><span class="sxs-lookup"><span data-stu-id="3a4a8-211">Click **Add new User** button.</span></span>

5. <span data-ttu-id="3a4a8-212">Escriba **hello nombre de usuario, el nombre o la descripción, correo electrónico, elija un valor predefinido o un grupo de nuevos miembros** de una cuenta válida de AAD que desee tooprovision.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-212">Enter **hello Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want tooprovision.</span></span>

6. <span data-ttu-id="3a4a8-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="3a4a8-214">Puede usar cualquier otra Thirdlight usuario cuenta herramienta de creación o las API proporcionadas por Thirdlight tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3a4a8-215">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a4a8-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3a4a8-216">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooThirdLight.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThirdLight.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3a4a8-218">**tooassign Britta Simon tooThirdLight, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3a4a8-218">**tooassign Britta Simon tooThirdLight, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a4a8-219">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3a4a8-221">En la lista de aplicaciones de hello, seleccione **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-221">In hello applications list, select **ThirdLight**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. <span data-ttu-id="3a4a8-223">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3a4a8-225">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-225">Click **Add** button.</span></span> <span data-ttu-id="3a4a8-226">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3a4a8-228">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3a4a8-229">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3a4a8-230">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3a4a8-231">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3a4a8-231">Testing single sign-on</span></span>

<span data-ttu-id="3a4a8-232">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3a4a8-233">Al hacer clic en icono de ThirdLight Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour ThirdLight aplicación.</span><span class="sxs-lookup"><span data-stu-id="3a4a8-233">When you click hello ThirdLight tile in hello Access Panel, you should get automatically signed-on tooyour ThirdLight application.</span></span>
<span data-ttu-id="3a4a8-234">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3a4a8-234">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3a4a8-235">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3a4a8-235">Additional resources</span></span>

* [<span data-ttu-id="3a4a8-236">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a4a8-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a4a8-237">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3a4a8-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png


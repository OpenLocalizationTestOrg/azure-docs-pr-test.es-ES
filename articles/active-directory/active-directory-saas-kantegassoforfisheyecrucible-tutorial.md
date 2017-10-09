---
title: "Tutorial: Integración de Azure Active Directory con Kantega SSO para FishEye/Crucible | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Kantega SSO para FishEye/placa."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fe951fd-1530-4d33-a1a4-390385b99ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: fdd68b5e90c3e2893887650735429a33e21ffa68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-fisheyecrucible"></a><span data-ttu-id="931c1-103">Tutorial: Integración de Azure Active Directory con Kantega SSO para FishEye/Crucible</span><span class="sxs-lookup"><span data-stu-id="931c1-103">Tutorial: Azure Active Directory integration with Kantega SSO for FishEye/Crucible</span></span>

<span data-ttu-id="931c1-104">En este tutorial, aprenderá cómo toointegrate Kantega SSO para FishEye/placa con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="931c1-104">In this tutorial, you learn how toointegrate Kantega SSO for FishEye/Crucible with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="931c1-105">Integración Kantega SSO para FishEye/placa con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="931c1-105">Integrating Kantega SSO for FishEye/Crucible with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="931c1-106">Puede controlar en Azure AD que tenga acceso tooKantega SSO para FishEye/placa</span><span class="sxs-lookup"><span data-stu-id="931c1-106">You can control in Azure AD who has access tooKantega SSO for FishEye/Crucible</span></span>
- <span data-ttu-id="931c1-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooKantega SSO para FishEye/placa (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="931c1-107">You can enable your users tooautomatically get signed-on tooKantega SSO for FishEye/Crucible (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="931c1-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="931c1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="931c1-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="931c1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="931c1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="931c1-110">Prerequisites</span></span>

<span data-ttu-id="931c1-111">integración de Azure AD con Kantega SSO para FishEye/placa tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="931c1-111">tooconfigure Azure AD integration with Kantega SSO for FishEye/Crucible, you need hello following items:</span></span>

- <span data-ttu-id="931c1-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="931c1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="931c1-113">Una suscripción habilitada para el inicio de sesión único de Kantega SSO para FishEye/Crucible</span><span class="sxs-lookup"><span data-stu-id="931c1-113">A Kantega SSO for FishEye/Crucible single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="931c1-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="931c1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="931c1-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="931c1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="931c1-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="931c1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="931c1-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="931c1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="931c1-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="931c1-118">Scenario description</span></span>
<span data-ttu-id="931c1-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="931c1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="931c1-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="931c1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="931c1-121">Agregar Kantega SSO para FishEye/placa de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="931c1-121">Adding Kantega SSO for FishEye/Crucible from hello gallery</span></span>
2. <span data-ttu-id="931c1-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="931c1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-fisheyecrucible-from-hello-gallery"></a><span data-ttu-id="931c1-123">Agregar Kantega SSO para FishEye/placa de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="931c1-123">Adding Kantega SSO for FishEye/Crucible from hello gallery</span></span>
<span data-ttu-id="931c1-124">integración de hello tooconfigure de Kantega SSO para FishEye/placa en Azure AD, necesitará tooadd Kantega SSO para FishEye/placa de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="931c1-124">tooconfigure hello integration of Kantega SSO for FishEye/Crucible into Azure AD, you need tooadd Kantega SSO for FishEye/Crucible from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="931c1-125">**tooadd Kantega SSO para FishEye/placa de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="931c1-125">**tooadd Kantega SSO for FishEye/Crucible from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="931c1-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="931c1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="931c1-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="931c1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="931c1-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="931c1-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="931c1-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="931c1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="931c1-133">En el cuadro de búsqueda de hello, escriba **Kantega SSO para FishEye/placa**.</span><span class="sxs-lookup"><span data-stu-id="931c1-133">In hello search box, type **Kantega SSO for FishEye/Crucible**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_search.png)

5. <span data-ttu-id="931c1-135">En el panel de resultados de hello, seleccione **Kantega SSO para FishEye/placa**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="931c1-135">In hello results panel, select **Kantega SSO for FishEye/Crucible**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="931c1-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="931c1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="931c1-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Kantega SSO para FishEye/Crucible con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="931c1-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="931c1-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Kantega SSO para FishEye/placa es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="931c1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for FishEye/Crucible is tooa user in Azure AD.</span></span> <span data-ttu-id="931c1-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Kantega SSO para FishEye/placa debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="931c1-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for FishEye/Crucible needs toobe established.</span></span>

<span data-ttu-id="931c1-141">En Kantega SSO para FishEye/placa, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="931c1-141">In Kantega SSO for FishEye/Crucible, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="931c1-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Kantega SSO para FishEye/placa, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="931c1-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="931c1-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="931c1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="931c1-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="931c1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="931c1-145">**[Crear un SSO Kantega de usuario de prueba de FishEye/placa](#creating-a-kantega-sso-for-fisheyecrucible-test-user)**  -toohave un equivalente de Britta Simon en Kantega SSO para FishEye/placa es representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="931c1-145">**[Creating a Kantega SSO for FishEye/Crucible test user](#creating-a-kantega-sso-for-fisheyecrucible-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for FishEye/Crucible that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="931c1-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="931c1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="931c1-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="931c1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="931c1-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="931c1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="931c1-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en el SSO Kantega para aplicaciones de FishEye/placa.</span><span class="sxs-lookup"><span data-stu-id="931c1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for FishEye/Crucible application.</span></span>

<span data-ttu-id="931c1-150">**tooconfigure inicio de sesión único en Azure AD con Kantega SSO para FishEye/placa, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="931c1-150">**tooconfigure Azure AD single sign-on with Kantega SSO for FishEye/Crucible, perform hello following steps:**</span></span>

1. <span data-ttu-id="931c1-151">En el portal de Azure, en Hola Hola **Kantega SSO para FishEye/placa** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="931c1-151">In hello Azure portal, on hello **Kantega SSO for FishEye/Crucible** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="931c1-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="931c1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_samlbase.png)

3. <span data-ttu-id="931c1-155">En **IDP** inicia el modo, hello **Kantega SSO de dominio FishEye/placa y direcciones URL** sección realizar Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="931c1-155">In **IDP** initiated mode, on hello **Kantega SSO for FishEye/Crucible Domain and URLs** section perform hello following step :</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url1.png)

    <span data-ttu-id="931c1-157">a.</span><span class="sxs-lookup"><span data-stu-id="931c1-157">a.</span></span> <span data-ttu-id="931c1-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="931c1-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="931c1-159">b.</span><span class="sxs-lookup"><span data-stu-id="931c1-159">b.</span></span> <span data-ttu-id="931c1-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="931c1-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="931c1-161">En **SP** modo iniciado, verificación **mostrar avanzadas de configuración de la URL** y realizar Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="931c1-161">In **SP** initiated mode, check **Show advanced URL settings** and perform hello following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url2.png)

    <span data-ttu-id="931c1-163">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="931c1-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="931c1-164">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="931c1-164">These values are not real.</span></span> <span data-ttu-id="931c1-165">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="931c1-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="931c1-166">Estos valores se reciben durante la configuración de Hola de complemento FishEye/placa que se explica más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="931c1-166">These values are recieved during hello configuration of FishEye/Crucible plugin which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="931c1-167">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="931c1-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_certificate.png) 

6. <span data-ttu-id="931c1-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="931c1-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="931c1-171">En una ventana del explorador web diferente, inicie sesión en tooyour FishEye/placa en el servidor local como administrador.</span><span class="sxs-lookup"><span data-stu-id="931c1-171">In a different web browser window, log in tooyour FishEye/Crucible on premise server as an administrator.</span></span>

8. <span data-ttu-id="931c1-172">Mantenga el mouse sobre el icono de engranaje y haga clic en hello **complementos**.</span><span class="sxs-lookup"><span data-stu-id="931c1-172">Hover on cog and click hello **Add-ons**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon1.png)

9. <span data-ttu-id="931c1-174">En la sección Configuración del sistema, haga clic en **Find new add-ons** (Buscar nuevos complementos).</span><span class="sxs-lookup"><span data-stu-id="931c1-174">Under System Settings section, click **Find new add-ons**.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/add-on2.png)

10. <span data-ttu-id="931c1-176">Búsqueda **Kantega SSO para placa** y haga clic en **instalar** tooinstall botón Hola nuevo complemento SAML.</span><span class="sxs-lookup"><span data-stu-id="931c1-176">Search **Kantega SSO for Crucible** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon2.png)

11. <span data-ttu-id="931c1-178">se inicia la instalación del complemento Hola.</span><span class="sxs-lookup"><span data-stu-id="931c1-178">hello plugin installation starts.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon33.png)

12. <span data-ttu-id="931c1-180">Una vez completada la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="931c1-180">Once hello installation is complete.</span></span> <span data-ttu-id="931c1-181">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="931c1-181">Click **Close**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon34.png)

13. <span data-ttu-id="931c1-183">Haga clic en **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="931c1-183">Click **Manage**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon35.png)

14. <span data-ttu-id="931c1-185">Haga clic en **configurar** tooconfigure Hola nuevo complemento.</span><span class="sxs-lookup"><span data-stu-id="931c1-185">Click **Configure** tooconfigure hello new plugin.</span></span>  

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon3.png)

15. <span data-ttu-id="931c1-187">Hola **SAML** sección.</span><span class="sxs-lookup"><span data-stu-id="931c1-187">In hello **SAML** section.</span></span> <span data-ttu-id="931c1-188">Seleccione **Azure Active Directory (Azure AD)** de hello **Agregar proveedor de identidades** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="931c1-188">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon4.png)

16. <span data-ttu-id="931c1-190">Seleccione el nivel de suscripción **Básica**.</span><span class="sxs-lookup"><span data-stu-id="931c1-190">Select subscription level as **Basic**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon5.png)

17. <span data-ttu-id="931c1-192">En hello **propiedades de la aplicación** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="931c1-192">On hello **App properties** section, perform following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon6.png)

    <span data-ttu-id="931c1-194">a.</span><span class="sxs-lookup"><span data-stu-id="931c1-194">a.</span></span> <span data-ttu-id="931c1-195">Hola copia **App ID URI** valor y utilizarlo como **identificador, dirección URL de respuesta y dirección URL de inicio de sesión** en hello **Kantega SSO de dominio FishEye/placa y direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="931c1-195">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for FishEye/Crucible Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="931c1-196">b.</span><span class="sxs-lookup"><span data-stu-id="931c1-196">b.</span></span> <span data-ttu-id="931c1-197">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="931c1-197">Click **Next**.</span></span>

18. <span data-ttu-id="931c1-198">En hello **importación de metadatos** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="931c1-198">On hello **Metadata import** section, perform following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon7.png)

    <span data-ttu-id="931c1-200">a.</span><span class="sxs-lookup"><span data-stu-id="931c1-200">a.</span></span> <span data-ttu-id="931c1-201">Seleccione **Archivo de metadatos en el equipo** y cargue el archivo de metadatos que descargó desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="931c1-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="931c1-202">b.</span><span class="sxs-lookup"><span data-stu-id="931c1-202">b.</span></span> <span data-ttu-id="931c1-203">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="931c1-203">Click **Next**.</span></span>

19. <span data-ttu-id="931c1-204">En hello **nombre y SSO ubicación** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="931c1-204">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon8.png)

    <span data-ttu-id="931c1-206">a.</span><span class="sxs-lookup"><span data-stu-id="931c1-206">a.</span></span> <span data-ttu-id="931c1-207">Agregar nombre de proveedor de identidades de hello en **el nombre del proveedor de identidad** cuadro de texto (por ejemplo, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="931c1-207">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="931c1-208">b.</span><span class="sxs-lookup"><span data-stu-id="931c1-208">b.</span></span> <span data-ttu-id="931c1-209">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="931c1-209">Click **Next**.</span></span>

20. <span data-ttu-id="931c1-210">Comprobar el certificado de firma de Hola y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="931c1-210">Verify hello Signing certificate and click **Next**.</span></span>    

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon9.png)

21. <span data-ttu-id="931c1-212">En hello **cuentas de usuario de ojo de pez** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="931c1-212">On hello **FishEye user accounts** section, perform following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon10.png)

    <span data-ttu-id="931c1-214">a.</span><span class="sxs-lookup"><span data-stu-id="931c1-214">a.</span></span> <span data-ttu-id="931c1-215">Seleccione **crear usuarios en el directorio interno del FishEye si es necesario** y escriba nombre adecuado Hola del grupo de Hola para los usuarios (puede ser no varios.</span><span class="sxs-lookup"><span data-stu-id="931c1-215">Select **Create users in FishEye's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="931c1-216">de grupos separados por coma).</span><span class="sxs-lookup"><span data-stu-id="931c1-216">of groups separated by comma).</span></span>

    <span data-ttu-id="931c1-217">b.</span><span class="sxs-lookup"><span data-stu-id="931c1-217">b.</span></span> <span data-ttu-id="931c1-218">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="931c1-218">Click **Next**.</span></span>

22. <span data-ttu-id="931c1-219">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="931c1-219">Click **Finish**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon11.png)

23. <span data-ttu-id="931c1-221">En hello **conoce dominios para Azure AD** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="931c1-221">On hello **Known domains for Azure AD** section, perform following steps:</span></span>   

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon12.png)

    <span data-ttu-id="931c1-223">a.</span><span class="sxs-lookup"><span data-stu-id="931c1-223">a.</span></span> <span data-ttu-id="931c1-224">Seleccione **conoce dominios** desde el panel izquierdo de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="931c1-224">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="931c1-225">b.</span><span class="sxs-lookup"><span data-stu-id="931c1-225">b.</span></span> <span data-ttu-id="931c1-226">Escriba el nombre de dominio en hello **conoce dominios** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="931c1-226">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="931c1-227">c.</span><span class="sxs-lookup"><span data-stu-id="931c1-227">c.</span></span> <span data-ttu-id="931c1-228">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="931c1-228">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="931c1-229">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="931c1-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="931c1-230">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="931c1-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="931c1-231">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="931c1-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="931c1-232">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="931c1-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="931c1-233">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="931c1-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="931c1-235">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="931c1-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="931c1-236">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="931c1-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="931c1-238">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="931c1-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="931c1-240">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="931c1-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="931c1-242">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="931c1-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="931c1-244">a.</span><span class="sxs-lookup"><span data-stu-id="931c1-244">a.</span></span> <span data-ttu-id="931c1-245">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="931c1-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="931c1-246">b.</span><span class="sxs-lookup"><span data-stu-id="931c1-246">b.</span></span> <span data-ttu-id="931c1-247">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="931c1-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="931c1-248">c.</span><span class="sxs-lookup"><span data-stu-id="931c1-248">c.</span></span> <span data-ttu-id="931c1-249">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="931c1-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="931c1-250">d.</span><span class="sxs-lookup"><span data-stu-id="931c1-250">d.</span></span> <span data-ttu-id="931c1-251">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="931c1-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-fisheyecrucible-test-user"></a><span data-ttu-id="931c1-252">Creación de un usuario de prueba de Kantega SSO para FishEye/Crucible</span><span class="sxs-lookup"><span data-stu-id="931c1-252">Creating a Kantega SSO for FishEye/Crucible test user</span></span>

<span data-ttu-id="931c1-253">toolog de los usuarios de Azure AD tooenable en tooFishEye/placa, se les deben aprovisionar en FishEye/placa.</span><span class="sxs-lookup"><span data-stu-id="931c1-253">tooenable Azure AD users toolog in tooFishEye/Crucible, they must be provisioned into FishEye/Crucible.</span></span> <span data-ttu-id="931c1-254">En Kantega SSO para FishEye/Crucible, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="931c1-254">In Kantega SSO for FishEye/Crucible, provisioning is a manual task.</span></span>

<span data-ttu-id="931c1-255">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="931c1-255">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="931c1-256">Inicie sesión en tooyour placa en el servidor local como administrador.</span><span class="sxs-lookup"><span data-stu-id="931c1-256">Log in tooyour Crucible on premise server as an administrator.</span></span>

2. <span data-ttu-id="931c1-257">Mantenga el mouse sobre el icono de engranaje y haga clic en hello **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="931c1-257">Hover on cog and click hello **Users**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user1.png) 

3. <span data-ttu-id="931c1-259">En la sección de la pestaña **Usuarios**, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="931c1-259">Under **Users** tab section, click **Add user**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user2.png)

4. <span data-ttu-id="931c1-261">En hello **Agregar nuevo usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="931c1-261">On hello **Add New User** dialog page, perform hello following steps:</span></span>

    ![Agregar empleado](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user3.png) 

    <span data-ttu-id="931c1-263">a.</span><span class="sxs-lookup"><span data-stu-id="931c1-263">a.</span></span> <span data-ttu-id="931c1-264">Hola **nombre de usuario** Hola de tipo de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="931c1-264">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="931c1-265">b.</span><span class="sxs-lookup"><span data-stu-id="931c1-265">b.</span></span> <span data-ttu-id="931c1-266">Hola **nombre para mostrar** cuadro de texto, nombre completo del tipo de usuario de hello como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="931c1-266">In hello **Display Name** textbox, type display name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="931c1-267">c.</span><span class="sxs-lookup"><span data-stu-id="931c1-267">c.</span></span> <span data-ttu-id="931c1-268">Hola **dirección de correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="931c1-268">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="931c1-269">d.</span><span class="sxs-lookup"><span data-stu-id="931c1-269">d.</span></span> <span data-ttu-id="931c1-270">Hola **contraseña** cuadro de texto, escriba la contraseña de saludo del usuario.</span><span class="sxs-lookup"><span data-stu-id="931c1-270">In hello **Password** textbox, type hello password of user.</span></span>  

    <span data-ttu-id="931c1-271">e.</span><span class="sxs-lookup"><span data-stu-id="931c1-271">e.</span></span> <span data-ttu-id="931c1-272">Hola **Confirmar contraseña** cuadro de texto, volver a entrar Hola contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="931c1-272">In hello **Confirm Password** textbox, reenter hello password of user.</span></span>

    <span data-ttu-id="931c1-273">f.</span><span class="sxs-lookup"><span data-stu-id="931c1-273">f.</span></span> <span data-ttu-id="931c1-274">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="931c1-274">Click **Add**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="931c1-275">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="931c1-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="931c1-276">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooKantega SSO para FishEye/placa.</span><span class="sxs-lookup"><span data-stu-id="931c1-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for FishEye/Crucible.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="931c1-278">**tooassign Britta Simon tooKantega SSO para FishEye/placa, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="931c1-278">**tooassign Britta Simon tooKantega SSO for FishEye/Crucible, perform hello following steps:**</span></span>

1. <span data-ttu-id="931c1-279">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="931c1-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="931c1-281">En la lista de aplicaciones de hello, seleccione **Kantega SSO para FishEye/placa**.</span><span class="sxs-lookup"><span data-stu-id="931c1-281">In hello applications list, select **Kantega SSO for FishEye/Crucible**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_app.png) 

3. <span data-ttu-id="931c1-283">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="931c1-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="931c1-285">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="931c1-285">Click **Add** button.</span></span> <span data-ttu-id="931c1-286">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="931c1-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="931c1-288">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="931c1-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="931c1-289">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="931c1-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="931c1-290">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="931c1-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="931c1-291">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="931c1-291">Testing single sign-on</span></span>

<span data-ttu-id="931c1-292">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="931c1-292">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="931c1-293">Al hacer clic en hello Kantega SSO de icono FishEye/placa Hola Panel de acceso, obtendrá automáticamente ha iniciado sesión tooyour Kantega SSO para aplicaciones de FishEye/placa.</span><span class="sxs-lookup"><span data-stu-id="931c1-293">When you click hello Kantega SSO for FishEye/Crucible tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for FishEye/Crucible application.</span></span>
<span data-ttu-id="931c1-294">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="931c1-294">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="931c1-295">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="931c1-295">Additional resources</span></span>

* [<span data-ttu-id="931c1-296">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="931c1-296">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="931c1-297">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="931c1-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_203.png


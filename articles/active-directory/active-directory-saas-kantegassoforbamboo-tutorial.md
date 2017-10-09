---
title: "Tutorial: Integración de Azure Active Directory con Kantega SSO para Bamboo | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Kantega SSO para bambú."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e238b574-9e9b-43b7-ab98-d2a87ff89d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 8bf637ff440e8e3948db882861bee6e73f8aa879
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bamboo"></a><span data-ttu-id="9a869-103">Tutorial: Integración de Azure Active Directory con Kantega SSO para Bamboo</span><span class="sxs-lookup"><span data-stu-id="9a869-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bamboo</span></span>

<span data-ttu-id="9a869-104">En este tutorial, aprenderá cómo toointegrate Kantega SSO para bambú con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9a869-104">In this tutorial, you learn how toointegrate Kantega SSO for Bamboo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a869-105">Integración Kantega SSO para bambú con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9a869-105">Integrating Kantega SSO for Bamboo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9a869-106">Puede controlar en Azure AD que tenga acceso tooKantega SSO para bambú</span><span class="sxs-lookup"><span data-stu-id="9a869-106">You can control in Azure AD who has access tooKantega SSO for Bamboo</span></span>
- <span data-ttu-id="9a869-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooKantega SSO para bambú (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a869-107">You can enable your users tooautomatically get signed-on tooKantega SSO for Bamboo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9a869-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9a869-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9a869-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9a869-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a869-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9a869-110">Prerequisites</span></span>

<span data-ttu-id="9a869-111">integración de Azure AD con Kantega SSO para bambú tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9a869-111">tooconfigure Azure AD integration with Kantega SSO for Bamboo, you need hello following items:</span></span>

- <span data-ttu-id="9a869-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a869-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a869-113">Una suscripción habilitada para el inicio de sesión único de Kantega SSO para Bamboo</span><span class="sxs-lookup"><span data-stu-id="9a869-113">A Kantega SSO for Bamboo single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a869-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9a869-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a869-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9a869-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a869-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9a869-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a869-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a869-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a869-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9a869-118">Scenario description</span></span>
<span data-ttu-id="9a869-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9a869-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a869-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="9a869-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a869-121">Agregar Kantega SSO para bambú desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9a869-121">Adding Kantega SSO for Bamboo from hello gallery</span></span>
2. <span data-ttu-id="9a869-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a869-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bamboo-from-hello-gallery"></a><span data-ttu-id="9a869-123">Agregar Kantega SSO para bambú desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9a869-123">Adding Kantega SSO for Bamboo from hello gallery</span></span>
<span data-ttu-id="9a869-124">integración de hello tooconfigure de Kantega SSO para bambú en Azure AD, necesitará tooadd Kantega SSO bambú de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="9a869-124">tooconfigure hello integration of Kantega SSO for Bamboo into Azure AD, you need tooadd Kantega SSO for Bamboo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9a869-125">**tooadd Kantega SSO para bambú desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9a869-125">**tooadd Kantega SSO for Bamboo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a869-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9a869-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9a869-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9a869-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9a869-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9a869-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9a869-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9a869-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9a869-133">En el cuadro de búsqueda de hello, escriba **Kantega SSO para bambú**.</span><span class="sxs-lookup"><span data-stu-id="9a869-133">In hello search box, type **Kantega SSO for Bamboo**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_search.png)

5. <span data-ttu-id="9a869-135">En el panel de resultados de hello, seleccione **Kantega SSO para bambú**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9a869-135">In hello results panel, select **Kantega SSO for Bamboo**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9a869-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a869-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9a869-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Kantega SSO para Bamboo con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9a869-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bamboo based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9a869-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Kantega SSO para bambú es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a869-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for Bamboo is tooa user in Azure AD.</span></span> <span data-ttu-id="9a869-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Kantega SSO para bambú debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="9a869-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for Bamboo needs toobe established.</span></span>

<span data-ttu-id="9a869-141">En Kantega SSO para bambú, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9a869-141">In Kantega SSO for Bamboo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9a869-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Kantega SSO para bambú, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9a869-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for Bamboo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9a869-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="9a869-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9a869-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a869-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a869-145">**[Crear un SSO Kantega de usuario de prueba de bambú](#creating-a-kantega-sso-for-bamboo-test-user)**  -toohave un equivalente de Britta Simon en Kantega SSO para bambú que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="9a869-145">**[Creating a Kantega SSO for Bamboo test user](#creating-a-kantega-sso-for-bamboo-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for Bamboo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a869-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9a869-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a869-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9a869-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9a869-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a869-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9a869-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en el SSO Kantega para aplicación bambú.</span><span class="sxs-lookup"><span data-stu-id="9a869-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for Bamboo application.</span></span>

<span data-ttu-id="9a869-150">**tooconfigure inicio de sesión único en Azure AD con Kantega SSO para bambú, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9a869-150">**tooconfigure Azure AD single sign-on with Kantega SSO for Bamboo, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a869-151">En el portal de Azure, en Hola Hola **Kantega SSO para bambú** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9a869-151">In hello Azure portal, on hello **Kantega SSO for Bamboo** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9a869-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9a869-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_samlbase.png)

3. <span data-ttu-id="9a869-155">En **IDP** inicia el modo, hello **Kantega SSO de dominio bambú y direcciones URL** sección realizar Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="9a869-155">In **IDP** initiated mode, on hello **Kantega SSO for Bamboo Domain and URLs** section perform hello following step :</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url1.png)
    
    <span data-ttu-id="9a869-157">a.</span><span class="sxs-lookup"><span data-stu-id="9a869-157">a.</span></span> <span data-ttu-id="9a869-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="9a869-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="9a869-159">b.</span><span class="sxs-lookup"><span data-stu-id="9a869-159">b.</span></span> <span data-ttu-id="9a869-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="9a869-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="9a869-161">En **SP** modo iniciado, verificación **mostrar avanzadas de configuración de la URL** y realizar Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="9a869-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform hello following step :</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url2.png)
    
    <span data-ttu-id="9a869-163">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="9a869-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9a869-164">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9a869-164">These values are not real.</span></span> <span data-ttu-id="9a869-165">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="9a869-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9a869-166">Estos valores se reciben durante la configuración de Hola de bambú complemento que se explica más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="9a869-166">These values are recieved during hello configuration of Bamboo plugin which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="9a869-167">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9a869-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_certificate.png) 

6. <span data-ttu-id="9a869-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9a869-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="9a869-171">En una ventana del explorador web diferente, inicie sesión en tooyour bambú en servidor local como administrador.</span><span class="sxs-lookup"><span data-stu-id="9a869-171">In a different web browser window, log in tooyour Bamboo  on premise server as an administrator.</span></span>

8. <span data-ttu-id="9a869-172">Mantenga el mouse sobre el icono de engranaje y haga clic en hello **complementos**.</span><span class="sxs-lookup"><span data-stu-id="9a869-172">Hover on cog and click hello **Add-ons**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon1.png)

9. <span data-ttu-id="9a869-174">En la sección de la pestaña Complementos, haga clic en **Find new add-ons** (Buscar nuevos complementos).</span><span class="sxs-lookup"><span data-stu-id="9a869-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="9a869-175">Búsqueda **Kantega SSO para bambú (SAML & Kerberos)** y haga clic en **instalar** tooinstall botón Hola nuevo complemento SAML.</span><span class="sxs-lookup"><span data-stu-id="9a869-175">Search **Kantega SSO for Bamboo (SAML & Kerberos)** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon2.png)

10. <span data-ttu-id="9a869-177">se iniciará la instalación del complemento Hola.</span><span class="sxs-lookup"><span data-stu-id="9a869-177">hello plugin installation will start.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon21.png)

11. <span data-ttu-id="9a869-179">Una vez completada la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9a869-179">Once hello installation is complete.</span></span> <span data-ttu-id="9a869-180">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="9a869-180">Click **Close**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon33.png)

12. <span data-ttu-id="9a869-182">Haga clic en **Administrar**.</span><span class="sxs-lookup"><span data-stu-id="9a869-182">Click **Manage**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon34.png)
    
13. <span data-ttu-id="9a869-184">Haga clic en **configurar** tooconfigure Hola nuevo complemento.</span><span class="sxs-lookup"><span data-stu-id="9a869-184">Click **Configure** tooconfigure hello new plugin.</span></span>  

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon3.png)

14. <span data-ttu-id="9a869-186">Hola **SAML** sección.</span><span class="sxs-lookup"><span data-stu-id="9a869-186">In hello **SAML** section.</span></span> <span data-ttu-id="9a869-187">Seleccione **Azure Active Directory (Azure AD)** de hello **Agregar proveedor de identidades** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="9a869-187">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon4.png)

15. <span data-ttu-id="9a869-189">Seleccione el nivel de suscripción **Básica**.</span><span class="sxs-lookup"><span data-stu-id="9a869-189">Select subscription level as **Basic**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon5.png)

16. <span data-ttu-id="9a869-191">En hello **propiedades de la aplicación** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9a869-191">On hello **App properties** section, perform following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon6.png)

    <span data-ttu-id="9a869-193">a.</span><span class="sxs-lookup"><span data-stu-id="9a869-193">a.</span></span> <span data-ttu-id="9a869-194">Hola copia **App ID URI** valor y utilizarlo como **identificador, dirección URL de respuesta y dirección URL de inicio de sesión** en hello **Kantega SSO de dominio bambú y direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9a869-194">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for Bamboo Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="9a869-195">b.</span><span class="sxs-lookup"><span data-stu-id="9a869-195">b.</span></span> <span data-ttu-id="9a869-196">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9a869-196">Click **Next**.</span></span>

17. <span data-ttu-id="9a869-197">En hello **importación de metadatos** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9a869-197">On hello **Metadata import** section, perform following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon7.png)

    <span data-ttu-id="9a869-199">a.</span><span class="sxs-lookup"><span data-stu-id="9a869-199">a.</span></span> <span data-ttu-id="9a869-200">Seleccione **Archivo de metadatos en el equipo** y cargue el archivo de metadatos que descargó desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9a869-200">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="9a869-201">b.</span><span class="sxs-lookup"><span data-stu-id="9a869-201">b.</span></span> <span data-ttu-id="9a869-202">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9a869-202">Click **Next**.</span></span>

18. <span data-ttu-id="9a869-203">En hello **nombre y SSO ubicación** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9a869-203">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon8.png)

    <span data-ttu-id="9a869-205">a.</span><span class="sxs-lookup"><span data-stu-id="9a869-205">a.</span></span> <span data-ttu-id="9a869-206">Agregar nombre de proveedor de identidades de hello en **el nombre del proveedor de identidad** cuadro de texto (por ejemplo, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9a869-206">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="9a869-207">b.</span><span class="sxs-lookup"><span data-stu-id="9a869-207">b.</span></span> <span data-ttu-id="9a869-208">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9a869-208">Click **Next**.</span></span>

19. <span data-ttu-id="9a869-209">Comprobar el certificado de firma de Hola y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9a869-209">Verify hello Signing certificate and click **Next**.</span></span>    

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon9.png)

20. <span data-ttu-id="9a869-211">En hello **cuentas de usuario de bambú** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9a869-211">On hello **Bamboo user accounts** section, perform following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon10.png)

    <span data-ttu-id="9a869-213">a.</span><span class="sxs-lookup"><span data-stu-id="9a869-213">a.</span></span> <span data-ttu-id="9a869-214">Seleccione **crear usuarios en el directorio interno del bambú si es necesario** y escriba nombre adecuado Hola del grupo de Hola para los usuarios (puede ser no varios.</span><span class="sxs-lookup"><span data-stu-id="9a869-214">Select **Create users in Bamboo's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="9a869-215">de grupos separados por coma).</span><span class="sxs-lookup"><span data-stu-id="9a869-215">of groups separated by comma).</span></span>

    <span data-ttu-id="9a869-216">b.</span><span class="sxs-lookup"><span data-stu-id="9a869-216">b.</span></span> <span data-ttu-id="9a869-217">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9a869-217">Click **Next**.</span></span>

21. <span data-ttu-id="9a869-218">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="9a869-218">Click **Finish**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon11.png)

22. <span data-ttu-id="9a869-220">En hello **conoce dominios para Azure AD** sección, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9a869-220">On hello **Known domains for Azure AD** section, perform following steps:</span></span>   

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon12.png)

    <span data-ttu-id="9a869-222">a.</span><span class="sxs-lookup"><span data-stu-id="9a869-222">a.</span></span> <span data-ttu-id="9a869-223">Seleccione **conoce dominios** desde el panel izquierdo de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="9a869-223">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="9a869-224">b.</span><span class="sxs-lookup"><span data-stu-id="9a869-224">b.</span></span> <span data-ttu-id="9a869-225">Escriba el nombre de dominio en hello **conoce dominios** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="9a869-225">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="9a869-226">c.</span><span class="sxs-lookup"><span data-stu-id="9a869-226">c.</span></span> <span data-ttu-id="9a869-227">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9a869-227">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9a869-228">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="9a869-228">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9a869-229">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="9a869-229">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9a869-230">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9a869-230">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9a869-231">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a869-231">Creating an Azure AD test user</span></span>
<span data-ttu-id="9a869-232">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9a869-232">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9a869-234">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9a869-234">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a869-235">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9a869-235">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9a869-237">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9a869-237">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9a869-239">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9a869-239">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9a869-241">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="9a869-241">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9a869-243">a.</span><span class="sxs-lookup"><span data-stu-id="9a869-243">a.</span></span> <span data-ttu-id="9a869-244">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a869-244">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a869-245">b.</span><span class="sxs-lookup"><span data-stu-id="9a869-245">b.</span></span> <span data-ttu-id="9a869-246">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9a869-246">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9a869-247">c.</span><span class="sxs-lookup"><span data-stu-id="9a869-247">c.</span></span> <span data-ttu-id="9a869-248">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9a869-248">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9a869-249">d.</span><span class="sxs-lookup"><span data-stu-id="9a869-249">d.</span></span> <span data-ttu-id="9a869-250">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9a869-250">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bamboo-test-user"></a><span data-ttu-id="9a869-251">Crear un usuario de prueba de Kantega SSO para Bamboo</span><span class="sxs-lookup"><span data-stu-id="9a869-251">Creating a Kantega SSO for Bamboo test user</span></span>

<span data-ttu-id="9a869-252">toolog de los usuarios de Azure AD tooenable en tooBamboo, se les deben aprovisionar en bambú.</span><span class="sxs-lookup"><span data-stu-id="9a869-252">tooenable Azure AD users toolog in tooBamboo, they must be provisioned into Bamboo.</span></span> <span data-ttu-id="9a869-253">En Kantega SSO para Bamboo, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="9a869-253">In Kantega SSO for Bamboo, provisioning is a manual task.</span></span>

<span data-ttu-id="9a869-254">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9a869-254">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a869-255">Inicie sesión en tooyour bambú en servidor local como administrador.</span><span class="sxs-lookup"><span data-stu-id="9a869-255">Log in tooyour Bamboo on premise server as an administrator.</span></span>

2. <span data-ttu-id="9a869-256">Mantenga el mouse sobre el icono de engranaje y haga clic en hello **administración de usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9a869-256">Hover on cog and click hello **User management**.</span></span>

    ![Agregar empleado](./media/active-directory-saas-kantegassoforbamboo-tutorial/user1.png) 

3. <span data-ttu-id="9a869-258">Haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9a869-258">Click **Users**.</span></span> <span data-ttu-id="9a869-259">En hello **para agregar un usuario** sección, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9a869-259">Under hello **Add user** section, Perform follwing steps:</span></span>

    ![Agregar empleado](./media/active-directory-saas-kantegassoforbamboo-tutorial/user2.png) 

    <span data-ttu-id="9a869-261">a.</span><span class="sxs-lookup"><span data-stu-id="9a869-261">a.</span></span> <span data-ttu-id="9a869-262">Hola **nombre de usuario** Hola de tipo de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9a869-262">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="9a869-263">b.</span><span class="sxs-lookup"><span data-stu-id="9a869-263">b.</span></span> <span data-ttu-id="9a869-264">Hola **contraseña** cuadro de texto, escriba la contraseña de saludo del usuario.</span><span class="sxs-lookup"><span data-stu-id="9a869-264">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="9a869-265">c.</span><span class="sxs-lookup"><span data-stu-id="9a869-265">c.</span></span> <span data-ttu-id="9a869-266">Hola **Confirmar contraseña** cuadro de texto, volver a entrar Hola contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="9a869-266">In hello **Confirm Password** textbox, reenter hello password of user.</span></span>
    
    <span data-ttu-id="9a869-267">d.</span><span class="sxs-lookup"><span data-stu-id="9a869-267">d.</span></span> <span data-ttu-id="9a869-268">Hola **nombre completo** cuadro de texto, nombre completo del tipo de usuario de hello como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a869-268">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="9a869-269">e.</span><span class="sxs-lookup"><span data-stu-id="9a869-269">e.</span></span> <span data-ttu-id="9a869-270">Hola **correo electrónico** tipo hello dirección de correo electrónico del usuario, cuadro de texto, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9a869-270">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="9a869-271">f.</span><span class="sxs-lookup"><span data-stu-id="9a869-271">f.</span></span> <span data-ttu-id="9a869-272">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9a869-272">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9a869-273">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a869-273">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9a869-274">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooKantega SSO para bambú.</span><span class="sxs-lookup"><span data-stu-id="9a869-274">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for Bamboo.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9a869-276">**tooassign Britta Simon tooKantega SSO para bambú, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9a869-276">**tooassign Britta Simon tooKantega SSO for Bamboo, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a869-277">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9a869-277">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9a869-279">En la lista de aplicaciones de hello, seleccione **Kantega SSO para bambú**.</span><span class="sxs-lookup"><span data-stu-id="9a869-279">In hello applications list, select **Kantega SSO for Bamboo**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_app.png) 

3. <span data-ttu-id="9a869-281">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9a869-281">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9a869-283">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9a869-283">Click **Add** button.</span></span> <span data-ttu-id="9a869-284">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9a869-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9a869-286">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9a869-286">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9a869-287">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9a869-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a869-288">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9a869-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9a869-289">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9a869-289">Testing single sign-on</span></span>

<span data-ttu-id="9a869-290">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9a869-290">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9a869-291">Al hacer clic en hello Kantega SSO para mosaico bambú Hola Panel de acceso, obtendrá automáticamente ha iniciado sesión tooyour Kantega SSO para aplicaciones de bambú.</span><span class="sxs-lookup"><span data-stu-id="9a869-291">When you click hello Kantega SSO for Bamboo tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for Bamboo application.</span></span>
<span data-ttu-id="9a869-292">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9a869-292">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9a869-293">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9a869-293">Additional resources</span></span>

* [<span data-ttu-id="9a869-294">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a869-294">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a869-295">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a869-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_203.png


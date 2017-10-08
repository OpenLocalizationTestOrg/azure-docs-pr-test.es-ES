---
title: "Tutorial: integración de Azure Active Directory con Igloo Software | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Igloo Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="99e8c-103">Tutorial: Integración de Azure Active Directory con Igloo Software</span><span class="sxs-lookup"><span data-stu-id="99e8c-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="99e8c-104">En este tutorial, aprenderá cómo toointegrate Igloo Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="99e8c-104">In this tutorial, you learn how toointegrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="99e8c-105">Integración Igloo Software con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="99e8c-105">Integrating Igloo Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="99e8c-106">Puede controlar en Azure AD que tenga acceso tooIgloo Software</span><span class="sxs-lookup"><span data-stu-id="99e8c-106">You can control in Azure AD who has access tooIgloo Software</span></span>
- <span data-ttu-id="99e8c-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooIgloo Software (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99e8c-107">You can enable your users tooautomatically get signed-on tooIgloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="99e8c-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="99e8c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="99e8c-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="99e8c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99e8c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="99e8c-110">Prerequisites</span></span>

<span data-ttu-id="99e8c-111">integración de Azure AD con Igloo Software tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="99e8c-111">tooconfigure Azure AD integration with Igloo Software, you need hello following items:</span></span>

- <span data-ttu-id="99e8c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99e8c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="99e8c-113">Una suscripción habilitada para el inicio de sesión único en Igloo Software</span><span class="sxs-lookup"><span data-stu-id="99e8c-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="99e8c-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="99e8c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="99e8c-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="99e8c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="99e8c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="99e8c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="99e8c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99e8c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="99e8c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="99e8c-118">Scenario description</span></span>
<span data-ttu-id="99e8c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="99e8c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="99e8c-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="99e8c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="99e8c-121">Agregar Igloo Software desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="99e8c-121">Adding Igloo Software from hello gallery</span></span>
2. <span data-ttu-id="99e8c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99e8c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-hello-gallery"></a><span data-ttu-id="99e8c-123">Agregar Igloo Software desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="99e8c-123">Adding Igloo Software from hello gallery</span></span>
<span data-ttu-id="99e8c-124">integración de hello tooconfigure de Igloo Software en Azure AD, deberá tooadd Igloo Software de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="99e8c-124">tooconfigure hello integration of Igloo Software into Azure AD, you need tooadd Igloo Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="99e8c-125">**tooadd Igloo Software desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="99e8c-125">**tooadd Igloo Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="99e8c-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="99e8c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="99e8c-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="99e8c-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="99e8c-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="99e8c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="99e8c-133">En el cuadro de búsqueda de hello, escriba **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-133">In hello search box, type **Igloo Software**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="99e8c-135">En el panel de resultados de hello, seleccione **Igloo Software**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="99e8c-135">In hello results panel, select **Igloo Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="99e8c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99e8c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="99e8c-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Igloo Software con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="99e8c-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="99e8c-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Igloo Software es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99e8c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Igloo Software is tooa user in Azure AD.</span></span> <span data-ttu-id="99e8c-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Igloo Software necesita toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="99e8c-140">In other words, a link relationship between an Azure AD user and hello related user in Igloo Software needs toobe established.</span></span>

<span data-ttu-id="99e8c-141">En Igloo Software, asignar el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="99e8c-141">In Igloo Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="99e8c-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Igloo Software, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="99e8c-142">tooconfigure and test Azure AD single sign-on with Igloo Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="99e8c-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="99e8c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="99e8c-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99e8c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="99e8c-145">**[Creación de un usuario de prueba Igloo Software](#creating-an-igloo-software-test-user)**  -toohave un equivalente de Britta Simon en Igloo Software que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="99e8c-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - toohave a counterpart of Britta Simon in Igloo Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="99e8c-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="99e8c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="99e8c-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="99e8c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="99e8c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99e8c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="99e8c-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="99e8c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="99e8c-150">**inicio de sesión único en Azure AD tooconfigure con Igloo Software, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="99e8c-150">**tooconfigure Azure AD single sign-on with Igloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="99e8c-151">En el portal de Azure, en Hola Hola **Igloo Software** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-151">In hello Azure portal, on hello **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="99e8c-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="99e8c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="99e8c-155">En hello **Igloo Software dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="99e8c-155">On hello **Igloo Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="99e8c-157">a.</span><span class="sxs-lookup"><span data-stu-id="99e8c-157">a.</span></span> <span data-ttu-id="99e8c-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="99e8c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="99e8c-159">b.</span><span class="sxs-lookup"><span data-stu-id="99e8c-159">b.</span></span> <span data-ttu-id="99e8c-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="99e8c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="99e8c-161">c.</span><span class="sxs-lookup"><span data-stu-id="99e8c-161">c.</span></span> <span data-ttu-id="99e8c-162">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="99e8c-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="99e8c-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="99e8c-163">These values are not real.</span></span> <span data-ttu-id="99e8c-164">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="99e8c-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="99e8c-165">Póngase en contacto con [equipo de soporte técnico de Igloo Software cliente](https://www.igloosoftware.com/services/support) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="99e8c-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="99e8c-166">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="99e8c-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="99e8c-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="99e8c-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="99e8c-170">En hello **Igloo Software configuración** sección, haga clic en **configurar Igloo Software** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="99e8c-170">On hello **Igloo Software Configuration** section, click **Configure Igloo Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="99e8c-171">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="99e8c-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="99e8c-173">En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía Igloo Software tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="99e8c-173">In a different web browser window, log in tooyour Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="99e8c-174">Vaya toohello **el Panel de Control**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-174">Go toohello **Control Panel**.</span></span>
   
     <span data-ttu-id="99e8c-175">![Panel de control](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Panel de control")</span><span class="sxs-lookup"><span data-stu-id="99e8c-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="99e8c-176">Hola **pertenencia** , haga clic en **configuración de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-176">In hello **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="99e8c-177">![Configuración de inicio de sesión](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Configuración de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="99e8c-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="99e8c-178">En la sección de configuración de SAML de hello, haga clic en **configurar autenticación SAML**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-178">In hello SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="99e8c-179">![Configuración de SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="99e8c-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="99e8c-180">Hola **configuración General** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="99e8c-180">In hello **General Configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="99e8c-181">![Configuración general](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "Configuración general")</span><span class="sxs-lookup"><span data-stu-id="99e8c-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="99e8c-182">a.</span><span class="sxs-lookup"><span data-stu-id="99e8c-182">a.</span></span> <span data-ttu-id="99e8c-183">Hola **nombre de la conexión** cuadro de texto, escriba un nombre personalizado para la configuración.</span><span class="sxs-lookup"><span data-stu-id="99e8c-183">In hello **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="99e8c-184">b.</span><span class="sxs-lookup"><span data-stu-id="99e8c-184">b.</span></span> <span data-ttu-id="99e8c-185">Hola **dirección URL de inicio de sesión IdP** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="99e8c-185">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="99e8c-186">c.</span><span class="sxs-lookup"><span data-stu-id="99e8c-186">c.</span></span> <span data-ttu-id="99e8c-187">Hola **IdP Logout URL** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="99e8c-187">In hello **IdP Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="99e8c-188">d.</span><span class="sxs-lookup"><span data-stu-id="99e8c-188">d.</span></span> <span data-ttu-id="99e8c-189">Seleccione **Logout Response and Request HTTP Type** (Respuesta de cierre de sesión y tipo de solicitud HTTP) como **POST**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="99e8c-190">e.</span><span class="sxs-lookup"><span data-stu-id="99e8c-190">e.</span></span> <span data-ttu-id="99e8c-191">Abra su **base-64** codificado certificado en el Bloc de notas que se descarga desde el portal de Azure, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado público** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="99e8c-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="99e8c-192">Hola **respuesta y la configuración de autenticación**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="99e8c-192">In hello **Response and Authentication Configuration**, perform hello following steps:</span></span>
    
    <span data-ttu-id="99e8c-193">![Configuración de autenticación y respuesta](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Configuración de autenticación y respuesta")</span><span class="sxs-lookup"><span data-stu-id="99e8c-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="99e8c-194">a.</span><span class="sxs-lookup"><span data-stu-id="99e8c-194">a.</span></span> <span data-ttu-id="99e8c-195">En **Identity Provider** (Proveedor de identidades), seleccione **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="99e8c-196">b.</span><span class="sxs-lookup"><span data-stu-id="99e8c-196">b.</span></span> <span data-ttu-id="99e8c-197">En **Identifier Type** (Tipo de identificador), seleccione **Email Address** (Dirección de correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="99e8c-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="99e8c-198">c.</span><span class="sxs-lookup"><span data-stu-id="99e8c-198">c.</span></span> <span data-ttu-id="99e8c-199">Hola **atributo de correo electrónico** cuadro de texto, tipo **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-199">In hello **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="99e8c-200">d.</span><span class="sxs-lookup"><span data-stu-id="99e8c-200">d.</span></span> <span data-ttu-id="99e8c-201">Hola **atributo de nombre** cuadro de texto, tipo **givenname**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-201">In hello **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="99e8c-202">e.</span><span class="sxs-lookup"><span data-stu-id="99e8c-202">e.</span></span> <span data-ttu-id="99e8c-203">Hola **último atributo de nombre** cuadro de texto, tipo **apellido**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-203">In hello **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="99e8c-204">Lleve a cabo Hola siguiente pasos toocomplete Hola configuración:</span><span class="sxs-lookup"><span data-stu-id="99e8c-204">Perform hello following steps toocomplete hello configuration:</span></span>
    
    <span data-ttu-id="99e8c-205">![Creación de usuario de inicio de sesión](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "Creación de usuario de inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="99e8c-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="99e8c-206">a.</span><span class="sxs-lookup"><span data-stu-id="99e8c-206">a.</span></span> <span data-ttu-id="99e8c-207">En **User creation on Sign in** (Creación de usuario al inicio de sesión), seleccione **Create a new user in your site when they sign in** (Crear un nuevo usuario en el sitio cuando se inicia sesión).</span><span class="sxs-lookup"><span data-stu-id="99e8c-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="99e8c-208">b.</span><span class="sxs-lookup"><span data-stu-id="99e8c-208">b.</span></span> <span data-ttu-id="99e8c-209">En **Sign in Settings** (Configuración de inicio de sesión), seleccione **Use SAML button on "Sign in" screen** (Usar botón SAML en la pantalla "Iniciar sesión").</span><span class="sxs-lookup"><span data-stu-id="99e8c-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="99e8c-210">c.</span><span class="sxs-lookup"><span data-stu-id="99e8c-210">c.</span></span> <span data-ttu-id="99e8c-211">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="99e8c-212">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="99e8c-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="99e8c-213">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="99e8c-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="99e8c-214">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="99e8c-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="99e8c-215">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="99e8c-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="99e8c-216">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="99e8c-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="99e8c-218">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="99e8c-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="99e8c-219">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="99e8c-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="99e8c-221">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="99e8c-223">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="99e8c-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="99e8c-225">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="99e8c-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="99e8c-227">a.</span><span class="sxs-lookup"><span data-stu-id="99e8c-227">a.</span></span> <span data-ttu-id="99e8c-228">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="99e8c-229">b.</span><span class="sxs-lookup"><span data-stu-id="99e8c-229">b.</span></span> <span data-ttu-id="99e8c-230">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="99e8c-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="99e8c-231">c.</span><span class="sxs-lookup"><span data-stu-id="99e8c-231">c.</span></span> <span data-ttu-id="99e8c-232">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="99e8c-233">d.</span><span class="sxs-lookup"><span data-stu-id="99e8c-233">d.</span></span> <span data-ttu-id="99e8c-234">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="99e8c-235">Creación de un usuario de prueba de Igloo Software</span><span class="sxs-lookup"><span data-stu-id="99e8c-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="99e8c-236">No hay ningún elemento de acción tooconfigure de aprovisionamiento de usuarios tooIgloo Software.</span><span class="sxs-lookup"><span data-stu-id="99e8c-236">There is no action item for you tooconfigure user provisioning tooIgloo Software.</span></span>  

<span data-ttu-id="99e8c-237">Cuando un usuario asignado intenta toolog en tooIgloo Software mediante el panel de acceso de hello, Igloo Software comprueba si existe el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="99e8c-237">When an assigned user tries toolog in tooIgloo Software using hello access panel, Igloo Software checks whether hello user exists.</span></span>  <span data-ttu-id="99e8c-238">Si no hay cuentas de usuario disponibles, Igloo Software crea una automáticamente.</span><span class="sxs-lookup"><span data-stu-id="99e8c-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="99e8c-239">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="99e8c-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="99e8c-240">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooIgloo Software.</span><span class="sxs-lookup"><span data-stu-id="99e8c-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIgloo Software.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="99e8c-242">**tooassign Britta Simon tooIgloo Software, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="99e8c-242">**tooassign Britta Simon tooIgloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="99e8c-243">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="99e8c-245">En la lista de aplicaciones de hello, seleccione **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-245">In hello applications list, select **Igloo Software**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="99e8c-247">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="99e8c-249">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-249">Click **Add** button.</span></span> <span data-ttu-id="99e8c-250">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="99e8c-252">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="99e8c-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="99e8c-253">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="99e8c-254">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="99e8c-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="99e8c-255">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="99e8c-255">Testing single sign-on</span></span>

<span data-ttu-id="99e8c-256">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="99e8c-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="99e8c-257">Al hacer clic en icono de Igloo Software Hola Hola Panel de acceso, deberá obtener la aplicación de Igloo Software tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="99e8c-257">When you click hello Igloo Software tile in hello Access Panel, you should get automatically signed-on tooyour Igloo Software application.</span></span>
<span data-ttu-id="99e8c-258">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="99e8c-258">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="99e8c-259">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="99e8c-259">Additional resources</span></span>

* [<span data-ttu-id="99e8c-260">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99e8c-260">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="99e8c-261">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="99e8c-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png


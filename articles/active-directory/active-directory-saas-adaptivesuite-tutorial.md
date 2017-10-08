---
title: "Tutorial: Integración de Azure Active Directory con Adaptive Suite | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Suite adaptable."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: af309c27ab74098c1e229c80adb11c96dc2774fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="0d173-103">Tutorial: Integración de Azure Active Directory con Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="0d173-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="0d173-104">En este tutorial, aprenderá cómo toointegrate adaptable Suite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0d173-104">In this tutorial, you learn how toointegrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0d173-105">Integración Suite adaptable con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0d173-105">Integrating Adaptive Suite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0d173-106">Puede controlar en Azure AD que tenga acceso tooAdaptive Suite</span><span class="sxs-lookup"><span data-stu-id="0d173-106">You can control in Azure AD who has access tooAdaptive Suite</span></span>
- <span data-ttu-id="0d173-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAdaptive Suite (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d173-107">You can enable your users tooautomatically get signed-on tooAdaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0d173-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0d173-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0d173-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0d173-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d173-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0d173-110">Prerequisites</span></span>

<span data-ttu-id="0d173-111">tooconfigure integración de Azure AD con Suite adaptable, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0d173-111">tooconfigure Azure AD integration with Adaptive Suite, you need hello following items:</span></span>

- <span data-ttu-id="0d173-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d173-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0d173-113">Una suscripción habilitada para el inicio de sesión único en Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="0d173-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0d173-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0d173-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0d173-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0d173-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0d173-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0d173-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0d173-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0d173-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0d173-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0d173-118">Scenario description</span></span>
<span data-ttu-id="0d173-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0d173-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0d173-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="0d173-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0d173-121">Agregar conjunto adaptable de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0d173-121">Adding Adaptive Suite from hello gallery</span></span>
2. <span data-ttu-id="0d173-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d173-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-hello-gallery"></a><span data-ttu-id="0d173-123">Agregar conjunto adaptable de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0d173-123">Adding Adaptive Suite from hello gallery</span></span>
<span data-ttu-id="0d173-124">integración de hello tooconfigure de Suite adaptable en Azure AD, deberá tooadd Suite adaptable de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="0d173-124">tooconfigure hello integration of Adaptive Suite into Azure AD, you need tooadd Adaptive Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0d173-125">**tooadd Suite adaptable de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d173-125">**tooadd Adaptive Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d173-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0d173-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0d173-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0d173-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0d173-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0d173-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0d173-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0d173-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0d173-133">En el cuadro de búsqueda de hello, escriba **Suite adaptable**.</span><span class="sxs-lookup"><span data-stu-id="0d173-133">In hello search box, type **Adaptive Suite**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="0d173-135">En el panel de resultados de hello, seleccione **Suite adaptable**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0d173-135">In hello results panel, select **Adaptive Suite**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0d173-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d173-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0d173-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Adaptive Suite con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0d173-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0d173-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en conjunto adaptable es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d173-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adaptive Suite is tooa user in Azure AD.</span></span> <span data-ttu-id="0d173-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en conjunto adaptable debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="0d173-140">In other words, a link relationship between an Azure AD user and hello related user in Adaptive Suite needs toobe established.</span></span>

<span data-ttu-id="0d173-141">En conjunto adaptable, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d173-141">In Adaptive Suite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0d173-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Suite adaptable, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0d173-142">tooconfigure and test Azure AD single sign-on with Adaptive Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0d173-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="0d173-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0d173-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0d173-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0d173-145">**[Creación de un usuario de prueba del conjunto adaptable](#creating-an-adaptive-suite-test-user)**  -toohave un equivalente de Britta Simon en conjunto adaptable representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="0d173-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - toohave a counterpart of Britta Simon in Adaptive Suite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0d173-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0d173-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0d173-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0d173-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0d173-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d173-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0d173-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Suite adaptable.</span><span class="sxs-lookup"><span data-stu-id="0d173-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="0d173-150">**inicio de sesión único en tooconfigure Azure AD con Suite adaptable, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d173-150">**tooconfigure Azure AD single sign-on with Adaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d173-151">En el portal de Azure, en Hola Hola **Suite adaptable** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0d173-151">In hello Azure portal, on hello **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0d173-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0d173-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="0d173-155">En hello **adaptable de conjunto de dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0d173-155">On hello **Adaptive Suite Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="0d173-157">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="0d173-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="0d173-158">Puede obtener este valor de hello Suite adaptable **configuración de SSO de SAML** página.</span><span class="sxs-lookup"><span data-stu-id="0d173-158">You can get this value from hello Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="0d173-159">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0d173-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="0d173-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0d173-161">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0d173-163">En hello **adaptable de conjunto de configuración** sección, haga clic en **configurar adaptable Suite** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="0d173-163">On hello **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0d173-164">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="0d173-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="0d173-166">En una ventana del explorador web diferente, inicie sesión en el sitio de la empresa adaptable Suite tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="0d173-166">In a different web browser window, log in tooyour Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="0d173-167">Vaya demasiado**administración**.</span><span class="sxs-lookup"><span data-stu-id="0d173-167">Go too**Admin**.</span></span>
   
    <span data-ttu-id="0d173-168">![Administración](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="0d173-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="0d173-169">Hola **usuarios y Roles** sección, haga clic en **Administrar configuración de SSO de SAML**.</span><span class="sxs-lookup"><span data-stu-id="0d173-169">In hello **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="0d173-170">![Manage SAML SSO Settings (Administrar configuración de SSO de SAML)](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings (Administrar configuración de SSO de SAML)")</span><span class="sxs-lookup"><span data-stu-id="0d173-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="0d173-171">En hello **configuración de SSO de SAML** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0d173-171">On hello **SAML SSO Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="0d173-172">![SAML SSO Settings (Configuración de SSO de) SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings (Configuración de SSO de) SAML")</span><span class="sxs-lookup"><span data-stu-id="0d173-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="0d173-173">a.</span><span class="sxs-lookup"><span data-stu-id="0d173-173">a.</span></span> <span data-ttu-id="0d173-174">Hola **el nombre del proveedor de identidad** cuadro de texto, escriba un nombre para la configuración.</span><span class="sxs-lookup"><span data-stu-id="0d173-174">In hello **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="0d173-175">b.</span><span class="sxs-lookup"><span data-stu-id="0d173-175">b.</span></span> <span data-ttu-id="0d173-176">Hola pegar **Id. de entidad SAML** valor copiado del portal de Azure en hello **proveedor de identidades de Id. de entidad** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0d173-176">Paste hello **SAML Entity ID** value copied from Azure portal into hello **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="0d173-177">c.</span><span class="sxs-lookup"><span data-stu-id="0d173-177">c.</span></span> <span data-ttu-id="0d173-178">Hola pegar **SAML Single Sign-On dirección URL del servicio** valor copiado del portal de Azure en hello **proveedor de identidades de dirección URL SSO** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0d173-178">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="0d173-179">d.</span><span class="sxs-lookup"><span data-stu-id="0d173-179">d.</span></span> <span data-ttu-id="0d173-180">Hola pegar **SAML Single Sign-On dirección URL del servicio** valor copiado del portal de Azure en hello **URL de cierre de sesión personalizada** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0d173-180">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="0d173-181">e.</span><span class="sxs-lookup"><span data-stu-id="0d173-181">e.</span></span> <span data-ttu-id="0d173-182">tooupload el certificado descargado, haga clic en **Elegir archivo**.</span><span class="sxs-lookup"><span data-stu-id="0d173-182">tooupload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="0d173-183">f.</span><span class="sxs-lookup"><span data-stu-id="0d173-183">f.</span></span> <span data-ttu-id="0d173-184">Seleccione siguiente hello, para:</span><span class="sxs-lookup"><span data-stu-id="0d173-184">Select hello following, for:</span></span>
    * <span data-ttu-id="0d173-185">En **SAML user id** (identificador de usuario de SAML), seleccione **User’s Adaptive Insights user name** (Nombre de usuario de Adaptive Insights del usuario).</span><span class="sxs-lookup"><span data-stu-id="0d173-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="0d173-186">En **SAML user id location** (Ubicación del id. de usuario de SAML), seleccione **User id in NameID of Subject** (identificador de usuario en NameID del tema).</span><span class="sxs-lookup"><span data-stu-id="0d173-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="0d173-187">En **SAML NameID format** (Formato de NameID de SAML), seleccione **Email address** (Dirección de correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="0d173-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="0d173-188">En **Enable SAML** (Habilitar SAML), seleccione **Allow SAML SSO and direct Adaptive Insights login** (Permitir inicio de sesión único de SAML e inicio de sesión directo de Adaptive Insights).</span><span class="sxs-lookup"><span data-stu-id="0d173-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="0d173-189">g.</span><span class="sxs-lookup"><span data-stu-id="0d173-189">g.</span></span> <span data-ttu-id="0d173-190">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0d173-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0d173-191">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="0d173-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0d173-192">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="0d173-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0d173-193">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0d173-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0d173-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d173-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="0d173-195">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="0d173-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0d173-197">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d173-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d173-198">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0d173-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0d173-200">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0d173-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0d173-202">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d173-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0d173-204">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0d173-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0d173-206">a.</span><span class="sxs-lookup"><span data-stu-id="0d173-206">a.</span></span> <span data-ttu-id="0d173-207">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0d173-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0d173-208">b.</span><span class="sxs-lookup"><span data-stu-id="0d173-208">b.</span></span> <span data-ttu-id="0d173-209">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0d173-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0d173-210">c.</span><span class="sxs-lookup"><span data-stu-id="0d173-210">c.</span></span> <span data-ttu-id="0d173-211">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0d173-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0d173-212">d.</span><span class="sxs-lookup"><span data-stu-id="0d173-212">d.</span></span> <span data-ttu-id="0d173-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0d173-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="0d173-214">Creación de un usuario de prueba de Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="0d173-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="0d173-215">toolog de los usuarios de Azure AD tooenable en tooAdaptive Suite, se les deben aprovisionar en conjunto adaptable.</span><span class="sxs-lookup"><span data-stu-id="0d173-215">tooenable Azure AD users toolog in tooAdaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="0d173-216">En caso de hello de Suite adaptable, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="0d173-216">In hello case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="0d173-217">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d173-217">**tooconfigure user provisioning, perform hello following steps:**</span></span> 

1. <span data-ttu-id="0d173-218">Inicie sesión en tooyour **Suite adaptable** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="0d173-218">Log in tooyour **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="0d173-219">Vaya demasiado**administración**.</span><span class="sxs-lookup"><span data-stu-id="0d173-219">Go too**Admin**.</span></span>
   
   <span data-ttu-id="0d173-220">![Administración](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="0d173-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="0d173-221">Hola **usuarios y Roles** sección, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="0d173-221">In hello **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="0d173-222">![Agregar usuario](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="0d173-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="0d173-223">Hola **nuevo usuario** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0d173-223">In hello **New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="0d173-224">![Enviar](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Enviar")</span><span class="sxs-lookup"><span data-stu-id="0d173-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="0d173-225">a.</span><span class="sxs-lookup"><span data-stu-id="0d173-225">a.</span></span> <span data-ttu-id="0d173-226">Hola de tipo **nombre**, **inicio de sesión**, **correo electrónico**, **contraseña** de un usuario válido de Azure Active Directory que quiera tooprovision en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="0d173-226">Type hello **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
  
   <span data-ttu-id="0d173-227">b.</span><span class="sxs-lookup"><span data-stu-id="0d173-227">b.</span></span> <span data-ttu-id="0d173-228">Seleccione un **Role**(rol).</span><span class="sxs-lookup"><span data-stu-id="0d173-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="0d173-229">c.</span><span class="sxs-lookup"><span data-stu-id="0d173-229">c.</span></span> <span data-ttu-id="0d173-230">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="0d173-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="0d173-231">Puede usar cualquier otro conjunto adaptable herramienta cuentas de usuario creación o las API proporcionadas por conjunto adaptable tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="0d173-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0d173-232">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d173-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0d173-233">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAdaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="0d173-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdaptive Suite.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0d173-235">**tooassign Britta Simon tooAdaptive Suite, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d173-235">**tooassign Britta Simon tooAdaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d173-236">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0d173-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0d173-238">En la lista de aplicaciones de hello, seleccione **Suite adaptable**.</span><span class="sxs-lookup"><span data-stu-id="0d173-238">In hello applications list, select **Adaptive Suite**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="0d173-240">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0d173-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0d173-242">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0d173-242">Click **Add** button.</span></span> <span data-ttu-id="0d173-243">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0d173-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0d173-245">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d173-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0d173-246">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0d173-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0d173-247">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0d173-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0d173-248">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0d173-248">Testing single sign-on</span></span>

<span data-ttu-id="0d173-249">objetivo de Hola de esta sección es tootest el inicio de sesión único en Microsoft Azure AD de configuración mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0d173-249">hello objective of this section is tootest your Microsoft Azure AD Single Sign-On configuration using hello Access Panel.</span></span>

<span data-ttu-id="0d173-250">Al hacer clic en icono de Suite adaptable Hola Hola Panel de acceso, deberá obtener aplicaciones de conjunto adaptable tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="0d173-250">When you click hello Adaptive Suite tile in hello Access Panel, you should get automatically signed-on tooyour Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0d173-251">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0d173-251">Additional resources</span></span>

* [<span data-ttu-id="0d173-252">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d173-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0d173-253">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0d173-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png


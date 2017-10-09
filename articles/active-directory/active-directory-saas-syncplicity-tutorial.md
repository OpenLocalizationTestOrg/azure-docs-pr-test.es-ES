---
title: "Tutorial: integración de Azure Active Directory con Syncplicity | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Syncplicity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="31aa8-103">Tutorial: integración de Azure Active Directory con Syncplicity</span><span class="sxs-lookup"><span data-stu-id="31aa8-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="31aa8-104">En este tutorial, aprenderá cómo toointegrate Syncplicity con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="31aa8-104">In this tutorial, you learn how toointegrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31aa8-105">Integración Syncplicity con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="31aa8-105">Integrating Syncplicity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="31aa8-106">Puede controlar en Azure AD que tenga acceso tooSyncplicity</span><span class="sxs-lookup"><span data-stu-id="31aa8-106">You can control in Azure AD who has access tooSyncplicity</span></span>
- <span data-ttu-id="31aa8-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSyncplicity (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31aa8-107">You can enable your users tooautomatically get signed-on tooSyncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31aa8-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="31aa8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="31aa8-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="31aa8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31aa8-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="31aa8-110">Prerequisites</span></span>

<span data-ttu-id="31aa8-111">integración de Azure AD con Syncplicity tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="31aa8-111">tooconfigure Azure AD integration with Syncplicity, you need hello following items:</span></span>

- <span data-ttu-id="31aa8-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31aa8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="31aa8-113">Una suscripción habilitada para el inicio de sesión único en Syncplicity</span><span class="sxs-lookup"><span data-stu-id="31aa8-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31aa8-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="31aa8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31aa8-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="31aa8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31aa8-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="31aa8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="31aa8-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="31aa8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31aa8-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="31aa8-118">Scenario description</span></span>
<span data-ttu-id="31aa8-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="31aa8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31aa8-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="31aa8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31aa8-121">Agregar Syncplicity desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="31aa8-121">Adding Syncplicity from hello gallery</span></span>
2. <span data-ttu-id="31aa8-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31aa8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-hello-gallery"></a><span data-ttu-id="31aa8-123">Agregar Syncplicity desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="31aa8-123">Adding Syncplicity from hello gallery</span></span>
<span data-ttu-id="31aa8-124">integración de hello tooconfigure de Syncplicity en Azure AD, deberá tooadd Syncplicity de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="31aa8-124">tooconfigure hello integration of Syncplicity into Azure AD, you need tooadd Syncplicity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="31aa8-125">**tooadd Syncplicity de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="31aa8-125">**tooadd Syncplicity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="31aa8-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="31aa8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="31aa8-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="31aa8-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="31aa8-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31aa8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="31aa8-133">En el cuadro de búsqueda de hello, escriba **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-133">In hello search box, type **Syncplicity**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="31aa8-135">En el panel de resultados de hello, seleccione **Syncplicity**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="31aa8-135">In hello results panel, select **Syncplicity**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31aa8-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31aa8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31aa8-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Syncplicity con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31aa8-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="31aa8-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Syncplicity es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31aa8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Syncplicity is tooa user in Azure AD.</span></span> <span data-ttu-id="31aa8-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Syncplicity debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="31aa8-140">In other words, a link relationship between an Azure AD user and hello related user in Syncplicity needs toobe established.</span></span>

<span data-ttu-id="31aa8-141">En Syncplicity, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="31aa8-141">In Syncplicity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="31aa8-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Syncplicity, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="31aa8-142">tooconfigure and test Azure AD single sign-on with Syncplicity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="31aa8-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="31aa8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="31aa8-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="31aa8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31aa8-145">**[Crear un usuario de prueba de Syncplicity](#creating-a-syncplicity-test-user)**  -toohave un equivalente de Britta Simon en Syncplicity que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="31aa8-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - toohave a counterpart of Britta Simon in Syncplicity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="31aa8-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="31aa8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31aa8-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="31aa8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31aa8-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31aa8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31aa8-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="31aa8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="31aa8-150">**inicio de sesión único en tooconfigure Azure AD con Syncplicity, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="31aa8-150">**tooconfigure Azure AD single sign-on with Syncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="31aa8-151">En el portal de Azure, en Hola Hola **Syncplicity** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-151">In hello Azure portal, on hello **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="31aa8-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="31aa8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="31aa8-155">En hello **Syncplicity dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="31aa8-155">On hello **Syncplicity Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="31aa8-157">a.</span><span class="sxs-lookup"><span data-stu-id="31aa8-157">a.</span></span> <span data-ttu-id="31aa8-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="31aa8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="31aa8-159">b.</span><span class="sxs-lookup"><span data-stu-id="31aa8-159">b.</span></span> <span data-ttu-id="31aa8-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="31aa8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="31aa8-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="31aa8-161">These values are not real.</span></span> <span data-ttu-id="31aa8-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="31aa8-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="31aa8-163">Póngase en contacto con [equipo de soporte técnico de cliente de Syncplicity](https://www.syncplicity.com/contact-us) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="31aa8-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) tooget these values.</span></span> 
 

4. <span data-ttu-id="31aa8-164">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="31aa8-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="31aa8-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="31aa8-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="31aa8-168">En hello **configuración de Syncplicity** sección, haga clic en **configurar Syncplicity** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="31aa8-168">On hello **Syncplicity Configuration** section, click **Configure Syncplicity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="31aa8-169">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="31aa8-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="31aa8-171">Inicie sesión en tooyour **Syncplicity** inquilino.</span><span class="sxs-lookup"><span data-stu-id="31aa8-171">Sign in tooyour **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="31aa8-172">En el menú de hello en la parte superior de hello, haga clic en **administración**, seleccione **configuración**y, a continuación, haga clic en **dominio personalizado y single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-172">In hello menu on hello top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="31aa8-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="31aa8-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="31aa8-174">En hello **inicio de sesión único (SSO)** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="31aa8-174">On hello **Single Sign-On (SSO)** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="31aa8-175">![Inicio de sesión único \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="31aa8-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="31aa8-176">a.</span><span class="sxs-lookup"><span data-stu-id="31aa8-176">a.</span></span> <span data-ttu-id="31aa8-177">Hola **dominio personalizado** cuadro de texto, nombre de tipo hello de su dominio.</span><span class="sxs-lookup"><span data-stu-id="31aa8-177">In hello **Custom Domain** textbox, type hello name of your domain.</span></span>
  
    <span data-ttu-id="31aa8-178">b.</span><span class="sxs-lookup"><span data-stu-id="31aa8-178">b.</span></span> <span data-ttu-id="31aa8-179">Seleccione **Enabled** (Habilitado) como **Single Sign-On Status** (Estado de inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="31aa8-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="31aa8-180">c.</span><span class="sxs-lookup"><span data-stu-id="31aa8-180">c.</span></span> <span data-ttu-id="31aa8-181">Hola **Id. de entidad** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="31aa8-181">In hello **Entity Id** textbox, Paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="31aa8-182">d.</span><span class="sxs-lookup"><span data-stu-id="31aa8-182">d.</span></span> <span data-ttu-id="31aa8-183">Hola **URL de la página de inicio de sesión** cuadro de texto, hello pegar **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="31aa8-183">In hello **Sign-in page URL** textbox, Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="31aa8-184">e.</span><span class="sxs-lookup"><span data-stu-id="31aa8-184">e.</span></span> <span data-ttu-id="31aa8-185">Hola **URL de la página de cierre de sesión** cuadro de texto, hello pegar **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="31aa8-185">In hello **Logout page URL** textbox, Paste hello **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="31aa8-186">f.</span><span class="sxs-lookup"><span data-stu-id="31aa8-186">f.</span></span> <span data-ttu-id="31aa8-187">En **certificado del proveedor de identidad**, haga clic en **Elegir archivo**y, a continuación, cargar el certificado de Hola que ha descargado de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="31aa8-187">In **Identity Provider Certificate**, click **Choose file**, and then upload hello certificate which you have downloaded from hello Azure portal.</span></span> 

    <span data-ttu-id="31aa8-188">g.</span><span class="sxs-lookup"><span data-stu-id="31aa8-188">g.</span></span> <span data-ttu-id="31aa8-189">Haga clic en **GURDAR CAMBIOS**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="31aa8-190">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="31aa8-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="31aa8-191">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="31aa8-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="31aa8-192">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="31aa8-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31aa8-193">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="31aa8-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="31aa8-194">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="31aa8-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="31aa8-196">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="31aa8-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="31aa8-197">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="31aa8-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="31aa8-199">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="31aa8-201">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="31aa8-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="31aa8-203">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="31aa8-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31aa8-205">a.</span><span class="sxs-lookup"><span data-stu-id="31aa8-205">a.</span></span> <span data-ttu-id="31aa8-206">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31aa8-207">b.</span><span class="sxs-lookup"><span data-stu-id="31aa8-207">b.</span></span> <span data-ttu-id="31aa8-208">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="31aa8-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31aa8-209">c.</span><span class="sxs-lookup"><span data-stu-id="31aa8-209">c.</span></span> <span data-ttu-id="31aa8-210">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="31aa8-211">d.</span><span class="sxs-lookup"><span data-stu-id="31aa8-211">d.</span></span> <span data-ttu-id="31aa8-212">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="31aa8-213">Creación de un usuario de prueba de Syncplicity</span><span class="sxs-lookup"><span data-stu-id="31aa8-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="31aa8-214">Para AAD a los usuarios toobe puede toosign en, deben ser aprovisionados tooSyncplicity aplicación.</span><span class="sxs-lookup"><span data-stu-id="31aa8-214">For AAD users toobe able toosign in, they must be provisioned tooSyncplicity application.</span></span> <span data-ttu-id="31aa8-215">Esta sección describe cómo las cuentas de usuario AAD de toocreate en Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="31aa8-215">This section describes how toocreate AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="31aa8-216">**tooprovision un tooSyncplicity de cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="31aa8-216">**tooprovision a user account tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="31aa8-217">Inicie sesión en tooyour **Syncplicity** inquilino (por ejemplo: `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="31aa8-217">Log in tooyour **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="31aa8-218">Haga clic en **admin** y seleccione **cuentas de usuario**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="31aa8-219">Haga clic en **ADD A USER** (AGREGAR UN USUARIO).</span><span class="sxs-lookup"><span data-stu-id="31aa8-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="31aa8-220">![Administración de usuarios](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Administración de usuarios")</span><span class="sxs-lookup"><span data-stu-id="31aa8-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="31aa8-221">Hola de tipo **direcciones de correo electrónico** de una cuenta AAD que desee tooprovision, seleccione **usuario** como **rol**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-221">Type hello **Email addressess** of an AAD account you want tooprovision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="31aa8-222">![Información de la cuenta](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Información de la cuenta")</span><span class="sxs-lookup"><span data-stu-id="31aa8-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="31aa8-223">titular de la cuenta de Hello AAD Obtiene un correo electrónico con un vínculo tooconfirm y activar la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="31aa8-223">hello AAD account holder  gets an email including a link tooconfirm and activate hello account.</span></span> 
    > 

5. <span data-ttu-id="31aa8-224">Seleccione un grupo de la compañía de la que debe convertirse en miembro su nuevo usuario y haga clic en **NEXT**(SIGUIENTE).</span><span class="sxs-lookup"><span data-stu-id="31aa8-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="31aa8-225">![Pertenencia a grupos](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Pertenencia a grupos")</span><span class="sxs-lookup"><span data-stu-id="31aa8-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="31aa8-226">Si no se muestra ningún grupo, haga clic en **NEXT**(SIGUIENTE).</span><span class="sxs-lookup"><span data-stu-id="31aa8-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="31aa8-227">Seleccione las carpetas de Hola que desee tooplace Syncplicity controle en el equipo del usuario de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-227">Select hello folders you would like tooplace under Syncplicity’s control on hello user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="31aa8-228">![Carpetas de Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Carpetas de Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="31aa8-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="31aa8-229">Puede usar cualquier otra Syncplicity usuario cuenta herramienta de creación o las API proporcionadas por Syncplicity tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="31aa8-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="31aa8-230">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="31aa8-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="31aa8-231">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSyncplicity.</span><span class="sxs-lookup"><span data-stu-id="31aa8-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSyncplicity.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="31aa8-233">**tooassign Britta Simon tooSyncplicity, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="31aa8-233">**tooassign Britta Simon tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="31aa8-234">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="31aa8-236">En la lista de aplicaciones de hello, seleccione **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-236">In hello applications list, select **Syncplicity**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="31aa8-238">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="31aa8-240">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-240">Click **Add** button.</span></span> <span data-ttu-id="31aa8-241">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="31aa8-243">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="31aa8-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="31aa8-244">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31aa8-245">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="31aa8-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31aa8-246">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="31aa8-246">Testing single sign-on</span></span>

<span data-ttu-id="31aa8-247">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="31aa8-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="31aa8-248">Al hacer clic en icono de Syncplicity Hola Hola Panel de acceso, deberá obtener aplicaciones de Syncplicity tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="31aa8-248">When you click hello Syncplicity tile in hello Access Panel, you should get automatically signed-on tooyour Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="31aa8-249">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="31aa8-249">Additional resources</span></span>

* [<span data-ttu-id="31aa8-250">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31aa8-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31aa8-251">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="31aa8-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png


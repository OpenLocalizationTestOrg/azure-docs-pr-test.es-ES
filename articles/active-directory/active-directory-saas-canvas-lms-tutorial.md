---
title: "Tutorial: Integración de Azure Active Directory con Canvas Lms | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Canvas LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="93140-103">Tutorial: integración de Azure Active Directory con Canvas Lms</span><span class="sxs-lookup"><span data-stu-id="93140-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="93140-104">En este tutorial, aprenderá cómo toointegrate lienzo con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="93140-104">In this tutorial, you learn how toointegrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="93140-105">Integración lienzo con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="93140-105">Integrating Canvas with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="93140-106">Puede controlar en Azure AD que tenga acceso tooCanvas</span><span class="sxs-lookup"><span data-stu-id="93140-106">You can control in Azure AD who has access tooCanvas</span></span>
- <span data-ttu-id="93140-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooCanvas (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="93140-107">You can enable your users tooautomatically get signed-on tooCanvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="93140-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="93140-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="93140-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="93140-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93140-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="93140-110">Prerequisites</span></span>

<span data-ttu-id="93140-111">tooconfigure integración de Azure AD con Canvas, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="93140-111">tooconfigure Azure AD integration with Canvas, you need hello following items:</span></span>

- <span data-ttu-id="93140-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="93140-112">An Azure AD subscription</span></span>
- <span data-ttu-id="93140-113">Una suscripción habilitada para el inicio de sesión único en Canvas</span><span class="sxs-lookup"><span data-stu-id="93140-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="93140-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="93140-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="93140-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="93140-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="93140-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="93140-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="93140-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="93140-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="93140-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="93140-118">Scenario description</span></span>
<span data-ttu-id="93140-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="93140-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="93140-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="93140-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="93140-121">Agregar lienzo de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="93140-121">Adding Canvas from hello gallery</span></span>
2. <span data-ttu-id="93140-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="93140-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-hello-gallery"></a><span data-ttu-id="93140-123">Agregar lienzo de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="93140-123">Adding Canvas from hello gallery</span></span>
<span data-ttu-id="93140-124">integración de hello tooconfigure del lienzo en Azure AD, deberá tooadd lienzo de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="93140-124">tooconfigure hello integration of Canvas into Azure AD, you need tooadd Canvas from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="93140-125">**tooadd lienzo de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="93140-125">**tooadd Canvas from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="93140-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="93140-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="93140-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="93140-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="93140-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="93140-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="93140-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="93140-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="93140-133">En el cuadro de búsqueda de hello, escriba **lienzo**.</span><span class="sxs-lookup"><span data-stu-id="93140-133">In hello search box, type **Canvas**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="93140-135">En el panel de resultados de hello, seleccione **lienzo**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="93140-135">In hello results panel, select **Canvas**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="93140-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="93140-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="93140-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Canvas con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="93140-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="93140-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el lienzo es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93140-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Canvas is tooa user in Azure AD.</span></span> <span data-ttu-id="93140-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el lienzo debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="93140-140">In other words, a link relationship between an Azure AD user and hello related user in Canvas needs toobe established.</span></span>

<span data-ttu-id="93140-141">En el lienzo, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="93140-141">In Canvas, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="93140-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Canvas, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="93140-142">tooconfigure and test Azure AD single sign-on with Canvas, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="93140-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="93140-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="93140-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="93140-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="93140-145">**[Crear un usuario de prueba de lienzo](#creating-a-canvas-test-user)**  -toohave un equivalente de Britta Simon en lienzo que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="93140-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - toohave a counterpart of Britta Simon in Canvas that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="93140-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="93140-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="93140-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="93140-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="93140-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="93140-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="93140-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación del lienzo.</span><span class="sxs-lookup"><span data-stu-id="93140-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="93140-150">**inicio de sesión único en tooconfigure Azure AD con Canvas, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="93140-150">**tooconfigure Azure AD single sign-on with Canvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="93140-151">En el portal de Azure, en Hola Hola **lienzo** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="93140-151">In hello Azure portal, on hello **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="93140-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="93140-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="93140-155">En hello **lienzo de dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="93140-155">On hello **Canvas Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="93140-157">a.</span><span class="sxs-lookup"><span data-stu-id="93140-157">a.</span></span> <span data-ttu-id="93140-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="93140-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="93140-159">b.</span><span class="sxs-lookup"><span data-stu-id="93140-159">b.</span></span> <span data-ttu-id="93140-160">Hola **identificador** cuadro de texto, valor de tipo hello mediante Hola sigue el patrón:`https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="93140-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="93140-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="93140-161">These values are not real.</span></span> <span data-ttu-id="93140-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="93140-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="93140-163">Póngase en contacto con [equipo de soporte técnico de cliente de lienzo](https://community.canvaslms.com/community/help) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="93140-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) tooget these values.</span></span> 
 
4. <span data-ttu-id="93140-164">En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** el valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="93140-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="93140-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="93140-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="93140-168">En hello **configuración lienzo** sección, haga clic en **configurar lienzo** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="93140-168">On hello **Canvas Configuration** section, click **Configure Canvas** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="93140-169">Hola copia **cambiar dirección URL de contraseña, dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="93140-169">Copy hello **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="93140-171">En una ventana del explorador web diferente, inicie sesión en el sitio de empresa de Canvas de tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="93140-171">In a different web browser window, log in tooyour Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="93140-172">Vaya demasiado**cursos \> cuentas administradas \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="93140-172">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="93140-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="93140-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="93140-174">En el panel de navegación de Hola Hola izquierda, seleccione **autenticación**y, a continuación, haga clic en **agregar nueva configuración de SAML**.</span><span class="sxs-lookup"><span data-stu-id="93140-174">In hello navigation pane on hello left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="93140-175">![Autenticación](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Autenticación")</span><span class="sxs-lookup"><span data-stu-id="93140-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="93140-176">En la página de integración actual de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="93140-176">On hello Current Integration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="93140-177">![Integración actual](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Integración actual")</span><span class="sxs-lookup"><span data-stu-id="93140-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="93140-178">a.</span><span class="sxs-lookup"><span data-stu-id="93140-178">a.</span></span> <span data-ttu-id="93140-179">En **Id. de entidad IdP** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="93140-179">In **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="93140-180">b.</span><span class="sxs-lookup"><span data-stu-id="93140-180">b.</span></span> <span data-ttu-id="93140-181">En **dirección URL de registro** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="93140-181">In **Log On URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="93140-182">c.</span><span class="sxs-lookup"><span data-stu-id="93140-182">c.</span></span> <span data-ttu-id="93140-183">En **URL de cierre de registro** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="93140-183">In **Log Out URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="93140-184">d.</span><span class="sxs-lookup"><span data-stu-id="93140-184">d.</span></span> <span data-ttu-id="93140-185">En **vínculo de cambio de contraseña** cuadro de texto, pegue Hola valo **cambiar dirección URL de contraseña** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="93140-185">In **Change Password Link** textbox, paste hello value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="93140-186">e.</span><span class="sxs-lookup"><span data-stu-id="93140-186">e.</span></span> <span data-ttu-id="93140-187">En **huella digital de certificado** cuadro de texto, pegue hello **huella digital** el valor de certificado que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="93140-187">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="93140-188">f.</span><span class="sxs-lookup"><span data-stu-id="93140-188">f.</span></span> <span data-ttu-id="93140-189">De hello **atributo de inicio de sesión** lista, seleccione **NameID**.</span><span class="sxs-lookup"><span data-stu-id="93140-189">From hello **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="93140-190">g.</span><span class="sxs-lookup"><span data-stu-id="93140-190">g.</span></span> <span data-ttu-id="93140-191">De hello **formato de identificador** lista, seleccione **emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="93140-191">From hello **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="93140-192">h.</span><span class="sxs-lookup"><span data-stu-id="93140-192">h.</span></span> <span data-ttu-id="93140-193">Haga clic en **Guardar configuración de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="93140-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="93140-194">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="93140-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="93140-195">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="93140-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="93140-196">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="93140-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="93140-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="93140-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="93140-198">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="93140-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="93140-200">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="93140-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="93140-201">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="93140-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="93140-203">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="93140-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="93140-205">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="93140-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="93140-207">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="93140-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="93140-209">a.</span><span class="sxs-lookup"><span data-stu-id="93140-209">a.</span></span> <span data-ttu-id="93140-210">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="93140-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="93140-211">b.</span><span class="sxs-lookup"><span data-stu-id="93140-211">b.</span></span> <span data-ttu-id="93140-212">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="93140-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="93140-213">c.</span><span class="sxs-lookup"><span data-stu-id="93140-213">c.</span></span> <span data-ttu-id="93140-214">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="93140-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="93140-215">d.</span><span class="sxs-lookup"><span data-stu-id="93140-215">d.</span></span> <span data-ttu-id="93140-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="93140-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="93140-217">Creación de un usuario de prueba de Canvas</span><span class="sxs-lookup"><span data-stu-id="93140-217">Creating a Canvas test user</span></span>

<span data-ttu-id="93140-218">toolog de los usuarios de Azure AD tooenable en tooCanvas, se les deben aprovisionar en el lienzo.</span><span class="sxs-lookup"><span data-stu-id="93140-218">tooenable Azure AD users toolog in tooCanvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="93140-219">En el caso de Canvas, el aprovisionamiento de usuario es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="93140-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="93140-220">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="93140-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="93140-221">Inicie sesión en tooyour **lienzo** inquilino.</span><span class="sxs-lookup"><span data-stu-id="93140-221">Log in tooyour **Canvas** tenant.</span></span>

2. <span data-ttu-id="93140-222">Vaya demasiado**cursos \> cuentas administradas \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="93140-222">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="93140-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="93140-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="93140-224">Haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="93140-224">Click **Users**.</span></span>
   
   <span data-ttu-id="93140-225">![Usuarios](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="93140-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="93140-226">Haga clic en **Add New User**(Agregar nuevo usuario).</span><span class="sxs-lookup"><span data-stu-id="93140-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="93140-227">![Usuarios](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="93140-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="93140-228">En hello agregar una página de diálogo nuevo usuario, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="93140-228">On hello Add a New User dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="93140-229">![Agregar usuario](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="93140-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="93140-230">a.</span><span class="sxs-lookup"><span data-stu-id="93140-230">a.</span></span> <span data-ttu-id="93140-231">Hola **nombre completo** cuadro de texto, escriba Hola nombre de usuario como **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="93140-231">In hello **Full Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="93140-232">b.</span><span class="sxs-lookup"><span data-stu-id="93140-232">b.</span></span> <span data-ttu-id="93140-233">Hola **correo electrónico** cuadro de texto, escriba el correo electrónico de saludo del usuario como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="93140-233">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="93140-234">c.</span><span class="sxs-lookup"><span data-stu-id="93140-234">c.</span></span> <span data-ttu-id="93140-235">Hola **inicio de sesión** cuadro de texto, escriba la dirección de correo electrónico del usuario de hello Azure AD como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="93140-235">In hello **Login** textbox, enter hello user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="93140-236">d.</span><span class="sxs-lookup"><span data-stu-id="93140-236">d.</span></span> <span data-ttu-id="93140-237">Seleccione **usuario Hola de correo electrónico acerca de la creación de esta cuenta**.</span><span class="sxs-lookup"><span data-stu-id="93140-237">Select **Email hello user about this account creation**.</span></span>

   <span data-ttu-id="93140-238">e.</span><span class="sxs-lookup"><span data-stu-id="93140-238">e.</span></span> <span data-ttu-id="93140-239">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="93140-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="93140-240">Puede usar cualquier otra lienzo usuario cuenta herramienta de creación o las API proporcionadas por Canvas tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="93140-240">You can use any other Canvas user account creation tools or APIs provided by Canvas tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="93140-241">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="93140-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="93140-242">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCanvas.</span><span class="sxs-lookup"><span data-stu-id="93140-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCanvas.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="93140-244">**tooassign Britta Simon tooCanvas, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="93140-244">**tooassign Britta Simon tooCanvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="93140-245">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="93140-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="93140-247">En la lista de aplicaciones de hello, seleccione **lienzo**.</span><span class="sxs-lookup"><span data-stu-id="93140-247">In hello applications list, select **Canvas**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="93140-249">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="93140-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="93140-251">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="93140-251">Click **Add** button.</span></span> <span data-ttu-id="93140-252">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="93140-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="93140-254">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="93140-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="93140-255">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="93140-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="93140-256">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="93140-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="93140-257">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="93140-257">Testing single sign-on</span></span>

<span data-ttu-id="93140-258">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="93140-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="93140-259">Al hacer clic en icono de lienzo Hola Hola Panel de acceso, deberá obtener la aplicación de lienzo tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="93140-259">When you click hello Canvas tile in hello Access Panel, you should get automatically signed-on tooyour Canvas application.</span></span>
<span data-ttu-id="93140-260">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="93140-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="93140-261">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="93140-261">Additional resources</span></span>

* [<span data-ttu-id="93140-262">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93140-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="93140-263">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="93140-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png


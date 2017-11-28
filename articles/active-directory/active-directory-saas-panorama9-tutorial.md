---
title: "Tutorial: Integración de Azure Active Directory con Panorama9 | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Panorama9."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 548fb6434d920e076db98a0193f8dfdf8a958a91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="4c776-103">Tutorial: Integración de Azure Active Directory con Panorama9</span><span class="sxs-lookup"><span data-stu-id="4c776-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="4c776-104">En este tutorial, aprenderá cómo toointegrate Panorama9 con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c776-104">In this tutorial, you learn how toointegrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c776-105">Integración de Panorama9 con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="4c776-105">Integrating Panorama9 with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4c776-106">Puede controlar en Azure AD que tenga acceso tooPanorama9</span><span class="sxs-lookup"><span data-stu-id="4c776-106">You can control in Azure AD who has access tooPanorama9</span></span>
- <span data-ttu-id="4c776-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPanorama9 (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c776-107">You can enable your users tooautomatically get signed-on tooPanorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c776-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4c776-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4c776-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c776-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c776-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4c776-110">Prerequisites</span></span>

<span data-ttu-id="4c776-111">integración de Azure AD con Panorama9 tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4c776-111">tooconfigure Azure AD integration with Panorama9, you need hello following items:</span></span>

- <span data-ttu-id="4c776-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c776-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c776-113">Una suscripción habilitada para el inicio de sesión único en Panorama9</span><span class="sxs-lookup"><span data-stu-id="4c776-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c776-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4c776-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c776-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="4c776-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c776-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4c776-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c776-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c776-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c776-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="4c776-118">Scenario description</span></span>
<span data-ttu-id="4c776-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="4c776-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c776-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="4c776-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c776-121">Agregar Panorama9 desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4c776-121">Adding Panorama9 from hello gallery</span></span>
2. <span data-ttu-id="4c776-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c776-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-hello-gallery"></a><span data-ttu-id="4c776-123">Agregar Panorama9 desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="4c776-123">Adding Panorama9 from hello gallery</span></span>
<span data-ttu-id="4c776-124">integración de hello tooconfigure de Panorama9 en Azure AD, deberá tooadd Panorama9 de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="4c776-124">tooconfigure hello integration of Panorama9 into Azure AD, you need tooadd Panorama9 from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4c776-125">**tooadd Panorama9 de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4c776-125">**tooadd Panorama9 from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c776-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4c776-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4c776-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="4c776-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4c776-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4c776-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="4c776-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c776-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="4c776-133">En el cuadro de búsqueda de hello, escriba **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="4c776-133">In hello search box, type **Panorama9**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="4c776-135">En el panel de resultados de hello, seleccione **Panorama9**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4c776-135">In hello results panel, select **Panorama9**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c776-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c776-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="4c776-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Panorama9 con un usuario de prueba llamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4c776-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4c776-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Panorama9 es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c776-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panorama9 is tooa user in Azure AD.</span></span> <span data-ttu-id="4c776-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Panorama9 debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="4c776-140">In other words, a link relationship between an Azure AD user and hello related user in Panorama9 needs toobe established.</span></span>

<span data-ttu-id="4c776-141">En Panorama9, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c776-141">In Panorama9, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4c776-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Panorama9, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="4c776-142">tooconfigure and test Azure AD single sign-on with Panorama9, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4c776-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="4c776-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4c776-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c776-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c776-145">**[Crear un usuario de prueba de Panorama9](#creating-a-panorama9-test-user)**  -toohave un equivalente de Britta Simon en Panorama9 que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="4c776-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - toohave a counterpart of Britta Simon in Panorama9 that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4c776-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4c776-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c776-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="4c776-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c776-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c776-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c776-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Panorama9.</span><span class="sxs-lookup"><span data-stu-id="4c776-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="4c776-150">**inicio de sesión único en Azure AD tooconfigure con Panorama9, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4c776-150">**tooconfigure Azure AD single sign-on with Panorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c776-151">En el portal de Azure, en Hola Hola **Panorama9** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="4c776-151">In hello Azure portal, on hello **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="4c776-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="4c776-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="4c776-155">En hello **Panorama9 dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4c776-155">On hello **Panorama9 Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="4c776-157">a.</span><span class="sxs-lookup"><span data-stu-id="4c776-157">a.</span></span> <span data-ttu-id="4c776-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL como:`https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="4c776-158">In hello **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="4c776-159">b.</span><span class="sxs-lookup"><span data-stu-id="4c776-159">b.</span></span> <span data-ttu-id="4c776-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="4c776-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4c776-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="4c776-161">These values are not real.</span></span> <span data-ttu-id="4c776-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="4c776-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4c776-163">Póngase en contacto con [equipo de soporte técnico de cliente de Panorama9](https://support.panorama9.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="4c776-163">Contact [Panorama9 Client support team](https://support.panorama9.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="4c776-164">En hello **el certificado de firma de SAML** Hola de copia, en una sección **huella digital** el valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="4c776-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="4c776-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="4c776-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4c776-168">En hello **configuración de Panorama9** sección, haga clic en **configurar Panorama9** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="4c776-168">On hello **Panorama9 Configuration** section, click **Configure Panorama9** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4c776-169">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="4c776-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="4c776-171">En otra ventana del explorador web, inicie sesión en el sitio de la compañía Panorama9 como administrador.</span><span class="sxs-lookup"><span data-stu-id="4c776-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="4c776-172">En la barra de herramientas de hello en la parte superior de hello, haga clic en **administrar**y, a continuación, haga clic en **extensiones**.</span><span class="sxs-lookup"><span data-stu-id="4c776-172">In hello toolbar on hello top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="4c776-173">![Extensiones](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensiones")</span><span class="sxs-lookup"><span data-stu-id="4c776-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="4c776-174">En hello **extensiones** cuadro de diálogo, haga clic en **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4c776-174">On hello **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="4c776-175">![Inicio de sesión único](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="4c776-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="4c776-176">Hola **configuración** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4c776-176">In hello **Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="4c776-177">![Configuración](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="4c776-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="4c776-178">a.</span><span class="sxs-lookup"><span data-stu-id="4c776-178">a.</span></span> <span data-ttu-id="4c776-179">En **dirección URL del proveedor de identidad** cuadro de texto, pegue Hola valo **URL de servicio de inicio de sesión único**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c776-179">In **Identity provider URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="4c776-180">b.</span><span class="sxs-lookup"><span data-stu-id="4c776-180">b.</span></span> <span data-ttu-id="4c776-181">En **huella digital de certificado** cuadro de texto, pegue hello **huella digital** valor de certificado en el que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c776-181">In **Certificate fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="4c776-182">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4c776-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4c776-183">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="4c776-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4c776-184">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="4c776-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4c776-185">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4c776-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c776-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c776-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="4c776-187">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="4c776-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="4c776-189">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4c776-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c776-190">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="4c776-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4c776-192">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4c776-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4c776-194">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c776-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4c776-196">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="4c776-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c776-198">a.</span><span class="sxs-lookup"><span data-stu-id="4c776-198">a.</span></span> <span data-ttu-id="4c776-199">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c776-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c776-200">b.</span><span class="sxs-lookup"><span data-stu-id="4c776-200">b.</span></span> <span data-ttu-id="4c776-201">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4c776-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c776-202">c.</span><span class="sxs-lookup"><span data-stu-id="4c776-202">c.</span></span> <span data-ttu-id="4c776-203">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="4c776-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4c776-204">d.</span><span class="sxs-lookup"><span data-stu-id="4c776-204">d.</span></span> <span data-ttu-id="4c776-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4c776-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="4c776-206">Creación de un usuario de prueba de Panorama9</span><span class="sxs-lookup"><span data-stu-id="4c776-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="4c776-207">En orden tooenable toolog de los usuarios de Azure AD en Panorama9, se les deben aprovisionar en Panorama9.</span><span class="sxs-lookup"><span data-stu-id="4c776-207">In order tooenable Azure AD users toolog into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="4c776-208">En caso de hello de Panorama9, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="4c776-208">In hello case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="4c776-209">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4c776-209">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c776-210">Inicie sesión en tooyour **Panorama9** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="4c776-210">Log in tooyour **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="4c776-211">En el menú de hello en la parte superior de hello, haga clic en **administrar**y, a continuación, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="4c776-211">In hello menu on hello top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="4c776-212">![Usuarios](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="4c776-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="4c776-213">En la sección usuarios hello, haga clic en  **+**  tooadd nuevo usuario.</span><span class="sxs-lookup"><span data-stu-id="4c776-213">In hello Users section, Click **+** tooadd new user.</span></span>

 <span data-ttu-id="4c776-214">![Usuarios](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="4c776-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="4c776-215">Vaya toohello sección de datos de usuario, Hola de tipo dirección de correo electrónico de un usuario válido de Azure Active Directory que desee tooprovision en hello **correo electrónico** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="4c776-215">Go toohello User data section, type hello email address of a valid Azure Active Directory user you want tooprovision into hello **Email** textbox.</span></span>

5. <span data-ttu-id="4c776-216">Proceder toohello sección usuarios, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="4c776-216">Come toohello Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="4c776-217">titular de la cuenta de Hello Azure Active Directory recibe un correo electrónico y sigue un vínculo tooconfirm su cuenta antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="4c776-217">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4c776-218">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c776-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4c776-219">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooPanorama9.</span><span class="sxs-lookup"><span data-stu-id="4c776-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanorama9.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="4c776-221">**tooassign Britta Simon tooPanorama9, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="4c776-221">**tooassign Britta Simon tooPanorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c776-222">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4c776-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="4c776-224">En la lista de aplicaciones de hello, seleccione **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="4c776-224">In hello applications list, select **Panorama9**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="4c776-226">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4c776-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="4c776-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4c776-228">Click **Add** button.</span></span> <span data-ttu-id="4c776-229">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4c776-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="4c776-231">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c776-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4c776-232">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="4c776-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c776-233">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="4c776-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c776-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="4c776-234">Testing single sign-on</span></span>

<span data-ttu-id="4c776-235">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="4c776-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4c776-236">Al hacer clic en icono hello Panorama9 Hola Panel de acceso, deberá obtener la aplicación tooPanorama9 automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="4c776-236">When you click hello Panorama9 tile in hello Access Panel, you should get automatically signed-on tooPanorama9 application.</span></span>
<span data-ttu-id="4c776-237">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4c776-237">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c776-238">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="4c776-238">Additional resources</span></span>

* [<span data-ttu-id="4c776-239">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c776-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c776-240">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4c776-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png


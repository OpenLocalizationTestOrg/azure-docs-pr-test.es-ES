---
title: "Tutorial: Integración de Azure Active Directory con Marketo | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Marketo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="9cba4-103">Tutorial: integración de Azure Active Directory con Marketo</span><span class="sxs-lookup"><span data-stu-id="9cba4-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="9cba4-104">En este tutorial, aprenderá cómo toointegrate Marketo con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9cba4-104">In this tutorial, you learn how toointegrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9cba4-105">Integración de Marketo con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9cba4-105">Integrating Marketo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9cba4-106">Puede controlar en Azure AD que tenga acceso tooMarketo</span><span class="sxs-lookup"><span data-stu-id="9cba4-106">You can control in Azure AD who has access tooMarketo</span></span>
- <span data-ttu-id="9cba4-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooMarketo (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cba4-107">You can enable your users tooautomatically get signed-on tooMarketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9cba4-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9cba4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9cba4-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9cba4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cba4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9cba4-110">Prerequisites</span></span>

<span data-ttu-id="9cba4-111">integración de Azure AD con Marketo tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9cba4-111">tooconfigure Azure AD integration with Marketo, you need hello following items:</span></span>

- <span data-ttu-id="9cba4-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cba4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9cba4-113">Una suscripción habilitada para el inicio de sesión único en Marketo</span><span class="sxs-lookup"><span data-stu-id="9cba4-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9cba4-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9cba4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9cba4-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9cba4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9cba4-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9cba4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9cba4-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9cba4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9cba4-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9cba4-118">Scenario description</span></span>
<span data-ttu-id="9cba4-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9cba4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9cba4-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="9cba4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9cba4-121">Agregar Marketo desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9cba4-121">Adding Marketo from hello gallery</span></span>
2. <span data-ttu-id="9cba4-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cba4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-hello-gallery"></a><span data-ttu-id="9cba4-123">Agregar Marketo desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9cba4-123">Adding Marketo from hello gallery</span></span>
<span data-ttu-id="9cba4-124">integración de hello tooconfigure de Marketo en Azure AD, deberá tooadd Marketo de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="9cba4-124">tooconfigure hello integration of Marketo into Azure AD, you need tooadd Marketo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9cba4-125">**tooadd Marketo desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9cba4-125">**tooadd Marketo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cba4-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9cba4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9cba4-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9cba4-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="9cba4-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cba4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="9cba4-133">En el cuadro de búsqueda de hello, escriba **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-133">In hello search box, type **Marketo**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="9cba4-135">En el panel de resultados de hello, seleccione **Marketo**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9cba4-135">In hello results panel, select **Marketo**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9cba4-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cba4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9cba4-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Marketo con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9cba4-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9cba4-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Marketo es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cba4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Marketo is tooa user in Azure AD.</span></span> <span data-ttu-id="9cba4-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Marketo debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="9cba4-140">In other words, a link relationship between an Azure AD user and hello related user in Marketo needs toobe established.</span></span>

<span data-ttu-id="9cba4-141">En Marketo, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cba4-141">In Marketo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9cba4-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Marketo, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9cba4-142">tooconfigure and test Azure AD single sign-on with Marketo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9cba4-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="9cba4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9cba4-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9cba4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9cba4-145">**[Crear un usuario de prueba de Marketo](#creating-a-marketo-test-user)**  -toohave un equivalente de Britta Simon en Marketo que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="9cba4-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - toohave a counterpart of Britta Simon in Marketo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9cba4-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9cba4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9cba4-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9cba4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9cba4-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cba4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9cba4-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Marketo.</span><span class="sxs-lookup"><span data-stu-id="9cba4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="9cba4-150">**inicio de sesión único en Azure AD tooconfigure con Marketo, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9cba4-150">**tooconfigure Azure AD single sign-on with Marketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cba4-151">En el portal de Azure, en Hola Hola **Marketo** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-151">In hello Azure portal, on hello **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="9cba4-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9cba4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="9cba4-155">En hello **Marketo dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9cba4-155">On hello **Marketo Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="9cba4-157">a.</span><span class="sxs-lookup"><span data-stu-id="9cba4-157">a.</span></span> <span data-ttu-id="9cba4-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="9cba4-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="9cba4-159">b.</span><span class="sxs-lookup"><span data-stu-id="9cba4-159">b.</span></span> <span data-ttu-id="9cba4-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="9cba4-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9cba4-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="9cba4-161">These values are not real.</span></span> <span data-ttu-id="9cba4-162">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="9cba4-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="9cba4-163">Póngase en contacto con [equipo de soporte técnico de Marketo](http://investors.marketo.com/contactus.cfm) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="9cba4-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) tooget these values.</span></span>
 
4. <span data-ttu-id="9cba4-164">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9cba4-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="9cba4-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9cba4-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9cba4-168">En hello **configuración de Marketo** sección, haga clic en **configurar Marketo** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="9cba4-168">On hello **Marketo Configuration** section, click **Configure Marketo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9cba4-169">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="9cba4-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="9cba4-171">tooget Munchkin identificador de la aplicación, inicie sesión en tooMarketo usando credenciales de administrador y realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="9cba4-171">tooget Munchkin Id of your application, log in tooMarketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="9cba4-172">a.</span><span class="sxs-lookup"><span data-stu-id="9cba4-172">a.</span></span> <span data-ttu-id="9cba4-173">Inicie sesión en la aplicación tooMarketo usando credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="9cba4-173">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="9cba4-174">b.</span><span class="sxs-lookup"><span data-stu-id="9cba4-174">b.</span></span> <span data-ttu-id="9cba4-175">Haga clic en hello **administración** botón en el panel de navegación superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cba4-175">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="9cba4-177">c.</span><span class="sxs-lookup"><span data-stu-id="9cba4-177">c.</span></span> <span data-ttu-id="9cba4-178">Navegar por el menú de la integración de toohello y haga clic en hello **vínculo Munchkin**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-178">Navigate toohello Integration menu and click hello **Munchkin link**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="9cba4-180">d.</span><span class="sxs-lookup"><span data-stu-id="9cba4-180">d.</span></span> <span data-ttu-id="9cba4-181">Copie Hola Id. de Munchkin mostrado en pantalla de bienvenida y completar la dirección URL de respuesta en el Asistente para configuración de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cba4-181">Copy hello Munchkin Id shown on hello screen and complete your Reply URL in hello Azure AD configuration wizard.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="9cba4-183">Hola tooconfigure SSO en la aplicación hello, siga Hola pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9cba4-183">tooconfigure hello SSO in hello application, follow hello below steps:</span></span>
   
    <span data-ttu-id="9cba4-184">a.</span><span class="sxs-lookup"><span data-stu-id="9cba4-184">a.</span></span> <span data-ttu-id="9cba4-185">Inicie sesión en la aplicación tooMarketo usando credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="9cba4-185">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="9cba4-186">b.</span><span class="sxs-lookup"><span data-stu-id="9cba4-186">b.</span></span> <span data-ttu-id="9cba4-187">Haga clic en hello **administración** botón en el panel de navegación superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cba4-187">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="9cba4-189">c.</span><span class="sxs-lookup"><span data-stu-id="9cba4-189">c.</span></span> <span data-ttu-id="9cba4-190">Navegar por el menú de la integración de toohello y haga clic en **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-190">Navigate toohello Integration menu and click **Single Sign On**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="9cba4-192">d.</span><span class="sxs-lookup"><span data-stu-id="9cba4-192">d.</span></span> <span data-ttu-id="9cba4-193">Hola tooenable configuración de SAML, haga clic en **editar** botón.</span><span class="sxs-lookup"><span data-stu-id="9cba4-193">tooenable hello SAML Settings, click **Edit** button.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="9cba4-195">e.</span><span class="sxs-lookup"><span data-stu-id="9cba4-195">e.</span></span> <span data-ttu-id="9cba4-196">Ya está la configuración de inicio de sesión único **habilitada**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="9cba4-197">f.</span><span class="sxs-lookup"><span data-stu-id="9cba4-197">f.</span></span> <span data-ttu-id="9cba4-198">Hola pegar **Id. de entidad SAML**, Hola **Id. del emisor** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="9cba4-198">Paste hello **SAML Entity ID**, in hello **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="9cba4-199">g.</span><span class="sxs-lookup"><span data-stu-id="9cba4-199">g.</span></span> <span data-ttu-id="9cba4-200">Hola **Id. de entidad** cuadro de texto, escriba la dirección URL de hello como `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="9cba4-200">In hello **Entity ID** textbox, enter hello URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="9cba4-201">h.</span><span class="sxs-lookup"><span data-stu-id="9cba4-201">h.</span></span> <span data-ttu-id="9cba4-202">Hola seleccione ubicación del identificador de usuario como **elemento de identificador de nombre**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-202">Select hello User ID Location as **Name Identifier element**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="9cba4-204">Si el identificador de usuario no es el valor UPN, a continuación, cambiar el valor de hello en la pestaña del atributo Hola.</span><span class="sxs-lookup"><span data-stu-id="9cba4-204">If your User Identifier is not UPN value then change hello value in hello Attribute tab.</span></span>
   
    <span data-ttu-id="9cba4-205">i.</span><span class="sxs-lookup"><span data-stu-id="9cba4-205">i.</span></span> <span data-ttu-id="9cba4-206">Cargar certificado de hello, que ha descargado desde el Asistente para configuración de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cba4-206">Upload hello certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="9cba4-207">**Guardar** Hola configuración.</span><span class="sxs-lookup"><span data-stu-id="9cba4-207">**Save** hello settings.</span></span>
   
    <span data-ttu-id="9cba4-208">j.</span><span class="sxs-lookup"><span data-stu-id="9cba4-208">j.</span></span> <span data-ttu-id="9cba4-209">Editar la configuración de redirección de páginas de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cba4-209">Edit hello Redirect Pages settings.</span></span>
   
    <span data-ttu-id="9cba4-210">k.</span><span class="sxs-lookup"><span data-stu-id="9cba4-210">k.</span></span> <span data-ttu-id="9cba4-211">Hola pegar **SAML Single Sign-On dirección URL del servicio** en hello **dirección URL de inicio de sesión** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="9cba4-211">Paste hello **SAML Single Sign-On Service URL** in hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="9cba4-212">l.</span><span class="sxs-lookup"><span data-stu-id="9cba4-212">l.</span></span> <span data-ttu-id="9cba4-213">Hola pegar **dirección URL de cierre de sesión** en hello **Logout URL** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="9cba4-213">Paste hello **Sign-Out URL** in hello **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="9cba4-214">m.</span><span class="sxs-lookup"><span data-stu-id="9cba4-214">m.</span></span> <span data-ttu-id="9cba4-215">Hola **URL del Error**, copia el **URL de la instancia de Marketo** y haga clic en **guardar** botón toosave configuración.</span><span class="sxs-lookup"><span data-stu-id="9cba4-215">In hello **Error URL**, copy your **Marketo instance URL** and click **Save** button toosave settings.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="9cba4-217">tooenable Hola SSO para los usuarios, Hola completa siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="9cba4-217">tooenable hello SSO for users, complete hello following actions:</span></span>
   
    <span data-ttu-id="9cba4-218">a.</span><span class="sxs-lookup"><span data-stu-id="9cba4-218">a.</span></span> <span data-ttu-id="9cba4-219">Inicie sesión en la aplicación tooMarketo usando credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="9cba4-219">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="9cba4-220">b.</span><span class="sxs-lookup"><span data-stu-id="9cba4-220">b.</span></span> <span data-ttu-id="9cba4-221">Haga clic en hello **administración** botón en el panel de navegación superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cba4-221">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="9cba4-223">c.</span><span class="sxs-lookup"><span data-stu-id="9cba4-223">c.</span></span> <span data-ttu-id="9cba4-224">Navegue toohello **seguridad** menú y haga clic en **configuración de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-224">Navigate toohello **Security** menu and click **Login Settings**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="9cba4-226">d.</span><span class="sxs-lookup"><span data-stu-id="9cba4-226">d.</span></span> <span data-ttu-id="9cba4-227">Comprobar hello **requieren SSO** opción y **guardar** Hola configuración.</span><span class="sxs-lookup"><span data-stu-id="9cba4-227">Check hello **Require SSO** option and **Save** hello settings.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="9cba4-229">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="9cba4-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9cba4-230">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="9cba4-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9cba4-231">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9cba4-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9cba4-232">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cba4-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="9cba4-233">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9cba4-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="9cba4-235">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9cba4-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cba4-236">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9cba4-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9cba4-238">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9cba4-240">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cba4-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9cba4-242">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="9cba4-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9cba4-244">a.</span><span class="sxs-lookup"><span data-stu-id="9cba4-244">a.</span></span> <span data-ttu-id="9cba4-245">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9cba4-246">b.</span><span class="sxs-lookup"><span data-stu-id="9cba4-246">b.</span></span> <span data-ttu-id="9cba4-247">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9cba4-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9cba4-248">c.</span><span class="sxs-lookup"><span data-stu-id="9cba4-248">c.</span></span> <span data-ttu-id="9cba4-249">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9cba4-250">d.</span><span class="sxs-lookup"><span data-stu-id="9cba4-250">d.</span></span> <span data-ttu-id="9cba4-251">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="9cba4-252">Creación de un usuario de prueba de Marketo</span><span class="sxs-lookup"><span data-stu-id="9cba4-252">Creating a Marketo test user</span></span>

<span data-ttu-id="9cba4-253">En esta sección, creará un usuario llamado Britta Simon en Marketo.</span><span class="sxs-lookup"><span data-stu-id="9cba4-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="9cba4-254">Siga estos toocreate pasos un usuario en la plataforma de Marketo.</span><span class="sxs-lookup"><span data-stu-id="9cba4-254">follow these steps toocreate a user in Marketo platform.</span></span>

1. <span data-ttu-id="9cba4-255">Inicie sesión en la aplicación tooMarketo usando credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="9cba4-255">Log in tooMarketo app using admin credentials.</span></span>

2. <span data-ttu-id="9cba4-256">Haga clic en hello **administración** botón en el panel de navegación superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cba4-256">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="9cba4-258">Navegue toohello **seguridad** menú y haga clic en **a los usuarios y Roles**</span><span class="sxs-lookup"><span data-stu-id="9cba4-258">Navigate toohello **Security** menu and click **Users & Roles**</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="9cba4-260">Haga clic en hello **invitar a un nuevo usuario** vínculo en la ficha de usuarios de Hola</span><span class="sxs-lookup"><span data-stu-id="9cba4-260">Click hello **Invite New User** link on hello Users tab</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="9cba4-262">Hola Hola del relleno del Asistente de invitar a un nuevo usuario después de información</span><span class="sxs-lookup"><span data-stu-id="9cba4-262">In hello Invite New User wizard fill hello following information</span></span>
   
    <span data-ttu-id="9cba4-263">a.</span><span class="sxs-lookup"><span data-stu-id="9cba4-263">a.</span></span> <span data-ttu-id="9cba4-264">Escriba Hola usuario **correo electrónico** dirección en el cuadro de texto de Hola</span><span class="sxs-lookup"><span data-stu-id="9cba4-264">Enter hello user **Email** address in hello textbox</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="9cba4-266">b.</span><span class="sxs-lookup"><span data-stu-id="9cba4-266">b.</span></span> <span data-ttu-id="9cba4-267">Escriba hello **nombre** en el cuadro de texto de Hola</span><span class="sxs-lookup"><span data-stu-id="9cba4-267">Enter hello **First Name** in hello textbox</span></span>
   
    <span data-ttu-id="9cba4-268">c.</span><span class="sxs-lookup"><span data-stu-id="9cba4-268">c.</span></span> <span data-ttu-id="9cba4-269">Escriba hello **Last Name** en el cuadro de texto de Hola</span><span class="sxs-lookup"><span data-stu-id="9cba4-269">Enter hello **Last Name**  in hello textbox</span></span>
   
    <span data-ttu-id="9cba4-270">d.</span><span class="sxs-lookup"><span data-stu-id="9cba4-270">d.</span></span> <span data-ttu-id="9cba4-271">Haga clic en **Siguiente**</span><span class="sxs-lookup"><span data-stu-id="9cba4-271">Click **Next**</span></span>

6. <span data-ttu-id="9cba4-272">Hola **permisos** ficha, seleccione hello **userRoles** y haga clic en **siguiente**</span><span class="sxs-lookup"><span data-stu-id="9cba4-272">In hello **Permissions** tab, select hello **userRoles** and click **Next**</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="9cba4-274">Haga clic en hello **enviar** botón invitación de usuario de hello toosend</span><span class="sxs-lookup"><span data-stu-id="9cba4-274">Click hello **Send** button toosend hello user invitation</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="9cba4-276">Usuario recibe la notificación de correo electrónico de Hola y tiene tooclick Hola vincular y cambiar la cuenta de hello contraseña tooactivate Hola.</span><span class="sxs-lookup"><span data-stu-id="9cba4-276">User receives hello email notification and has tooclick hello link and change hello password tooactivate hello account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9cba4-277">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cba4-277">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9cba4-278">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooMarketo.</span><span class="sxs-lookup"><span data-stu-id="9cba4-278">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMarketo.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="9cba4-280">**tooassign Britta Simon tooMarketo, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9cba4-280">**tooassign Britta Simon tooMarketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cba4-281">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-281">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9cba4-283">En la lista de aplicaciones de hello, seleccione **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-283">In hello applications list, select **Marketo**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="9cba4-285">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-285">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="9cba4-287">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-287">Click **Add** button.</span></span> <span data-ttu-id="9cba4-288">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="9cba4-290">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cba4-290">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9cba4-291">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9cba4-292">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9cba4-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9cba4-293">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="9cba4-293">Testing single sign-on</span></span>

<span data-ttu-id="9cba4-294">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9cba4-294">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9cba4-295">Al hacer clic en icono de Marketo Hola Hola Panel de acceso, deberá obtener aplicaciones de Marketo tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="9cba4-295">When you click hello Marketo tile in hello Access Panel, you should get automatically signed-on tooyour Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9cba4-296">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9cba4-296">Additional resources</span></span>

* [<span data-ttu-id="9cba4-297">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9cba4-297">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9cba4-298">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9cba4-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png


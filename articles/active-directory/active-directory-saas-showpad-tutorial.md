---
title: "Tutorial: Integración de Azure Active Directory con Showpad | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Showpad."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2c8c306b4b94c368a93f92123d3abe9fe35167db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="0d9c1-103">Tutorial: integración de Azure Active Directory con Showpad</span><span class="sxs-lookup"><span data-stu-id="0d9c1-103">Tutorial: Azure Active Directory integration with Showpad</span></span>

<span data-ttu-id="0d9c1-104">En este tutorial, aprenderá cómo toointegrate Showpad con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0d9c1-104">In this tutorial, you learn how toointegrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0d9c1-105">Integración Showpad con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0d9c1-105">Integrating Showpad with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0d9c1-106">Puede controlar en Azure AD que tenga acceso tooShowpad</span><span class="sxs-lookup"><span data-stu-id="0d9c1-106">You can control in Azure AD who has access tooShowpad</span></span>
- <span data-ttu-id="0d9c1-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooShowpad (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d9c1-107">You can enable your users tooautomatically get signed-on tooShowpad (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0d9c1-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0d9c1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0d9c1-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0d9c1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d9c1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0d9c1-110">Prerequisites</span></span>

<span data-ttu-id="0d9c1-111">integración de Azure AD con Showpad tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0d9c1-111">tooconfigure Azure AD integration with Showpad, you need hello following items:</span></span>

- <span data-ttu-id="0d9c1-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d9c1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0d9c1-113">Una suscripción habilitada para el inicio de sesión único en Showpad</span><span class="sxs-lookup"><span data-stu-id="0d9c1-113">A Showpad single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0d9c1-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0d9c1-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0d9c1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0d9c1-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0d9c1-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0d9c1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0d9c1-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0d9c1-118">Scenario description</span></span>
<span data-ttu-id="0d9c1-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0d9c1-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="0d9c1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0d9c1-121">Agregar Showpad desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0d9c1-121">Adding Showpad from hello gallery</span></span>
2. <span data-ttu-id="0d9c1-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d9c1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-hello-gallery"></a><span data-ttu-id="0d9c1-123">Agregar Showpad desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0d9c1-123">Adding Showpad from hello gallery</span></span>

<span data-ttu-id="0d9c1-124">integración de hello tooconfigure de Showpad en Azure AD, deberá tooadd Showpad de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-124">tooconfigure hello integration of Showpad into Azure AD, you need tooadd Showpad from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0d9c1-125">**tooadd Showpad de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d9c1-125">**tooadd Showpad from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d9c1-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0d9c1-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0d9c1-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0d9c1-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0d9c1-133">En el cuadro de búsqueda de hello, escriba **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-133">In hello search box, type **Showpad**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_search.png)

5. <span data-ttu-id="0d9c1-135">En el panel de resultados de hello, seleccione **Showpad**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-135">In hello results panel, select **Showpad**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0d9c1-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d9c1-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="0d9c1-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Showpad con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0d9c1-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0d9c1-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Showpad es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Showpad is tooa user in Azure AD.</span></span> <span data-ttu-id="0d9c1-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Showpad debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-140">In other words, a link relationship between an Azure AD user and hello related user in Showpad needs toobe established.</span></span>

<span data-ttu-id="0d9c1-141">En Showpad, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-141">In Showpad, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0d9c1-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Showpad, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0d9c1-142">tooconfigure and test Azure AD single sign-on with Showpad, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0d9c1-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0d9c1-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0d9c1-145">**[Crear un usuario de prueba Showpad](#creating-a-showpad-test-user) ** -toohave un equivalente de Britta Simon en Showpad que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - toohave a counterpart of Britta Simon in Showpad that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0d9c1-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0d9c1-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0d9c1-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d9c1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0d9c1-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Showpad.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="0d9c1-150">**inicio de sesión único en Azure AD tooconfigure con Showpad, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d9c1-150">**tooconfigure Azure AD single sign-on with Showpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d9c1-151">En el portal de Azure, en Hola Hola **Showpad** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-151">In hello Azure portal, on hello **Showpad** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0d9c1-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_samlbase.png)

3. <span data-ttu-id="0d9c1-155">En hello **Showpad dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0d9c1-155">On hello **Showpad Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_url.png)

    <span data-ttu-id="0d9c1-157">a.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-157">a.</span></span> <span data-ttu-id="0d9c1-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<comapany-name>.showpad.biz/login`</span><span class="sxs-lookup"><span data-stu-id="0d9c1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<comapany-name>.showpad.biz/login`</span></span>

    <span data-ttu-id="0d9c1-159">b.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-159">b.</span></span> <span data-ttu-id="0d9c1-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company-name>.showpad.biz`</span><span class="sxs-lookup"><span data-stu-id="0d9c1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.showpad.biz`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0d9c1-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-161">These values are not real.</span></span> <span data-ttu-id="0d9c1-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0d9c1-163">Póngase en contacto con [equipo de soporte técnico de Showpad](https://help.showpad.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-163">Contact [Showpad support team](https://help.showpad.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="0d9c1-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_certificate.png) 

5. <span data-ttu-id="0d9c1-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0d9c1-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-showpad-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0d9c1-168">Inicio de sesión tooyour Showpad inquilino como administrador.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-168">Sign-on tooyour Showpad tenant as an administrator.</span></span>

7. <span data-ttu-id="0d9c1-169">En el menú de hello en la parte superior de hello, haga clic en hello **configuración**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-169">In hello menu on hello top, click hello **Settings**.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_001.png) 

8. <span data-ttu-id="0d9c1-171">Navegue demasiado"**Single Sign-On**"y haga clic en"**habilitar**."</span><span class="sxs-lookup"><span data-stu-id="0d9c1-171">Navigate too"**Single Sign-On**" and click "**Enable**."</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_002.png)

9. <span data-ttu-id="0d9c1-173">En hello **agregar un servicio de SAML 2.0** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0d9c1-173">On hello **Add a SAML 2.0 Service** dialog, perform hello following steps:</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="0d9c1-175">a.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-175">a.</span></span> <span data-ttu-id="0d9c1-176">Hola **nombre** cuadro de texto Nombre de Hola de tipo de identificador de proveedor (por ejemplo: nombre de su empresa).</span><span class="sxs-lookup"><span data-stu-id="0d9c1-176">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="0d9c1-177">b.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-177">b.</span></span> <span data-ttu-id="0d9c1-178">Como **origen de metadatos**, seleccione **XML**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-178">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="0d9c1-179">c.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-179">c.</span></span> <span data-ttu-id="0d9c1-180">Copiar el contenido de hello del archivo XML de metadatos, que ha descargado de hello portal de Azure, y, a continuación, péguelo en hello **Metadata XML** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-180">Copy hello content of metadata XML file, which you have downloaded from hello Azure portal, and then paste it into hello **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="0d9c1-181">d.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-181">d.</span></span> <span data-ttu-id="0d9c1-182">Seleccione **Aprovisionar cuentas automáticamente para nuevos usuarios cuando inicien sesión**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-182">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="0d9c1-183">e.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-183">e.</span></span> <span data-ttu-id="0d9c1-184">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-184">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="0d9c1-185">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="0d9c1-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0d9c1-186">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0d9c1-187">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0d9c1-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0d9c1-188">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d9c1-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="0d9c1-189">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0d9c1-191">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d9c1-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d9c1-192">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0d9c1-194">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0d9c1-196">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0d9c1-198">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0d9c1-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0d9c1-200">a.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-200">a.</span></span> <span data-ttu-id="0d9c1-201">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0d9c1-202">b.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-202">b.</span></span> <span data-ttu-id="0d9c1-203">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0d9c1-204">c.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-204">c.</span></span> <span data-ttu-id="0d9c1-205">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0d9c1-206">d.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-206">d.</span></span> <span data-ttu-id="0d9c1-207">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-207">Click **Create**.</span></span>
 
### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="0d9c1-208">Creación de usuarios de prueba de Showpad</span><span class="sxs-lookup"><span data-stu-id="0d9c1-208">Creating a Showpad test user</span></span>

<span data-ttu-id="0d9c1-209">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Showpad toocreate.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-209">hello objective of this section is toocreate a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="0d9c1-210">Showpad admite el aprovisionamiento Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-210">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="0d9c1-211">Ya lo ha habilitado en **[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span></span> 

<span data-ttu-id="0d9c1-212">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-212">There is no action item for you in this section.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0d9c1-213">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d9c1-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0d9c1-214">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooShowpad.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooShowpad.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0d9c1-216">**tooassign Britta Simon tooShowpad, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0d9c1-216">**tooassign Britta Simon tooShowpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d9c1-217">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0d9c1-219">En la lista de aplicaciones de hello, seleccione **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-219">In hello applications list, select **Showpad**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_app.png) 

3. <span data-ttu-id="0d9c1-221">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0d9c1-223">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-223">Click **Add** button.</span></span> <span data-ttu-id="0d9c1-224">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0d9c1-226">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0d9c1-227">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0d9c1-228">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0d9c1-229">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0d9c1-229">Testing single sign-on</span></span>

<span data-ttu-id="0d9c1-230">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0d9c1-231">Al hacer clic en icono de Showpad Hola Hola Panel de acceso, deberá obtener la aplicación tooShowpad automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="0d9c1-231">When you click hello Showpad tile in hello Access Panel, you should get automatically signed-on tooShowpad application.</span></span>
<span data-ttu-id="0d9c1-232">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0d9c1-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0d9c1-233">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0d9c1-233">Additional resources</span></span>

* [<span data-ttu-id="0d9c1-234">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d9c1-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0d9c1-235">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0d9c1-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_203.png

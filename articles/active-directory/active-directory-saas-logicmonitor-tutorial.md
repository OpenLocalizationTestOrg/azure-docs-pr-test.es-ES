---
title: "Tutorial: integración de Azure Active Directory con LogicMonitor | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y LogicMonitor."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: ea5cb8b574d763cb114286e3b2a5c94ab5546756
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="c9c8b-103">Tutorial: Integración de Azure Active Directory con LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="c9c8b-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="c9c8b-104">En este tutorial, aprenderá cómo toointegrate LogicMonitor con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c9c8b-104">In this tutorial, you learn how toointegrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c9c8b-105">Integración LogicMonitor con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="c9c8b-105">Integrating LogicMonitor with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c9c8b-106">Puede controlar en Azure AD que tenga acceso tooLogicMonitor</span><span class="sxs-lookup"><span data-stu-id="c9c8b-106">You can control in Azure AD who has access tooLogicMonitor</span></span>
- <span data-ttu-id="c9c8b-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooLogicMonitor (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9c8b-107">You can enable your users tooautomatically get signed-on tooLogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c9c8b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c9c8b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c9c8b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c9c8b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9c8b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c9c8b-110">Prerequisites</span></span>

<span data-ttu-id="c9c8b-111">integración de Azure AD con LogicMonitor tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c9c8b-111">tooconfigure Azure AD integration with LogicMonitor, you need hello following items:</span></span>

- <span data-ttu-id="c9c8b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9c8b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c9c8b-113">Una suscripción habilitada para el inicio de sesión único en LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="c9c8b-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c9c8b-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c9c8b-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c9c8b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c9c8b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c9c8b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9c8b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c9c8b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c9c8b-118">Scenario description</span></span>
<span data-ttu-id="c9c8b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c9c8b-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="c9c8b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9c8b-121">Agregar LogicMonitor desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c9c8b-121">Adding LogicMonitor from hello gallery</span></span>
2. <span data-ttu-id="c9c8b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9c8b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-hello-gallery"></a><span data-ttu-id="c9c8b-123">Agregar LogicMonitor desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="c9c8b-123">Adding LogicMonitor from hello gallery</span></span>
<span data-ttu-id="c9c8b-124">integración de hello tooconfigure de LogicMonitor en Azure AD, deberá tooadd LogicMonitor de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-124">tooconfigure hello integration of LogicMonitor into Azure AD, you need tooadd LogicMonitor from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c9c8b-125">**tooadd LogicMonitor de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c9c8b-125">**tooadd LogicMonitor from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9c8b-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c9c8b-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c9c8b-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c9c8b-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c9c8b-133">En el cuadro de búsqueda de hello, escriba **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-133">In hello search box, type **LogicMonitor**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="c9c8b-135">En el panel de resultados de hello, seleccione **LogicMonitor**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-135">In hello results panel, select **LogicMonitor**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c9c8b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9c8b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c9c8b-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con LogicMonitor con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c9c8b-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c9c8b-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en LogicMonitor es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LogicMonitor is tooa user in Azure AD.</span></span> <span data-ttu-id="c9c8b-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en LogicMonitor debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-140">In other words, a link relationship between an Azure AD user and hello related user in LogicMonitor needs toobe established.</span></span>

<span data-ttu-id="c9c8b-141">En LogicMonitor, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-141">In LogicMonitor, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c9c8b-142">tooconfigure y prueba de inicio de sesión único en Azure AD con LogicMonitor, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c9c8b-142">tooconfigure and test Azure AD single sign-on with LogicMonitor, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c9c8b-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c9c8b-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c9c8b-145">**[Crear un usuario de prueba de LogicMonitor](#creating-a-logicmonitor-test-user)**  -toohave un equivalente de Britta Simon en LogicMonitor que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - toohave a counterpart of Britta Simon in LogicMonitor that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c9c8b-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9c8b-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c9c8b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9c8b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c9c8b-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="c9c8b-150">**inicio de sesión único en Azure AD tooconfigure con LogicMonitor, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c9c8b-150">**tooconfigure Azure AD single sign-on with LogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9c8b-151">En el portal de Azure, en Hola Hola **LogicMonitor** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-151">In hello Azure portal, on hello **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c9c8b-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="c9c8b-155">En hello **LogicMonitor dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c9c8b-155">On hello **LogicMonitor Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="c9c8b-157">a.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-157">a.</span></span> <span data-ttu-id="c9c8b-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="c9c8b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="c9c8b-159">b.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-159">b.</span></span> <span data-ttu-id="c9c8b-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="c9c8b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c9c8b-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-161">These values are not real.</span></span> <span data-ttu-id="c9c8b-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c9c8b-163">Póngase en contacto con [equipo de soporte técnico de cliente de LogicMonitor](https://www.logicmonitor.com/contact/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) tooget these values.</span></span> 
 


4. <span data-ttu-id="c9c8b-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="c9c8b-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c9c8b-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c9c8b-168">Inicie sesión en tooyour **LogicMonitor** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-168">Log in tooyour **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="c9c8b-169">En el menú de hello en la parte superior de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-169">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="c9c8b-170">![Configuración](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="c9c8b-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="c9c8b-171">En hello bat de navegación en el lado izquierdo de hello, haga clic en **inicio de sesión único**</span><span class="sxs-lookup"><span data-stu-id="c9c8b-171">In hello navigation bat on hello left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="c9c8b-172">![Inicio de sesión único](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c9c8b-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="c9c8b-173">Hola **configuración de inicio de sesión único (SSO)** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c9c8b-173">In hello **Single Sign-on (SSO) settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="c9c8b-174">![Configuración de inicio de sesión único](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Configuración de inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="c9c8b-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="c9c8b-175">a.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-175">a.</span></span> <span data-ttu-id="c9c8b-176">Seleccione **Habilitar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="c9c8b-177">b.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-177">b.</span></span> <span data-ttu-id="c9c8b-178">En **Default Role Assignment** (Asignación de rol predeterminado), seleccione **readonly**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="c9c8b-179">c.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-179">c.</span></span> <span data-ttu-id="c9c8b-180">Abra el archivo de metadatos de hello descargado en el Bloc de notas y, a continuación, pegue el contenido del archivo hello en hello **metadatos del proveedor de identidades** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-180">Open hello downloaded metadata file in notepad, and then paste content of hello file into hello **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="c9c8b-181">d.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-181">d.</span></span> <span data-ttu-id="c9c8b-182">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="c9c8b-183">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="c9c8b-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c9c8b-184">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c9c8b-185">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c9c8b-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c9c8b-186">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9c8b-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="c9c8b-187">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c9c8b-189">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c9c8b-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9c8b-190">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c9c8b-192">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c9c8b-194">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c9c8b-196">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c9c8b-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c9c8b-198">a.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-198">a.</span></span> <span data-ttu-id="c9c8b-199">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c9c8b-200">b.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-200">b.</span></span> <span data-ttu-id="c9c8b-201">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c9c8b-202">c.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-202">c.</span></span> <span data-ttu-id="c9c8b-203">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c9c8b-204">d.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-204">d.</span></span> <span data-ttu-id="c9c8b-205">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="c9c8b-206">Creación de un usuario de prueba de LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="c9c8b-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="c9c8b-207">Para AAD a los usuarios toobe puede toosign en, deben ser aprovisionado toohello aplicación LogicMonitor con los nombres de usuario de Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-207">For AAD users toobe able toosign in, they must be provisioned toohello LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="c9c8b-208">**tooconfigure aprovisionamiento de usuario, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c9c8b-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9c8b-209">Inicie sesión en tooyour sitio de la empresa LogicMonitor como administrador.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-209">Log in tooyour LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="c9c8b-210">En el menú de hello en la parte superior de hello, haga clic en **configuración**y, a continuación, haga clic en **Roles y usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-210">In hello menu on hello top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="c9c8b-211">![Roles y usuarios](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles y usuarios")</span><span class="sxs-lookup"><span data-stu-id="c9c8b-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="c9c8b-212">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-212">Click **Add**.</span></span>

4. <span data-ttu-id="c9c8b-213">Hola **agregar una cuenta** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c9c8b-213">In hello **Add an account** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="c9c8b-214">![Agregar una cuenta](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Agregar una cuenta")</span><span class="sxs-lookup"><span data-stu-id="c9c8b-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="c9c8b-215">a.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-215">a.</span></span> <span data-ttu-id="c9c8b-216">Hola de tipo **nombre de usuario**, **correo electrónico**, **contraseña**, y **vuelva a escribir contraseña** valores de usuario de Azure Active Directory de Hola que desea tooprovision en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-216">Type hello **Username**, **Email**, **Password**, and **Retype password** values of hello Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="c9c8b-217">b.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-217">b.</span></span> <span data-ttu-id="c9c8b-218">Seleccione **Roles**, **permisos para ver**, hello y **estado**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-218">Select **Roles**, **View Permissions**, and hello **Status**.</span></span>
   
   <span data-ttu-id="c9c8b-219">c.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-219">c.</span></span> <span data-ttu-id="c9c8b-220">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="c9c8b-221">Puede usar cualquier otra LogicMonitor usuario cuenta herramienta de creación o las API proporcionadas por LogicMonitor tooprovision Azure Active Directory las cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor tooprovision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c9c8b-222">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9c8b-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c9c8b-223">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooLogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLogicMonitor.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c9c8b-225">**tooassign Britta Simon tooLogicMonitor, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="c9c8b-225">**tooassign Britta Simon tooLogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9c8b-226">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c9c8b-228">En la lista de aplicaciones de hello, seleccione **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-228">In hello applications list, select **LogicMonitor**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="c9c8b-230">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c9c8b-232">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-232">Click **Add** button.</span></span> <span data-ttu-id="c9c8b-233">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c9c8b-235">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c9c8b-236">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c9c8b-237">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c9c8b-238">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c9c8b-238">Testing single sign-on</span></span>

<span data-ttu-id="c9c8b-239">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="c9c8b-240">Al hacer clic en icono de LogicMonitor Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour LogicMonitor aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9c8b-240">When you click hello LogicMonitor tile in hello Access Panel, you should get automatically signed-on tooyour LogicMonitor application.</span></span>
<span data-ttu-id="c9c8b-241">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c9c8b-241">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c9c8b-242">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c9c8b-242">Additional resources</span></span>

* [<span data-ttu-id="c9c8b-243">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9c8b-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9c8b-244">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c9c8b-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png


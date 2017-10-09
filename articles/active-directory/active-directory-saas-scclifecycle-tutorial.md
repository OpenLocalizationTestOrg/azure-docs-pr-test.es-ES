---
title: "Tutorial: Integración de Azure Active Directory con SCC LifeCycle | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SCC LifeCycle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 63623c5bd2d951612040f0121615a406bf83e890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="0dad0-103">Tutorial: Integración de Azure Active Directory con SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="0dad0-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>

<span data-ttu-id="0dad0-104">En este tutorial, aprenderá cómo toointegrate SCC LifeCycle con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0dad0-104">In this tutorial, you learn how toointegrate SCC LifeCycle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0dad0-105">Integración de SCC LifeCycle con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0dad0-105">Integrating SCC LifeCycle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0dad0-106">Puede controlar en Azure AD que tenga acceso tooSCC del ciclo de vida</span><span class="sxs-lookup"><span data-stu-id="0dad0-106">You can control in Azure AD who has access tooSCC LifeCycle</span></span>
- <span data-ttu-id="0dad0-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSCC del ciclo de vida (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dad0-107">You can enable your users tooautomatically get signed-on tooSCC LifeCycle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0dad0-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0dad0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0dad0-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0dad0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dad0-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0dad0-110">Prerequisites</span></span>

<span data-ttu-id="0dad0-111">tooconfigure integración de Azure AD con SCC LifeCycle, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0dad0-111">tooconfigure Azure AD integration with SCC LifeCycle, you need hello following items:</span></span>

- <span data-ttu-id="0dad0-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dad0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0dad0-113">Una suscripción habilitada para el inicio de sesión único en SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="0dad0-113">An SCC LifeCycle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0dad0-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0dad0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0dad0-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0dad0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0dad0-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0dad0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0dad0-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0dad0-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0dad0-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0dad0-118">Scenario description</span></span>
<span data-ttu-id="0dad0-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0dad0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0dad0-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="0dad0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0dad0-121">Adición de SCC LifeCycle desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="0dad0-121">Adding SCC LifeCycle from hello gallery</span></span>
2. <span data-ttu-id="0dad0-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dad0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scc-lifecycle-from-hello-gallery"></a><span data-ttu-id="0dad0-123">Adición de SCC LifeCycle desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="0dad0-123">Adding SCC LifeCycle from hello gallery</span></span>
<span data-ttu-id="0dad0-124">integración de hello tooconfigure de SCC LifeCycle en Azure AD, deberá tooadd SCC LifeCycle de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="0dad0-124">tooconfigure hello integration of SCC LifeCycle into Azure AD, you need tooadd SCC LifeCycle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0dad0-125">**tooadd SCC LifeCycle de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0dad0-125">**tooadd SCC LifeCycle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dad0-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0dad0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0dad0-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0dad0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0dad0-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0dad0-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0dad0-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0dad0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0dad0-133">En el cuadro de búsqueda de hello, escriba **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="0dad0-133">In hello search box, type **SCC LifeCycle**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_search.png)

5. <span data-ttu-id="0dad0-135">En el panel de resultados de hello, seleccione **SCC LifeCycle**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0dad0-135">In hello results panel, select **SCC LifeCycle**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0dad0-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dad0-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="0dad0-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SCC LifeCycle con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0dad0-138">In this section, you configure and test Azure AD single sign-on with SCC LifeCycle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0dad0-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en SCC LifeCycle es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0dad0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SCC LifeCycle is tooa user in Azure AD.</span></span> <span data-ttu-id="0dad0-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SCC LifeCycle debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="0dad0-140">In other words, a link relationship between an Azure AD user and hello related user in SCC LifeCycle needs toobe established.</span></span>

<span data-ttu-id="0dad0-141">En SCC LifeCycle, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dad0-141">In SCC LifeCycle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0dad0-142">tooconfigure y prueba de inicio de sesión único en Azure AD con SCC LifeCycle, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0dad0-142">tooconfigure and test Azure AD single sign-on with SCC LifeCycle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0dad0-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="0dad0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0dad0-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0dad0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0dad0-145">**[Creación de un usuario de prueba de SCC LifeCycle](#creating-an-scc-lifecycle-test-user)**  -toohave un equivalente de Britta Simon en SCC LifeCycle que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="0dad0-145">**[Creating an SCC LifeCycle test user](#creating-an-scc-lifecycle-test-user)** - toohave a counterpart of Britta Simon in SCC LifeCycle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0dad0-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0dad0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0dad0-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0dad0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0dad0-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dad0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0dad0-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="0dad0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SCC LifeCycle application.</span></span>

<span data-ttu-id="0dad0-150">**inicio de sesión único en Azure AD tooconfigure con SCC LifeCycle, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0dad0-150">**tooconfigure Azure AD single sign-on with SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dad0-151">En el portal de Azure, en Hola Hola **SCC LifeCycle** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0dad0-151">In hello Azure portal, on hello **SCC LifeCycle** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0dad0-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0dad0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_samlbase.png)

3. <span data-ttu-id="0dad0-155">En hello **SCC LifeCycle dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0dad0-155">On hello **SCC LifeCycle Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_url.png)

    <span data-ttu-id="0dad0-157">a.</span><span class="sxs-lookup"><span data-stu-id="0dad0-157">a.</span></span> <span data-ttu-id="0dad0-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`</span><span class="sxs-lookup"><span data-stu-id="0dad0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub-domain>.scc.com/ic7/welcome/customer/PICTtest.aspx`</span></span>

    <span data-ttu-id="0dad0-159">b.</span><span class="sxs-lookup"><span data-stu-id="0dad0-159">b.</span></span> <span data-ttu-id="0dad0-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="0dad0-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|--|
    | `https://bs1.scc.com/<entity>`|
    | `https://lifecycle.scc.com/<entity>`|
    
    > [!NOTE] 
    > <span data-ttu-id="0dad0-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="0dad0-161">These values are not real.</span></span> <span data-ttu-id="0dad0-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="0dad0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0dad0-163">Póngase en contacto con [equipo de soporte técnico de SCC LifeCycle cliente](mailto:lifecycle.support@scc.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="0dad0-163">Contact [SCC LifeCycle Client support team](mailto:lifecycle.support@scc.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="0dad0-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0dad0-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_certificate.png) 

5. <span data-ttu-id="0dad0-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0dad0-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0dad0-168">inicio de sesión único en tooconfigure en **SCC LifeCycle** lado, necesita hello toosend descargado **Metadata XML** demasiado[equipo de soporte técnico de SCC LifeCycle](mailto:lifecycle.support@scc.com).</span><span class="sxs-lookup"><span data-stu-id="0dad0-168">tooconfigure single sign-on on **SCC LifeCycle** side, you need toosend hello downloaded **Metadata XML** too[SCC LifeCycle support team](mailto:lifecycle.support@scc.com).</span></span> <span data-ttu-id="0dad0-169">Establecen esta Hola de toohave configuración configurada correctamente en ambos lados de la conexión de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="0dad0-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

     >[!NOTE]
   ><span data-ttu-id="0dad0-170">Inicio de sesión único tiene toobe habilitada por Hola, equipo de soporte técnico de SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="0dad0-170">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

> [!TIP]
> <span data-ttu-id="0dad0-171">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="0dad0-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0dad0-172">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="0dad0-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0dad0-173">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0dad0-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0dad0-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dad0-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="0dad0-175">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="0dad0-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0dad0-177">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0dad0-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dad0-178">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0dad0-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0dad0-180">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0dad0-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0dad0-182">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dad0-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0dad0-184">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0dad0-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-scclifecycle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0dad0-186">a.</span><span class="sxs-lookup"><span data-stu-id="0dad0-186">a.</span></span> <span data-ttu-id="0dad0-187">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0dad0-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0dad0-188">b.</span><span class="sxs-lookup"><span data-stu-id="0dad0-188">b.</span></span> <span data-ttu-id="0dad0-189">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0dad0-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0dad0-190">c.</span><span class="sxs-lookup"><span data-stu-id="0dad0-190">c.</span></span> <span data-ttu-id="0dad0-191">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0dad0-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0dad0-192">d.</span><span class="sxs-lookup"><span data-stu-id="0dad0-192">d.</span></span> <span data-ttu-id="0dad0-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0dad0-193">Click **Create**.</span></span>
 
### <a name="creating-an-scc-lifecycle-test-user"></a><span data-ttu-id="0dad0-194">Creación de un usuario de prueba de SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="0dad0-194">Creating an SCC LifeCycle test user</span></span>

<span data-ttu-id="0dad0-195">En orden tooenable toolog de los usuarios de Azure AD en SCC LifeCycle, se les deben aprovisionar en SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="0dad0-195">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="0dad0-196">No hay ningún elemento de acción tooconfigure de aprovisionamiento de usuarios tooSCC del ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="0dad0-196">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="0dad0-197">Cuando un toolog de intentos de usuario asignado en SCC LifeCycle, automáticamente se crea una cuenta de SCC LifeCycle si es necesario.</span><span class="sxs-lookup"><span data-stu-id="0dad0-197">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

> [!NOTE]
    > <span data-ttu-id="0dad0-198">titular de la cuenta de Hello Azure Active Directory recibe un correo electrónico y sigue un vínculo tooconfirm su cuenta antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="0dad0-198">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0dad0-199">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dad0-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0dad0-200">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSCC del ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="0dad0-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSCC LifeCycle.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0dad0-202">**tooassign Britta Simon tooSCC ciclo de vida, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0dad0-202">**tooassign Britta Simon tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dad0-203">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="0dad0-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications.**</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0dad0-205">En la lista de aplicaciones de hello, seleccione **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="0dad0-205">In hello applications list, select **SCC LifeCycle**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-scclifecycle-tutorial/tutorial_scclifecycle_app.png) 

3. <span data-ttu-id="0dad0-207">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0dad0-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0dad0-209">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0dad0-209">Click **Add** button.</span></span> <span data-ttu-id="0dad0-210">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0dad0-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0dad0-212">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dad0-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0dad0-213">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0dad0-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0dad0-214">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0dad0-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0dad0-215">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0dad0-215">Testing single sign-on</span></span>

<span data-ttu-id="0dad0-216">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0dad0-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0dad0-217">Al hacer clic en hello SCC LifeCycle disponer en mosaico en hello Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooSCC aplicación de ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="0dad0-217">When you click hello SCC LifeCycle tile in hello Access Panel, you should get automatically signed-on tooSCC LifeCycle application.</span></span>
<span data-ttu-id="0dad0-218">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0dad0-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0dad0-219">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0dad0-219">Additional resources</span></span>

* [<span data-ttu-id="0dad0-220">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0dad0-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0dad0-221">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0dad0-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scclifecycle-tutorial/tutorial_general_203.png


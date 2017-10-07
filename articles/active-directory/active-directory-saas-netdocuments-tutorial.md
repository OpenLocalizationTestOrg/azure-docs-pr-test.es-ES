---
title: "Tutorial: Integración de Azure Active Directory con NetDocuments | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y NetDocuments."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee9887553595a2492642aed4cb4abcd11d9cf599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="7fdb6-103">Tutorial: Integración de Azure Active Directory con NetDocuments</span><span class="sxs-lookup"><span data-stu-id="7fdb6-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="7fdb6-104">En este tutorial, aprenderá cómo toointegrate NetDocuments con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7fdb6-104">In this tutorial, you learn how toointegrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7fdb6-105">Integración de NetDocuments con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7fdb6-105">Integrating NetDocuments with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7fdb6-106">Puede controlar en Azure AD que tenga acceso tooNetDocuments</span><span class="sxs-lookup"><span data-stu-id="7fdb6-106">You can control in Azure AD who has access tooNetDocuments</span></span>
- <span data-ttu-id="7fdb6-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooNetDocuments (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fdb6-107">You can enable your users tooautomatically get signed-on tooNetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7fdb6-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7fdb6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7fdb6-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7fdb6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fdb6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7fdb6-110">Prerequisites</span></span>

<span data-ttu-id="7fdb6-111">integración de Azure AD con NetDocuments tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7fdb6-111">tooconfigure Azure AD integration with NetDocuments, you need hello following items:</span></span>

- <span data-ttu-id="7fdb6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fdb6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7fdb6-113">Una suscripción habilitada para el inicio de sesión único en NetDocuments</span><span class="sxs-lookup"><span data-stu-id="7fdb6-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7fdb6-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7fdb6-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="7fdb6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7fdb6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7fdb6-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7fdb6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7fdb6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="7fdb6-118">Scenario description</span></span>
<span data-ttu-id="7fdb6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7fdb6-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="7fdb6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7fdb6-121">Agregar NetDocuments desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7fdb6-121">Adding NetDocuments from hello gallery</span></span>
2. <span data-ttu-id="7fdb6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fdb6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-hello-gallery"></a><span data-ttu-id="7fdb6-123">Agregar NetDocuments desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7fdb6-123">Adding NetDocuments from hello gallery</span></span>
<span data-ttu-id="7fdb6-124">integración de hello tooconfigure de NetDocuments en Azure AD, deberá tooadd NetDocuments de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-124">tooconfigure hello integration of NetDocuments into Azure AD, you need tooadd NetDocuments from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7fdb6-125">**tooadd NetDocuments de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7fdb6-125">**tooadd NetDocuments from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fdb6-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7fdb6-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7fdb6-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="7fdb6-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="7fdb6-133">En el cuadro de búsqueda de hello, escriba **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-133">In hello search box, type **NetDocuments**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="7fdb6-135">En el panel de resultados de hello, seleccione **NetDocuments**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-135">In hello results panel, select **NetDocuments**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7fdb6-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fdb6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7fdb6-138">En esta sección, puede configurar y probar el inicio de sesión único de Azure AD con NetDocuments con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7fdb6-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7fdb6-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en NetDocuments es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in NetDocuments is tooa user in Azure AD.</span></span> <span data-ttu-id="7fdb6-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en NetDocuments debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-140">In other words, a link relationship between an Azure AD user and hello related user in NetDocuments needs toobe established.</span></span>

<span data-ttu-id="7fdb6-141">En NetDocuments, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-141">In NetDocuments, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7fdb6-142">tooconfigure y prueba de inicio de sesión único en Azure AD con NetDocuments, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="7fdb6-142">tooconfigure and test Azure AD single sign-on with NetDocuments, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7fdb6-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7fdb6-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7fdb6-145">**[Crear un usuario de prueba de NetDocuments](#creating-a-netdocuments-test-user) ** -toohave un equivalente de Britta Simon en NetDocuments que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - toohave a counterpart of Britta Simon in NetDocuments that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7fdb6-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7fdb6-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7fdb6-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fdb6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7fdb6-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="7fdb6-150">**inicio de sesión único en Azure AD tooconfigure con NetDocuments, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7fdb6-150">**tooconfigure Azure AD single sign-on with NetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fdb6-151">En el portal de Azure, en Hola Hola **NetDocuments** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-151">In hello Azure portal, on hello **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="7fdb6-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="7fdb6-155">En hello **NetDocuments dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7fdb6-155">On hello **NetDocuments Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="7fdb6-157">a.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-157">a.</span></span> <span data-ttu-id="7fdb6-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="7fdb6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="7fdb6-159">b.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-159">b.</span></span> <span data-ttu-id="7fdb6-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="7fdb6-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7fdb6-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-161">These values are not real.</span></span> <span data-ttu-id="7fdb6-162">Actualizar estos valores con la URL de inicio de sesión real de Hola y la dirección URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="7fdb6-163">Póngase en contacto con [equipo de soporte técnico de NetDocuments](https://support.netdocuments.com/hc/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) tooget these values.</span></span>
 
4. <span data-ttu-id="7fdb6-164">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="7fdb6-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="7fdb6-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7fdb6-168">En otra ventana del explorador web, inicie sesión en como administrador en el sitio de la compañía de NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="7fdb6-169">Vaya demasiado**administración**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-169">Go too**Admin**.</span></span>

8. <span data-ttu-id="7fdb6-170">Haga clic en **Agregar y quitar usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="7fdb6-171">![Repositorio](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repositorio")</span><span class="sxs-lookup"><span data-stu-id="7fdb6-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="7fdb6-172">Haga clic en **Configurar opciones de autenticación avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="7fdb6-173">![Configurar opciones de autenticación avanzadas](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configurar opciones de autenticación avanzadas")</span><span class="sxs-lookup"><span data-stu-id="7fdb6-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="7fdb6-174">En hello **identidad federada** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7fdb6-174">On hello **Federated Identity** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="7fdb6-175">![Identidad federada](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Identidad federada")</span><span class="sxs-lookup"><span data-stu-id="7fdb6-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="7fdb6-176">a.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-176">a.</span></span> <span data-ttu-id="7fdb6-177">Como **Tipo de servidor de identidad federada**, seleccione **Servicios de federación de Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="7fdb6-178">b.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-178">b.</span></span> <span data-ttu-id="7fdb6-179">Haga clic en **Elegir archivo**, hello tooupload descargado el archivo de metadatos que ha descargado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-179">Click **Choose file**, tooupload hello downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="7fdb6-180">c.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-180">c.</span></span> <span data-ttu-id="7fdb6-181">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="7fdb6-182">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="7fdb6-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7fdb6-183">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7fdb6-184">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7fdb6-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7fdb6-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fdb6-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="7fdb6-186">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="7fdb6-188">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7fdb6-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fdb6-189">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7fdb6-191">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7fdb6-193">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7fdb6-195">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="7fdb6-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7fdb6-197">a.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-197">a.</span></span> <span data-ttu-id="7fdb6-198">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7fdb6-199">b.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-199">b.</span></span> <span data-ttu-id="7fdb6-200">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7fdb6-201">c.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-201">c.</span></span> <span data-ttu-id="7fdb6-202">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7fdb6-203">d.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-203">d.</span></span> <span data-ttu-id="7fdb6-204">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="7fdb6-205">Creación de un usuario de prueba de NetDocuments</span><span class="sxs-lookup"><span data-stu-id="7fdb6-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="7fdb6-206">toolog de los usuarios de Azure AD tooenable en tooNetDocuments, se les deben aprovisionar en NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-206">tooenable Azure AD users toolog in tooNetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="7fdb6-207">En caso de hello de NetDocuments, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-207">In hello case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="7fdb6-208">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7fdb6-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fdb6-209">Inicie sesión en tooyour **NetDocuments** como administrador.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-209">Sing on tooyour **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="7fdb6-210">En el menú de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-210">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="7fdb6-211">![Administración](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="7fdb6-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="7fdb6-212">Haga clic en **Agregar y quitar usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="7fdb6-213">![Repositorio](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repositorio")</span><span class="sxs-lookup"><span data-stu-id="7fdb6-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="7fdb6-214">Hola **dirección de correo electrónico** cuadro de texto, escriba Hola dirección de correo electrónico de una cuenta válida de Azure Active Directory que desee tooprovision y, a continuación, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-214">In hello **Email Address** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="7fdb6-215">![Dirección de correo electrónico](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Dirección de correo electrónico")</span><span class="sxs-lookup"><span data-stu-id="7fdb6-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="7fdb6-216">titular de cuenta de Hello Azure Active Directory recibirá un correo electrónico que incluye una cuenta de hello tooconfirm vínculo antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-216">hello Azure Active Directory account holder will get an email that includes a link tooconfirm hello account before it becomes active.</span></span> <span data-ttu-id="7fdb6-217">Puede usar cualquier otra NetDocuments usuario cuenta herramienta de creación o las API proporcionadas por NetDocuments tooprovision Azure Active Directory las cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7fdb6-218">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fdb6-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7fdb6-219">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooNetDocuments.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetDocuments.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="7fdb6-221">**tooassign Britta Simon tooNetDocuments, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7fdb6-221">**tooassign Britta Simon tooNetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="7fdb6-222">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7fdb6-224">En la lista de aplicaciones de hello, seleccione **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-224">In hello applications list, select **NetDocuments**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="7fdb6-226">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="7fdb6-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-228">Click **Add** button.</span></span> <span data-ttu-id="7fdb6-229">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="7fdb6-231">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7fdb6-232">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7fdb6-233">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7fdb6-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="7fdb6-234">Testing single sign-on</span></span>

<span data-ttu-id="7fdb6-235">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7fdb6-236">Al hacer clic en hello NetDocuments disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour aplicación de NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="7fdb6-236">When you click hello NetDocuments tile in hello Access Panel, you should get automatically signed-on tooyour NetDocuments application.</span></span>
<span data-ttu-id="7fdb6-237">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7fdb6-237">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7fdb6-238">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7fdb6-238">Additional resources</span></span>

* [<span data-ttu-id="7fdb6-239">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7fdb6-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7fdb6-240">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7fdb6-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png


---
title: "Tutorial: Integración de Azure Active Directory con Springer Link | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y vínculo Springer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 58cdf029-bdc0-43c4-a469-b921c2a669bd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: jeedes
ms.openlocfilehash: dabd2f72b3a195fc359826a4863a197e5019f5c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springer-link"></a><span data-ttu-id="82d29-103">Tutorial: Integración de Azure Active Directory con Springer Link</span><span class="sxs-lookup"><span data-stu-id="82d29-103">Tutorial: Azure Active Directory integration with Springer Link</span></span>

<span data-ttu-id="82d29-104">En este tutorial, aprenderá cómo toointegrate Springer vincular con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="82d29-104">In this tutorial, you learn how toointegrate Springer Link with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="82d29-105">Integración Springer vínculo con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="82d29-105">Integrating Springer Link with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="82d29-106">Puede controlar en Azure AD que tenga acceso tooSpringer vínculo.</span><span class="sxs-lookup"><span data-stu-id="82d29-106">You can control in Azure AD who has access tooSpringer Link.</span></span>
- <span data-ttu-id="82d29-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSpringer vínculo (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82d29-107">You can enable your users tooautomatically get signed-on tooSpringer Link (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="82d29-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="82d29-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="82d29-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="82d29-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82d29-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="82d29-110">Prerequisites</span></span>

<span data-ttu-id="82d29-111">integración de Azure AD con vínculo Springer tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="82d29-111">tooconfigure Azure AD integration with Springer Link, you need hello following items:</span></span>

- <span data-ttu-id="82d29-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82d29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="82d29-113">Una suscripción habilitada para el inicio de sesión único en Springer Link</span><span class="sxs-lookup"><span data-stu-id="82d29-113">A Springer Link single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="82d29-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="82d29-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="82d29-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="82d29-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="82d29-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="82d29-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="82d29-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="82d29-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="82d29-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="82d29-118">Scenario description</span></span>
<span data-ttu-id="82d29-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="82d29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="82d29-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="82d29-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="82d29-121">Agregar vínculo Springer desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="82d29-121">Adding Springer Link from hello gallery</span></span>
2. <span data-ttu-id="82d29-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82d29-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springer-link-from-hello-gallery"></a><span data-ttu-id="82d29-123">Agregar vínculo Springer desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="82d29-123">Adding Springer Link from hello gallery</span></span>
<span data-ttu-id="82d29-124">integración de hello tooconfigure de vínculo Springer en Azure AD, deberá tooadd Springer vínculo de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="82d29-124">tooconfigure hello integration of Springer Link into Azure AD, you need tooadd Springer Link from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="82d29-125">**tooadd Springer vínculo desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="82d29-125">**tooadd Springer Link from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="82d29-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="82d29-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="82d29-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="82d29-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="82d29-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="82d29-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="82d29-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="82d29-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="82d29-133">En el cuadro de búsqueda de hello, escriba **vínculo Springer**, seleccione **vínculo Springer** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="82d29-133">In hello search box, type **Springer Link**, select **Springer Link** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Vínculo Springer Hola la lista de resultados](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="82d29-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="82d29-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="82d29-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Springer Link con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="82d29-136">In this section, you configure and test Azure AD single sign-on with Springer Link based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="82d29-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en vínculo Springer es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82d29-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Springer Link is tooa user in Azure AD.</span></span> <span data-ttu-id="82d29-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en vínculo Springer debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="82d29-138">In other words, a link relationship between an Azure AD user and hello related user in Springer Link needs toobe established.</span></span>

<span data-ttu-id="82d29-139">En el vínculo de Springer, asigne el valor de Hola de Hola **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="82d29-139">In Springer Link, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="82d29-140">tooconfigure y prueba de inicio de sesión único en Azure AD con vínculo Springer, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="82d29-140">tooconfigure and test Azure AD single sign-on with Springer Link, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="82d29-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="82d29-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="82d29-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82d29-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="82d29-143">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="82d29-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="82d29-144">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="82d29-144">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="82d29-145">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82d29-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="82d29-146">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Springer vínculo.</span><span class="sxs-lookup"><span data-stu-id="82d29-146">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Springer Link application.</span></span>

<span data-ttu-id="82d29-147">**inicio de sesión único en tooconfigure Azure AD con vínculo Springer, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="82d29-147">**tooconfigure Azure AD single sign-on with Springer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="82d29-148">En el portal de Azure, en Hola Hola **vínculo Springer** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="82d29-148">In hello Azure portal, on hello **Springer Link** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="82d29-150">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="82d29-150">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_samlbase.png)

3. <span data-ttu-id="82d29-152">En hello **Springer vincular dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="82d29-152">On hello **Springer Link Domain and URLs** section,  If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Información de inicio de sesión único de Dominio y direcciones URL de Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url1.png)

    <span data-ttu-id="82d29-154">a.</span><span class="sxs-lookup"><span data-stu-id="82d29-154">a.</span></span> <span data-ttu-id="82d29-155">Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://fsso.springer.com`</span><span class="sxs-lookup"><span data-stu-id="82d29-155">In hello **Identifier** textbox, type hello URL: `https://fsso.springer.com`</span></span>

    <span data-ttu-id="82d29-156">b.</span><span class="sxs-lookup"><span data-stu-id="82d29-156">b.</span></span> <span data-ttu-id="82d29-157">Hola **dirección URL de respuesta** cuadro de texto, escriba la dirección URL hello:`https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="82d29-157">In hello **Reply URL** textbox, type hello URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

4. <span data-ttu-id="82d29-158">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="82d29-158">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="82d29-159">Si desea que aplicación de hello tooconfigure en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="82d29-159">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Información de inicio de sesión único de Dominio y direcciones URL de Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url.png)

    <span data-ttu-id="82d29-161">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:`https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="82d29-161">In hello **Sign-on URL** textbox, type hello URL : `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

5. <span data-ttu-id="82d29-162">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="82d29-162">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-springerlink-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="82d29-164">Hola toogenerate **metadatos** dirección url, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="82d29-164">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="82d29-165">a.</span><span class="sxs-lookup"><span data-stu-id="82d29-165">a.</span></span> <span data-ttu-id="82d29-166">Haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="82d29-166">Click **App registrations**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appregistrations.png)
   
    <span data-ttu-id="82d29-168">b.</span><span class="sxs-lookup"><span data-stu-id="82d29-168">b.</span></span> <span data-ttu-id="82d29-169">Haga clic en **extremos** tooopen **extremos** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="82d29-169">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpointicon.png)

    <span data-ttu-id="82d29-171">c.</span><span class="sxs-lookup"><span data-stu-id="82d29-171">c.</span></span> <span data-ttu-id="82d29-172">Haga clic en hello copia botón toocopy **documento de metadatos de federación** dirección url y péguela en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="82d29-172">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpoint.png)
     
    <span data-ttu-id="82d29-174">d.</span><span class="sxs-lookup"><span data-stu-id="82d29-174">d.</span></span> <span data-ttu-id="82d29-175">Ahora vaya toohello página de propiedades de **vínculo Springer** copia hello y **Id. de aplicación** con **copia** botón y péguelo en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="82d29-175">Now go toohello property page of **Springer Link** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appid.png)

    <span data-ttu-id="82d29-177">e.</span><span class="sxs-lookup"><span data-stu-id="82d29-177">e.</span></span> <span data-ttu-id="82d29-178">Generar hello **dirección URL de metadatos** con hello sigue el patrón:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="82d29-178">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="82d29-179">tooconfigure inicio de sesión único en **vínculo Springer** lado, necesita hello toosend genera **dirección URL de metadatos** demasiado[equipo de soporte técnico de vínculo Springer](mailto:identity@springernature.com).</span><span class="sxs-lookup"><span data-stu-id="82d29-179">tooconfigure single sign-on on **Springer Link** side, you need toosend hello generated **Metadata URL** too[Springer Link support team](mailto:identity@springernature.com).</span></span>

> [!TIP]
> <span data-ttu-id="82d29-180">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="82d29-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="82d29-181">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="82d29-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="82d29-182">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="82d29-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="82d29-183">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="82d29-183">Create an Azure AD test user</span></span>

<span data-ttu-id="82d29-184">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="82d29-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="82d29-186">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="82d29-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="82d29-187">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="82d29-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-springerlink-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="82d29-189">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="82d29-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-springerlink-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="82d29-191">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="82d29-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-springerlink-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="82d29-193">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="82d29-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-springerlink-tutorial/create_aaduser_04.png)

    <span data-ttu-id="82d29-195">a.</span><span class="sxs-lookup"><span data-stu-id="82d29-195">a.</span></span> <span data-ttu-id="82d29-196">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="82d29-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="82d29-197">b.</span><span class="sxs-lookup"><span data-stu-id="82d29-197">b.</span></span> <span data-ttu-id="82d29-198">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82d29-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="82d29-199">c.</span><span class="sxs-lookup"><span data-stu-id="82d29-199">c.</span></span> <span data-ttu-id="82d29-200">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="82d29-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="82d29-201">d.</span><span class="sxs-lookup"><span data-stu-id="82d29-201">d.</span></span> <span data-ttu-id="82d29-202">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="82d29-202">Click **Create**.</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="82d29-203">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="82d29-203">Assign hello Azure AD test user</span></span>

<span data-ttu-id="82d29-204">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSpringer vínculo.</span><span class="sxs-lookup"><span data-stu-id="82d29-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringer Link.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="82d29-206">**tooassign Britta Simon tooSpringer vínculo, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="82d29-206">**tooassign Britta Simon tooSpringer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="82d29-207">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="82d29-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="82d29-209">En la lista de aplicaciones de hello, seleccione **vínculo Springer**.</span><span class="sxs-lookup"><span data-stu-id="82d29-209">In hello applications list, select **Springer Link**.</span></span>

    ![Hola Springer vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_app.png)  

3. <span data-ttu-id="82d29-211">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="82d29-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="82d29-213">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="82d29-213">Click **Add** button.</span></span> <span data-ttu-id="82d29-214">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="82d29-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="82d29-216">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="82d29-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="82d29-217">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="82d29-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="82d29-218">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="82d29-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="82d29-219">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="82d29-219">Test single sign-on</span></span>

<span data-ttu-id="82d29-220">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="82d29-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="82d29-221">Al hacer clic en icono de vínculo Springer Hola Hola Panel de acceso, deberá obtener aplicaciones de vínculo Springer tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="82d29-221">When you click hello Springer Link tile in hello Access Panel, you should get automatically signed-on tooyour Springer Link application.</span></span>
<span data-ttu-id="82d29-222">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="82d29-222">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="82d29-223">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="82d29-223">Additional resources</span></span>

* [<span data-ttu-id="82d29-224">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82d29-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="82d29-225">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="82d29-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_203.png


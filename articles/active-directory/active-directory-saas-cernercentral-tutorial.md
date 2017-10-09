---
title: "Tutorial: Integración de Azure Active Directory con Cerner Central | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Cerner Central."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 3493d180e8f229b7cd228769f780f10208114889
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="53410-103">Tutorial: Integración de Azure Active Directory con Cerner Central</span><span class="sxs-lookup"><span data-stu-id="53410-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="53410-104">En este tutorial, aprenderá cómo toointegrate Cerner Central con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="53410-104">In this tutorial, you learn how toointegrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="53410-105">Integración Cerner Central con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="53410-105">Integrating Cerner Central with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="53410-106">Puede controlar en Azure AD que tenga acceso tooCerner Central</span><span class="sxs-lookup"><span data-stu-id="53410-106">You can control in Azure AD who has access tooCerner Central</span></span>
- <span data-ttu-id="53410-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooCerner Central (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="53410-107">You can enable your users tooautomatically get signed-on tooCerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="53410-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="53410-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="53410-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="53410-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53410-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="53410-110">Prerequisites</span></span>

<span data-ttu-id="53410-111">integración de Azure AD con Cerner Central tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="53410-111">tooconfigure Azure AD integration with Cerner Central, you need hello following items:</span></span>

- <span data-ttu-id="53410-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="53410-112">An Azure AD subscription</span></span>
- <span data-ttu-id="53410-113">Una cuenta de sistema de Cerner Central aprobada</span><span class="sxs-lookup"><span data-stu-id="53410-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="53410-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="53410-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="53410-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="53410-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="53410-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="53410-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="53410-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="53410-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="53410-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="53410-118">Scenario description</span></span>
<span data-ttu-id="53410-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="53410-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="53410-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="53410-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="53410-121">Agregar Cerner Central desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="53410-121">Adding Cerner Central from hello gallery</span></span>
2. <span data-ttu-id="53410-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="53410-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-hello-gallery"></a><span data-ttu-id="53410-123">Agregar Cerner Central desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="53410-123">Adding Cerner Central from hello gallery</span></span>
<span data-ttu-id="53410-124">integración de hello tooconfigure del Cerner Central en Azure AD, deberá tooadd Cerner centro de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="53410-124">tooconfigure hello integration of Cerner Central into Azure AD, you need tooadd Cerner Central from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="53410-125">**tooadd Cerner Central desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="53410-125">**tooadd Cerner Central from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="53410-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="53410-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="53410-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="53410-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="53410-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="53410-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="53410-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón encima de cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="53410-131">tooadd new application, click **New application** button on top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="53410-133">En el cuadro de búsqueda de hello, escriba **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="53410-133">In hello search box, type **Cerner Central**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="53410-135">En el panel de resultados de hello, seleccione **Cerner Central**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="53410-135">In hello results panel, select **Cerner Central**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="53410-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="53410-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="53410-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Cerner Central con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="53410-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="53410-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en el centro de Cerner es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53410-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cerner Central is tooa user in Azure AD.</span></span> <span data-ttu-id="53410-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el centro de Cerner debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="53410-140">In other words, a link relationship between an Azure AD user and hello related user in Cerner Central needs toobe established.</span></span>

<span data-ttu-id="53410-141">tooconfigure y prueba de inicio de sesión único en Azure AD con Cerner Central, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="53410-141">tooconfigure and test Azure AD single sign-on with Cerner Central, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="53410-142">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="53410-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="53410-143">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="53410-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="53410-144">**[Crear un usuario de prueba de centro de Cerner](#creating-a-cerner-central-test-user)**  -toohave un equivalente de Britta Simon en Centro de Cerner es representación toohello vinculado Azure AD del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="53410-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - toohave a counterpart of Britta Simon in Cerner Central that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="53410-145">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="53410-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="53410-146">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="53410-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="53410-147">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="53410-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="53410-148">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de centro de Cerner.</span><span class="sxs-lookup"><span data-stu-id="53410-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="53410-149">**inicio de sesión único en tooconfigure Azure AD con Cerner Central, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="53410-149">**tooconfigure Azure AD single sign-on with Cerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="53410-150">En el portal de Azure, en Hola Hola **Cerner Central** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="53410-150">In hello Azure portal, on hello **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="53410-152">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="53410-152">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="53410-154">En hello **Cerner Central dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="53410-154">On hello **Cerner Central Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="53410-156">a.</span><span class="sxs-lookup"><span data-stu-id="53410-156">a.</span></span> <span data-ttu-id="53410-157">Hola **identificador** cuadro de texto, valor de tipo hello mediante Hola siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="53410-157">In hello **Identifier** textbox, type hello value using hello following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="53410-158">b.</span><span class="sxs-lookup"><span data-stu-id="53410-158">b.</span></span> <span data-ttu-id="53410-159">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL con hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="53410-159">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="53410-160">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="53410-160">These values are not hello real.</span></span> <span data-ttu-id="53410-161">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="53410-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="53410-162">Póngase en contacto con [equipo de soporte técnico de centro de Cerner](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="53410-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget these values.</span></span>
 
4. <span data-ttu-id="53410-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="53410-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="53410-165">Hola toogenerate **metadatos** dirección url, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="53410-165">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="53410-166">a.</span><span class="sxs-lookup"><span data-stu-id="53410-166">a.</span></span> <span data-ttu-id="53410-167">Haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="53410-167">Click **App registrations**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="53410-169">b.</span><span class="sxs-lookup"><span data-stu-id="53410-169">b.</span></span> <span data-ttu-id="53410-170">Haga clic en **extremos** tooopen **extremos** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="53410-170">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="53410-172">c.</span><span class="sxs-lookup"><span data-stu-id="53410-172">c.</span></span> <span data-ttu-id="53410-173">Haga clic en hello copia botón toocopy **documento de metadatos de federación** dirección url y péguela en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="53410-173">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="53410-175">d.</span><span class="sxs-lookup"><span data-stu-id="53410-175">d.</span></span> <span data-ttu-id="53410-176">Ahora vaya toohello página de propiedades de **Cerner Central** copia hello y **Id. de aplicación** con **copia** botón y péguelo en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="53410-176">Now go toohello property page of **Cerner Central** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="53410-178">e.</span><span class="sxs-lookup"><span data-stu-id="53410-178">e.</span></span> <span data-ttu-id="53410-179">Generar hello **dirección URL de metadatos** con hello sigue el patrón:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="53410-179">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="53410-180">tooconfigure inicio de sesión único en **Cerner Central** lateral, necesita hello toosend **dirección URL de metadatos** demasiado[soporte técnico de centro de Cerner](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="53410-180">tooconfigure single sign-on on **Cerner Central** side, you need toosend hello **Metadata URL** too[Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="53410-181">Configuran Hola SSO en la integración de aplicaciones lado toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="53410-181">They configure hello SSO on application side toocomplete hello integration.</span></span>

> [!TIP]
> <span data-ttu-id="53410-182">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="53410-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="53410-183">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="53410-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="53410-184">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="53410-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="53410-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="53410-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="53410-186">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="53410-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span> 

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="53410-188">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="53410-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="53410-189">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="53410-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="53410-191">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="53410-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="53410-193">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="53410-193">tooopen hello **User** dialog, click **Add**.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="53410-195">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="53410-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="53410-197">a.</span><span class="sxs-lookup"><span data-stu-id="53410-197">a.</span></span> <span data-ttu-id="53410-198">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="53410-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="53410-199">b.</span><span class="sxs-lookup"><span data-stu-id="53410-199">b.</span></span> <span data-ttu-id="53410-200">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="53410-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="53410-201">c.</span><span class="sxs-lookup"><span data-stu-id="53410-201">c.</span></span> <span data-ttu-id="53410-202">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="53410-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="53410-203">d.</span><span class="sxs-lookup"><span data-stu-id="53410-203">d.</span></span> <span data-ttu-id="53410-204">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="53410-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="53410-205">Crear un usuario de prueba de Cerner Central</span><span class="sxs-lookup"><span data-stu-id="53410-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="53410-206">La aplicación **Cerner Central** permite la autenticación desde cualquier proveedor de identidades federado.</span><span class="sxs-lookup"><span data-stu-id="53410-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="53410-207">Si un usuario es capaz de toolog en página de inicio de aplicación toohello, que están federados y no necesitan ningún aprovisionamiento manual.</span><span class="sxs-lookup"><span data-stu-id="53410-207">If a user is able toolog in toohello application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="53410-208">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="53410-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="53410-209">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooCerner Central.</span><span class="sxs-lookup"><span data-stu-id="53410-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCerner Central.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="53410-211">**tooassign Britta Simon tooCerner Central, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="53410-211">**tooassign Britta Simon tooCerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="53410-212">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="53410-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="53410-214">En la lista de aplicaciones de hello, seleccione **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="53410-214">In hello applications list, select **Cerner Central**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="53410-216">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="53410-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="53410-218">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="53410-218">Click **Add** button.</span></span> <span data-ttu-id="53410-219">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="53410-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="53410-221">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="53410-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="53410-222">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="53410-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="53410-223">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="53410-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="53410-224">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="53410-224">Testing single sign-on</span></span>

<span data-ttu-id="53410-225">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="53410-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="53410-226">Al hacer clic en hello Cerner centro disponer en mosaico en hello Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="53410-226">When you click hello Cerner Central tile in hello Access Panel, you should get automatically signed-on tooyour Cerner Central application.</span></span> <span data-ttu-id="53410-227">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="53410-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="53410-228">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="53410-228">Additional resources</span></span>

* [<span data-ttu-id="53410-229">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53410-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="53410-230">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="53410-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png


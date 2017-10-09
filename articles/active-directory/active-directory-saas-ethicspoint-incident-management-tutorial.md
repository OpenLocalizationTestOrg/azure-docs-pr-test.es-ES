---
title: "Tutorial: Integración de Azure Active Directory con EthicsPoint Incident Management (EPIM) | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y administración de incidentes de EthicsPoint (EPIM)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8cb31a4c-9309-469b-93ac-daf0d3c7a3e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 73ef5fab815cddb3728f4b23173f99e62aec5bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ethicspoint-incident-management-epim"></a><span data-ttu-id="ce112-103">Tutorial: Integración de Azure Active Directory con EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="ce112-103">Tutorial: Azure Active Directory integration with EthicsPoint Incident Management (EPIM)</span></span>

<span data-ttu-id="ce112-104">En este tutorial, aprenderá cómo toointegrate administración de incidentes de EthicsPoint (EPIM) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ce112-104">In this tutorial, you learn how toointegrate EthicsPoint Incident Management (EPIM) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce112-105">Integración de administración de incidentes de EthicsPoint (EPIM) con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ce112-105">Integrating EthicsPoint Incident Management (EPIM) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ce112-106">Puede controlar en Azure AD que tenga acceso tooEthicsPoint administración de incidentes (EPIM)</span><span class="sxs-lookup"><span data-stu-id="ce112-106">You can control in Azure AD who has access tooEthicsPoint Incident Management (EPIM)</span></span>
- <span data-ttu-id="ce112-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión con tooEthicsPoint administración de incidentes (EPIM) (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce112-107">You can enable your users tooautomatically get signed-on tooEthicsPoint Incident Management (EPIM) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ce112-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ce112-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ce112-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ce112-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce112-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ce112-110">Prerequisites</span></span>

<span data-ttu-id="ce112-111">tooconfigure integración de Azure AD con administración de incidentes de EthicsPoint (EPIM), necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ce112-111">tooconfigure Azure AD integration with EthicsPoint Incident Management (EPIM), you need hello following items:</span></span>

- <span data-ttu-id="ce112-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce112-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce112-113">Una suscripción habilitada para el inicio de sesión único en EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="ce112-113">A EthicsPoint Incident Management (EPIM) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ce112-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ce112-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ce112-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ce112-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ce112-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ce112-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ce112-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce112-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ce112-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ce112-118">Scenario description</span></span>
<span data-ttu-id="ce112-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ce112-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ce112-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="ce112-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ce112-121">Adición de administración de incidentes de EthicsPoint (EPIM) desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ce112-121">Adding EthicsPoint Incident Management (EPIM) from hello gallery</span></span>
2. <span data-ttu-id="ce112-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce112-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ethicspoint-incident-management-epim-from-hello-gallery"></a><span data-ttu-id="ce112-123">Adición de administración de incidentes de EthicsPoint (EPIM) desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ce112-123">Adding EthicsPoint Incident Management (EPIM) from hello gallery</span></span>
<span data-ttu-id="ce112-124">integración de hello tooconfigure de administración de incidentes de EthicsPoint (EPIM) en Azure AD, deberá tooadd administración de incidentes de EthicsPoint (EPIM) de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="ce112-124">tooconfigure hello integration of EthicsPoint Incident Management (EPIM) into Azure AD, you need tooadd EthicsPoint Incident Management (EPIM) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ce112-125">**tooadd administración de incidentes de EthicsPoint (EPIM) desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ce112-125">**tooadd EthicsPoint Incident Management (EPIM) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce112-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="ce112-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ce112-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ce112-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ce112-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ce112-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="ce112-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce112-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="ce112-133">En el cuadro de búsqueda de hello, escriba **administración de incidentes de EthicsPoint (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="ce112-133">In hello search box, type **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_search.png)

5. <span data-ttu-id="ce112-135">En el panel de resultados de hello, seleccione **administración de incidentes de EthicsPoint (EPIM)**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ce112-135">In hello results panel, select **EthicsPoint Incident Management (EPIM)**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ce112-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce112-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ce112-138">En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con EthicsPoint Incident Management (EPIM) con un usuario de prueba llamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="ce112-138">In this section, you configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM) based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ce112-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en administración de incidentes de EthicsPoint (EPIM) es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce112-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EthicsPoint Incident Management (EPIM) is tooa user in Azure AD.</span></span> <span data-ttu-id="ce112-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en administración de incidentes de EthicsPoint (EPIM) debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="ce112-140">In other words, a link relationship between an Azure AD user and hello related user in EthicsPoint Incident Management (EPIM) needs toobe established.</span></span>

<span data-ttu-id="ce112-141">En administración de incidentes de EthicsPoint (EPIM), asignar un valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce112-141">In EthicsPoint Incident Management (EPIM), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ce112-142">tooconfigure y prueba de inicio de sesión único en Azure AD con administración de incidentes de EthicsPoint (EPIM), deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ce112-142">tooconfigure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ce112-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="ce112-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ce112-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ce112-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ce112-145">**[Crear un usuario de prueba de administración de incidentes de EthicsPoint (EPIM)](#creating-a-ethicspoint-incident-management-epim-test-user)**  -toohave un equivalente de Britta Simon administración de incidentes en EthicsPoint (EPIM) que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="ce112-145">**[Creating a EthicsPoint Incident Management (EPIM) test user](#creating-a-ethicspoint-incident-management-epim-test-user)** - toohave a counterpart of Britta Simon in EthicsPoint Incident Management (EPIM) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ce112-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ce112-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ce112-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ce112-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ce112-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce112-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ce112-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de administración de incidentes de EthicsPoint (EPIM).</span><span class="sxs-lookup"><span data-stu-id="ce112-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EthicsPoint Incident Management (EPIM) application.</span></span>

<span data-ttu-id="ce112-150">**tooconfigure inicio de sesión único en Azure AD con administración de incidentes de EthicsPoint (EPIM), lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ce112-150">**tooconfigure Azure AD single sign-on with EthicsPoint Incident Management (EPIM), perform hello following steps:**</span></span>

1. <span data-ttu-id="ce112-151">En el portal de Azure, en Hola Hola **administración de incidentes de EthicsPoint (EPIM)** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ce112-151">In hello Azure portal, on hello **EthicsPoint Incident Management (EPIM)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="ce112-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ce112-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_samlbase.png)

3. <span data-ttu-id="ce112-155">En hello **dominio de administración de incidentes de EthicsPoint (EPIM) y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ce112-155">On hello **EthicsPoint Incident Management (EPIM) Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_url.png)

    <span data-ttu-id="ce112-157">a.</span><span class="sxs-lookup"><span data-stu-id="ce112-157">a.</span></span> <span data-ttu-id="ce112-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="ce112-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.navexglobal.com`|
    | `https://<companyname>.ethicspointvp.com`|

    <span data-ttu-id="ce112-159">b.</span><span class="sxs-lookup"><span data-stu-id="ce112-159">b.</span></span> <span data-ttu-id="ce112-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.navexglobal.com/adfs/services/trust`</span><span class="sxs-lookup"><span data-stu-id="ce112-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.navexglobal.com/adfs/services/trust`</span></span>

    <span data-ttu-id="ce112-161">c.</span><span class="sxs-lookup"><span data-stu-id="ce112-161">c.</span></span> <span data-ttu-id="ce112-162">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<servername>.navexglobal.com/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="ce112-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.navexglobal.com/adfs/ls/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ce112-163">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="ce112-163">These values are not real.</span></span> <span data-ttu-id="ce112-164">Actualizar estos valores con la dirección URL de respuesta real hello, el identificador y la dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ce112-164">Update these values with hello actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="ce112-165">Póngase en contacto con [equipo de soporte técnico de cliente de administración de incidentes de EthicsPoint (EPIM)](http://www.navexglobal.com/company/contact-us) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="ce112-165">Contact [EthicsPoint Incident Management (EPIM) Client support team](http://www.navexglobal.com/company/contact-us) tooget these values.</span></span> 

4. <span data-ttu-id="ce112-166">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ce112-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_certificate.png) 

5. <span data-ttu-id="ce112-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="ce112-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="ce112-170">tooconfigure inicio de sesión único en **administración de incidentes de EthicsPoint (EPIM)** lado, necesita hello toosend descargado **Metadata XML** demasiado[soporte de administración de incidentes de EthicsPoint (EPIM) equipo](http://www.navexglobal.com/company/contact-us).</span><span class="sxs-lookup"><span data-stu-id="ce112-170">tooconfigure single sign-on on **EthicsPoint Incident Management (EPIM)** side, you need toosend hello downloaded **Metadata XML** too[EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="ce112-171">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="ce112-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ce112-172">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="ce112-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ce112-173">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ce112-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ce112-174">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce112-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="ce112-175">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="ce112-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="ce112-177">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ce112-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce112-178">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="ce112-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ce112-180">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ce112-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ce112-182">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce112-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ce112-184">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="ce112-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ce112-186">a.</span><span class="sxs-lookup"><span data-stu-id="ce112-186">a.</span></span> <span data-ttu-id="ce112-187">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ce112-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce112-188">b.</span><span class="sxs-lookup"><span data-stu-id="ce112-188">b.</span></span> <span data-ttu-id="ce112-189">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ce112-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ce112-190">c.</span><span class="sxs-lookup"><span data-stu-id="ce112-190">c.</span></span> <span data-ttu-id="ce112-191">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ce112-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ce112-192">d.</span><span class="sxs-lookup"><span data-stu-id="ce112-192">d.</span></span> <span data-ttu-id="ce112-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ce112-193">Click **Create**.</span></span>
 
### <a name="creating-a-ethicspoint-incident-management-epim-test-user"></a><span data-ttu-id="ce112-194">Creación de un usuario de prueba de EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="ce112-194">Creating a EthicsPoint Incident Management (EPIM) test user</span></span>

<span data-ttu-id="ce112-195">En esta sección, creará un usuario llamado Britta Simon en EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="ce112-195">In this section, you create a user called Britta Simon in EthicsPoint Incident Management (EPIM).</span></span> <span data-ttu-id="ce112-196">Trabaje con [equipo de soporte técnico de administración de incidentes de EthicsPoint (EPIM)](http://www.navexglobal.com/company/contact-us) tooadd los usuarios de hello en la plataforma de administración de incidentes de EthicsPoint (EPIM) Hola.</span><span class="sxs-lookup"><span data-stu-id="ce112-196">Please work with [EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us) tooadd hello users in hello EthicsPoint Incident Management (EPIM) platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ce112-197">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce112-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ce112-198">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooEthicsPoint administración de incidentes (EPIM).</span><span class="sxs-lookup"><span data-stu-id="ce112-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEthicsPoint Incident Management (EPIM).</span></span>

![Asignar usuario][200] 

<span data-ttu-id="ce112-200">**tooassign Britta Simon tooEthicsPoint administración de incidentes (EPIM), lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ce112-200">**tooassign Britta Simon tooEthicsPoint Incident Management (EPIM), perform hello following steps:**</span></span>

1. <span data-ttu-id="ce112-201">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ce112-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ce112-203">En la lista de aplicaciones de hello, seleccione **administración de incidentes de EthicsPoint (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="ce112-203">In hello applications list, select **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_app.png) 

3. <span data-ttu-id="ce112-205">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ce112-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="ce112-207">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ce112-207">Click **Add** button.</span></span> <span data-ttu-id="ce112-208">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ce112-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="ce112-210">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce112-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ce112-211">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ce112-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ce112-212">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ce112-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ce112-213">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="ce112-213">Testing single sign-on</span></span>

<span data-ttu-id="ce112-214">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ce112-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="ce112-215">Al hacer clic en icono de administración de incidentes de EthicsPoint (EPIM) Hola Hola Panel de acceso, deberá obtener la aplicación de administración de incidentes de EthicsPoint (EPIM) tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="ce112-215">When you click hello EthicsPoint Incident Management (EPIM) tile in hello Access Panel, you should get automatically signed-on tooyour EthicsPoint Incident Management (EPIM) application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ce112-216">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ce112-216">Additional resources</span></span>

* [<span data-ttu-id="ce112-217">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce112-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce112-218">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ce112-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_203.png


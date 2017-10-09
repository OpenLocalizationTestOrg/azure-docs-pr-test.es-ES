---
title: "Tutorial: integración de Azure Active Directory con StatusPage | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y la página de estado."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 7c6717017984241e9e459273ead4b5e062311120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="0954e-103">Tutorial: Integración de Azure Active Directory con StatusPage</span><span class="sxs-lookup"><span data-stu-id="0954e-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="0954e-104">En este tutorial, aprenderá cómo toointegrate página de estado con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0954e-104">In this tutorial, you learn how toointegrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0954e-105">Página de estado de integración con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0954e-105">Integrating StatusPage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0954e-106">Puede controlar en Azure AD que tenga acceso tooStatusPage</span><span class="sxs-lookup"><span data-stu-id="0954e-106">You can control in Azure AD who has access tooStatusPage</span></span>
- <span data-ttu-id="0954e-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooStatusPage (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0954e-107">You can enable your users tooautomatically get signed-on tooStatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0954e-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0954e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0954e-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0954e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0954e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0954e-110">Prerequisites</span></span>

<span data-ttu-id="0954e-111">tooconfigure integración de Azure AD con la página de estado, deberá Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0954e-111">tooconfigure Azure AD integration with StatusPage, you need hello following items:</span></span>

- <span data-ttu-id="0954e-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0954e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0954e-113">Una suscripción habilitada para inicio de sesión único en StatusPage</span><span class="sxs-lookup"><span data-stu-id="0954e-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0954e-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0954e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0954e-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0954e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0954e-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0954e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0954e-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0954e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0954e-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0954e-118">Scenario description</span></span>
<span data-ttu-id="0954e-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0954e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0954e-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="0954e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0954e-121">Agregar página de estado de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0954e-121">Adding StatusPage from hello gallery</span></span>
2. <span data-ttu-id="0954e-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0954e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-hello-gallery"></a><span data-ttu-id="0954e-123">Agregar página de estado de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="0954e-123">Adding StatusPage from hello gallery</span></span>
<span data-ttu-id="0954e-124">integración de hello tooconfigure de página de estado en Azure AD, deberá tooadd página de estado de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="0954e-124">tooconfigure hello integration of StatusPage into Azure AD, you need tooadd StatusPage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0954e-125">**tooadd página de estado de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0954e-125">**tooadd StatusPage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0954e-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0954e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0954e-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0954e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0954e-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0954e-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0954e-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0954e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0954e-133">En el cuadro de búsqueda de hello, escriba **página de estado**.</span><span class="sxs-lookup"><span data-stu-id="0954e-133">In hello search box, type **StatusPage**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="0954e-135">En el panel de resultados de hello, seleccione **página de estado**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0954e-135">In hello results panel, select **StatusPage**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0954e-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0954e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0954e-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con StatusPage con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0954e-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0954e-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en la página de estado es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0954e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in StatusPage is tooa user in Azure AD.</span></span> <span data-ttu-id="0954e-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en la página de estado debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="0954e-140">In other words, a link relationship between an Azure AD user and hello related user in StatusPage needs toobe established.</span></span>

<span data-ttu-id="0954e-141">En la página de estado, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0954e-141">In StatusPage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0954e-142">tooconfigure y prueba de inicio de sesión único en Azure AD con página de estado, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0954e-142">tooconfigure and test Azure AD single sign-on with StatusPage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0954e-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="0954e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0954e-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0954e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0954e-145">**[Crear un usuario de prueba de la página de estado](#creating-a-statuspage-test-user)**  -toohave un equivalente de Britta Simon en la página de estado que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="0954e-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - toohave a counterpart of Britta Simon in StatusPage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0954e-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0954e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0954e-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0954e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0954e-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0954e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0954e-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de la página de estado.</span><span class="sxs-lookup"><span data-stu-id="0954e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="0954e-150">**inicio de sesión único en tooconfigure Azure AD con la página de estado, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0954e-150">**tooconfigure Azure AD single sign-on with StatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="0954e-151">En el portal de Azure, en Hola Hola **página de estado** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0954e-151">In hello Azure portal, on hello **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0954e-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0954e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="0954e-155">En hello **dominio de la página de estado y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0954e-155">On hello **StatusPage Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="0954e-157">a.</span><span class="sxs-lookup"><span data-stu-id="0954e-157">a.</span></span> <span data-ttu-id="0954e-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="0954e-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="0954e-159">b.</span><span class="sxs-lookup"><span data-stu-id="0954e-159">b.</span></span> <span data-ttu-id="0954e-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="0954e-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="0954e-161">Póngase en contacto con el equipo de soporte técnico de página de estado de hello en [ SupportTeam@statuspage.io ](mailto:SupportTeam@statuspage.io)toorequest metadatos necesarios tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0954e-161">Contact hello StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)toorequest metadata necessary tooconfigure single sign-on.</span></span> 
    >
    ><span data-ttu-id="0954e-162">a.</span><span class="sxs-lookup"><span data-stu-id="0954e-162">a.</span></span> <span data-ttu-id="0954e-163">En los metadatos de hello, copie el valor del emisor de hello y, a continuación, péguelo en hello **identificador** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0954e-163">From hello metadata, copy hello Issuer value, and then paste it into hello **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="0954e-164">b.</span><span class="sxs-lookup"><span data-stu-id="0954e-164">b.</span></span> <span data-ttu-id="0954e-165">En los metadatos de hello, copie Hola dirección URL de respuesta y, a continuación, péguelo en hello **dirección URL de respuesta** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0954e-165">From hello metadata, copy hello Reply URL, and then paste it into hello **Reply URL** textbox.</span></span>

4. <span data-ttu-id="0954e-166">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0954e-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="0954e-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0954e-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0954e-170">En hello **configuración de página de estado** sección, haga clic en **Configurar página de estado** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="0954e-170">On hello **StatusPage Configuration** section, click **Configure StatusPage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0954e-171">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="0954e-171">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="0954e-173">En otra ventana del explorador, inicie sesión en el sitio de empresa de página de estado de tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="0954e-173">In another browser window, sign on tooyour StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="0954e-174">En la barra de herramientas principal de hello, haga clic en **administrar cuenta**.</span><span class="sxs-lookup"><span data-stu-id="0954e-174">In hello main toolbar, click **Manage Account**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="0954e-176">Haga clic en hello **Single Sign-on** ficha.</span><span class="sxs-lookup"><span data-stu-id="0954e-176">Click hello **Single Sign-on** tab.</span></span> 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="0954e-178">En la página de configuración de SSO de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="0954e-178">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="0954e-181">a.</span><span class="sxs-lookup"><span data-stu-id="0954e-181">a.</span></span> <span data-ttu-id="0954e-182">Hola **dirección URL de destino de SSO** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0954e-182">In hello **SSO Target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0954e-183">b.</span><span class="sxs-lookup"><span data-stu-id="0954e-183">b.</span></span> <span data-ttu-id="0954e-184">Abra el certificado descargado en el Bloc de notas, Hola copiar contenido y, a continuación, péguelo en hello **certificado** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="0954e-184">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span> 

    <span data-ttu-id="0954e-185">c.</span><span class="sxs-lookup"><span data-stu-id="0954e-185">c.</span></span> <span data-ttu-id="0954e-186">Haga clic en **GUARDAR CONFIGURACIÓN**.</span><span class="sxs-lookup"><span data-stu-id="0954e-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="0954e-187">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="0954e-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0954e-188">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="0954e-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0954e-189">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0954e-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0954e-190">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0954e-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="0954e-191">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="0954e-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0954e-193">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0954e-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0954e-194">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="0954e-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0954e-196">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0954e-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0954e-198">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0954e-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0954e-200">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0954e-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0954e-202">a.</span><span class="sxs-lookup"><span data-stu-id="0954e-202">a.</span></span> <span data-ttu-id="0954e-203">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0954e-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0954e-204">b.</span><span class="sxs-lookup"><span data-stu-id="0954e-204">b.</span></span> <span data-ttu-id="0954e-205">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0954e-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0954e-206">c.</span><span class="sxs-lookup"><span data-stu-id="0954e-206">c.</span></span> <span data-ttu-id="0954e-207">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0954e-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0954e-208">d.</span><span class="sxs-lookup"><span data-stu-id="0954e-208">d.</span></span> <span data-ttu-id="0954e-209">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0954e-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="0954e-210">Creación de un usuario de prueba de StatusPage</span><span class="sxs-lookup"><span data-stu-id="0954e-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="0954e-211">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en la página de estado.</span><span class="sxs-lookup"><span data-stu-id="0954e-211">hello objective of this section is toocreate a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="0954e-212">StatusPage admite el aprovisionamiento Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="0954e-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="0954e-213">Ya lo ha habilitado en [Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="0954e-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="0954e-214">**toocreate un usuario llamado Britta Simon en la página de estado, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0954e-214">**toocreate a user called Britta Simon in StatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="0954e-215">Sitio de empresa de página de estado de tooyour inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="0954e-215">Sign-on tooyour StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="0954e-216">En el menú de hello en la parte superior de hello, haga clic en **administrar cuenta**.</span><span class="sxs-lookup"><span data-stu-id="0954e-216">In hello menu on hello top, click **Manage Account**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="0954e-218">Haga clic en hello **los miembros del equipo** ficha.</span><span class="sxs-lookup"><span data-stu-id="0954e-218">Click hello **Team Members** tab.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="0954e-220">Haga clic en **ADD TEAM MEMBER**(Agregar miembro del equipo).</span><span class="sxs-lookup"><span data-stu-id="0954e-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="0954e-222">Hola de tipo **dirección de correo electrónico**, **nombre**, y **apellidos** de un usuario válido que quiera tooprovision en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="0954e-222">Type hello **Email Address**, **First Name**, and **Sur Name** of a valid user you want tooprovision into hello related textboxes.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="0954e-224">En **Rol**, elija **Administrador de clientes**.</span><span class="sxs-lookup"><span data-stu-id="0954e-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="0954e-225">Haga clic en **CREATE ACCOUNT** (CREAR CUENTA).</span><span class="sxs-lookup"><span data-stu-id="0954e-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0954e-226">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0954e-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0954e-227">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooStatusPage.</span><span class="sxs-lookup"><span data-stu-id="0954e-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooStatusPage.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0954e-229">**tooassign Britta Simon tooStatusPage, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="0954e-229">**tooassign Britta Simon tooStatusPage, perform hello following steps:**</span></span>

1. <span data-ttu-id="0954e-230">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0954e-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0954e-232">En la lista de aplicaciones de hello, seleccione **página de estado**.</span><span class="sxs-lookup"><span data-stu-id="0954e-232">In hello applications list, select **StatusPage**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="0954e-234">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0954e-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0954e-236">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0954e-236">Click **Add** button.</span></span> <span data-ttu-id="0954e-237">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0954e-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0954e-239">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="0954e-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0954e-240">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0954e-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0954e-241">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0954e-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0954e-242">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0954e-242">Testing single sign-on</span></span>

<span data-ttu-id="0954e-243">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0954e-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0954e-244">Al hacer clic en icono de la página de estado de Hola Hola Panel de acceso, deberá obtener la aplicación de la página de estado de tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="0954e-244">When you click hello StatusPage tile in hello Access Panel, you should get automatically signed-on tooyour StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0954e-245">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0954e-245">Additional resources</span></span>

* [<span data-ttu-id="0954e-246">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0954e-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0954e-247">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0954e-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png


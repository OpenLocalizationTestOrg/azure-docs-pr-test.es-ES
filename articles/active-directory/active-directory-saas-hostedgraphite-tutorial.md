---
title: "Tutorial: Integración de Azure Active Directory con Hosted Graphite | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y gris hospedado."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a1ac4d7f-d079-4f3c-b6da-0f520d427ceb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: d8914f6417ba8fbdef1a48e1b36635200ba130d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hosted-graphite"></a><span data-ttu-id="018e4-103">Tutorial: Integración de Azure Active Directory con Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="018e4-103">Tutorial: Azure Active Directory integration with Hosted Graphite</span></span>

<span data-ttu-id="018e4-104">En este tutorial, aprenderá cómo toointegrate Hosted gris con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="018e4-104">In this tutorial, you learn how toointegrate Hosted Graphite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="018e4-105">Integración hospedado gris con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="018e4-105">Integrating Hosted Graphite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="018e4-106">Puede controlar en Azure AD que tenga acceso tooHosted gris</span><span class="sxs-lookup"><span data-stu-id="018e4-106">You can control in Azure AD who has access tooHosted Graphite</span></span>
- <span data-ttu-id="018e4-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooHosted gris (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="018e4-107">You can enable your users tooautomatically get signed-on tooHosted Graphite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="018e4-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="018e4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="018e4-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="018e4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="018e4-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="018e4-110">Prerequisites</span></span>

<span data-ttu-id="018e4-111">tooconfigure integración de Azure AD con hospedado gris, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="018e4-111">tooconfigure Azure AD integration with Hosted Graphite, you need hello following items:</span></span>

- <span data-ttu-id="018e4-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="018e4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="018e4-113">Una suscripción habilitada para el inicio de sesión único en Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="018e4-113">A Hosted Graphite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="018e4-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="018e4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="018e4-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="018e4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="018e4-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="018e4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="018e4-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="018e4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="018e4-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="018e4-118">Scenario description</span></span>
<span data-ttu-id="018e4-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="018e4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="018e4-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="018e4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="018e4-121">Agregar hospedado gris de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="018e4-121">Adding Hosted Graphite from hello gallery</span></span>
2. <span data-ttu-id="018e4-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="018e4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hosted-graphite-from-hello-gallery"></a><span data-ttu-id="018e4-123">Agregar hospedado gris de la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="018e4-123">Adding Hosted Graphite from hello gallery</span></span>
<span data-ttu-id="018e4-124">integración de hello tooconfigure de gris hospedado en Azure AD, deberá tooadd gris hospedados en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="018e4-124">tooconfigure hello integration of Hosted Graphite into Azure AD, you need tooadd Hosted Graphite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="018e4-125">**tooadd Hosted gris de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="018e4-125">**tooadd Hosted Graphite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="018e4-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="018e4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="018e4-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="018e4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="018e4-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="018e4-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="018e4-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="018e4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="018e4-133">En el cuadro de búsqueda de hello, escriba **gris hospedado**.</span><span class="sxs-lookup"><span data-stu-id="018e4-133">In hello search box, type **Hosted Graphite**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_search.png)

5. <span data-ttu-id="018e4-135">En el panel de resultados de hello, seleccione **gris hospedado**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="018e4-135">In hello results panel, select **Hosted Graphite**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="018e4-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="018e4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="018e4-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Hosted Graphite con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="018e4-138">In this section, you configure and test Azure AD single sign-on with Hosted Graphite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="018e4-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en gris hospedado es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="018e4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Hosted Graphite is tooa user in Azure AD.</span></span> <span data-ttu-id="018e4-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en gris hospedado debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="018e4-140">In other words, a link relationship between an Azure AD user and hello related user in Hosted Graphite needs toobe established.</span></span>

<span data-ttu-id="018e4-141">En gris hospedado, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="018e4-141">In Hosted Graphite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="018e4-142">tooconfigure y prueba de inicio de sesión único en Azure AD con gris hospedado, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="018e4-142">tooconfigure and test Azure AD single sign-on with Hosted Graphite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="018e4-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="018e4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="018e4-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="018e4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="018e4-145">**[Crear un usuario de prueba hospedada gris](#creating-a-hosted-graphite-test-user)**  -toohave un equivalente de Britta Simon en gris hospedado que está vinculado toohello Azure AD representación del usuario.</span><span class="sxs-lookup"><span data-stu-id="018e4-145">**[Creating a Hosted Graphite test user](#creating-a-hosted-graphite-test-user)** - toohave a counterpart of Britta Simon in Hosted Graphite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="018e4-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="018e4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="018e4-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="018e4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="018e4-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="018e4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="018e4-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación hospedada gris.</span><span class="sxs-lookup"><span data-stu-id="018e4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Hosted Graphite application.</span></span>

<span data-ttu-id="018e4-150">**inicio de sesión único en tooconfigure Azure AD con gris hospedado, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="018e4-150">**tooconfigure Azure AD single sign-on with Hosted Graphite, perform hello following steps:**</span></span>

1. <span data-ttu-id="018e4-151">En el portal de Azure, en Hola Hola **gris hospedado** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="018e4-151">In hello Azure portal, on hello **Hosted Graphite** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="018e4-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="018e4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_samlbase.png)

3. <span data-ttu-id="018e4-155">En hello **hospedado gris dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado por IDP**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="018e4-155">On hello **Hosted Graphite Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_url.png)

    <span data-ttu-id="018e4-157">a.</span><span class="sxs-lookup"><span data-stu-id="018e4-157">a.</span></span> <span data-ttu-id="018e4-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.hostedgraphite.com/metadata/<user id>`</span><span class="sxs-lookup"><span data-stu-id="018e4-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/metadata/<user id>`</span></span>

    <span data-ttu-id="018e4-159">b.</span><span class="sxs-lookup"><span data-stu-id="018e4-159">b.</span></span> <span data-ttu-id="018e4-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.hostedgraphite.com/complete/saml/<user id>`</span><span class="sxs-lookup"><span data-stu-id="018e4-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/complete/saml/<user id>`</span></span>

4. <span data-ttu-id="018e4-161">En hello **hospedado gris dominio y las direcciones URL** sección, si desea que aplicación de hello tooconfigure en **modo iniciado en SP**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="018e4-161">On hello **Hosted Graphite Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_10.png)
  
    <span data-ttu-id="018e4-163">a.</span><span class="sxs-lookup"><span data-stu-id="018e4-163">a.</span></span> <span data-ttu-id="018e4-164">Haga clic en hello **mostrar avanzadas de configuración de direcciones URL** opción</span><span class="sxs-lookup"><span data-stu-id="018e4-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="018e4-165">b.</span><span class="sxs-lookup"><span data-stu-id="018e4-165">b.</span></span> <span data-ttu-id="018e4-166">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://www.hostedgraphite.com/login/saml/<user id>/`</span><span class="sxs-lookup"><span data-stu-id="018e4-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://www.hostedgraphite.com/login/saml/<user id>/`</span></span>   

    > [!NOTE] 
    > <span data-ttu-id="018e4-167">Tenga en cuenta que estos no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="018e4-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="018e4-168">Tiene estos valores con hello tooupdate real identificador, la dirección URL de respuesta y la dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="018e4-168">You have tooupdate these values with hello actual Identifier, Reply URL and Sign On URL.</span></span> <span data-ttu-id="018e4-169">tooget estos valores, puede ir tooAccess -> configuración de SAML en el lado de la aplicación o póngase en contacto con [equipo de soporte técnico de gris hospedado](mailto:help@hostedgraphite.com).</span><span class="sxs-lookup"><span data-stu-id="018e4-169">tooget these values, you can go tooAccess->SAML setup on your Application side or Contact [Hosted Graphite support team](mailto:help@hostedgraphite.com).</span></span>
    >
 
5. <span data-ttu-id="018e4-170">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="018e4-170">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_certificate.png) 

6. <span data-ttu-id="018e4-172">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="018e4-172">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="018e4-174">En hello **configuración hospedada en gris** sección, haga clic en **configurar gris hospedado** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="018e4-174">On hello **Hosted Graphite Configuration** section, click **Configure Hosted Graphite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="018e4-175">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="018e4-175">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_configure.png) 

8. <span data-ttu-id="018e4-177">Inquilino de gris hospedado tooyour inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="018e4-177">Sign-on tooyour Hosted Graphite tenant as an administrator.</span></span>

9. <span data-ttu-id="018e4-178">Vaya toohello **página de configuración de SAML** en sidebar hello (**acceso -> configuración de SAML**).</span><span class="sxs-lookup"><span data-stu-id="018e4-178">Go toohello **SAML Setup page** in hello sidebar (**Access -> SAML Setup**).</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_000.png)

10. <span data-ttu-id="018e4-180">Confirme que estas direcciones URL coincide con la configuración que se realiza en hello **hospedado gris dominio y las direcciones URL** sección de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="018e4-180">Confirm these URls match your configuration done on hello **Hosted Graphite Domain and URLs** section of hello Azure portal.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_001.png)

11. <span data-ttu-id="018e4-182">En **entidad o Id. del emisor** y **dirección URL de inicio de sesión SSO** cuadros de texto, pegue el valor de Hola de **Id. de entidad SAML** y **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="018e4-182">In  **Entity or Issuer ID** and **SSO Login URL** textboxes, paste hello value of **SAML Entity ID** and **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
   
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_002.png)
   

12. <span data-ttu-id="018e4-184">Seleccione "**Solo lectura**" en **Default User Role** (Rol de usuario predeterminado).</span><span class="sxs-lookup"><span data-stu-id="018e4-184">Select "**Read-only**" as **Default User Role**.</span></span>
    
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_004.png)

13. <span data-ttu-id="018e4-186">Abra el certificado codificado en base 64 en el Bloc de notas que se descarga desde el portal de Azure, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado X.509** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="018e4-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
    
    ![Configuración del inicio de sesión único en la aplicación](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_005.png)

14. <span data-ttu-id="018e4-188">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="018e4-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="018e4-189">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="018e4-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="018e4-190">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="018e4-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="018e4-191">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="018e4-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="018e4-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="018e4-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="018e4-193">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="018e4-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="018e4-195">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="018e4-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="018e4-196">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="018e4-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="018e4-198">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="018e4-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="018e4-200">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="018e4-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="018e4-202">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="018e4-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="018e4-204">a.</span><span class="sxs-lookup"><span data-stu-id="018e4-204">a.</span></span> <span data-ttu-id="018e4-205">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="018e4-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="018e4-206">b.</span><span class="sxs-lookup"><span data-stu-id="018e4-206">b.</span></span> <span data-ttu-id="018e4-207">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="018e4-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="018e4-208">c.</span><span class="sxs-lookup"><span data-stu-id="018e4-208">c.</span></span> <span data-ttu-id="018e4-209">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="018e4-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="018e4-210">d.</span><span class="sxs-lookup"><span data-stu-id="018e4-210">d.</span></span> <span data-ttu-id="018e4-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="018e4-211">Click **Create**.</span></span>
 
### <a name="creating-a-hosted-graphite-test-user"></a><span data-ttu-id="018e4-212">Creación de un usuario de prueba de Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="018e4-212">Creating a Hosted Graphite test user</span></span>

<span data-ttu-id="018e4-213">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en gris hospedado.</span><span class="sxs-lookup"><span data-stu-id="018e4-213">hello objective of this section is toocreate a user called Britta Simon in Hosted Graphite.</span></span> <span data-ttu-id="018e4-214">Hosted Graphite admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="018e4-214">Hosted Graphite supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="018e4-215">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="018e4-215">There is no action item for you in this section.</span></span> <span data-ttu-id="018e4-216">Si no existe todavía, se creará un nuevo usuario durante un tooaccess intento Hosted gris.</span><span class="sxs-lookup"><span data-stu-id="018e4-216">A new user will be created during an attempt tooaccess Hosted Graphite if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="018e4-217">Si necesita un usuario toocreate manualmente, necesita equipo de soporte técnico de toocontact Hola gris hospedado a través de < mailto:help@hostedgraphite.com >.</span><span class="sxs-lookup"><span data-stu-id="018e4-217">If you need toocreate a user manually, you need toocontact hello Hosted Graphite support team via <mailto:help@hostedgraphite.com>.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="018e4-218">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="018e4-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="018e4-219">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooHosted gris.</span><span class="sxs-lookup"><span data-stu-id="018e4-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHosted Graphite.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="018e4-221">**tooassign Britta Simon tooHosted gris, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="018e4-221">**tooassign Britta Simon tooHosted Graphite, perform hello following steps:**</span></span>

1. <span data-ttu-id="018e4-222">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="018e4-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="018e4-224">En la lista de aplicaciones de hello, seleccione **gris hospedado**.</span><span class="sxs-lookup"><span data-stu-id="018e4-224">In hello applications list, select **Hosted Graphite**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_app.png) 

3. <span data-ttu-id="018e4-226">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="018e4-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="018e4-228">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="018e4-228">Click **Add** button.</span></span> <span data-ttu-id="018e4-229">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="018e4-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="018e4-231">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="018e4-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="018e4-232">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="018e4-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="018e4-233">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="018e4-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="018e4-234">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="018e4-234">Testing single sign-on</span></span>

<span data-ttu-id="018e4-235">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="018e4-235">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="018e4-236">Al hacer clic en icono gris hospedado Hola Hola Panel de acceso, deberá obtener aplicaciones de gris hospedado tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="018e4-236">When you click hello Hosted Graphite tile in hello Access Panel, you should get automatically signed-on tooyour Hosted Graphite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="018e4-237">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="018e4-237">Additional resources</span></span>

* [<span data-ttu-id="018e4-238">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="018e4-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="018e4-239">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="018e4-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_203.png


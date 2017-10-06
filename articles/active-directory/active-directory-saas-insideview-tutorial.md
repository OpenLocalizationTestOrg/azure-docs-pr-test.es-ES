---
title: "Tutorial: integración de Azure Active Directory con InsideView | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y InsideView."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 979c0c24f3a18a193616061b8c2e78292233a56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a><span data-ttu-id="ddac3-103">Tutorial: integración de Azure Active Directory con InsideView</span><span class="sxs-lookup"><span data-stu-id="ddac3-103">Tutorial: Azure Active Directory integration with InsideView</span></span>

<span data-ttu-id="ddac3-104">En este tutorial, aprenderá cómo toointegrate InsideView con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ddac3-104">In this tutorial, you learn how toointegrate InsideView with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ddac3-105">Integración de InsideView con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="ddac3-105">Integrating InsideView with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ddac3-106">Puede controlar en Azure AD que tenga acceso tooInsideView</span><span class="sxs-lookup"><span data-stu-id="ddac3-106">You can control in Azure AD who has access tooInsideView</span></span>
- <span data-ttu-id="ddac3-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooInsideView (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddac3-107">You can enable your users tooautomatically get signed-on tooInsideView (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ddac3-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ddac3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ddac3-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ddac3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddac3-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ddac3-110">Prerequisites</span></span>

<span data-ttu-id="ddac3-111">integración de Azure AD con InsideView tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ddac3-111">tooconfigure Azure AD integration with InsideView, you need hello following items:</span></span>

- <span data-ttu-id="ddac3-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddac3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ddac3-113">Una suscripción habilitada para el inicio de sesión único en InsideView</span><span class="sxs-lookup"><span data-stu-id="ddac3-113">A InsideView single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ddac3-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="ddac3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ddac3-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="ddac3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ddac3-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ddac3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ddac3-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ddac3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ddac3-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="ddac3-118">Scenario description</span></span>
<span data-ttu-id="ddac3-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="ddac3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ddac3-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="ddac3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ddac3-121">Agregar InsideView desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ddac3-121">Adding InsideView from hello gallery</span></span>
2. <span data-ttu-id="ddac3-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddac3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insideview-from-hello-gallery"></a><span data-ttu-id="ddac3-123">Agregar InsideView desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="ddac3-123">Adding InsideView from hello gallery</span></span>
<span data-ttu-id="ddac3-124">integración de hello tooconfigure de InsideView en tooAzure AD, deberá tooadd InsideView de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="ddac3-124">tooconfigure hello integration of InsideView in tooAzure AD, you need tooadd InsideView from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ddac3-125">**tooadd InsideView de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ddac3-125">**tooadd InsideView from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddac3-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="ddac3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ddac3-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ddac3-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="ddac3-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ddac3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="ddac3-133">En el cuadro de búsqueda de hello, escriba **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-133">In hello search box, type **InsideView**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. <span data-ttu-id="ddac3-135">En el panel de resultados de hello, seleccione **InsideView**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ddac3-135">In hello results panel, select **InsideView**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ddac3-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddac3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ddac3-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con InsideView con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ddac3-138">In this section, you configure and test Azure AD single sign-on with InsideView based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ddac3-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en InsideView es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ddac3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in InsideView is tooa user in Azure AD.</span></span> <span data-ttu-id="ddac3-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en InsideView debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="ddac3-140">In other words, a link relationship between an Azure AD user and hello related user in InsideView needs toobe established.</span></span>

<span data-ttu-id="ddac3-141">En InsideView, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddac3-141">In InsideView, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ddac3-142">tooconfigure y prueba de inicio de sesión único en Azure AD con InsideView, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="ddac3-142">tooconfigure and test Azure AD single sign-on with InsideView, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ddac3-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="ddac3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ddac3-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ddac3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ddac3-145">**[Crear un usuario de prueba de InsideView](#creating-a-insideview-test-user)**  -toohave un equivalente de Britta Simon en InsideView que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="ddac3-145">**[Creating a InsideView test user](#creating-a-insideview-test-user)** - toohave a counterpart of Britta Simon in InsideView that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ddac3-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ddac3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ddac3-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="ddac3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ddac3-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddac3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ddac3-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de InsideView.</span><span class="sxs-lookup"><span data-stu-id="ddac3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your InsideView application.</span></span>

<span data-ttu-id="ddac3-150">**inicio de sesión único en Azure AD tooconfigure con InsideView, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ddac3-150">**tooconfigure Azure AD single sign-on with InsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddac3-151">En el portal de Azure, en Hola Hola **InsideView** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-151">In hello Azure portal, on hello **InsideView** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="ddac3-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ddac3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. <span data-ttu-id="ddac3-155">En hello **InsideView dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ddac3-155">On hello **InsideView Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    <span data-ttu-id="ddac3-157">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://my.insideview.com/iv/<STS Name>/login.iv`</span><span class="sxs-lookup"><span data-stu-id="ddac3-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://my.insideview.com/iv/<STS Name>/login.iv`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ddac3-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="ddac3-158">This value is not real.</span></span> <span data-ttu-id="ddac3-159">Actualizar este valor con la dirección URL de respuesta real Hola.</span><span class="sxs-lookup"><span data-stu-id="ddac3-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="ddac3-160">Póngase en contacto con [equipo de soporte técnico de InsideView ](mailto:support@insideview.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="ddac3-160">Contact [InsideView support team ](mailto:support@insideview.com) tooget this value.</span></span>
 
4. <span data-ttu-id="ddac3-161">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Raw)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ddac3-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. <span data-ttu-id="ddac3-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="ddac3-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ddac3-165">En hello **configuración de InsideView** sección, haga clic en **configurar InsideView** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="ddac3-165">On hello **InsideView Configuration** section, click **Configure InsideView** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ddac3-166">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="ddac3-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. <span data-ttu-id="ddac3-168">En una ventana del explorador web diferente, inicie sesión en el sitio de empresa de InsideView tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="ddac3-168">In a different web browser window, log in tooyour InsideView company site as an administrator.</span></span>

8. <span data-ttu-id="ddac3-169">En la barra de herramientas de hello en la parte superior de hello, haga clic en **administración**, **configuración de SingleSignOn**y, a continuación, haga clic en **agregar SAML**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-169">In hello toolbar on hello top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span></span>
   
   <span data-ttu-id="ddac3-170">![Configuración de inicio de sesión único de SAML](./media/active-directory-saas-insideview-tutorial/ic794135.png "Cnfiguración de inicio de sesión único de SAML")</span><span class="sxs-lookup"><span data-stu-id="ddac3-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span></span>

9. <span data-ttu-id="ddac3-171">Hola **agregar un nuevo SAML** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ddac3-171">In hello **Add a New SAML** section, perform hello following steps:</span></span>

    <span data-ttu-id="ddac3-172">![Adición de un nuevo SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Adición de un nuevo SAML")</span><span class="sxs-lookup"><span data-stu-id="ddac3-172">![Add a New SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Add a New SAML")</span></span>
   
    <span data-ttu-id="ddac3-173">a.</span><span class="sxs-lookup"><span data-stu-id="ddac3-173">a.</span></span> <span data-ttu-id="ddac3-174">Hola **STS Name** cuadro de texto, escriba un nombre para la configuración.</span><span class="sxs-lookup"><span data-stu-id="ddac3-174">In hello **STS Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="ddac3-175">b.</span><span class="sxs-lookup"><span data-stu-id="ddac3-175">b.</span></span> <span data-ttu-id="ddac3-176">En **extremo no solicitado de SamlP/WS-Fed** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ddac3-176">In **SamlP/WS-Fed Unsolicited EndPoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="ddac3-177">c.</span><span class="sxs-lookup"><span data-stu-id="ddac3-177">c.</span></span> <span data-ttu-id="ddac3-178">Abra el certificado codificado en base 64, que ha descargado de Azure portal, Hola copia contenido del mismo en el Portapapeles, y, a continuación, péguelo toohello **STS Certificate** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="ddac3-178">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **STS Certificate** textbox.</span></span>

    <span data-ttu-id="ddac3-179">d.</span><span class="sxs-lookup"><span data-stu-id="ddac3-179">d.</span></span> <span data-ttu-id="ddac3-180">Hola **asignación de Id. de usuario de Crm** cuadro de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="ddac3-180">In hello **Crm User Id Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
        
    <span data-ttu-id="ddac3-181">e.</span><span class="sxs-lookup"><span data-stu-id="ddac3-181">e.</span></span> <span data-ttu-id="ddac3-182">Hola **asignación de correo electrónico de Crm** cuadro de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="ddac3-182">In hello **Crm Email Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="ddac3-183">f.</span><span class="sxs-lookup"><span data-stu-id="ddac3-183">f.</span></span> <span data-ttu-id="ddac3-184">Hola **asignación de nombre de Crm** cuadro de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="ddac3-184">In hello **Crm First Name Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="ddac3-185">g.</span><span class="sxs-lookup"><span data-stu-id="ddac3-185">g.</span></span> <span data-ttu-id="ddac3-186">Hola **apellidos de Crm asignación** cuadro de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="ddac3-186">In hello **Crm lastName Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>  

    <span data-ttu-id="ddac3-187">h.</span><span class="sxs-lookup"><span data-stu-id="ddac3-187">h.</span></span> <span data-ttu-id="ddac3-188">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ddac3-189">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="ddac3-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ddac3-190">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="ddac3-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ddac3-191">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ddac3-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ddac3-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddac3-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="ddac3-193">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="ddac3-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="ddac3-195">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ddac3-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddac3-196">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="ddac3-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ddac3-198">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ddac3-200">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddac3-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ddac3-202">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="ddac3-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ddac3-204">a.</span><span class="sxs-lookup"><span data-stu-id="ddac3-204">a.</span></span> <span data-ttu-id="ddac3-205">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ddac3-206">b.</span><span class="sxs-lookup"><span data-stu-id="ddac3-206">b.</span></span> <span data-ttu-id="ddac3-207">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ddac3-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ddac3-208">c.</span><span class="sxs-lookup"><span data-stu-id="ddac3-208">c.</span></span> <span data-ttu-id="ddac3-209">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ddac3-210">d.</span><span class="sxs-lookup"><span data-stu-id="ddac3-210">d.</span></span> <span data-ttu-id="ddac3-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-211">Click **Create**.</span></span>
 
### <a name="creating-a-insideview-test-user"></a><span data-ttu-id="ddac3-212">Creación de un usuario de prueba de InsideView</span><span class="sxs-lookup"><span data-stu-id="ddac3-212">Creating a InsideView test user</span></span>

<span data-ttu-id="ddac3-213">toolog de los usuarios de Azure AD tooenable en tooInsideView, se les deben aprovisionar en tooInsideView.</span><span class="sxs-lookup"><span data-stu-id="ddac3-213">tooenable Azure AD users toolog in tooInsideView, they must be provisioned in tooInsideView.</span></span> <span data-ttu-id="ddac3-214">En caso de hello de InsideView, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="ddac3-214">In hello case of InsideView, provisioning is a manual task.</span></span>

<span data-ttu-id="ddac3-215">tooget usuarios o contactos crean en InsideView, póngase en contacto con [equipo de soporte técnico de InsideView](mailto:support@insideview.com).</span><span class="sxs-lookup"><span data-stu-id="ddac3-215">tooget users or contacts created in InsideView, Contact [InsideView support team](mailto:support@insideview.com).</span></span>

>[!NOTE]
><span data-ttu-id="ddac3-216">Puede usar cualquier otra InsideView usuario cuenta herramienta de creación o las API proporcionadas por InsideView tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ddac3-216">You can use any other InsideView user account creation tools or APIs provided by InsideView tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ddac3-217">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddac3-217">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ddac3-218">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooInsideView.</span><span class="sxs-lookup"><span data-stu-id="ddac3-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInsideView.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="ddac3-220">**tooassign Britta Simon tooInsideView, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="ddac3-220">**tooassign Britta Simon tooInsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddac3-221">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="ddac3-223">En la lista de aplicaciones de hello, seleccione **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-223">In hello applications list, select **InsideView**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. <span data-ttu-id="ddac3-225">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="ddac3-227">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-227">Click **Add** button.</span></span> <span data-ttu-id="ddac3-228">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="ddac3-230">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddac3-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ddac3-231">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ddac3-232">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="ddac3-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ddac3-233">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="ddac3-233">Testing single sign-on</span></span>

<span data-ttu-id="ddac3-234">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ddac3-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ddac3-235">Al hacer clic en icono de InsideView Hola Hola Panel de acceso, deberá obtener aplicaciones de InsideView tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="ddac3-235">When you click hello InsideView tile in hello Access Panel, you should get automatically signed-on tooyour InsideView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ddac3-236">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ddac3-236">Additional resources</span></span>

* [<span data-ttu-id="ddac3-237">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ddac3-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ddac3-238">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ddac3-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_203.png


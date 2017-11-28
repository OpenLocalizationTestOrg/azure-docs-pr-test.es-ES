---
title: "Tutorial: Integración de Azure Active Directory con Pagerduty | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y PagerDuty."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="e40d7-103">Tutorial: Integración de Azure Active Directory con Pagerduty</span><span class="sxs-lookup"><span data-stu-id="e40d7-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="e40d7-104">En este tutorial, aprenderá cómo toointegrate PagerDuty con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e40d7-104">In this tutorial, you learn how toointegrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e40d7-105">Integración PagerDuty con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e40d7-105">Integrating PagerDuty with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e40d7-106">Puede controlar en Azure AD que tenga acceso tooPagerDuty</span><span class="sxs-lookup"><span data-stu-id="e40d7-106">You can control in Azure AD who has access tooPagerDuty</span></span>
- <span data-ttu-id="e40d7-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPagerDuty (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e40d7-107">You can enable your users tooautomatically get signed-on tooPagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e40d7-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e40d7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e40d7-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e40d7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e40d7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e40d7-110">Prerequisites</span></span>

<span data-ttu-id="e40d7-111">integración de Azure AD con PagerDuty tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e40d7-111">tooconfigure Azure AD integration with PagerDuty, you need hello following items:</span></span>

- <span data-ttu-id="e40d7-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e40d7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e40d7-113">Una suscripción habilitada para el inicio de sesión único en PagerDuty</span><span class="sxs-lookup"><span data-stu-id="e40d7-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e40d7-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e40d7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e40d7-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e40d7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e40d7-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e40d7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e40d7-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e40d7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e40d7-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e40d7-118">Scenario description</span></span>
<span data-ttu-id="e40d7-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e40d7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e40d7-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="e40d7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e40d7-121">Agregar PagerDuty desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e40d7-121">Adding PagerDuty from hello gallery</span></span>
2. <span data-ttu-id="e40d7-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e40d7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-hello-gallery"></a><span data-ttu-id="e40d7-123">Agregar PagerDuty desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e40d7-123">Adding PagerDuty from hello gallery</span></span>
<span data-ttu-id="e40d7-124">integración de hello tooconfigure de PagerDuty en Azure AD, deberá tooadd PagerDuty de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="e40d7-124">tooconfigure hello integration of PagerDuty into Azure AD, you need tooadd PagerDuty from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e40d7-125">**tooadd PagerDuty de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e40d7-125">**tooadd PagerDuty from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e40d7-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e40d7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="e40d7-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e40d7-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="e40d7-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e40d7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="e40d7-133">En el cuadro de búsqueda de hello, escriba **PagerDuty**, seleccione **PagerDuty** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e40d7-133">In hello search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e40d7-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="e40d7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e40d7-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con PagerDuty con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e40d7-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e40d7-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en PagerDuty es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e40d7-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PagerDuty is tooa user in Azure AD.</span></span> <span data-ttu-id="e40d7-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en PagerDuty debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="e40d7-138">In other words, a link relationship between an Azure AD user and hello related user in PagerDuty needs toobe established.</span></span>

<span data-ttu-id="e40d7-139">En PagerDuty, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e40d7-139">In PagerDuty, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e40d7-140">tooconfigure y prueba de inicio de sesión único en Azure AD con PagerDuty, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e40d7-140">tooconfigure and test Azure AD single sign-on with PagerDuty, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e40d7-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="e40d7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e40d7-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e40d7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e40d7-143">**[Crear un usuario de prueba de PagerDuty](#create-a-pagerduty-test-user)**  -toohave un equivalente de Britta Simon en PagerDuty que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="e40d7-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - toohave a counterpart of Britta Simon in PagerDuty that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e40d7-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e40d7-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e40d7-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e40d7-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e40d7-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e40d7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e40d7-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="e40d7-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="e40d7-148">**inicio de sesión único en tooconfigure Azure AD con PagerDuty, realice Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e40d7-148">**tooconfigure Azure AD single sign-on with PagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="e40d7-149">En el portal de Azure, en Hola Hola **PagerDuty** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-149">In hello Azure portal, on hello **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="e40d7-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e40d7-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="e40d7-153">En hello **PagerDuty dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e40d7-153">On hello **PagerDuty Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="e40d7-155">a.</span><span class="sxs-lookup"><span data-stu-id="e40d7-155">a.</span></span> <span data-ttu-id="e40d7-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="e40d7-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="e40d7-157">b.</span><span class="sxs-lookup"><span data-stu-id="e40d7-157">b.</span></span> <span data-ttu-id="e40d7-158">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="e40d7-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e40d7-159">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="e40d7-159">These values are not real.</span></span> <span data-ttu-id="e40d7-160">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="e40d7-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e40d7-161">Póngase en contacto con [equipo de soporte técnico de cliente de PagerDuty](https://www.pagerduty.com/support/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="e40d7-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="e40d7-162">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e40d7-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="e40d7-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e40d7-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e40d7-166">En hello **configuración de PagerDuty** sección, haga clic en **configurar PagerDuty** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="e40d7-166">On hello **PagerDuty Configuration** section, click **Configure PagerDuty** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e40d7-167">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="e40d7-167">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="e40d7-169">En otra ventana del explorador web, inicie sesión en el sitio de la compañía Pagerduty como administrador.</span><span class="sxs-lookup"><span data-stu-id="e40d7-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="e40d7-170">En el menú de hello en la parte superior de hello, haga clic en **configuración de la cuenta**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-170">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="e40d7-171">![Configuración de la cuenta](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "configuración de la cuenta")</span><span class="sxs-lookup"><span data-stu-id="e40d7-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="e40d7-172">Haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="e40d7-173">![Inicio de sesión único](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="e40d7-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="e40d7-174">En hello **habilitar inicio de sesión único (SSO)** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="e40d7-174">On hello **Enable Single Sign-on (SSO)** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="e40d7-175">![Habilitar inicio de sesión único](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Habilitar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="e40d7-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="e40d7-176">a.</span><span class="sxs-lookup"><span data-stu-id="e40d7-176">a.</span></span> <span data-ttu-id="e40d7-177">Abra el certificado codificado en base 64 descargado desde el portal de Azure en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado X.509** cuadro de texto</span><span class="sxs-lookup"><span data-stu-id="e40d7-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="e40d7-178">b.</span><span class="sxs-lookup"><span data-stu-id="e40d7-178">b.</span></span> <span data-ttu-id="e40d7-179">Hola **dirección URL de inicio de sesión** cuadro de texto, pegue **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e40d7-179">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="e40d7-180">c.</span><span class="sxs-lookup"><span data-stu-id="e40d7-180">c.</span></span> <span data-ttu-id="e40d7-181">Hola **Logout URL** cuadro de texto, pegue **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e40d7-181">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="e40d7-182">d.</span><span class="sxs-lookup"><span data-stu-id="e40d7-182">d.</span></span> <span data-ttu-id="e40d7-183">Seleccione **Activar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="e40d7-184">e.</span><span class="sxs-lookup"><span data-stu-id="e40d7-184">e.</span></span> <span data-ttu-id="e40d7-185">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="e40d7-186">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="e40d7-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e40d7-187">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="e40d7-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e40d7-188">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e40d7-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e40d7-189">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e40d7-189">Create an Azure AD test user</span></span>

<span data-ttu-id="e40d7-190">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="e40d7-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="e40d7-192">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e40d7-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e40d7-193">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="e40d7-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e40d7-195">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e40d7-197">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e40d7-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botón de agregar Hola](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e40d7-199">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="e40d7-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e40d7-201">a.</span><span class="sxs-lookup"><span data-stu-id="e40d7-201">a.</span></span> <span data-ttu-id="e40d7-202">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e40d7-203">b.</span><span class="sxs-lookup"><span data-stu-id="e40d7-203">b.</span></span> <span data-ttu-id="e40d7-204">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e40d7-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e40d7-205">c.</span><span class="sxs-lookup"><span data-stu-id="e40d7-205">c.</span></span> <span data-ttu-id="e40d7-206">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e40d7-207">d.</span><span class="sxs-lookup"><span data-stu-id="e40d7-207">d.</span></span> <span data-ttu-id="e40d7-208">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="e40d7-209">Creación de un usuario de prueba de PagerDuty</span><span class="sxs-lookup"><span data-stu-id="e40d7-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="e40d7-210">toolog de los usuarios de Azure AD tooenable en tooPagerDuty, se les deben aprovisionar en PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="e40d7-210">tooenable Azure AD users toolog in tooPagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="e40d7-211">En caso de hello de PagerDuty, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="e40d7-211">In hello case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="e40d7-212">Puede usar cualquier otra Pagerduty usuario cuenta herramienta de creación o las API proporcionadas por Pagerduty tooprovision Azure Active Directory las cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="e40d7-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="e40d7-213">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e40d7-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e40d7-214">Inicie sesión en tooyour **Pagerduty** inquilino.</span><span class="sxs-lookup"><span data-stu-id="e40d7-214">Log in tooyour **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="e40d7-215">En el menú de hello en la parte superior de hello, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-215">In hello menu on hello top, click **Users**.</span></span>

3. <span data-ttu-id="e40d7-216">Haga clic en **Agregar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="e40d7-217">![Agregar usuarios](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Agregar usuarios")</span><span class="sxs-lookup"><span data-stu-id="e40d7-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="e40d7-218">En hello **invite a su equipo** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e40d7-218">On hello **Invite your team** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="e40d7-219">![Invite your team (Invitar a su equipo)](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team (Invitar a su equipo)")</span><span class="sxs-lookup"><span data-stu-id="e40d7-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="e40d7-220">a.</span><span class="sxs-lookup"><span data-stu-id="e40d7-220">a.</span></span> <span data-ttu-id="e40d7-221">Hola de tipo **nombre y apellido** del usuario como **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-221">Type hello **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="e40d7-222">b.</span><span class="sxs-lookup"><span data-stu-id="e40d7-222">b.</span></span> <span data-ttu-id="e40d7-223">Escriba el **Email** (correo electrónico) del usuario, por ejemplo **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="e40d7-224">c.</span><span class="sxs-lookup"><span data-stu-id="e40d7-224">c.</span></span> <span data-ttu-id="e40d7-225">Haga clic en **Add** (Agregar) y después en **Send Invites** (Enviar invitaciones).</span><span class="sxs-lookup"><span data-stu-id="e40d7-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="e40d7-226">Todos los usuarios agregados recibirán una toocreate invitar a una cuenta de PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="e40d7-226">All added users will receive an invite toocreate a PagerDuty account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e40d7-227">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e40d7-227">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e40d7-228">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooPagerDuty.</span><span class="sxs-lookup"><span data-stu-id="e40d7-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPagerDuty.</span></span>

![Asigne el rol de usuario de Hola][200]

<span data-ttu-id="e40d7-230">**tooassign Britta Simon tooPagerDuty, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e40d7-230">**tooassign Britta Simon tooPagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="e40d7-231">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e40d7-233">En la lista de aplicaciones de hello, seleccione **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-233">In hello applications list, select **PagerDuty**.</span></span>

    ![vínculo de PagerDuty Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="e40d7-235">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="e40d7-237">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-237">Click **Add** button.</span></span> <span data-ttu-id="e40d7-238">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="e40d7-240">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="e40d7-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e40d7-241">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e40d7-242">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e40d7-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e40d7-243">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="e40d7-243">Test single sign-on</span></span>

<span data-ttu-id="e40d7-244">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e40d7-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e40d7-245">Al hacer clic en icono de PagerDuty Hola Hola acceso Panelyou debería obtener automáticamente ha iniciado sesión tooyour PagerDuty aplicación.</span><span class="sxs-lookup"><span data-stu-id="e40d7-245">When you click hello PagerDuty tile in hello Access Panelyou should get automatically signed-on tooyour PagerDuty application.</span></span>

<span data-ttu-id="e40d7-246">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e40d7-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e40d7-247">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e40d7-247">Additional resources</span></span>

* [<span data-ttu-id="e40d7-248">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e40d7-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e40d7-249">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e40d7-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

